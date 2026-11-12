# Kiểm thử — gửi bài từ liên kết

Ngày: 12/11/2026. Kiểm tra trên Linux với SQLite, API và worker thật của ứng dụng; Telegram được thay bằng FakeBackend. Không dùng session được tải lên hoặc gửi bài lên Telegram thật.

## Kết quả

- Bộ Python chọn lọc: **89 passed, 40 deselected** (post routes, routes/jobs API, forwarding E2E, engine, accounts, migrations). Sau sửa cuối kiểm thử lại post routes + forward engine **32 passed, 7 deselected**, rồi post routes **11 passed, 8 deselected**, gồm kiểm tra bổ sung việc hạn chế ngay trong xác minh. Các lần chạy có trùng test, không cộng tổng.
- Frontend: **96 passed, 12 files**, gồm 3 kiểm thử mới cho form TXT, cổng kiểm tra quyền trước khi gửi và chọn giữ nhóm hợp lệ.
- `npm run build`: TypeScript + Vite thành công, dist được đóng kèm ZIP.
- Chromium: kiểm tra toàn luồng upload TXT, dán link, chọn SS, lưu nháp, xác minh, bắt đầu, tạm dừng/chạy tiếp và kết thúc; xác nhận 3 nhóm duy nhất nhận đúng message 123 một lần trong tình huống bình thường. Nháp và xác minh không gửi bài. Khoảng cách gửi đo được tối thiểu 5 giây với cấu hình thử 5 giây. Giao diện vừa màn hình 390 và 1600 px, không lỗi JavaScript/HTTP 500.

## Các hành vi được kiểm tra

- Chỉ chấp nhận link Telegram hợp lệ, xử lý link riêng/topic, chuẩn hóa và bỏ trùng nhóm; từ chối domain lạ hoặc dòng lỗi.
- Xác minh thông qua tài khoản được chọn; kiểm tra quyền thành viên, hạn chế mặc định và bảo vệ nguồn bằng kiểu dữ liệu Telethon thật, nhưng RPC được giả lập. Link mời chỉ CheckChatInvite, không JoinChat.
- Kết quả xác minh cũ không ghi đè bản nháp đã chỉnh; một nhóm lỗi chặn bắt đầu; không tự bỏ nhóm lỗi rồi gửi phần còn lại.
- Mỗi đợt tạo hàng đợi một lần, không bật watcher cho nguồn bài. Pause/resume/stop/start không nhân hàng đợi. Lịch gửi tương lai chưa được claim; việc quá hạn không gửi dồn sau pause.
- SS đang tắt được bật khi bắt đầu; SS hạn chế/đóng băng bị chặn. PeerFlood dừng SS và tạm dừng các tuyến liên quan. FloodWait và giới hạn hiện có tiếp tục được áp dụng.
- Lease tạm trong lúc xác minh nhiều nhóm được gia hạn cùng epoch; mất lease hủy thao tác và dọn task. Worker khác hoặc epoch cũ không gia hạn được.
- Migration 0013 và tuyến watch cũ được kiểm tra trong bộ chọn lọc.

## Phạm vi chưa thử

Chưa chạy Docker Desktop/Windows hoặc PostgreSQL thực trong lượt này. Chưa thử với Telegram thật; quyền truy cập, slow mode và hạn chế thực tế do Telegram quyết định. Khôi phục sau lỗi ở khoảng giữa Telegram nhận bài và API nhận kết quả vẫn có khả năng gửi lại như cơ chế hàng đợi hiện có.
