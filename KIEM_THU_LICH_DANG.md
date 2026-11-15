# Kiểm thử lịch đăng theo cụm

Phiên bản: `2026.11.15-scheduled-posts`, ngày 15/11/2026.

- **100 kiểm thử API/worker trên SQLite đạt**: cụm, lịch, bài theo liên kết, động cơ gửi, nhiều SS, hàng đợi và các cơ chế chống trùng/hạn chế. 49 kiểm thử chức năng thay đổi và 51 kiểm thử hồi quy liên quan.
- **22 kiểm thử PostgreSQL đạt**: lưu/cập nhật cụm, lịch gửi, phân công SS, chống trùng, FloodWait, quyền/hạn chế và kết quả gửi chưa rõ.
- **134 kiểm thử frontend đạt**, TypeScript và production build đạt.
- **Chromium desktop 1440px / mobile 390px đạt** với API mô phỏng: mở Lên lịch không tự tạo lượt, dùng bài đã lưu, đổi 09:30 giờ Việt Nam thành 02:30 UTC, kiểm tra quyền rồi xếp hàng đúng một lần, hiện Chờ lịch, thao tác tạm dừng/dừng và không tràn ngang trên điện thoại.

Các tình huống hồi quy mới gồm lịch thiếu múi giờ/quá khứ/quá 90 ngày bị từ chối; chuẩn hóa múi giờ; không tạo lượt trùng khi thử lại kể cả đã qua giờ hẹn; cùng mã yêu cầu nhưng đổi giờ bị từ chối; hàng đợi không được nhận trước giờ hẹn và vẫn đọc được sau tải lại; tạm dừng chặn nhận việc; tiếp tục giữ hàng chờ; kiểm tra lại quyền thành viên trước mỗi lần gửi; SS không có quyền, rời nhóm hoặc FloodWait không tiếp tục gửi. Lượt cũ yêu cầu quyền quản trị vẫn giữ điều kiện cũ.

Không dùng Telegram thật và không gửi bài/tham gia nhóm thật trong kiểm thử. Docker Desktop/Windows thật chưa được kiểm thử trong môi trường này. Không đổi schema database; vẫn dùng migration 0017 đã có. Giữ nguyên setup/run, bước nhập mật khẩu hiển thị và cơ chế tự kết nối worker của bản trước.
