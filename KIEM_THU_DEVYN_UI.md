# Kiểm thử DEVYN FORWARDER UI — 11/11/2026

- `npm run build`: TypeScript và Vite production build thành công.
- `npm test`: **51 passed**, 6 tệp. Bao gồm các kiểm thử import, quản lý session, bulk delete, kháng nghị theo mẫu và kiểm tra class CSS.
- Chromium thật với API/SQLite riêng và dữ liệu giả: đăng nhập, hiện/ẩn mật khẩu, tiêu đề DEVYN FORWARDER và favicon trả 200.
- Điều hướng cả 9 trang ở desktop 1600×1100 và điện thoại 390×844; tiêu đề hiển thị đúng, không tràn ngang toàn trang. Bảng rộng cuộn bên trong.
- Đổi giao diện sáng/tối, đồng bộ lựa chọn trong Cài đặt. Menu điện thoại mở/đóng qua điều hướng, Escape và nền ngoài menu.
- Mở/đóng cửa sổ nhập session, thêm tài khoản và kháng nghị theo mẫu trên desktop/điện thoại; biểu mẫu hiển thị, Escape đóng được.
- Không có lỗi JavaScript hoặc HTTP 500 trong vòng kiểm tra điều hướng.

Bộ dữ liệu kiểm thử tổng quan/session là giả. Không chạy worker Telegram và không dùng session người dùng, không gửi tin hoặc kháng nghị tới Telegram. Thay đổi chỉ ở frontend; không chạy lại bộ Python, không kiểm chứng build sạch Docker trên Windows trong đợt sửa giao diện này. Các báo cáo bản trước mô tả kiểm thử backend ở thời điểm tương ứng.

ZIP loại trừ database, session, .env riêng, khóa, node_modules và dữ liệu runtime. Bao gồm source và bản web production build, setup.cmd và run.cmd.
