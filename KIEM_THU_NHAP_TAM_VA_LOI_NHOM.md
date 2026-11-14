# Kiểm thử nhóm lỗi và lưu tạm — 14/11/2026

- **35** kiểm thử Python đạt: parser, endpoint kiểm tra định dạng, lỗi nhiều dòng, giới hạn dữ liệu phản hồi, không tạo đợt dở dang và hồi quy gửi bài/phân công/chống trùng/bảo mật.
- **118** kiểm thử frontend đạt; TypeScript/Vite production build đạt.
- Kiểm tra lưu ngay khi đóng trang, tự lưu, khôi phục toàn bộ biểu mẫu, giữ mã yêu cầu khi thử lại sau lỗi mạng, phân biệt người dùng/biểu mẫu, hết hạn 7 ngày và báo lỗi khi trình duyệt hết dung lượng lưu.
- Chromium + API thật: nhập TXT 83 dòng có lỗi ở 81 và 83, hiện đúng tên/link, chọn đúng dòng để sửa; đóng rồi chuyển trang, tải lại vẫn còn SS/link/nhóm/chế độ/thời gian nghỉ và mã yêu cầu.
- Lưu có lỗi giữ bản tạm và không tạo route/job. Sửa xong lưu thành công tạo bản nháp 83 nhóm, xóa bản tạm, vẫn không tạo tác vụ gửi.
- Giao diện desktop 1600px/mobile 390px không tràn ngang; không lỗi JavaScript/HTTP 500.

Không kết nối hay gửi Telegram thật. Bản này không thay schema database hoặc launcher Windows; giữ migration 0015 và các tính năng trước.
