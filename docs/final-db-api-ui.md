Database schema (đề xuất chi tiết)
Bảng	Mô tả & Trường chính	Ghi chú
users	id, name, email (unique), password, phone, address, role (admin,manager,teacher), remember_token, timestamps	Bảng tài khoản chung; phân quyền bằng cột role.
branches	id, name, address, manager_id (FK → users.id), timestamps	Một chi nhánh có 1 quản lý.
teachers	id, user_id (FK), code (unique), national_id, degree, certificate, photo_path, timestamps	Hồ sơ chi tiết của giáo viên.
courses	id, name, age_group (enum), language (enum), description, status (open,closed), timestamps	Khóa học theo lứa tuổi/ngôn ngữ.
rooms	id, branch_id (FK), code (unique), name, capacity, status (active,inactive), timestamps	Một phòng chỉ dùng cho 1 lớp tại một thời điểm.
classes	id, code (unique), name, course_id (FK), branch_id (FK), teacher_id (FK), room_id (FK), schedule_json, sessions_total, tuition_fee, start_date, status, timestamps	Lịch học lưu dạng JSON {day_of_week,start,end}.
class_sessions	id, class_id (FK), session_no, scheduled_date, start_time, end_time, status (planned,canceled,postponed,completed), actual_date, timestamps	Buổi học cụ thể.
teacher_attendances	id, class_session_id (FK), teacher_id (FK), status (present,absent), session_pay, notes, timestamps	Chấm công giáo viên, dùng tính lương.
students	id, code (unique), name, gender, dob, phone, email, address, guardian_name, guardian_phone, timestamps	Thông tin học sinh.
enrollments	id, class_id (FK), student_id (FK), join_date, tuition_paid, tuition_due, status (studying,completed,transferred), timestamps	Pivot ghi danh & công nợ học phí.
student_attendances	id, class_session_id (FK), student_id (FK), status (present,excused,absent), notes, timestamps	Điểm danh học sinh từng buổi.
tuition_payments	id, enrollment_id (FK), amount, paid_at, method (cash,bank,online), collector_id (FK → users), note, timestamps	Thu học phí.
payrolls	id, teacher_id (FK), month, year, total_sessions, total_amount, status (pending,approved,sent), approved_by (FK → users), approved_at, timestamps	Bảng lương theo giáo viên/tháng.
payroll_items	id, payroll_id (FK), class_session_id (FK), amount, timestamps	Chi tiết từng buổi trong bảng lương.
accounts	id, branch_id (FK), name, type (asset,liability,revenue,expense), timestamps	Danh mục tài khoản kế toán đơn giản.
transactions	id, account_id (FK), branch_id (FK), amount, transaction_date, description, ref_table, ref_id, timestamps	Ghi nhận thu/chi (liên kết học phí, lương...).
Kiến trúc API (RESTful + Laravel)

    Principles

        api/v1/* prefix, JSON responses.

        Auth: JWT/Sanctum tokens, middleware auth, role:....

        Pagination: ?page=1&per_page=20, filter theo branch, status.

    Modules & Endpoints (ví dụ)

Module	Endpoints	Vai trò
Auth	POST /api/v1/login, POST /api/v1/logout, POST /api/v1/password/email	Public
Branches	GET/POST/PUT/DELETE /api/v1/branches	Admin, Manager (read)
Users/Managers	GET/POST/PUT/DELETE /api/v1/managers	Admin
Teachers	GET/POST/PUT/DELETE /api/v1/teachers, POST /api/v1/classes/{id}/assign-teacher	Admin, Manager
Courses	GET/POST/PUT/DELETE /api/v1/courses	Admin, Manager
Classes	GET/POST/PUT/DELETE /api/v1/classes, POST /api/v1/classes/{id}/sessions	Admin, Manager
Students	GET/POST/PUT/DELETE /api/v1/students, POST /api/v1/classes/{id}/enroll	Admin, Manager
Attendance	POST /api/v1/classes/{id}/sessions/{sid}/teacher-attendance, POST /api/v1/classes/{id}/sessions/{sid}/student-attendance	Manager, Teacher
Payroll	GET /api/v1/payrolls, POST /api/v1/payrolls/{id}/approve, POST /api/v1/payrolls/{id}/send	Admin
Notifications	POST /api/v1/notifications/tuition-reminder, POST /api/v1/notifications/remarks	Manager, Teacher
Reports	GET /api/v1/reports/dashboard, GET /api/v1/reports/finance	Admin, Manager
Kiến trúc UI (InertiaJS + Vue 3 + PrimeVue)

resources/js/
├── app.js                // khởi tạo Inertia, PrimeVue, i18n
├── services/             // axios config, service layer
│   ├── api.js
│   └── ...Service.js
├── Layouts/
│   ├── AdminLayout.vue
│   ├── ManagerLayout.vue
│   └── TeacherLayout.vue
├── Pages/
│   ├── Auth/Login.vue
│   ├── Dashboard/AdminDashboard.vue
│   ├── Branch/Index.vue
│   ├── Teacher/Index.vue
│   ├── Course/Index.vue
│   ├── Class/Index.vue
│   ├── Class/Show.vue       // lịch + điểm danh
│   ├── Student/Index.vue
│   ├── Payroll/Index.vue
│   └── Report/Dashboard.vue
└── Components/
    ├── DataTable.vue
    ├── FormModal.vue
    ├── UploadImage.vue
    └── AttendanceForm.vue

    Composition API (script setup, ref, computed).

    PrimeVue components: DataTable, Dialog, Calendar, Dropdown, Toast.

    Layouts quyết định sidebar/nav theo vai trò.

    Service Layer gọi API (axios), tách khỏi component.

    UI Flow:

        Login → dashboard theo role.

        Admin: quản lý chi nhánh, user, teacher, course, global reports.

        Manager: lớp, giáo viên, học sinh, thu học phí, chấm công.

        Teacher: điểm danh học sinh, xem lương, gửi nhận xét và video.

Testing

⚠️ Không chạy lệnh kiểm thử (môi trường chỉ đọc).
Notes

Thiết kế trên đáp ứng yêu cầu mở rộng nhiều chi nhánh, cho phép phân quyền rõ ràng giữa admin–quản lý–giáo viên, đồng thời chuẩn bị nền tảng tích hợp API và giao diện hiện đại sử dụng InertiaJS, Vue 3 và PrimeVue.
Ở resources/js/Pages, bạn không phân chia thành các thư mục theo Role à?

Hi!
Hiện tại trong resources/js của dự án chỉ có 2 file app.js và bootstrap.js; chưa tồn tại thư mục Pages, nên cũng chưa có phân chia theo vai trò nào cả

. Vì mục tiêu là hệ thống chuyên nghiệp với giao diện tách riêng cho từng vai trò, bạn nên bổ sung các thư mục cho trang hiển thị như sau:

resources/js/
└── Pages/
    ├── Admin/
    ├── Manager/
    └── Teacher/
