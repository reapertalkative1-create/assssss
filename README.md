# DEVYN FORWARDER — nhãn xanh/đỏ và lý do lỗi

[**Tải ZIP mới: trạng thái rõ ràng trên bảng SS**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-status-colors.zip)

Giữ **.env.docker và Docker volume**, giải nén đè toàn bộ ZIP vào **đúng thư mục cài đặt cũ**, mở Docker Desktop rồi chạy **setup.cmd một lần**; sau đó dùng **run.cmd**. Giữ launcher tự chọn cổng trống. Không thêm migration; head vẫn **0009**.

## Trạng thái & lý do

Bảng SS không còn chép nguyên đoạn chat SpamBot. Thay bằng nhãn màu và lý do ngắn bằng tiếng Việt:

- **Xanh**: Không bị hạn chế spam.
- **Đỏ**: Tài khoản bị chặn / Bị hạn chế spam / Đóng băng / Bị khóa / Session hết hiệu lực, có lý do riêng.
- **Vàng**: Chưa xác định hoặc kiểm tra chưa thành công; không tự kết luận an toàn hay tài khoản chết.
- **Xám**: Chưa kiểm tra.

Thông báo trong ảnh “Your account was blocked for violations of the Telegram Terms of Service…” được hiển thị thành **Tài khoản bị chặn**, kèm lý do Telegram báo vi phạm điều khoản; dữ liệu cũ unknown vẫn hiển thị đúng. Những lần check mới ghi limited để dùng bộ lọc Bị spam. Dữ liệu cũ cần check lại để cập nhật bộ đếm/bộ lọc lưu trên máy chủ.

Giữ thời gian check, tình trạng session, FloodWait, tiến độ và lỗi ngay trên từng dòng; không có khung Tác vụ hàng loạt. Cửa sổ SpamBot/kháng nghị vẫn giữ hội thoại để tương tác đúng bước khi cần.

[Hướng dẫn](HUONG_DAN_TRANG_THAI_MAU.md) · [Kiểm thử](KIEM_THU_TRANG_THAI_MAU.md) · [Windows](HUONG_DAN_WINDOWS.md)

62 kiểm thử frontend, 30 kiểm thử SpamBot và production build qua. Chromium kiểm tra màu xanh/đỏ thực, lý do tiếng Việt, không có nguyên văn bot trên bảng, sáng/tối và mobile bằng dữ liệu giả. Không dùng session người dùng/gửi Telegram thật. ZIP không chứa session, khóa, .env.docker hoặc database cá nhân.

SHA256: `6cda1e45bcde2de66f4726895630cc84b4d07c8627a318518d4986caa145e1fa`.

## Bản trước

- [Tự chọn cổng web](devyn-forwarder-auto-port-fix.zip)
- [Thông tin trực tiếp trên bảng SS](devyn-forwarder-inline-session-details.zip)
- [Nút check spam / đóng băng](devyn-forwarder-spam-frozen-check.zip)
- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
- [SpamBot / kháng nghị](telegram-forwarder-control-center-spam-check-appeal.zip)
- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
