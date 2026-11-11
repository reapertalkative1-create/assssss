# Kiểm thử kháng nghị hàng loạt theo mẫu — 11/11/2026

- Python local toàn bộ: **309 passed, 165 deselected**, `pytest -q -m 'not integration and not telegram_live'`.
- Nhóm cuối sau bổ sung khóa nháp và giữ FloodWait: **11 passed, 9 deselected** (bulk appeal + bulk delete). Các nhóm chồng lặp, không cộng thành tổng.
- Frontend: **51 passed** trong 6 tệp; TypeScript/Vite build thành công.
- Migration 0009 nâng/hạ SQLite và so sánh model/schema: qua.
- Unit: thay biến một lượt, không thay lại biến nằm trong tên SS, báo thiếu email/phone, kiểm tra lời nhắc SpamBot đang yêu cầu mô tả, đọc số từ get_me của session mà không gửi tin trong bước chuẩn bị.
- API: preview chưa gửi lệnh reply, email riêng ưu tiên email chung, chỉ gửi khi xác nhận sự thật và token đúng; xác nhận lại cùng tác vụ không tạo đợt gửi thứ hai. Kiểm tra RBAC/CSRF, hủy nháp và xóa nội dung cá nhân sau khi xếp gửi.
- Mẫu/email/nội dung đã điền được mã hóa; DB dump/audit/command result không giữ nội dung rõ. Kiểm tra/xoay khóa bao gồm nháp và bản cá nhân.
- Giữ các kiểm thử xóa hàng loạt trước đó.

## Chromium thật

API/SQLite, Vite, client/worker/AccountManager thật với phần Telegram dùng FakeBackend:

1. Chọn 3 SS giả, dùng email chung và một email riêng cho SS Beta.
2. Chuẩn bị: 2 bản sẵn sàng, 1 bản chưa đúng bước SpamBot.
3. Preview hiển thị đúng tên SS, số điện thoại và email tương ứng; chưa gửi tin nào.
4. Nút gửi bị khóa đến khi người dùng xác nhận nội dung đúng.
5. Sau xác nhận gửi đúng 2 bản; log FakeBackend chứng minh nội dung đúng từng tài khoản và không còn biến chưa điền.
6. Không có lỗi JavaScript.

Chưa sử dụng session người dùng để gửi kháng nghị Telegram thật; chưa xác minh xét duyệt/gỡ hạn chế, mọi ngôn ngữ/các bước bot, PostgreSQL integration toàn bộ hoặc build sạch Docker image. Không thêm dependency. Chỉ cho gửi tự động ở lời nhắc mô tả được nhận diện; bước khác cần hoàn tất trong hội thoại rồi tạo nháp mới.

Telegram không trả đầy đủ email qua session. Email phải do người dùng nhập chính xác; không suy đoán email bị che một phần. Nội dung câu “I never spam messages” là mẫu có thể sửa và cần người dùng xác nhận đúng sự thật, không phải kết luận của ứng dụng.

ZIP/GitHub không chứa session người dùng, .env.docker, khóa hoặc database thử nghiệm.
