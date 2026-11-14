# Mật khẩu hiển thị khi tạo tài khoản

Phiên bản: `2026.11.14-visible-password`.

1. Giữ `.env.docker` và Docker volume hiện tại. Giải nén đè bản mới vào đúng thư mục đang dùng.
2. Chạy `setup.cmd`. Nếu chưa có quản trị viên hoạt động, nhập tên đăng nhập rồi nhập mật khẩu hai lần. Cả hai lần đều hiện chữ trong cửa sổ setup.
3. Nếu hai lần khác nhau, nhập lại tại chỗ; setup không build lại. Nếu mật khẩu chưa đủ mạnh hoặc tên đã tồn tại, setup báo lý do và cho sửa.
4. Sau khi setup hoàn tất, chạy `run.cmd` và đăng nhập bằng tài khoản vừa tạo. Trên web dùng Ctrl+F5; cuối trang ghi **Mật khẩu hiển thị · 14.11.2026**.

Mật khẩu dài 12–128 ký tự, có ít nhất 5 ký tự khác nhau, không chứa tên đăng nhập và không thuộc danh sách mật khẩu phổ biến. Chữ hoa/thường và dấu cách được tính chính xác, không tự cắt hoặc đổi mật khẩu. Có thể dán cùng một mật khẩu vào cả hai lần nhập.

Nếu đã có quản trị viên hoạt động, setup giữ tài khoản đó và không yêu cầu tạo lại. Bản cập nhật không đổi mật khẩu đã có.

**Người dùng → Thêm người dùng:** ô Mật khẩu ban đầu cũng hiển thị rõ khi nhập.

Setup đọc mật khẩu tại PowerShell rồi chuyển qua stdin JSON UTF-8 tới Docker, không dùng nhập mật khẩu ẩn trong Docker TTY. Mật khẩu không nằm trong tham số dòng lệnh hoặc `.env.docker`; cơ sở dữ liệu tiếp tục chỉ lưu hash Argon2. Dữ liệu/migration vẫn ở phiên bản 0016.

Log được cung cấp cho thấy hai chuỗi nhập không khớp ở bước xác nhận. Log không chứa mật khẩu nên không xác định được hai chuỗi khác ở đâu. Bản này giúp nhìn và đối chiếu trực tiếp, đồng thời loại bỏ bước nhập ẩn qua Docker.
