# DEVYN FORWARDER — thời hạn hạn chế ngay trên dòng SS

[**Tải ZIP mới: thời hạn khóa / hạn chế**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-restriction-expiry.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để build API/web/worker. Sau đó dùng **run.cmd**. Không thêm migration, head vẫn **0012**.

Cột **Trạng thái** giữ nhãn Bị chặn / Bị spam / Đóng băng và thêm dòng gọn: **Vĩnh viễn**, **Còn 2 ngày 3 giờ**, **Còn 5 giờ 20 phút**, **Chưa rõ thời hạn** hoặc **Đã đến hạn · check lại**.

Chỉ hiện vĩnh viễn khi Telegram nói rõ; chỉ đếm ngược khi có hạn đủ rõ. Không suy diễn từ blocked/TOS/FROZEN/PHONE_NUMBER_BANNED, không dùng FloodWait, hạn kháng nghị hoặc ngày xóa tài khoản làm hạn mở khóa. Mốc tương đối dùng ngày của tin nhắn, không bắt đầu lại khi tải trang. Đếm ngược cập nhật mỗi phút; tới hạn vẫn giữ trạng thái hạn chế cho đến khi check mới xác nhận. Rê chuột xem mốc theo giờ Việt Nam.

Dữ liệu phản hồi đã lưu có thể dùng ngay; bấm Check spam / đóng băng để lấy kết quả mới khi chưa đủ dữ liệu. Không hiện nguyên chat trên bảng. Bỏ dòng Live phụ ở tài khoản bị hạn chế. Người vận hành nhận metadata thời hạn, không nhận chat riêng.

[Hướng dẫn](HUONG_DAN_THOI_HAN_SS.md) · [Kiểm thử](KIEM_THU_THOI_HAN_SS.md) · [Windows](HUONG_DAN_WINDOWS.md)

112 kiểm thử Python liên quan, 93 frontend và production build qua. Chromium + API/SQLite với dữ liệu giả xác nhận các nhóm thời hạn, phân biệt hạn kháng nghị, tăng đồng hồ qua deadline vẫn yêu cầu check lại, desktop/mobile không tràn trang, không lỗi JS/HTTP 500. Không dùng session người dùng hoặc Telegram thật; không chạy PostgreSQL integration hoặc build sạch Docker/Windows ở đợt này.

Giữ nút riêng check list proxy và xuất Live/Die, SS+proxy cùng lúc, API tự lưu trong Cài đặt, nút đỏ Xóa đã chọn và tự chọn cổng web.

ZIP gồm source/dist; không có session, khóa, .env riêng hoặc database. SHA256: `656e221d28159fb5ecb9f8ec8f10f46c936f817417fd7f056d84e582655e33c5`.

## Bản trước

- [Check list proxy độc lập](devyn-forwarder-proxy-list-checker.zip)
- [API lưu một lần](devyn-forwarder-saved-api-settings.zip)
- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
