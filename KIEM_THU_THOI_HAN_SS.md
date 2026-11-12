# Kiểm thử thời hạn hạn chế SS — 12/11/2026

- **70 kiểm thử Python qua** trong restriction_duration + spambot; **42 kiểm thử hồi quy qua** trong accounts_api + telegram_api_web + proxy_lists. Tổng 112 kiểm thử khác nhau; 51 lượt integration được loại bởi marker not integration and not telegram_live.
- **93 kiểm thử frontend qua**, 11 tệp; TypeScript/Vite production build qua.
- Nhận deadline English/VI ở các định dạng hỗ trợ, UTC/GMT và UTC offset; ngày ISO, tháng dài/ngắn, tháng May không bị nhầm với từ cảnh báo may. Cụm mở đầu I'm afraid/unfortunately được xử lý. Khoảng thời gian tương đối chỉ dùng mốc ngày tin nhắn có timezone, gồm 24 giờ.
- Vĩnh viễn cần phát biểu rõ cho tài khoản. Không suy diễn từ blocked/TOS/PHONE_NUMBER_BANNED/FROZEN hoặc thiếu deadline. Loại câu if/may/không bị, cảnh báo chung, ngày thiếu timezone/không hợp lệ/mơ hồ, các mốc xung đột; không dùng hạn kháng nghị/ngày xóa tài khoản.
- Không tái sử dụng hạn spam cũ cho đóng băng/ban RPC mới hoặc nhãn đóng băng thủ công. Khi check mới báo clear thì hết thông tin thời hạn; đọc được cache hợp lệ cũ không cần migration.
- API trả restriction_term/restriction_until cho bảng. Người vận hành nhận metadata thời hạn mà không nhận chat SpamBot riêng; kiểm thử quyền và bảo mật API cũ giữ nguyên.
- Giao diện hiển thị Vĩnh viễn / ngày-giờ / giờ-phút / Chưa rõ thời hạn. Đồng hồ cập nhật tại máy, tới hạn hiện Đã đến hạn · check lại và giữ nhãn hạn chế; không tự chuyển Live. Không hiện nguyên chat hay dòng Live phụ trên SS bị hạn chế.
- Chromium thật + API/SQLite, dữ liệu giả: kiểm tra 8 trường hợp trên bảng (permanent, ngày/giờ, giờ/phút, unknown, expired, appeal deadline, manual freeze, clear); tăng đồng hồ qua deadline vẫn giữ Bị spam và nhắc check lại. Tooltip/đếm ngược dùng mốc UTC và giờ Việt Nam. Desktop 1600px và mobile 390px không tràn trang. Nút check list proxy giữ nguyên. Không lỗi JS/HTTP 500.

Không dùng session người dùng hoặc gửi Telegram thật. Không chạy PostgreSQL integration hoặc build sạch Docker/Windows trong đợt này. Không thêm dependency/migration; head vẫn 0012. ZIP gồm source/dist, loại trừ session, .env riêng, khóa, database và runtime.
