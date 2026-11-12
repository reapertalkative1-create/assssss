# Kiểm thử nhập SS kèm proxy — 12/11/2026

- Python: **38 passed, 23 skipped** trong `test_session_proxy_import`, `test_session_import`, `test_account_proxy`, `test_proxy_worker`, `test_proxy_export`. Các lượt PostgreSQL được bỏ qua vì chưa cấu hình TFCC_TEST_DATABASE_URL.
- Frontend: **76 passed**, 7 tệp; TypeScript/Vite production build thành công.
- API bắt buộc đủ proxy nếu require_proxy=true; thiếu/sai/trùng proxy hoặc proxy thuộc SS khác từ chối trước khi tạo SS/lệnh trong lô. Kiểm tra cả URL tương đương để phát hiện trùng.
- Session/API/proxy được lưu trước lệnh import; proxy mã hóa, worker được giao tài khoản đọc được cấu hình trước khi xử lý. Không lộ username/password trên bảng/audit/response import. SS trùng giữ nguyên proxy; file lỗi/SS trùng không làm lệch các vị trí phía sau.
- API + database + worker/client thật, chỉ Telegram là FakeBackend: lần connect đầu đã nhận đúng proxy; proxy lỗi làm lệnh thất bại, không connect trực tiếp; retry dùng lại đúng proxy. Không yêu cầu OTP khi nhập session.
- Web mặc định bật nhập kèm proxy, hỗ trợ TXT/dán, scheme mặc định, BOM/comment/dòng trống, từ chối thiếu/trùng trước tải. Có thể chủ động tắt proxy để giữ cách nhập cũ. Kiểm tra chia 101 SS thành 100 + 1 và danh sách proxy tương ứng không lặp/lệch.
- Lỗi tải lô sau không bị xóa bởi cập nhật tiến độ của lô trước.
- Chromium thật + API/SQLite + worker thật + FakeBackend: tải ZIP 3 session tổng hợp và TXT proxy, thiếu proxy không tạo request tải SS; kết nối đầu của từng session khớp đúng proxy theo hash session; cả 3 xác thực và check SpamBot giả thành công. Bảng tiến độ chỉ hiện địa chỉ proxy, không hiện password. Form vừa desktop 1365px và mobile 390px, không tràn ngang, không lỗi JS/HTTP 500.
- Giữ test proxy transport cục bộ SOCKS5/HTTP CONNECT + TLS, lọc/xuất alive/dead và quyền truy cập.

Không dùng session của người dùng hoặc kết nối/gửi Telegram thật. Không chạy PostgreSQL integration hoặc build sạch Docker/Windows ở đợt này. Không thêm dependency/migration; head vẫn 0010. Giữ launcher tự chọn cổng, nút Xóa đã chọn và tính năng proxy trước.

ZIP loại trừ session, khóa, .env riêng, database và runtime; gồm source và frontend dist đã build.
