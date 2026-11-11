# Telegram Forwarder Control Center — nhập session hàng loạt

[**Tải ZIP bản mới — nhập tối đa 100 session trên web**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-session-import.zip)

Giữ nguyên **.env.docker** và Docker volume, giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để nâng migration 0006 và build image mới. Sau đó dùng **run.cmd**.

Trên web: **Tài khoản Telegram → Nhập session hàng loạt → chọn tối đa 100 file Telethon .session hoặc một ZIP → chọn worker Online → nhập API ID/hash → Nhập và kiểm tra session**.

Session hợp lệ không cần OTP lại. Worker kiểm tra 3 session cùng lúc, báo từng kết quả và bỏ qua trùng trong các lô đã nhập. Sau khi thành công, bạn có thể Bật tài khoản khi cần chạy chuyển tiếp. Tổng tải lên 10 MiB. Không hỗ trợ Pyrogram/tdata.

Xem [hướng dẫn nhập](HUONG_DAN_NHAP_SESSION.md), [hướng dẫn Windows](HUONG_DAN_WINDOWS.md), [kiểm thử](KIEM_THU_NHAP_SESSION.md).

269 kiểm thử Python, 45 kiểm thử giao diện qua; thử Chromium + worker với session giả. Chưa thử Telegram thật. Bản ZIP không chứa session người dùng hoặc .env.docker.

SHA256: `52f1d6331c8f06879843c38f9fb07f53aa12421264b8605a250f3c1ca4f6493e`.

## Bản trước

- [Nhập API ID/hash và OTP trên web](telegram-forwarder-control-center-web-login.zip)
- [BOM fix](telegram-forwarder-control-center-windows-autoconnect-bomfix.zip)
- [Tự kết nối worker](telegram-forwarder-control-center-windows-autoconnect.zip)
- [Windows cách ly](telegram-forwarder-control-center-windows-isolated.zip)
- [Khôi phục](telegram-forwarder-control-center-phase6-fixed-v2-recovered.zip)
