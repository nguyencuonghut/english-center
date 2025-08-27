Sơ đồ luồng dữ liệu

Hệ thống quản lý trung tâm ngoại ngữ (LCMS)
1. Sơ đồ ngữ cảnh (Context Diagram)

flowchart LR
    subgraph External Entities
        A(Admin)
        M(Quản lý)
        T(Giáo viên)
        S(Học sinh/Phụ huynh)
        PG(Cổng thanh toán)
        ES(Dịch vụ Email/Zalo)
    end

    LCMS[[Hệ thống LCMS]]

    A <--> LCMS
    M <--> LCMS
    T <--> LCMS
    S <--> LCMS
    PG <--> LCMS
    ES <--> LCMS

Luồng dữ liệu chính

    Admin: Quản lý cấu hình hệ thống, người dùng, duyệt lương, báo cáo tổng.

    Quản lý: Quản lý chi nhánh, lớp, giáo viên, thu học phí, gửi nhắc.

    Giáo viên: Điểm danh, ghi nhận xét, xem lương.

    Học sinh/Phụ huynh: Nhận thông báo, xem lịch/nhận xét.

    Cổng thanh toán: Ghi nhận thu học phí online.

    Dịch vụ Email/Zalo: Gửi thông báo, bảng lương.

2. DFD cấp 0 (Level‑0)

flowchart TB
    subgraph External Entities
        A(Admin)
        M(Quản lý)
        T(Giáo viên)
        S(Học sinh)
        PG(Cổng thanh toán)
        ES(Dịch vụ Email/Zalo)
    end

    subgraph Data Stores
        DS1[(User & Role)]
        DS2[(Branch)]
        DS3[(Course & Class)]
        DS4[(Room)]
        DS5[(Student & Enrollment)]
        DS6[(Attendance & Payroll)]
        DS7[(Transaction)]
    end

    P1[1. Quản lý chi nhánh & người dùng]
    P2[2. Quản lý khóa học & lớp học]
    P3[3. Ghi danh & học phí]
    P4[4. Chấm công & lương]
    P5[5. Thông báo & báo cáo]

    A --> P1
    M --> P1
    P1 --> DS1
    P1 --> DS2
    P1 --> A
    P1 --> M

    M --> P2
    P2 --> DS3
    P2 --> DS4

    S --> P3
    PG --> P3
    P3 --> DS5
    P3 --> DS7
    P3 --> S
    P3 --> PG

    T --> P4
    M --> P4
    P4 --> DS6
    P4 --> T
    P4 --> M
    P4 --> ES

    A --> P5
    M --> P5
    P5 --> ES
    P5 --> A
    P5 --> M
    P5 --> T
    P5 --> S

Mô tả quy trình chính

    Quản lý chi nhánh & người dùng

        Admin & Quản lý tạo/duyệt tài khoản, gán chi nhánh.

        Dữ liệu lưu tại User & Role, Branch.

    Quản lý khóa học & lớp học

        Quản lý thiết lập khóa, lớp, phòng; kiểm tra trùng lịch.

        Dữ liệu lưu tại Course & Class, Room.

    Ghi danh & học phí

        Quản lý/thu ngân đăng ký học viên, thu học phí (qua PG hoặc tiền mặt).

        Dữ liệu lưu tại Student & Enrollment, Transaction.

    Chấm công & lương

        Giáo viên điểm danh, Quản lý chấm công, Admin duyệt lương & gửi email.

        Dữ liệu lưu tại Attendance & Payroll.

    Thông báo & báo cáo

        Hệ thống gửi nhắc học phí, nhận xét, dashboard; sử dụng Email/Zalo.

        Không gian lưu dữ liệu: các kho trên kết hợp.

3. DFD cấp 1 (chi tiết các quy trình chính)
3.1 Quản lý chi nhánh & người dùng

flowchart LR
    A(Admin) --> P1_1[1.1 Tạo/Phân quyền]
    M(Quản lý) --> P1_2[1.2 Cập nhật chi nhánh]
    P1_1 --> DS1[(User & Role)]
    P1_2 --> DS2[(Branch)]
    DS1 --> P1_1
    DS2 --> P1_2

    1.1: Admin tạo tài khoản, gán vai trò, reset mật khẩu.

    1.2: Quản lý cập nhật thông tin chi nhánh của mình.

3.2 Quản lý khóa học & lớp học

flowchart LR
    M --> P2_1[2.1 Tạo khóa học]
    M --> P2_2[2.2 Tạo lớp]
    P2_1 --> DS3[(Course)]
    P2_2 --> DS3
    P2_2 --> DS4[(Room)]
    DS4 --> P2_2

    2.1: Quản lý thêm/sửa/xóa khóa học.

    2.2: Tạo lớp; kiểm tra phòng học & lịch trống.

3.3 Ghi danh & học phí

flowchart LR
    S(Học sinh) --> P3_1[3.1 Đăng ký]
    P3_1 --> DS5[(Student & Enrollment)]
    P3_1 --> P3_2[3.2 Tính/Thu học phí]
    PG --> P3_2
    P3_2 --> DS7[(Transaction)]
    P3_2 --> PG
    P3_2 --> S

    3.1: Nhập thông tin học sinh, gán lớp.

    3.2: Tính học phí theo buổi còn lại hoặc chuyển lớp, ghi nhận transaction.

3.4 Chấm công & lương

flowchart LR
    T --> P4_1[4.1 Điểm danh học sinh]
    M --> P4_2[4.2 Chấm công giáo viên]
    A --> P4_3[4.3 Duyệt & gửi lương]
    P4_1 --> DS6[(Attendance)]
    P4_2 --> DS6
    P4_3 --> DS6
    P4_3 --> ES(Email/Zalo)
    ES --> T

    4.1: Giáo viên điểm danh từng buổi.

    4.2: Quản lý xác nhận buổi dạy, định mức lương.

    4.3: Admin phê duyệt, gửi bảng lương.

3.5 Thông báo & báo cáo

flowchart LR
    P5_1[5.1 Gửi thông báo] --> ES
    P5_2[5.2 Tổng hợp báo cáo] --> A
    P5_2 --> M
    P5_1 --> S
    P5_1 --> T

    5.1: Hệ thống (qua Scheduler/Queue) gửi nhắc học phí, nhận xét, link video.

    5.2: Tổng hợp dữ liệu từ các kho, hiển thị dashboard.

4. Dữ liệu chính (Data Stores)
Mã	Tên kho dữ liệu	Nội dung chính
DS1	User & Role	thông tin tài khoản, vai trò
DS2	Branch	tên, địa chỉ, manager_id
DS3	Course & Class	khóa học, lớp, lịch học, trạng thái
DS4	Room	mã phòng, sức chứa
DS5	Student & Enrollment	thông tin học sinh, ghi danh, lịch sử chuyển lớp
DS6	Attendance & Payroll	điểm danh, chấm công, bảng lương
DS7	Transaction	thu/chi học phí, lương, các khoản khác
5. Tóm tắt

Tài liệu DFD trên mô tả toàn bộ luồng dữ liệu từ các tác nhân ngoại vi (Admin, Quản lý, Giáo viên, Học sinh/Phụ huynh, Cổng thanh toán, Dịch vụ Email/Zalo) vào hệ thống LCMS, qua các quy trình chính, và lưu trữ vào các kho dữ liệu tương ứng. Kiến trúc này giúp hệ thống mở rộng cho nhiều chi nhánh, hỗ trợ nghiệp vụ đào tạo, thu chi và báo cáo một cách chuyên nghiệp, minh bạch.
