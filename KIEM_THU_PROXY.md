# Kiểm thử proxy — 12/11/2026

- Python local: **345 passed, 178 deselected**, `pytest -q -m 'not integration and not telegram_live'`.
- Sau khi tăng kiểm tra xác thực tunnel: nhóm test_proxy_worker **5 passed**, cùng 5 trường hợp chồng lặp với bộ trên, không cộng thành tổng mới.
- Frontend: **65 passed**, 7 tệp; TypeScript/Vite production build thành công.
- Migration 0010 nâng lên head, so khớp model và hạ về base trên SQLite: qua trong bộ kiểm thử.
- Proxy parser: host:port, host:port:user:password, SOCKS/HTTP URL, IPv6, BOM, ký tự đặc biệt, dedup; từ chối dòng sai mà không chép credential vào thông báo lỗi.
- API: gán riêng từng SS, thiếu proxy không gán dở, chống dùng trùng ngoài lựa chọn, phạm vi lọc/bỏ tích, CSRF/RBAC, mã hóa và xoay khóa; worker khác không đọc được secret.
- Proxy check không cần Telegram session/API ID. Kết quả không đổi health/auth của session; kết quả cũ không ghi đè sau khi đổi proxy.
- Worker: gắn proxy vào backend Telethon, không fallback trực tiếp khi đọc proxy lỗi. Luồng API/client/AccountManager với FakeBackend đổi proxy khi đang chạy: kết nối cũ được đóng, kết nối mới dùng proxy mới, không mở hai kết nối cùng auth key.
- Kiểm tra tunnel thật cục bộ HTTP CONNECT + SOCKS5 có username/password và bắt tay TLS tới server thử nghiệm có chứng chỉ đúng hostname. Không gọi Telegram thật trong các ca này.
- Chromium thật với API/SQLite và dữ liệu giả: tải .txt cho 2 SS đã tích, giữ SS ngoài lựa chọn; dán để gán toàn bộ 6 SS; tạo lệnh check riêng/hàng loạt; không lộ mật khẩu trên dòng. Màu xanh/đỏ/trắng dùng fixture hiển thị và kiểm tra CSS thực. Dialog mobile 390px không tràn ngang toàn trang; không lỗi JavaScript/HTTP 500.

Không sử dụng session người dùng hoặc gửi Telegram thật. Chưa kiểm chứng proxy thương mại của người dùng, mọi loại auth/proxy, MTProto datacenter thực, PostgreSQL integration toàn bộ hoặc build sạch Docker Windows. Kết quả xanh xác nhận đường hầm và TLS HTTPS Telegram, không bảo đảm mọi thao tác Telegram thành công. SOCKS4 dựa trên hỗ trợ thư viện; hai ca tunnel thật là HTTP và SOCKS5.

ZIP loại trừ .env riêng, session, database, khóa và runtime; chứa migration 0010, launcher tự chọn cổng và source/web dist.
