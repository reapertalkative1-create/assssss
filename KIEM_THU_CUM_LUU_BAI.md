# Kiểm thử cụm lưu bài

Phiên bản `2026.11.15-saved-clusters`.

- **89 kiểm thử API/worker trên SQLite đạt**: lưu link/khoảng nghỉ, mặc định 150–180, từ chối mốc đảo ngược, tạo lượt không nhập lại link, retry cùng request ID, chặn phiên bản cấu hình cũ, lịch sử bất biến, kiểm tra quản trị, hàng đợi, FloodWait, hạn chế tài khoản và chống trùng.
- **19 kiểm thử PostgreSQL đạt** cho cụm và giới hạn chuyển tiếp.
- **Migration 0016 → 0017 đạt** trên PostgreSQL với dữ liệu phiên bản cũ: giữ khoảng nghỉ cố định, lấy bài gần nhất, giữ các tác vụ cũ với cooldown mặc định 0.
- **132 kiểm thử frontend đạt**. Sau chỉnh thông báo kết quả, chạy lại 9 kiểm thử cụm đều đạt. Kiểm tra lưu/khôi phục, sửa khoảng nghỉ, một lần bấm Chạy dùng link đã lưu, kiểm tra trước khi bắt đầu, không bắt đầu khi xác minh thất bại, và không nhân đôi khi bấm hai lần.
- **TypeScript + Vite production build đạt**.
- **Chromium desktop 1440px và mobile 390px đạt**: bỏ điều hướng Tuyến chuyển tiếp; đường dẫn cũ chuyển về cụm; sửa link/khoảng nghỉ rồi tải lại vẫn giữ; bấm Chạy kiểm tra trước khi bắt đầu; mặc định 150–180; trang/biểu mẫu không tràn ngang.
- Worker bị thiếu hỗ trợ kiểm tra quản trị phải từ chối gửi. SS mất quyền quản trị trước khi gửi bị chặn. Kiểm thử Telethon xác nhận không gọi lệnh tham gia nhóm.

Giao tiếp Telegram và backend trong kiểm tra trình duyệt được mô phỏng; kiểm tra API/PostgreSQL dùng cơ sở dữ liệu thật. Không tham gia nhóm hoặc gửi Telegram thật. Chưa chạy Docker Desktop/Windows thật trong phiên kiểm tra này.
