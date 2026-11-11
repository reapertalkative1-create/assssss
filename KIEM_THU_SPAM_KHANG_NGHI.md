# Kiểm thử SpamBot / kháng nghị — 11/11/2026

## Thay đổi

- Tự check phiên/API và SpamBot sau nhập khi chọn tùy chọn (mặc định bật trên web, API cũ giữ mặc định tắt để tương thích).
- Trạng thái spam tách khỏi sức khỏe phiên; nhận diện không rõ được giữ unknown và hiển thị phản hồi gốc.
- Check phiên + spam hàng loạt, lọc spam, giữ cooldown/FloodWait; lỗi SpamBot hiển thị riêng trong file nhập và tác vụ bulk, không làm mất session hợp lệ.
- Tương tác với bot chính thức @SpamBot: chỉ lấy nút text/callback được hỗ trợ, kiểm tra lại trước khi bấm; nhập nội dung và xác nhận trước khi gửi.
- Lấy phản hồi mới chỉ đọc, không gửi /start; không tự gửi kháng nghị hoặc phát lại khi không chắc kết quả. Idempotency key cho việc thử lại cùng HTTP request.
- Phản hồi bot và payload kháng nghị được mã hóa, không giữ nội dung trong command result/audit. Key verification/rotation bao gồm spam reports. Migration 0008 giữ dữ liệu cũ.

## Kết quả

- Bộ Python local toàn bộ tại mốc tích hợp: **293 passed, 153 deselected** (`pytest -q -m 'not integration and not telegram_live'`).
- Nhóm cuối sau các chỉnh sửa token snapshot, giữ FloodWait và bổ sung test: **30 passed, 18 deselected** (spam + bulk + migration).
- Hồi quy API tài khoản/worker accounts: **45 passed, 24 deselected**. Các nhóm chồng lặp, không cộng thành tổng.
- Frontend: **48 passed** trong 6 tệp; TypeScript/Vite build thành công.
- Kiểm thử parser phản hồi bảo thủ, không suy đoán mọi thông báo là clear/limited.
- Kiểm thử bot identity cố định, /start chỉ gửi khi check, reply chỉ gửi khi người dùng yêu cầu, đọc không gửi tin, stale context, nút callback mới, chặn nút URL/chia sẻ số điện thoại, dọn event handler.
- Đã chạy với Telethon **1.45.0**, hỗ trợ cấu trúc nút mới; có nhánh tương thích cấu trúc nút cũ nhưng chưa chạy ma trận mọi phiên bản Telethon.
- Kiểm thử API: mã hóa báo cáo/appeal, không lộ nội dung qua DB dump/audit/command result; RBAC/CSRF, không cho đích tùy ý, idempotency, trạng thái uncertain không tự phát lại, xử lý lệnh kháng nghị hết hạn chưa giao.
- Kiểm thử worker/client/API thật với FakeBackend: tự kiểm tra sau nhập không hỏi OTP; cả kết quả limited và lỗi SpamBot đều giữ session đã xác thực.
- Kiểm thử xoay khóa spam report và nâng/hạ migration SQLite khớp model.

## Chromium thật

API/SQLite, Vite và worker/AccountManager thật; phần Telegram dùng FakeBackend:

1. Nhập ZIP 3 session giả với tự check bật sẵn.
2. Nhận đủ ba kết quả clear, limited, unknown, phiên vẫn authorized.
3. Lọc tài khoản limited, mở SpamBot / kháng nghị.
4. Bấm nút bot và xác nhận: chỉ gửi sau xác nhận.
5. Nhập kháng nghị, xem trước: chưa gửi; xác nhận mới gửi đúng nội dung.
6. Nhận phản hồi đang chờ quyết định, đọc lại mà không gửi /start.
7. Không có lỗi JavaScript; nhật ký FakeBackend xác nhận đúng các thao tác check/check/check/button/reply/read.

Chưa gửi kháng nghị hoặc dùng session người dùng để kết nối Telegram thật; chưa kiểm chứng mọi ngôn ngữ/hội thoại thật, CAPTCHA, kết quả xét duyệt, PostgreSQL integration toàn bộ hoặc build sạch Docker image bản này. Không thêm dependency. Người dùng cần setup.cmd một lần để build mã mới/nâng database.

Đã gửi tin không đồng nghĩa Telegram đã nhận một phiếu hợp lệ hoặc duyệt gỡ hạn chế. Giao diện giữ phản hồi thật để người dùng theo dõi và hoàn tất các bước cần thao tác trong Telegram.

ZIP/GitHub không chứa session người dùng, .env.docker, database cá nhân hoặc khóa thử nghiệm.
