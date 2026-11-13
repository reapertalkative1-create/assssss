# Kiểm thử sửa nhóm SS — 13/11/2026

- PostgreSQL 16: 5 kiểm thử API nhóm trên database kiểm thử riêng (tạo/gán/chuyển/lọc, giữ tài khoản khi xóa nhóm, phân quyền và xóa SS). Database và role kiểm thử đã được xóa sau đó. Không dùng dữ liệu của người dùng.
- Frontend: 98 kiểm thử hồi quy cùng 2 kiểm thử mới cho mở nhóm/thêm SS trực tiếp và bắt buộc chọn đích trước khi thay đổi. TypeScript/Vite build thành công.
- Chromium + API SQLite: tạo nhóm, thêm SS trực tiếp, hiển thị thành viên, mở lại nhóm, tải lại trang và lọc nhóm. Thử tiếp 58 SS và chọn hai SS ở hai trang khác nhau; cả hai xuất hiện sau khi thêm. Không lỗi JavaScript/HTTP 500; giao diện vừa desktop/mobile.
- Không thử Telegram thật hoặc Docker Desktop trên Windows. Không thay đổi cơ sở dữ liệu; giữ cơ chế nhóm và các tính năng còn lại.
