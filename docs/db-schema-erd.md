Sơ đồ ERD tổng quát (Mermaid)

erDiagram
    USERS ||--o{ BRANCHES : "quản lý"
    USERS ||--o{ TEACHERS : "hồ sơ chi tiết"
    USERS ||--o{ PAYROLLS : "duyệt"
    BRANCHES ||--o{ ROOMS : "có"
    BRANCHES ||--o{ CLASSES : "tổ chức"
    COURSES ||--o{ CLASSES : "gồm nhiều"
    TEACHERS ||--o{ CLASSES : "phụ trách"
    CLASSES ||--o{ CLASS_SESSIONS : "gồm buổi"
    CLASS_SESSIONS ||--o{ TEACHER_ATTENDANCES : "chấm công GV"
    CLASS_SESSIONS ||--o{ STUDENT_ATTENDANCES : "điểm danh HS"
    STUDENTS ||--o{ ENROLLMENTS : "ghi danh"
    CLASSES ||--o{ ENROLLMENTS : "có học viên"
    ENROLLMENTS ||--o{ TUITION_PAYMENTS : "thu học phí"
    TEACHERS ||--o{ PAYROLL_ITEMS : "nhận lương"
    ACCOUNTS ||--o{ TRANSACTIONS : "ghi sổ"

Mô tả chi tiết bảng và cột
1. users
Cột	Kiểu	Giải thích
id	PK, bigint	Mã định danh người dùng.
name	string	Họ tên.
email	string (unique)	Email đăng nhập.
password	string	Mật khẩu (đã hash).
phone	string	Số điện thoại.
address	string	Địa chỉ.
role	enum(admin,manager,teacher)	Vai trò của người dùng.
remember_token	string, nullable	Token “remember me”.
timestamps	–	Thời gian tạo/cập nhật.

    Ghi chú: Admin và Quản lý dùng chung bảng users; thông tin chi tiết giáo viên nằm ở bảng teachers.

2. branches
Cột	Kiểu	Giải thích
id	PK	Mã chi nhánh.
name	string	Tên chi nhánh.
address	string	Địa chỉ chi nhánh.
manager_id	FK -> users.id	Người quản lý chi nhánh.
timestamps	–	Thời gian tạo/cập nhật.
3. teachers
Cột	Kiểu	Giải thích
id	PK	Mã hồ sơ giáo viên.
user_id	FK -> users.id	Tham chiếu tài khoản đăng nhập.
code	string (unique)	Mã giáo viên nội bộ.
national_id	string	Số CCCD/CMND.
degree	string	Bằng cấp cao nhất.
certificate	string	Chứng chỉ chuyên môn.
photo_path	string	Ảnh chân dung.
timestamps	–	Thời gian tạo/cập nhật.

    Ghi chú: Thông tin họ tên, email, điện thoại của giáo viên dùng chung từ bảng users.

4. courses
Cột	Kiểu	Giải thích
id	PK	Mã khóa học.
name	string	Tên khóa học.
age_group	enum(kid,teen,adult,exam)	Đối tượng lứa tuổi.
language	enum(en,zh,ko,ja)	Ngôn ngữ: Anh, Trung, Hàn, Nhật.
description	text	Mô tả ngắn.
status	enum(open,closed)	Trạng thái khóa học.
timestamps	–	Thời gian tạo/cập nhật.
5. rooms
Cột	Kiểu	Giải thích
id	PK	Mã phòng.
branch_id	FK -> branches.id	Thuộc chi nhánh.
code	string (unique)	Mã phòng.
name	string	Tên phòng.
capacity	integer	Số chỗ tối đa.
status	enum(active,inactive)	Trạng thái phòng.
timestamps	–	Thời gian tạo/cập nhật.
6. classes
Cột	Kiểu	Giải thích
id	PK	Mã lớp học.
code	string (unique)	Mã lớp (ví dụ: DVX_KA92).
name	string	Tên lớp.
course_id	FK -> courses.id	Khóa học liên kết.
branch_id	FK -> branches.id	Chi nhánh.
teacher_id	FK -> teachers.id	Giáo viên phụ trách.
room_id	FK -> rooms.id	Phòng học.
schedule_json	json	Lịch học tuần (ngày, giờ bắt đầu/kết thúc).
sessions_total	integer	Tổng số buổi học.
tuition_fee	decimal	Học phí toàn khóa.
start_date	date	Ngày bắt đầu khóa.
status	enum(open,closed)	Trạng thái lớp.
timestamps	–	Thời gian tạo/cập nhật.
7. class_sessions
Cột	Kiểu	Giải thích
id	PK	Mã buổi học.
class_id	FK -> classes.id	Thuộc lớp nào.
session_no	integer	Số thứ tự buổi.
scheduled_date	date	Ngày dự kiến.
start_time	time	Giờ bắt đầu.
end_time	time	Giờ kết thúc.
status	enum(planned,canceled,postponed,completed)	Trạng thái thực tế.
actual_date	date, nullable	Ngày diễn ra nếu dời.
timestamps	–	Thời gian tạo/cập nhật.
8. teacher_attendances
Cột	Kiểu	Giải thích
id	PK	Mã chấm công GV.
class_session_id	FK -> class_sessions.id	Buổi dạy.
teacher_id	FK -> teachers.id	Giáo viên.
status	enum(present,absent)	Trạng thái tham gia.
session_pay	decimal	Số tiền cho buổi này.
notes	text, nullable	Ghi chú.
timestamps	–	Thời gian tạo/cập nhật.
9. students
Cột	Kiểu	Giải thích
id	PK	Mã học sinh.
code	string (unique)	Mã học sinh nội bộ.
name	string	Họ tên.
gender	enum(male,female,other)	Giới tính.
dob	date	Ngày sinh.
phone	string	SĐT.
email	string	Email.
address	string	Địa chỉ.
guardian_name	string	Người giám hộ (nếu là trẻ em).
guardian_phone	string	SĐT người giám hộ.
timestamps	–	Thời gian tạo/cập nhật.
10. enrollments (pivot học sinh–lớp)
Cột	Kiểu	Giải thích
id	PK	Mã ghi danh.
class_id	FK -> classes.id	Lớp học.
student_id	FK -> students.id	Học sinh.
join_date	date	Ngày bắt đầu học thực tế.
tuition_paid	decimal	Số tiền đã đóng.
tuition_due	decimal	Học phí còn thiếu (+) / dư (-).
status	enum(studying,completed,transferred)	Trạng thái.
timestamps	–	Thời gian tạo/cập nhật.
11. student_attendances
Cột	Kiểu	Giải thích
id	PK	Mã điểm danh HS.
class_session_id	FK -> class_sessions.id	Buổi học.
student_id	FK -> students.id	Học sinh.
status	enum(present,excused,absent)	Có mặt/vắng có phép/vắng không phép.
notes	text, nullable	Ghi chú thêm.
timestamps	–	Thời gian tạo/cập nhật.
12. tuition_payments
Cột	Kiểu	Giải thích
id	PK	Mã lần đóng học phí.
enrollment_id	FK -> enrollments.id	Ghi danh liên quan.
amount	decimal	Số tiền thu.
paid_at	datetime	Thời điểm thu.
method	enum(cash,bank,online)	Phương thức thanh toán.
collector_id	FK -> users.id	Người thu tiền.
note	text, nullable	Ghi chú.
timestamps	–	Thời gian tạo/cập nhật.
13. payrolls
Cột	Kiểu	Giải thích
id	PK	Mã bảng lương (theo tháng).
teacher_id	FK -> teachers.id	Giáo viên.
month	integer	Tháng.
year	integer	Năm.
total_sessions	integer	Tổng buổi được tính lương.
total_amount	decimal	Tổng tiền lương.
status	enum(pending,approved,sent)	Trạng thái duyệt/gửi.
approved_by	FK -> users.id, nullable	Admin duyệt.
approved_at	datetime, nullable	Thời gian duyệt.
timestamps	–	Thời gian tạo/cập nhật.
14. payroll_items
Cột	Kiểu	Giải thích
id	PK	Mã dòng lương.
payroll_id	FK -> payrolls.id	Thuộc bảng lương.
class_session_id	FK -> class_sessions.id	Buổi dạy.
amount	decimal	Số tiền trả buổi này.
timestamps	–	Thời gian tạo/cập nhật.
15. accounts (kế toán đơn giản)
Cột	Kiểu	Giải thích
id	PK	Mã tài khoản kế toán.
branch_id	FK -> branches.id	Thuộc chi nhánh.
name	string	Tên tài khoản (Doanh thu, Chi phí…).
type	enum(asset,liability,revenue,expense)	Loại tài khoản.
timestamps	–	Thời gian tạo/cập nhật.
16. transactions
Cột	Kiểu	Giải thích
id	PK	Mã bút toán.
account_id	FK -> accounts.id	Tài khoản.
branch_id	FK -> branches.id	Chi nhánh.
amount	decimal	Số tiền (+ thu / - chi).
transaction_date	date	Ngày phát sinh.
description	string	Mô tả ngắn.
ref_table	string, nullable	Bảng tham chiếu (vd: tuition_payments).
ref_id	bigint, nullable	ID bản ghi tham chiếu.
timestamps	–	Thời gian tạo/cập nhật.
Ghi chú chung

    PK: Primary Key.

    FK: Foreign Key.

    Các bảng timestamps chứa cột created_at và updated_at.

    Các bảng pivot (enrollments, payroll_items) giúp liên kết quan hệ N-N hoặc chi tiết từng giao dịch.

    schedule_json lưu cấu trúc JSON: [{day_of_week: 5, start: "19:00", end: "21:00"}, ...] để linh hoạt cho nhiều buổi/tuần.

    Bảng accounts và transactions là nền tảng kế toán đơn giản, dễ mở rộng trong tương lai.

Thiết kế trên đáp ứng đầy đủ các nghiệp vụ quản lý trung tâm ngoại ngữ, đồng thời chuẩn bị nền tảng mở rộng cho nhiều chi nhánh và tích hợp các module kế toán, thông báo, báo cáo chuyên sâu.
