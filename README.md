# DEVYN FORWARDER — biểu mẫu gửi bài gọn

[**Tải ZIP mới tại đây**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-compact-send.zip)

Bỏ hai ô tên đợt và lịch gửi, ứng dụng tự đặt tên; bấm bắt đầu để gửi. Khoảng nghỉ giữa các nhóm là số giây cố định do bạn chọn. FloodWait được tôn trọng; SS bị hạn chế sẽ dừng. Chỉ gửi vào nhóm được phép. Khoảng nghỉ không bảo đảm tránh bị Telegram hạn chế.

Giữ **.env.docker và Docker volume**, giải nén đè vào đúng thư mục cũ, chạy **setup.cmd một lần**, rồi dùng **run.cmd**. Nếu sửa bản nháp cũ có lịch, lịch sẽ được xóa khi lưu. Các đợt đã tạo hàng đợi vẫn giữ lịch cũ.

[Hướng dẫn](HUONG_DAN_GUI_BAI_TU_LINK.md) · [Windows](HUONG_DAN_WINDOWS.md). Kiểm thử biểu mẫu 3/3 và build TypeScript/Vite thành công. ZIP không chứa session hay khóa riêng. SHA256 `6727bac0f4329f28e3991e18d29a69c35ea4fe856661495891766fe1469f22cc`.

## Bản trước

- [Gửi bài từ liên kết + TXT nhóm](devyn-forwarder-post-link-routes.zip)
- [Thời hạn hạn chế ngay trên dòng SS](devyn-forwarder-restriction-expiry.zip)
- [Check list proxy độc lập](devyn-forwarder-proxy-list-checker.zip)
- [API lưu một lần](devyn-forwarder-saved-api-settings.zip)
- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
