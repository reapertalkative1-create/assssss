# Telegram Forwarder — chạy riêng trên Windows

## Tải bản mới

[Tải ZIP có setup.cmd và run.cmd](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-windows-isolated.zip)

1. Cài và mở Docker Desktop, dùng Linux containers.
2. Giải nén toàn bộ ZIP. Bấm **setup.cmd** một lần, tạo tài khoản quản trị khi được hỏi.
3. Những lần sau bấm **run.cmd**. Mở **http://127.0.0.1:8787**.

Python, Node và PostgreSQL nằm trong container riêng; không cần cài chúng lên Windows. Cấu hình/khóa ở .env.docker và dữ liệu trong Docker volume riêng. Giữ file cấu hình và volume để giữ dữ liệu.

- [Hướng dẫn Windows](HUONG_DAN_WINDOWS.md)
- [Kết quả kiểm tra Docker/PowerShell](KIEM_THU_WINDOWS_DOCKER.md)

Đã build và chạy thử stack Docker, đăng nhập, 9 trang quản trị, WebSocket và bật/tắt/khởi động lại worker. Cú pháp/luồng PowerShell đã kiểm tra trên Linux; chưa chạy trực tiếp thao tác bấm đúp CMD trên Windows.

Nếu bật worker trong container, chọn nền tảng **Linux** trong giao diện dù host là Windows. Telegram thật cần credential của bạn.

SHA-256 ZIP mới: `953518b609fca1e53dbafa41ace99247df5ca8f6a1fe64dadd701f44d6c81bc8`.

## Bản thủ công trước đó

[Tải bản khôi phục v2 chạy thủ công](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-phase6-fixed-v2-recovered.zip)
