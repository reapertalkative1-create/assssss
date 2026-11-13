# Kiểm thử chọn nhiều SS gửi bài — 13/11/2026

- SQLite: 18 kiểm thử gửi bài/đa tài khoản đạt (17 kiểm thử tính năng và hồi quy, thêm 1 kiểm thử quy mô).
- PostgreSQL 16: 15 kiểm thử tương ứng đạt (14 tính năng/hồi quy, thêm 1 quy mô). Database/role kiểm thử riêng đã được xóa; không dùng database ứng dụng.
- 106 kiểm thử frontend đạt; TypeScript/Vite production build đạt.
- Quy mô: 105 SS, chọn mọi kết quả rồi loại 2 SS → nhận 103 SS vượt trang 50 dòng; 105 nhóm nhận được phân công một lần, lưu 103 bản nháp, chưa tạo tác vụ gửi.
- API: chọn theo nhóm có loại trừ, SS không đủ điều kiện, chống lưu lặp cùng request ID, đổi nội dung khi retry, thiếu tài khoản/đích sai không tạo bản nháp dở dang, phân quyền admin, kiểm tra quyền trước gửi, hạn chế không chuyển phần việc sang SS khác, chặn alias trùng nhóm Telegram.
- Chromium + API/worker thật với FakeBackend: tích hai SS ở bảng tài khoản → Gửi bài (N) → chọn nhóm → bỏ tích một SS → tải TXT có dòng trùng → lưu hai bản nháp → kiểm tra → gửi giả lập bốn nhóm duy nhất → tải lại vẫn xem được tiến độ. Không lỗi JavaScript hoặc HTTP 500.
- Thử thêm chuyển trang bằng menu và nút SS đã tích; kiểm tra giao diện desktop 1600px và mobile 390px không tràn ngang.

Tất cả session/backend đều giả lập, không kết nối hoặc gửi Telegram thật. Không thử Docker Desktop trên Windows. Giữ nguyên launcher và migration 0014. ZIP loại dữ liệu/session/khóa riêng của người dùng.
