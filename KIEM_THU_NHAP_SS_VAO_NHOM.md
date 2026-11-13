# Kiểm thử nhập SS vào nhóm — 13/11/2026

- SQLite: 10 kiểm thử nhóm/nhập nhóm và 29 kiểm thử hồi quy nhập session, proxy, API Telegram đã lưu, biểu mẫu API: đạt.
- PostgreSQL 16: 9 kiểm thử API nhóm/nhập nhóm: đạt. Dùng database/role kiểm thử riêng trong PostgreSQL; đã xóa sau kiểm thử, không thay đổi database ứng dụng.
- Frontend: 102 kiểm thử đạt; TypeScript + Vite production build đạt. Bao gồm nhóm mặc định khi tạo/nhập, đổi nhóm trong biểu mẫu, giữ nhóm ở cả hai lô của 101 file, chuyển nhóm theo bộ lọc có loại trừ và bỏ nhóm từng SS.
- Chromium + API SQLite thật: tạo/chọn nhóm → nhập session tổng hợp kèm proxy → hiển thị ngay → tải lại trang vẫn còn; đổi nhóm từng SS, chuyển SS đã tích; nhập trùng trực tiếp từ nhóm khác giữ session/proxy; tạo tài khoản theo nhóm đang chọn; chọn trang/chuyển/bỏ nhóm trong nhóm. Desktop 1600px và mobile 390px không tràn ngang, không lỗi JavaScript.
- Nhóm bị xóa được báo lỗi trước khi tạo tài khoản/nhập; không sinh SS không nhóm. SS nhập lỗi kiểm tra vẫn giữ nhóm đã chọn. Nhập trùng không chọn đích giữ nhóm hiện có.

Dùng session tổng hợp và worker giả lập; không đăng nhập hoặc gửi tin nhắn Telegram thật. Không chạy Docker Desktop trên Windows. Không thay đổi launcher hoặc migration; database head vẫn 0014. ZIP không chứa .env.docker, database, session người dùng hay khóa riêng.
