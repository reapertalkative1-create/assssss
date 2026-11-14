# Kiểm thử cụm làm việc — 14/11/2026

- **38** kiểm thử Python/SQLite đạt: cụm, parser danh sách, nhiều SS, giữ SS phụ trách nhóm, chống trùng, FloodWait và hồi quy gửi bài từ link.
- **15** kiểm thử PostgreSQL đạt: cụm, lịch sử/snapshot, retry, quyền truy cập và cơ chế bảo vệ gửi bài.
- **4** kiểm thử migration SQLite đạt; PostgreSQL **0015 → 0016** giữ session, API và tuyến cũ, lưu được cụm mới, schema khớp model. Downgrade về 0015 chỉ bỏ bảng cụm.
- **118** kiểm thử frontend hiện có và **5** kiểm thử cụm mới đạt. TypeScript/Vite production build đạt.
- Chromium + API: tạo 3 cụm qua TXT/SS đã chọn, tải lại vẫn còn; link bài chưa lưu được khôi phục; tạo bài 123 rồi sửa tên/cấu hình và tạo bài 124. Lượt cũ giữ 12 nhóm/90 giây, lượt mới 20 nhóm/120 giây; mở đúng lượt từ lịch sử.
- Trình duyệt kiểm tra giao diện sáng/tối, desktop 1500px/mobile 390px; menu thao tác hiển thị đủ trên mobile; không lỗi JavaScript/HTTP 500.
- Kiểm tra SS đã xóa, tên trùng, lỗi nhóm có số dòng, CSRF/role, sửa đồng thời bằng phiên bản, retry sau mất phản hồi và xóa cụm giữ SS/lượt gửi.

Dữ liệu kiểm thử giả lập. Không kết nối Telegram thật, không gửi bài thật. Kiểm thử trình duyệt chỉ tạo bản nháp và xác nhận không có tác vụ gửi. Launcher tiếp tục chạy Alembic tới `head`, không thay đổi cơ chế Windows/Docker của bản trước.
