Kế hoạch Sprint tổng thể
Sprint	Mục tiêu chính	Chi tiết công việc
Sprint 0	Khởi tạo nền tảng	- Cấu hình dự án Laravel, cấu trúc thư mục.
- Thiết lập môi trường .env, seed user mẫu.
- Thiết lập CI/CD, chuẩn hóa coding style (PSR-12), unit test khung.
- Viết README hướng dẫn cài đặt và quy ước commit.
Sprint 1	Authentication & phân quyền	- Migration thêm cột role cho users.
- Middleware RoleMiddleware và hệ thống đăng nhập/reset mật khẩu.
- Tạo seed dữ liệu mẫu: admin, manager, teacher.
- Unit test đăng nhập, phân quyền cơ bản.
Sprint 2	Quản lý chi nhánh	- Migration & model Branch (name, address, manager_id).
- CRUD chi nhánh, gán/quản lý manager.
- Giao diện/listing với filter, soft-delete/lock.
- Feature test cho CRUD chi nhánh và gán manager.
Sprint 3	Quản lý giáo viên	- Migration Teacher (code, CCCD, trình độ, chứng chỉ…).
- Giao diện CRUD giáo viên.
- Phân công giáo viên vào lớp (chuẩn bị cho Sprint 4).
- Test CRUD và phân công.
Sprint 4	Khóa học & Lớp học	- Migration Course & Class (lịch, học phí, số buổi…).
- Quản lý phòng học (migration Room, kiểm tra trùng lịch).
- Giao diện tạo/sửa/đóng lớp; điều chỉnh lịch buổi (hủy/dời).
- Unit/feature test: tạo lớp, kiểm tra phòng trống, chuyển trạng thái.
Sprint 5	Học sinh & Học phí	- Migration Student và pivot Enrollment (join_date, tuition_paid, tuition_due).
- Xử lý nhập học muộn, chuyển lớp, hoàn/thu thêm học phí.
- Thu học phí: phiếu thu, liên kết cổng thanh toán (mock).
- Test ghi danh, tính học phí, chuyển lớp.
Sprint 6	Chấm công & Lương	- Migration ClassSession & TeacherAttendance.
- Chức năng điểm danh học sinh, chấm công giáo viên theo buổi.
- Service Payroll tổng hợp lương; import Excel, duyệt & gửi email.
- Test chấm công, bảng lương, gửi mail giả lập.
Sprint 7	Thông báo	- Tích hợp gửi email/Zalo (queue + scheduler).
- Nhắc học phí, nhắc sắp hết khóa; gửi nhận xét và video.
- Màn hình quản lý/scheduling thông báo.
- Test queue gửi thông báo (mock service).
Sprint 8	Báo cáo & hoàn thiện	- Dashboard admin/manager: thống kê chi nhánh, lớp, học viên, doanh thu, công nợ.
- Báo cáo PDF/Excel theo chi nhánh/khoảng thời gian.
- Hoàn thiện tài liệu, kiểm thử hệ thống end-to-end, chuẩn bị deploy.
Ghi chú triển khai

    Mỗi sprint kéo dài 2–3 tuần (tuỳ quy mô đội ngũ).

    Sau mỗi sprint: demo, review code, cập nhật tài liệu và backlog cho sprint tiếp theo.

    Các tính năng mở rộng (quản lý phụ huynh, kế toán chi tiết, học online…) có thể lập kế hoạch sau Sprint 8 tùy nhu cầu phát triển tiếp theo.
    
    
============================================================
Backlog tổng thể
Sprint	Ticket	Mô tả ngắn gọn
1	Nền tảng & phân quyền	Cài đặt CI/CD, roles, module Chi nhánh
2	Giáo viên	Hồ sơ giáo viên, phân công lớp
3	Khóa & Lớp	Khóa học, phòng học, lịch lớp
4	Học viên & Học phí	Ghi danh, thu/hoàn học phí
5	Chấm công & Lương	Buổi học, payroll giáo viên
6	Thông báo	Email/Zalo học phí, nhận xét, video
7	Báo cáo	Dashboard, báo cáo thu chi
8	Hoàn thiện	Tối ưu, tài liệu, kiểm thử E2E
Sprint 1: Nền tảng & Phân quyền
1. Thiết lập CI/CD và seed dữ liệu mẫu
Suggested taskThiết lập CI/CD và seed dữ liệu mẫu
2. Bổ sung cột vai trò và middleware phân quyền
Suggested taskThêm cột role và middleware phân quyền
3. Module quản lý chi nhánh (migration, model, controller, route)
Suggested taskXây dựng module chi nhánh
4. Unit/Feature test cho chi nhánh và phân quyền
Suggested taskViết test cho module chi nhánh và phân quyền
Sprint 2–8 (Overview)
Sprint 2: Giáo viên
Suggested taskQuản lý giáo viên
Sprint 3: Khóa & Lớp
Suggested taskQuản lý khóa học và lớp học
Sprint 4: Học viên & Học phí
Suggested taskGhi danh và học phí
Sprint 5: Chấm công & Lương
Suggested taskChấm công và payroll giáo viên
Sprint 6: Thông báo
Suggested taskTích hợp thông báo Email/Zalo
Sprint 7: Báo cáo
Suggested taskBáo cáo và dashboard
Sprint 8: Hoàn thiện
Suggested taskTối ưu và tài liệu

