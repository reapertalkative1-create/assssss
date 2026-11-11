# Kiểm thử nút check spam / đóng băng — 11/11/2026

- Python: **66 passed, 48 deselected** cho test_spambot, test_account_bulk, test_accounts_api, test_accounts_e2e với marker `not integration and not telegram_live`.
- Bổ sung kiểm thử riêng phản hồi SpamBot nhiều tin: **1 passed**. Tổng 67 trường hợp qua trong hai lượt không trùng.
- Frontend: **54 passed**, 6 tệp. Build TypeScript/Vite thành công.
- Kiểm tra frozen_notice: nhận thông báo đóng băng rõ ràng; không nhận câu điều kiện “If your account is frozen”, khả năng “may be frozen” hoặc phủ định “not frozen”.
- Kiểm tra API không ghi Live khi get_me thành công nhưng SpamBot trả account_frozen; health=frozen, desired_state=stopped, giữ lỗi riêng và tổng số trong summary.
- Luồng API/worker với FakeBackend: nhập session và check spam limited/error/frozen; session hợp lệ vẫn authorized nhưng trường hợp frozen được đánh dấu riêng.
- Phản hồi nhiều tin giữ tín hiệu frozen dù tin cuối chỉ là hướng dẫn.
- Frontend kiểm tra nút tại dòng gửi đúng account ID; check toàn bộ theo bộ lọc gửi all_matching và spam filter đúng; bộ lọc đóng băng bỏ bộ lọc spam; lỗi tạo tác vụ hiển thị thay vì báo thành công.
- Chromium thật với API/SQLite và dữ liệu giả: nút check tại dòng, check mọi kết quả bị spam theo bộ lọc, lọc đóng băng/chưa check và màn hình 390px không tràn ngang toàn trang. Hai tác vụ test được tạo; không lỗi JavaScript.

Không dùng session người dùng hoặc gửi Telegram thật trong kiểm thử. Kiểm thử luồng worker dùng FakeBackend; browser dùng dữ liệu giả và không chạy worker Telegram. Chưa xác minh mọi nội dung/ngôn ngữ SpamBot hay mọi loại cấm gửi riêng từng nhóm. Không chạy PostgreSQL integration hoặc build sạch Docker Windows trong đợt này. Không thêm dependency/migration.

ZIP gồm source, web dist và setup.cmd/run.cmd; loại trừ session, database, khóa, .env riêng và dữ liệu runtime. Báo cáo các bản trước áp dụng tại thời điểm kiểm thử các bản đó.
