# Kiểm thử ô thống kê — 12/11/2026

- Python liên quan: **49 passed, 23 deselected**, nhóm blocked_stats, spambot, account_bulk, health, health_ready với marker not integration and not telegram_live.
- Frontend: **66 passed**, 7 tệp; production build TypeScript/Vite qua.
- Tách blocked khỏi limited, nhận đúng thông báo Telegram, không nhận câu điều kiện. Khôi phục dữ liệu mã hóa cũ idempotent; không đoán khi không giải mã được.
- Summary đếm đúng trên toàn bộ dữ liệu, lọc blocked có phân trang và phạm vi bulk + bỏ tích đúng; giữ frozen và generic spam riêng.
- Frontend có đúng 6 ô, không FloodWait/Lỗi kiểm tra hoặc chú thích bên dưới. Bấm blocked/frozen/all gửi bộ lọc đúng; nhóm có số 0 không bị hiển thị thành dấu gạch.
- Chromium thật + API/SQLite với dữ liệu giả: startup tự khôi phục 2 SS blocked từ limited/unknown cũ, số đếm và lọc qua các ô đúng, ô desktop cao 48px; sáng/tối và viewport 390px không tràn ngang toàn trang, mobile 3 hàng gọn. Không lỗi JavaScript/HTTP 500.

Không sử dụng session người dùng hoặc gửi Telegram thật. Không thay database schema/dependency/proxy transport/launcher. Chưa chạy PostgreSQL integration toàn bộ hoặc build sạch Docker Windows ở đợt này. ZIP không chứa session, khóa, .env riêng hay database runtime.
