# Kiểm thử bản khôi phục

Bản này được khôi phục từ ZIP gốc và các sửa đổi ghi lại trong cuộc trò chuyện; không phải bản sao bit-for-bit của ZIP v2 đã mất.

- Python local: 247 passed, 123 deselected. Lệnh: python -m pytest -q -m "not integration and not telegram_live".
- Web: 42 kiểm thử qua; npm run build thành công.
- Đã khôi phục sửa lỗi batch nhiều đích, lịch sử qua nhiều lượt, giữ kết quả/đệm khi lỗi hoặc hủy, shutdown worker/tài khoản, kiểm tra URL worker, chống vòng lặp khi sửa bộ lọc, quyền WebSocket và commit database trước phản hồi.
- Nhóm kiểm thử mới xác minh các luồng chính của các sửa đổi. Các bài kiểm thử gốc tiếp tục qua.
- Không thay đổi schema/migration.

Chưa chạy PostgreSQL integration và Telegram thật trong lần khôi phục này. Không khẳng định đã kiểm tra trình duyệt thật trong môi trường mới; kiểm thử giao diện dùng Vitest/jsdom. Cần credential/tài khoản Telegram của bạn để kiểm thử gửi tin thật.
