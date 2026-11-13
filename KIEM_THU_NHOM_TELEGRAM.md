# Kiểm thử nhóm tài khoản và nhóm chat — 13/11/2026

- Python: bộ chọn lọc API nhóm/migration/worker/bulk **39 passed**, cùng bộ API nhóm và worker E2E sau sửa cuối **6 passed**; có test trùng, không cộng số lượt. Thử tạo/đổi tên, gán/bỏ nhóm nhiều SS, lọc có/không nhóm, chọn toàn bộ lọc, phân quyền, xóa nhóm giữ SS, xóa SS cập nhật số lượng, migration upgrade/downgrade và FloodWait.
- Test worker E2E dùng FakeBackend đi qua API, AccountManager và kết quả command cho đúng SS. Test Telethon với entity thật nhưng client giả phân biệt nhóm thường, supergroup, chat cá nhân và kênh.
- Frontend: **98 tests passed**, 13 tệp; production TypeScript/Vite build qua.
- Chromium + API/SQLite: tạo/đổi tên/xóa nhóm, gán hai SS, lọc, giữ SS sau xóa nhóm, kích thước 1600 và 390 px, không lỗi JS/HTTP 500. Cửa sổ nhóm Telegram dùng command giả, kiểm tra tìm kiếm và tải TXT thật.

Không dùng session người dùng hoặc kết nối Telegram thật. Chưa thử Docker Desktop/Windows hay PostgreSQL thực trong lượt này. Danh sách chat Telegram có giới hạn 2.000 nhóm/lần, không tự join/leave và không xác nhận quyền gửi.
