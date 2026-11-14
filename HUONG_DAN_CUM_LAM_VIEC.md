# Cụm làm việc — DEVYN FORWARDER

## Cập nhật

Giữ `.env.docker` và Docker volume. Giải nén đè đúng thư mục ứng dụng cũ, chạy **setup.cmd** một lần để build và nâng database **0016**, rồi **run.cmd**. Trên web nhấn **Ctrl+F5**. Không xóa volume hoặc tạo lại cấu hình môi trường.

## Tạo cụm một lần

1. Mở **Tuyến chuyển tiếp → Cụm làm việc → + Tạo cụm làm việc**.
2. Đặt **Tên cụm làm việc**, ví dụ “Khách hàng miền Nam”.
3. Chọn SS từ tài khoản Telegram; có bộ lọc, nhóm tài khoản, chọn cả trang/kết quả hoặc SS đã tích như trước.
4. Tải TXT hoặc dán nhóm nhận, chọn cách gửi và thời gian nghỉ. Bấm **Tạo cụm**.

Chưa cần nhập bài viết khi tạo cụm. Cụm lưu trong cơ sở dữ liệu cùng ứng dụng, không hết hạn 7 ngày như bản nhập tạm. Đóng trình duyệt hoặc khởi động lại ứng dụng vẫn còn cụm.

## Hôm nay bài này, ngày mai bài khác

Trên thẻ cụm, bấm **Bài mới**, dán link bài và bấm **Tạo lượt gửi**. Tool dùng các SS, nhóm nhận và cấu hình đã lưu. Trong lượt mới, bấm **Kiểm tra tất cả**, xem kết quả rồi **Bắt đầu SS đã đạt**.

Ngày mai mở lại chính cụm đó, bấm **Bài mới** và dán link khác. Mỗi bài là một lượt độc lập, có tiến độ và kết quả riêng. **Lịch sử → Mở lượt** để kiểm tra hoặc tiếp tục lượt cũ.

Tạo cụm và tạo lượt chưa gửi Telegram. Cơ chế giữ SS phụ trách nhóm, chống gửi trùng, chờ FloodWait và dừng khi SS/proxy bị hạn chế vẫn hoạt động. SS lỗi có thể lưu trong cấu hình; chỉ SS đáp ứng kiểm tra mới bắt đầu gửi.

## Quản lý gọn trên thẻ cụm

- Thẻ hiển thị tên, số SS, số nhóm nhận, thời gian nghỉ và cách gửi.
- **Bài mới**: nhập link mới, không nhập lại danh sách SS/nhóm.
- **Lịch sử**: xem các bài đã tạo trong cụm, mở đúng lượt cần thao tác.
- **••• → Sửa tên & cấu hình**: đổi tên, SS, nhóm nhận, thời gian nghỉ hoặc cách gửi. Chỉ các lượt tạo sau đó dùng thay đổi này.
- **••• → Xóa cụm**: xóa cấu hình, giữ SS và lượt gửi đã có. Lượt đang chạy tiếp tục; vẫn truy cập được ở **Lịch sử / tuyến**.
- Ô tìm kiếm lọc theo tên cụm. Tài khoản vận hành chỉ xem; quản trị viên tạo/sửa/xóa cụm.

Lựa chọn SS được lưu bằng danh sách cụ thể. Khi đổi thành viên nhóm tài khoản, cần sửa cụm để cập nhật các SS tương ứng. Nếu SS bị xóa, tool báo và yêu cầu bỏ SS đó khỏi cấu hình trước khi tạo lượt; không tự chuyển việc sang tài khoản khác.

Biểu mẫu tạo/sửa cụm và ô link Bài mới có tự lưu tạm trong cùng trình duyệt 7 ngày. Bản tạm tách riêng từng cụm/phiên bản cấu hình/người đăng nhập, không chứa session, API hash hay mật khẩu. Khi cấu hình đã được sửa ở cửa sổ khác, mở lại để lấy phiên bản mới trước khi lưu/chạy. Thử lại yêu cầu tạo lượt không đổi sau khi mất phản hồi sẽ lấy lượt đã tạo, không nhân đôi.

Các tuyến cũ và gửi bài lẻ nằm trong tab **Lịch sử / tuyến**. Cụm làm việc không tự đặt lịch theo ngày; mỗi bài mới do bạn chủ động tạo và bắt đầu.
