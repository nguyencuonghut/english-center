1. Phân tích yêu cầu (Requirement Analysis)
1.1 Đối tượng & phạm vi quản lý
Đối tượng	Mục đích quản lý	Trường thông tin chính
Chi nhánh	Quản lý cơ sở theo địa phương	Tên, địa chỉ, quản lý phụ trách
Người quản lý	Điều phối lịch dạy, thu học phí, công việc hành chính	Họ tên, SĐT, email, địa chỉ
Giáo viên	Giảng dạy, chấm công, nhận lương	Mã, họ tên, SĐT, email, CCCD, ảnh, trình độ, chứng chỉ
Khóa học	Phân loại chương trình theo ngôn ngữ & lứa tuổi	Tên, đối tượng, ngôn ngữ, mô tả, trạng thái
Lớp học	Tổ chức lịch học, giáo viên, học sinh	Mã lớp, tên lớp, khóa, chi nhánh, lịch học, học phí, giáo viên
Phòng học	Quản lý tài nguyên vật lý	Mã phòng, tên phòng, sức chứa
Học sinh	Theo dõi tham gia lớp & học phí	Mã HS, họ tên, liên hệ, ngày nhập học, thông tin giám hộ
Ghi danh & Học phí	Tính toán học phí, công nợ, chuyển lớp	Join date, tiền đã đóng, còn thiếu/dư
Chấm công & Lương	Ghi nhận buổi dạy, tính lương theo lớp	Buổi học, trạng thái, tiền công/buổi
Thông báo & Báo cáo	Gửi email/Zalo, thống kê	Nhắc đóng học phí, nhận xét, dashboard
1.2 Nghiệp vụ chính

    CRUD chi nhánh, quản lý, giáo viên, khóa học, lớp học, phòng học.

    Phân quyền người dùng: Admin, Quản lý, Giáo viên.

    Đăng nhập bằng email, quên mật khẩu qua email.

    Điểm danh học sinh, chấm công giáo viên, tính lương, gửi bảng lương.

    Thu học phí, nhắc nợ, xử lý nhập học muộn, chuyển lớp, hoàn/thu thêm tiền.

    Gửi thông báo (Email/Zalo) về học phí, nhận xét, link video.

    Dashboard & báo cáo tổng hợp theo chi nhánh/toàn hệ thống.

2. Tài liệu SRS (Software Requirements Specification)
2.1 Giới thiệu
Mục	Nội dung
Mục tiêu	Xây dựng hệ thống quản lý đa chi nhánh, chuẩn hóa nghiệp vụ trung tâm ngoại ngữ, dễ mở rộng.
Đối tượng đọc	Chủ trung tâm, quản lý, giáo viên, đội phát triển & QA.
Phạm vi	Quản lý chi nhánh, giáo viên, khóa học, lớp, học sinh, học phí, chấm công–lương, thông báo và báo cáo.
2.2 Mô tả tổng quát

    Kiến trúc: Laravel MVC, REST API (có thể mở rộng GraphQL), queue xử lý bất đồng bộ.

    Người dùng:

        Admin: toàn quyền trên toàn hệ thống.

        Quản lý: thao tác trong phạm vi chi nhánh.

        Giáo viên: xem lớp dạy, điểm danh, nhận xét học sinh.

    Môi trường: PHP 8+, MySQL/PostgreSQL, Redis (cache/queue), trình duyệt hiện đại.

    Giới hạn: Mỗi phòng/lớp/giáo viên không trùng lịch; bảo mật mật khẩu, log thao tác.

2.3 Chức năng hệ thống (Functional Requirements)
Mã FR	Mô tả
FR-1	Tạo/sửa/xóa/khóa chi nhánh, gán quản lý.
FR-2	Quản lý tài khoản người quản lý & giáo viên (CRUD).
FR-3	Quản lý khóa học theo lứa tuổi, ngôn ngữ; mở/đóng khóa.
FR-4	Tạo lớp với mã duy nhất, lịch học (nhiều buổi), học phí, trạng thái.
FR-5	Gán lớp cho giáo viên & phòng học, kiểm tra trùng lịch.
FR-6	Ghi danh học sinh, xử lý nhập học muộn, chuyển lớp, hoàn/thu thêm học phí.
FR-7	Quản lý phòng học; đảm bảo 1 phòng chỉ có 1 lớp tại một thời điểm.
FR-8	Điểm danh học sinh từng buổi; chấm công giáo viên, tính lương buổi.
FR-9	Duyệt bảng lương, import từ Excel, gửi email/Zalo cho giáo viên.
FR-10	Thu học phí, theo dõi công nợ, nhắc đóng học phí qua email/Zalo.
FR-11	Gửi nhận xét, link video cho học sinh sau mỗi buổi/kết thúc khóa.
FR-12	Xem dashboard & báo cáo (thống kê chi nhánh, lớp, học phí, công nợ…).
FR-13	Đăng nhập bằng email, quên/reset mật khẩu.
FR-14	Phân quyền theo vai trò (Admin/Quản lý/Giáo viên).
FR-15	Ghi nhật ký (audit log) cho các thao tác quan trọng.
2.4 Yêu cầu phi chức năng (Non-Functional Requirements)
Mã NFR	Mô tả
NFR-1	Phản hồi giao diện dưới 2 giây với tải trung bình; cache dữ liệu tĩnh.
NFR-2	Mật khẩu hash (bcrypt/argon2); bảo vệ CSRF/XSS; xác thực qua middleware.
NFR-3	Backup dữ liệu hàng ngày, chính sách khôi phục thảm họa.
NFR-4	Logging & monitoring tập trung, cảnh báo khi lỗi/bottleneck.
NFR-5	Tuân theo PSR-12, có unit/feature test; CI/CD tự động chạy test & deploy.
NFR-6	Hỗ trợ đa ngôn ngữ (vi/en) và chuẩn bị đa tiền tệ.
NFR-7	Kiến trúc mô-đun, dễ mở rộng thêm chi nhánh, tích hợp dịch vụ ngoài (CRM, cổng thanh toán).
NFR-8	Giao diện thân thiện, cung cấp hướng dẫn & thông báo lỗi rõ ràng bằng tiếng Việt.
2.5 Phụ lục

    Từ khóa:

        Chi nhánh: cơ sở đào tạo vật lý.

        Khóa học: chương trình đào tạo theo đối tượng/ngôn ngữ.

        Lớp: nhóm học viên theo lịch cụ thể.

    Vấn đề mở: lựa chọn nhà cung cấp cổng thanh toán, chuẩn liên kết Zalo, phạm vi portal phụ huynh.

3. Kết luận

Tài liệu trên thống nhất các yêu cầu nghiệp vụ và kỹ thuật cho hệ thống quản lý trung tâm ngoại ngữ đa chi nhánh. Đây là cơ sở để chuyển sang giai đoạn thiết kế chi tiết (Database schema, kiến trúc API/UI) và triển khai theo quy trình SDLC chuyên nghiệp.
