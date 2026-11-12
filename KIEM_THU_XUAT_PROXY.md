# Kiểm thử lọc/xuất proxy và nút xóa — 12/11/2026

- Python liên quan: **31 passed, 20 deselected**, nhóm proxy_export, account_proxy, account_bulk, blocked_stats với marker not integration and not telegram_live.
- Frontend: **71 passed**, 7 tệp; TypeScript/Vite production build qua.
- API lọc alive/dead/unknown đúng, bỏ SS chưa có proxy khỏi nhóm chưa check; bộ lọc được chuyển tới thao tác hàng loạt. Xuất toàn bộ kết quả, không bị phân trang.
- Hai file TXT riêng, canonical URL giữ credential và nhập lại được. Nhóm sống/die do nút xuất quyết định; vẫn giữ các bộ lọc SS khác. Không xuất unknown/checking hoặc dòng đang xóa.
- Export chỉ admin, response no-store và Content-Disposition đúng; không có credential trong bảng/audit. Giải mã lỗi trả lỗi trước khi trả file, không lộ nội dung đã giải mã ở những dòng trước đó.
- Client tải Blob bằng session cùng origin và giữ xử lý lỗi API; menu báo nhóm rỗng, đóng bằng Escape/chạm ngoài và vừa màn hình.
- Xóa là nút đỏ trực tiếp, khóa khi chưa chọn, bật khi chọn; không còn lựa chọn Xóa lặp trong menu. Unit và Chromium xác nhận một lần bấm tạo đúng lệnh xóa, không modal/nhập xác nhận.
- Chromium + API/SQLite với dữ liệu giả: lọc proxy sống/die/chưa check, tải thật hai file TXT với nội dung đúng, chuyển bộ lọc proxy vào check hàng loạt, xóa đúng một SS giả; menu xuất trên tablet 1000px và mobile 390px không tràn ngang. Không lỗi JS/HTTP 500.

Màu/trạng thái proxy trong browser là fixture giả, không phải thử proxy người dùng. Proxy check transport không thay đổi, các báo cáo proxy trước mô tả test tunnel cục bộ HTTP/SOCKS5 + TLS. Không sử dụng session người dùng/gửi Telegram thật. Không chạy PostgreSQL integration toàn bộ hoặc build sạch Docker Windows ở đợt này. Không thêm dependency/migration.

ZIP loại trừ session, .env riêng, khóa, database, file xuất và runtime. Giữ launcher tự chọn cổng.
