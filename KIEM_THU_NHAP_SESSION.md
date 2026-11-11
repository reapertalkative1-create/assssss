# Kiểm thử nhập session hàng loạt — 11/11/2026

- Python: **269 passed, 138 deselected**, `pytest -q -m 'not integration and not telegram_live'`.
- Frontend: **45 passed** trong 6 tệp; TypeScript/Vite build thành công.
- Parser: tạo 100 SQLite session giả, nhập từ ZIP; chuyển đổi được Telethon StringSession đọc đúng auth key/DC/port. Kiểm tra ZIP lỗi, quá 100 file, không có session và đường dẫn trong ZIP; không giải nén ra ổ đĩa.
- API: nhập đủ 100 tài khoản trong một lô, lưu session/API pair mã hóa, bỏ qua trùng trong cùng/các lô đã nhập, trộn file lỗi với file đúng; kiểm tra RBAC/CSRF, trạng thái importing không được Bật, không có session trong audit/phản hồi/database dạng rõ.
- Worker: API/client/AccountManager thật với FakeBackend, nhập và xác thực session không dùng send_code/OTP; tối đa 3 kiểm tra cùng lúc ngay cả khi xếp 100 lệnh. Có thử lại và chặn thử sớm khi FloodWait.
- Migration 0006: nâng/hạ SQLite và so sánh schema với model thành công.
- Chromium thật + Vite + API/SQLite + worker thật/FakeBackend: tải ZIP chứa 3 session giả, tự chọn worker, nhập API pair, cả 3 authorized, không hỏi OTP, không có lỗi JavaScript.
- Chưa kiểm thử Telegram thật, biến thể PostgreSQL integration hoặc build sạch Docker image cho bản nhập session này. Không thêm dependency. setup.cmd trên máy người dùng sẽ nâng database và build API/web/worker từ mã nguồn mới.

File người dùng gửi chỉ được kiểm tra tên bảng/cột SQLite để nhận diện Telethon, không dùng kết nối Telegram. Mọi kiểm thử sử dụng auth key/session giả. Bản ZIP phát hành không chứa session người dùng, .env.docker, khóa hoặc database thử nghiệm.

Xem HUONG_DAN_NHAP_SESSION.md để cập nhật và sử dụng. Session hợp lệ được xác thực rồi giữ ở trạng thái Tắt; chưa tự chạy chuyển tiếp. Tốc độ thực tế phụ thuộc Telegram/mạng; không đảm bảo 100 session đều còn hiệu lực.
