# DEVYN FORWARDER — tự chọn cổng web

[**Tải ZIP mới: sửa lỗi port 8787 already allocated**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-auto-port-fix.zip)

Giữ **.env.docker và Docker volume**, giải nén đè toàn bộ ZIP vào **đúng thư mục cài đặt cũ**, mở Docker Desktop rồi chạy **setup.cmd lại**. Những lần sau dùng **run.cmd**. Không thêm migration; head vẫn **0009**.

## Sửa lỗi cổng

Build thành công nhưng web không khởi động được khi cổng 8787 bị ứng dụng/container khác giữ. Launcher mới:

- Kiểm tra binding Docker và khả năng bind loopback; tự chọn cổng trống và lưu vào .env.docker.
- Giữ cổng nếu thuộc chính web cùng project; không dừng container của bản cài khác.
- Nếu có xung đột phát sinh lúc khởi động, chọn lại cổng và thử lại, tối đa 3 lần. Lỗi API/database khác vẫn được báo đúng.
- Mở đúng địa chỉ thực tế ở dòng **Application running**, ví dụ http://127.0.0.1:8788; API allowed origins dùng cùng cổng.
- Giữ project, admin, khóa, credential và dữ liệu; không xóa volume.

Vẫn giữ bản UI mới: thông tin, phản hồi SpamBot, tiến độ và lỗi ngay trên dòng SS; không có khung Tác vụ hàng loạt phía dưới.

[Hướng dẫn cổng](HUONG_DAN_TU_CHON_CONG.md) · [Kiểm thử](KIEM_THU_TU_CHON_CONG.md) · [Windows](HUONG_DAN_WINDOWS.md) · [Bảng SS](HUONG_DAN_BANG_SS.md)

Kiểm thử PowerShell 7.4.6 trên Linux: socket bị chiếm thật, Docker binding/own listener, giữ cấu hình/khóa, lỗi cổng lúc startup và giới hạn retry; bộ hồi quy setup/run qua. Docker Compose config kiểm tra cổng web và API origins nhất quán. Chưa chạy trực tiếp Windows PowerShell 5.1/Docker Desktop của người dùng. ZIP không chứa session, khóa, .env.docker hoặc database cá nhân.

SHA256: `c51702216f15684f61eb5e56966604eab4186116bf2fffa996a9b725009fb69c`.

## Bản trước

- [Thông tin trực tiếp trên bảng SS](devyn-forwarder-inline-session-details.zip)
- [Nút check spam / đóng băng](devyn-forwarder-spam-frozen-check.zip)
- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
- [SpamBot / kháng nghị](telegram-forwarder-control-center-spam-check-appeal.zip)
- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
