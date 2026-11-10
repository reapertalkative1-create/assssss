# Xác minh bộ setup.cmd / run.cmd

## Đã kiểm tra

- Cú pháp PowerShell và luồng setup/run: sinh khóa ngẫu nhiên đúng định dạng, không ghi đè cấu hình khi chạy lại, kiểm tra cổng, Docker Linux/Compose version, nhánh worker đủ/thiếu cấu hình, tài khoản admin có sẵn/chưa có và dấu cài đặt thành công.
- Build thật cả ba image API, web và worker. Python/Node/PostgreSQL không được cài lên máy Windows bởi các script.
- PostgreSQL 16 trong Docker: đủ 4 migration chạy thành công; kiểm tra admin thiếu trả mã 3 và admin đã tồn tại được giữ lại.
- Luồng setup với Docker thật đã qua, dùng các image đã build riêng trước đó (môi trường cloud cần CA riêng ở bước build). Chạy lại setup giữ nguyên khóa, cấu hình và database.
- Luồng run thực sự qua PowerShell + Docker CLI: API, web và database healthy; worker Linux đăng ký online, được tái tạo và đăng ký lại khi run lần nữa, dừng với exit code 0 khi xóa cấu hình worker.
- Đăng nhập HTTP, CSRF, session và giữ nguyên tài khoản sau các lần run đều qua với PostgreSQL thật.
- Chromium: đăng nhập, 9 trang quản trị và WebSocket hello qua Nginx đều qua, không có lỗi JavaScript/HTTP 5xx.
- Web chỉ mở cổng 127.0.0.1:8787; API và PostgreSQL không publish cổng ra host.

## Giới hạn xác minh

Môi trường thử là Linux Docker và PowerShell 7.4.6. Chưa chạy trực tiếp việc bấm đúp CMD trên Windows/PowerShell 5.1; các CMD dùng CRLF/ASCII, và helper chỉ dùng cú pháp tương thích PowerShell 5.1. Cần Docker Desktop (Linux containers, Compose >=2.20) trên Windows 10/11.

Chưa đăng nhập/gửi tin qua Telegram thật. Kiểm tra worker dùng app credentials giả với không có tài khoản Telegram được gán, nên chỉ xác minh kênh worker ↔ API.

Các sửa lỗi ứng dụng và kết quả kiểm thử trước vẫn được giữ; xem KIEM_THU_BAN_KHOI_PHUC.md. Bộ này thêm cách chạy cách ly, không thay đổi schema/migration hay logic chuyển tiếp.

ZIP không kèm .env/.env.docker, dấu .docker-ready, database, credential hoặc dữ liệu thử. Mỗi lần cài mới tự tạo project/volume/khóa riêng.
