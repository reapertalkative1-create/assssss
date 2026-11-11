# Bản đăng nhập Telegram trên web

## Thay đổi

- Form Thêm tài khoản gồm tên hiển thị, worker, api_id và api_hash; lưu xong tự mở số điện thoại → OTP → 2FA nếu có.
- Tài khoản cũ có nút API Telegram; dừng tài khoản trước khi thay thông tin.
- Cặp API được mã hóa bằng khóa session hiện có, ràng buộc UUID tài khoản, chỉ cấp cho worker được gán. Web chỉ nhận cờ đã cấu hình, không nhận lại hash. Kiểm tra/xoay khóa bao gồm dữ liệu này.
- Backend riêng cho từng tài khoản, tránh lẫn API giữa các lần đăng nhập song song. Cấu hình môi trường cũ vẫn làm dự phòng.
- Migration 0005 thêm cột nullable, giữ dữ liệu cũ. setup.cmd/run.cmd và sửa BOM được giữ nguyên.

## Kiểm chứng ngày 11/11/2026

- Python: **262 passed, 134 deselected** với `pytest -q -m 'not integration and not telegram_live'`.
- Bộ kiểm thử tính năng cuối: **7 passed**, gồm API/RBAC/CSRF, không lộ hash qua phản hồi/audit/database, đúng worker, xác thực đầu vào, đăng nhập OTP/2FA qua API thật + worker thật với FakeBackend, tách cấu hình tài khoản và dự phòng môi trường.
- Xoay khóa: kiểm thử xác nhận API credentials vẫn giải mã được bằng khóa mới sau khi bỏ khóa cũ.
- Frontend: **44 passed** (6 files); TypeScript/Vite build thành công.
- Nâng PostgreSQL đang dùng từ 0004 lên 0005 thành công; admin/worker có sẵn được giữ lại.
- Chromium thật + Nginx/API/PostgreSQL: đăng nhập quản trị cũ, mở form, tự chọn worker, lưu API pair, nhập phone/OTP, nhận authorized; không có lỗi JavaScript. Telegram dùng FakeBackend, không gọi mạng Telegram thật.
- API/web chạy bằng image phụ thuộc có sẵn và gắn source/dist mới khi kiểm tra container. Chưa build sạch toàn bộ Docker image của bản này: ổ đĩa cloud dùng Docker vfs bị đầy khi tạo thêm container. Sau khi dọn container thử nghiệm, bộ Python cuối chạy qua đầy đủ. Thay đổi không thêm dependency; setup.cmd trên Windows sẽ build image từ source mới.
- Chưa chạy toàn bộ biến thể PostgreSQL integration hoặc Telegram thật; cần tài khoản và API credentials của người dùng để xác minh Telegram thực tế.

## Cập nhật

Giải nén đè mã nguồn vào thư mục cũ, giữ nguyên `.env.docker` và Docker volume. Chạy **setup.cmd một lần** để build image và nâng database, rồi dùng **run.cmd**. Trên web: **Tài khoản Telegram → Thêm tài khoản → api_id/api_hash → Tạo và đăng nhập → số điện thoại → OTP/2FA**.

Đây là thêm tài khoản Telegram đã tồn tại vào ứng dụng; tạo tài khoản Telegram mới bằng ứng dụng Telegram chính thức trước.
