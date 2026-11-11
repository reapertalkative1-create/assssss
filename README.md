# Telegram Forwarder Control Center — đăng nhập trên web

## Tải bản mới

[**Tải ZIP: nhập API ID/hash và đăng nhập Telegram trên web**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-web-login.zip)

Giải nén đè mã nguồn vào thư mục đang dùng, **giữ nguyên .env.docker và Docker volume**. Chạy **setup.cmd một lần** để build bản mới và nâng database, sau đó dùng **run.cmd**.

Trên web: **Tài khoản Telegram → Thêm tài khoản → chọn worker → nhập api_id/api_hash → Tạo và đăng nhập → số điện thoại → OTP/2FA**. Tài khoản cũ có nút **API Telegram**. Không cần sửa .env.docker để nhập API credentials.

Xem [hướng dẫn Windows](HUONG_DAN_WINDOWS.md) và [kết quả kiểm thử](KIEM_THU_DANG_NHAP_WEB.md). 262 kiểm thử Python và 44 kiểm thử giao diện qua; đã thử Chromium + PostgreSQL với Telegram giả lập. Chưa thử Telegram thật.

SHA256: `8b40fdbc9b07a1bbbecb1388c6624783d2ec6627b85930c75463e664a4e12d4d`.

## Bản trước

- [Bản sửa BOM](telegram-forwarder-control-center-windows-autoconnect-bomfix.zip)
- [Bản tự kết nối worker](telegram-forwarder-control-center-windows-autoconnect.zip)
- [Bản Windows cách ly](telegram-forwarder-control-center-windows-isolated.zip)
- [Bản khôi phục](telegram-forwarder-control-center-phase6-fixed-v2-recovered.zip)
