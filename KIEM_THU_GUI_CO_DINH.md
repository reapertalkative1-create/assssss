# Kiểm thử gửi bài cố định — 14/11/2026

- **87** kiểm thử Python đạt: hàng đợi, route, worker, phân công, bộ chọn, proxy và migration. Sau chỉnh hoàn tất đợt không bật lại SS khi hết việc, chạy lại **20** kiểm thử gửi bài liên quan đều đạt.
- **47** kiểm thử PostgreSQL đạt, gồm chèn đồng thời chống trùng, phân công cố định, FloodWait ba ngày, lỗi proxy và đối chiếu kết quả. Dùng database/role riêng, không dùng database ứng dụng.
- **111** kiểm thử frontend đạt; production build TypeScript/Vite đạt.
- Migration SQLite: schema khớp model, nâng/hạ được, nâng dữ liệu cũ 0014 giữ lịch sử gửi và phân công. Kiểm tra riêng PostgreSQL 0014 → 0015 với một đợt đã gửi thành công cũng đạt và schema khớp model.
- Quy mô dữ liệu giả lập: 1.000 SS được chọn, 200 nhóm tạo đúng 200 phân công và 800 SS không nhận việc. Lưu nháp không tạo job gửi.
- Trình duyệt Chromium với API và worker thật, backend Telegram giả lập: gửi hai nhóm, tạo đợt cùng bài lần nữa bỏ qua cả hai; lỗi mạng sau lần gửi giả lập làm đợt tạm dừng, đối chiếu “Đã gửi” không gọi gửi lại.
- Desktop 1600px và mobile 390px không tràn ngang; không lỗi JavaScript/HTTP 500 trong luồng trình duyệt.
- PowerShell: bộ kiểm thử launcher và chọn cổng đạt; đã kiểm tra thứ tự dừng worker → dừng API/web → migration, giữ khóa/admin khi chạy lại.
- Kiểm tra nguồn ZIP không chứa dữ liệu riêng, session, `.env.docker` hoặc khóa. Giữ BOM của PowerShell để Windows đọc tiếng Việt đúng.

Không gửi hoặc kết nối Telegram thật. Kiểm thử số lượng SS là dữ liệu mô phỏng, không phải thử tải 1.000 kết nối Telegram đồng thời. Kiểm thử launcher dùng PowerShell trên Linux với Docker được giả lập; chưa chạy trực tiếp Docker Desktop trên Windows.
