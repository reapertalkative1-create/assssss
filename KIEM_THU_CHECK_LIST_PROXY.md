# Kiểm thử list proxy độc lập — 12/11/2026

- **10 kiểm thử mới** trong test_proxy_lists qua: tạo lô không có SS/API, canonical dedup, mã hóa và không lộ credential, ràng buộc worker/người tạo lô, quyền admin/CSRF, retry tạo idempotent, giới hạn nhận 10 probe và concurrent claim, lease hết hạn/nhận lại/token cũ, hủy và phản hồi muộn, lọc/phân trang/xuất đủ nhóm, cấu hình hỏng không bị tính Die, xuất lỗi không trả file dở, verify/rotate keys, report retry không probe lặp, tự chạy trong Runner không có AccountManager.
- **32 kiểm thử nền qua**: migrations, worker_runtime, saved_telegram_api, proxy_worker (bao gồm HTTP CONNECT/SOCKS5 + TLS cục bộ). Sau sửa đồng bộ claim, chạy lại test_proxy_lists + migrations: **12 passed, 9 deselected**. Tổng 42 kiểm thử Python khác nhau ở hai nhóm; không chạy PostgreSQL integration.
- **85 kiểm thử frontend qua**, 9 tệp: nút riêng hoạt động khi zero SS, tải TXT không gửi account/API, hai lượt tải Blob Live/Die, lọc nhóm, mở lại lô, dừng, lỗi nhập giữ list và khóa khi thiếu worker. Giữ các kiểm thử API tự lưu/SS+proxy/nút xóa trước.
- TypeScript/Vite production build qua.
- Migration 0012 khớp models; upgrade từ schema cũ giữ API đã mã hóa và proxy của SS, downgrade sạch.
- Chromium thật + API/SQLite + Runner/client/transport proxy thật: không có account/Telegram API; nhập TXT gồm HTTP CONNECT + SOCKS5 với authentication và TLS cục bộ, một proxy sai authentication và một cổng đóng, cộng một dòng trùng. Chỉ tạo 4 item: 2 Live + 2 Die. Tải thật hai file TXT, nội dung/credential/thứ tự đúng; lọc Live, đóng/mở lô gần đây, giao diện vừa 1440px/390px. Không lỗi JavaScript/HTTP 500.

Các proxy/TLS server của browser test chỉ chạy loopback, dùng CA thử riêng trong tiến trình worker; không kết nối Telegram thật và không sử dụng session/proxy của người dùng. Không chạy build sạch Docker/Windows hoặc PostgreSQL integration ở đợt này. Không thêm dependency. ZIP gồm source/dist, loại trừ session, .env riêng, khóa, database và runtime.
