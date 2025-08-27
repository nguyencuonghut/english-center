Tổng hợp yêu cầu hệ thống quản lý trung tâm ngoại ngữ
1. Quản lý chi nhánh

    Mỗi chi nhánh có tên, địa chỉ, người quản lý riêng.

    Cho phép thêm/sửa/xóa/khóa chi nhánh và gán/quản lý người quản lý tương ứng.

2. Người quản lý

    Lưu họ tên, số điện thoại, email, địa chỉ.

    Chịu trách nhiệm lập lịch, phân công giáo viên, thu học phí, các hoạt động hành chính.

    Admin có quyền thêm/sửa/xóa/khóa người quản lý.

3. Giáo viên

    Thông tin: mã, họ tên, điện thoại, email, địa chỉ, CCCD, ảnh, trình độ, chứng chỉ.

    Phân công dạy một hoặc nhiều lớp; có thể thỏa thuận dạy thay nhau (có thông báo).

    Chấm công từng buổi; mức lương mỗi buổi tùy lớp.

4. Khóa học

    Phân loại theo lứa tuổi (trẻ em, học sinh, người đi làm, luyện thi TOEIC/IELTS) và theo ngôn ngữ (Anh, Trung, Hàn, Nhật).

    Quản lý thêm/sửa/xóa/đóng khóa học.

5. Lớp học

    Thuộc khóa học, chi nhánh, phòng học và giáo viên phụ trách.

    Lưu: mã lớp, tên, khóa, lịch học (ngày giờ), số buổi, học phí, ngày bắt đầu, trạng thái.

    Học sinh có thể nhập học muộn, chuyển lớp; cần tính toán học phí còn thiếu/thừa.

    Lịch buổi học có thể bị hủy hoặc dời, ảnh hưởng chấm công và điểm danh.

    Thao tác thêm/sửa/xóa/đóng lớp học.

6. Phòng học

    Mã, tên phòng, sức chứa; một thời điểm chỉ diễn ra một lớp.

    Hỗ trợ thêm/sửa/xóa/đóng phòng học; kiểm tra trùng lịch khi gán phòng cho lớp.

7. Học sinh & học phí

    Lưu thông tin cá nhân, liên hệ, ngày nhập học.

    Theo dõi lịch sử đóng học phí, công nợ; tính học phí khi nhập muộn hoặc chuyển lớp.

    Khả năng hoàn tiền hoặc thu thêm khi chuyển lớp.

8. Chấm công & lương giáo viên

    Ghi nhận buổi dạy, tính lương theo lớp.

    Admin duyệt bảng chấm công, import dữ liệu lương từ Excel, gửi email lương hàng loạt.

9. Vai trò & phân quyền

    Ba vai trò: Admin, Quản lý, Giáo viên.

    Admin: toàn quyền (quản lý chi nhánh, người quản lý, giáo viên, duyệt lương, dashboard tổng hợp).

    Quản lý: phân công giáo viên, chấm công, thu học phí, gửi nhắc học phí.

    Giáo viên: điểm danh học sinh, viết nhận xét cuối khóa, gửi nhận xét và link video qua Zalo.

10. Đăng nhập & bảo mật

    Đăng nhập bằng email, hỗ trợ quên/reset mật khẩu.

    Phân quyền middleware theo vai trò, lưu audit log.

    Mật khẩu được mã hóa; chuẩn bị nền tảng bảo mật mở rộng.

11. Thông báo & giao tiếp

    Gửi email hoặc Zalo đến học sinh/giáo viên:

        Nhắc đóng học phí, thông báo sắp hết khóa.

        Nhận xét cuối khóa, link video bài nói sau mỗi buổi.

    Hỗ trợ lên lịch gửi tự động và queue.

12. Báo cáo & dashboard

    Admin xem thống kê toàn hệ thống: chi nhánh, quản lý, giáo viên, học sinh, lớp, doanh thu, công nợ, học sinh sắp hết khóa, nợ học phí.

    Quản lý xem báo cáo chi nhánh của mình.

    Xuất báo cáo PDF/Excel theo khoảng thời gian.

13. Yêu cầu phi chức năng

    Bảo mật: phân quyền tường minh, nhật ký thao tác.

    Hiệu năng: phản hồi <2 giây, cache dữ liệu tĩnh.

    Sẵn sàng: sao lưu & khôi phục dữ liệu.

    Giám sát: log tập trung, cảnh báo khi lỗi.

    Quốc tế hóa: chuẩn bị đa ngôn ngữ, đa tiền tệ.

    CI/CD: kiểm thử tự động, build & deploy, rollback nhanh.

14. Khả năng mở rộng & kết nối

    API REST/GraphQL cho mobile app hoặc đối tác.

    Sẵn sàng tích hợp CRM, cổng thanh toán, hệ thống kế toán.

    Kiến trúc mô-đun/microservice khi hệ thống lớn.

15. Định hướng kế toán tối giản (bổ sung)

    Bảng Accounts, Transactions, PaymentRecords, ExpenseRecords.

    Dịch vụ AccountingService ghi nhận thu/chi.

    Báo cáo thu chi theo chi nhánh, theo thời gian.

16. Quy trình phát triển phần mềm (SDLC)

    Chuẩn hóa cấu hình, coding style, CI.

    Thiết kế role-based middleware, CRUD cho các module.

    Viết test (unit/feature), tài liệu hướng dẫn người dùng và kỹ thuật.

    Triển khai pipeline CI/CD, backup/rollback.
