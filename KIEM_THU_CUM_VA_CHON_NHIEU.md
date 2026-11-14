# Kiểm thử cụm và chọn nhiều

- **46** kiểm thử API/SQLite đạt: lựa chọn/lọc, tạo cụm từ lượt cũ, quyền/CSRF, cụm, các thao tác tuyến và cơ chế bảo vệ gửi bài.
- **4** kiểm thử PostgreSQL mới đạt: tìm theo SS/tên cụm, danh sách đã chọn, preview gộp SS/nhóm, lỗi và quyền truy cập.
- **127** kiểm thử frontend đạt; TypeScript/Vite production build đạt.
- PowerShell: phân tích cú pháp, run từ bản cũ tự cập nhật, cùng phiên bản không build lại, dừng trước migration, lỗi khởi động không ghi dấu đã cập nhật, giữ nguyên `.env.docker`, phát hiện web cũ. Kiểm tra bằng các hàm Docker giả lập, không cài Docker trên Windows thật trong môi trường này.
- Chromium + API thật với dữ liệu giả: 25 SS qua hai trang; giữ lựa chọn khi đổi bộ lọc; chỉ dừng/tạm dừng dòng đã tích; hiện lỗi đúng SS; chuyển 25 dòng cũ thành cụm 25 SS/50 nhóm, giữ nguyên các tuyến; tạo cụm từ 2 SS ở trang Tài khoản Telegram; cụm xuất hiện ngay và vẫn còn sau tải lại.
- Kiểm tra menu riêng, phiên bản web, giao diện desktop 1600px/mobile 390px. Không lỗi JavaScript/HTTP 500. Không tạo tác vụ gửi hay kết nối Telegram thật.

Schema vẫn 0016. Lịch sử, session, API/proxy và dữ liệu cụm của bản trước được giữ. Bản ZIP không chứa `.env.docker`, `.docker-version`, session hoặc dữ liệu kiểm thử runtime.
