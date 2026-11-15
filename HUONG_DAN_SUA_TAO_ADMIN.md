# Sửa bước tạo tài khoản quản trị

Phiên bản `2026.11.15-admin-input-fix`.

Log mới cho thấy hai lần nhập mật khẩu khớp nhau, sau đó tiến trình tạo tài khoản trong Docker trả lỗi. Bản trước đã bỏ mất phản hồi lỗi từ tiến trình này, nên log chỉ còn thông báo chung và không đủ để xác định lỗi gốc trên máy của bạn.

## Cập nhật

1. Giữ nguyên `.env.docker` và Docker volume hiện tại; không xóa database.
2. Giải nén đè **toàn bộ nội dung thư mục telegram-forwarder-control-center** vào đúng thư mục đang chạy, nơi có `setup.cmd` cũ.
3. Chạy **setup.cmd**. Khi chưa có admin, setup khởi động API và in **Checking setup input connection...** trước khi hỏi tài khoản.
4. Nhập tên đăng nhập, mật khẩu và xác nhận. Cả hai lần mật khẩu vẫn hiện rõ. Mật khẩu dài 12–128 ký tự, không chứa tên đăng nhập.
5. Sau khi setup hoàn tất, chạy **run.cmd** và đăng nhập.

Nếu đã có admin hoạt động, setup giữ tài khoản và mật khẩu đó, không yêu cầu tạo lại.

## Thay đổi

- Chuyển dữ liệu vào API đã chạy bằng `docker compose exec -T --interactive=true`, thay cho pipe ngay khi tạo container dùng một lần.
- Kiểm tra stdin bằng chuỗi thử có dấu/ký tự đặc biệt trước khi hỏi mật khẩu. Phép thử này không tạo tài khoản.
- Dữ liệu JSON dùng escape ASCII cho Unicode; helper cũng chấp nhận UTF-8 BOM từ các đường truyền Windows.
- Không bỏ mất JSON lỗi khi helper trả exit code khác 0. Mã lỗi phân biệt lỗi stdin, PostgreSQL, schema, quyền ghi, thiếu tài nguyên và mã hóa mật khẩu.
- Mật khẩu chỉ qua stdin, không đặt trong argv hoặc `.env.docker`, không xuất trong chẩn đoán. Database vẫn chỉ lưu hash Argon2. Không đổi schema (0016).

## Nếu vẫn có lỗi

Gửi dòng **ERROR** có mã trong dấu `[...]`, ví dụ `[stdin_empty]`, `[db_unavailable; ConnectionRefusedError]` hoặc `[db_resources; ...; SQLSTATE=53100]`. Không cần gửi dòng mật khẩu đã nhập.

`db_auth_failed` là lỗi mật khẩu kết nối PostgreSQL so với `.env.docker`, không phải mật khẩu web vừa nhập. `db_resources` là lỗi tài nguyên của PostgreSQL/Docker. Không xóa volume để thử sửa các lỗi này.
