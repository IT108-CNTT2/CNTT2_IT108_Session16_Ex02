# BÁO CÁO: PHÂN QUYỀN VÀ XỬ LÝ CHIA SẺ SAI QUYỀN

## 1. Mục tiêu

- Phân biệt và sử dụng đúng 3 quyền **Viewer**, **Commenter**, **Editor**.
- Kiểm tra người có quyền truy cập để hạn chế lộ thông tin ứng viên.
- Biết cách xử lý khi vô tình chia sẻ tệp cho người ngoài.

## 2. Phân tích tình huống

Startup đang lưu danh sách CV có **số điện thoại** và **mức lương kỳ vọng**. Đây là thông tin riêng tư, không nên chia sẻ công khai.

Trưởng phòng nhân sự muốn các trưởng bộ phận xem và góp ý, nhưng một nhân viên đã gửi nhầm liên kết có quyền **Editor** cho ứng viên bên ngoài. Người nhận có thể chỉnh sửa tệp nếu liên kết còn hiệu lực, và có nguy cơ xem hoặc sao chép dữ liệu.

## 3. Bản thiết kế phân quyền

| Đối tượng | Quyền phù hợp | Lý do |
|---|---|---|
| Trưởng phòng nhân sự | **Editor** | Quản lý và cập nhật danh sách ứng viên. |
| Nhân viên nhân sự được giao quản lý | **Editor** | Nhập và sửa thông tin theo nhiệm vụ. |
| Trưởng các bộ phận | **Commenter** | Xem và nhận xét, không sửa trực tiếp dữ liệu gốc. |
| Nhân viên chỉ cần xem báo cáo | **Viewer** | Chỉ xem phần thông tin được phép. |
| Ứng viên bên ngoài | **Không cấp quyền** | Không được xem danh sách CV của người khác. |

**Lưu ý:** Nếu không cần xem số điện thoại hay mức lương, nên tạo bản danh sách đã ẩn các cột nhạy cảm để chia sẻ thay vì cấp quyền vào tệp gốc.

### Quy tắc Cờ Đỏ Bảo mật

Em đề xuất kiểm tra ngay khi thấy các dấu hiệu sau:

- **Cờ đỏ 1:** Tệp chứa thông tin cá nhân nhưng đang bật chế độ **Anyone with the link** (ai có liên kết cũng truy cập được).
- **Cờ đỏ 2:** Người ngoài công ty có quyền **Editor**.
- **Cờ đỏ 3:** Người chỉ cần nhận xét lại có quyền sửa dữ liệu gốc.

Cách khắc phục: chuyển tệp sang **Restricted** (chỉ người được thêm mới truy cập), xóa người lạ và cấp lại quyền theo đúng nhiệm vụ.

## 4. Cách sử dụng Suggesting Mode

Nếu danh sách ứng viên được trình bày trong **Google Docs**, trưởng bộ phận có thể dùng chế độ **Suggesting** để đề xuất sửa nội dung. Thay đổi chỉ được áp dụng khi người quản lý chấp nhận.

**Cách thực hiện:** Mở Google Docs → chọn chế độ **Suggesting (Đề xuất)** → nhập nội dung muốn sửa → trưởng phòng nhân sự xem và chấp nhận hoặc từ chối.

**Chú ý:** Quyền **Commenter** cho phép góp ý và đề xuất trong Google Docs. Nếu danh sách nằm trong **Google Sheets**, không có chế độ Suggesting giống Google Docs; nên dùng **Comment (Nhận xét)** và để nhân sự tự cập nhật dữ liệu sau khi duyệt.

## 5. Kịch bản xử lý sự cố trong 3 bước

### Bước 1: Thu hồi quyền ngay

- Mở tệp trên Google Drive → chọn **Share (Chia sẻ)**.
- Đổi **General access** thành **Restricted** để vô hiệu hóa đường liên kết công khai.
- Trong danh sách người có quyền, **Remove access (Xóa quyền truy cập)** của ứng viên bên ngoài, rồi lưu thay đổi.
- Kiểm tra lại xem ứng viên có quyền qua nhóm hoặc thư mục dùng chung hay không; nếu có, phải gỡ quyền ở nguồn đó nữa.

### Bước 2: Kiểm tra lịch sử và mức độ ảnh hưởng

- Xem danh sách người được chia sẻ và lịch sử hoạt động của tệp.
- Kiểm tra **Version History** để phát hiện nội dung bị chỉnh sửa và khôi phục bản đúng nếu cần.
- Nếu công ty dùng Google Workspace và có quyền quản trị phù hợp, nhờ quản trị viên kiểm tra **Drive audit log** để tìm các sự kiện truy cập, tải xuống hoặc sao chép được hệ thống ghi nhận.
- Ghi lại thời điểm chia sẻ nhầm, tài khoản nhận và những sự kiện tìm được.

**Quan trọng:** Không phải tài khoản nào cũng xem được nhật ký chi tiết. Việc không thấy sự kiện tải xuống **không chứng minh** rằng người ngoài chưa xem, chụp màn hình hay sao chép dữ liệu. Nếu không xác minh được, cần báo cho người phụ trách bảo mật và xử lý như một nguy cơ rò rỉ thông tin.

### Bước 3: Khắc phục và phòng tránh tái diễn

- Nếu có sửa sai, dùng **Version History** để khôi phục phiên bản ổn định.
- Chỉ chia sẻ cho đúng email nội bộ, ưu tiên quyền **Viewer** hoặc **Commenter**.
- Tắt chia sẻ công khai và hạn chế quyền tải xuống/sao chép khi tính năng này được hỗ trợ; biện pháp này không ngăn được mọi cách ghi lại thông tin.
- Kiểm tra quyền truy cập định kỳ và hướng dẫn nhân viên kiểm tra người nhận trước khi gửi liên kết.

## 6. Kết luận

Qua tình huống này, em hiểu rằng không nên cấp quyền **Editor** cho tất cả mọi người. Mỗi người chỉ nên có quyền vừa đủ để làm việc. Khi gửi nhầm liên kết, cần **thu hồi quyền ngay**, **kiểm tra lịch sử hoạt động** và **thiết lập lại quyền an toàn**. Đặc biệt, dữ liệu cá nhân của ứng viên phải được bảo vệ cẩn thận.
