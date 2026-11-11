# Telegram Forwarder — Windows tự kết nối (đã sửa BOM)

[Tải ZIP đã sửa lỗi Unexpected UTF-8 BOM](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-windows-autoconnect-bomfix.zip)

**Nếu đang lỗi ở bước Connecting this computer:** giải nén đè vào đúng thư mục đang dùng, giữ .env.docker và Docker volume, rồi chạy setup.cmd lại một lần. Không cần cài lại Docker hay tạo lại tài khoản quản trị.

Setup tạo tài khoản và tự cấu hình worker. Những lần sau bấm run.cmd: worker tự Online và mở http://127.0.0.1:8787. Không cần chép credential hoặc URL. Telegram thật vẫn cần API ID/hash và OTP/2FA.

Bản này đọc JSON UTF-8 có/không BOM ở cả provision và wait-online; PowerShell gửi UTF-8 không BOM và khôi phục encoding sau lệnh. Đã tái hiện lỗi cũ và kiểm tra 6 trường hợp CLI trên Docker/PostgreSQL cùng các kiểm thử PowerShell; giữ nguyên worker/credential. Chưa thử trực tiếp Windows PowerShell 5.1 trên Windows.

[Hướng dẫn Windows](HUONG_DAN_WINDOWS.md) · [Kiểm thử](KIEM_THU_TU_KET_NOI.md)

SHA-256: `add964e8e068c92f5a5091440f5135191a6ca8118ed2bacf19cf11d15fad42a5`.
