# Kiểm thử bản sửa tạo admin

Phiên bản `2026.11.15-admin-input-fix`.

- 89 kiểm thử Python đạt trên SQLite và PostgreSQL: tạo admin, xác nhận mật khẩu, đăng nhập, quản lý người dùng, stdin rỗng/sai định dạng/BOM, mật khẩu có Unicode/ký tự đặc biệt/dấu cách, chẩn đoán SQLSTATE không lộ SQL/parameters.
- Migration đầy đủ 0001 → 0016 chạy thành công trên PostgreSQL mới; helper tạo admin thành công trên schema đã migrate.
- Luồng PowerShell → tiến trình Python thật → PostgreSQL: thử stdin có Unicode, xác nhận sai rồi nhập lại, tạo admin và đăng nhập HTTP thành công bằng đúng chuỗi mật khẩu đã nhập.
- Lỗi kết nối PostgreSQL được chủ động gây ra trong kiểm thử: helper exit 1; PowerShell vẫn giữ mã `db_unavailable` và `ConnectionRefusedError`, không thay thành lỗi mật khẩu chung.
- Bộ kiểm thử launcher PowerShell đạt: API sẵn sàng trước kiểm tra stdin; exec có stdin bật và không TTY; giữ cấu hình/tài khoản đã tồn tại; không có mật khẩu trong argv; giữ lỗi JSON khi exit khác 0; setup/run và khóa chống chạy trùng.
- Kiểm thử pipe UTF-8 qua tiến trình native đạt.

Giới hạn: PowerShell 7 chạy trên Linux; chưa kiểm thử Windows PowerShell 5.1/Docker Desktop thật. Docker cloud không khả dụng sau khi môi trường được khôi phục; kiểm thử dùng tiến trình Python thật và PostgreSQL thật, mô phỏng lệnh Docker. Log của người dùng thiếu lỗi gốc do bản trước che phản hồi nên không thể kết luận chính xác nguyên nhân trên máy người dùng. Bản sửa thay luồng truyền dữ liệu và bổ sung chẩn đoán để không lặp lại thông báo chung.

Không đổi mã giao diện trong bản này; giữ dist đã build ở bản trước, cập nhật version.json đồng bộ APP_VERSION. Không kết nối Telegram hoặc gửi tin nhắn thật.
