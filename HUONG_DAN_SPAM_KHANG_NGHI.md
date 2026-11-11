# Tự check sau nhập, kiểm tra spam và tương tác kháng nghị

## Cập nhật

Giữ nguyên `.env.docker` và Docker volume. Giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để nâng database lên **0008** và build API/web/worker. Lần sau dùng **run.cmd**.

## Tự kiểm tra sau nhập session

Trong **Tài khoản Telegram → Nhập session hàng loạt**, tùy chọn **Sau nhập: tự check phiên/API và spam qua @SpamBot (gửi /start)** mặc định được chọn.

Luồng gồm: đọc/chuyển đổi session → xác thực API/session → ghi nhận tình trạng phiên → gửi `/start` tới **@SpamBot** chính thức để hỏi hạn chế spam. Nếu muốn chỉ xác thực phiên, bỏ chọn tùy chọn này trước khi nhập.

Kết quả phiên và kết quả spam hiển thị riêng trong hộp nhập và danh sách. Session hợp lệ vẫn được giữ khi SpamBot lỗi mạng hoặc chưa phản hồi. Quyền đọc/gửi của từng tuyến tiếp tục dùng **Verify** trong mục Tuyến chuyển tiếp.

Ứng dụng không tự kháng nghị sau nhập; kháng nghị cần người dùng đọc nội dung và xác nhận gửi.

## Check lại và lọc hàng loạt

- Chọn tài khoản hoặc toàn bộ kết quả lọc, bấm **Check phiên + spam đã chọn**, xác nhận. Hoạt động này gửi `/start` tới SpamBot cho các tài khoản cần kiểm tra.
- Bộ lọc **Mọi tình trạng spam** gồm: chưa check, không hạn chế, bị hạn chế, cần đọc phản hồi và lỗi check.
- Check hàng loạt dùng lại kết quả mới trong 10 phút. Những tài khoản vừa tương tác kháng nghị trong 15 phút sẽ được bỏ qua để giữ cuộc hội thoại; đọc kết quả qua nút Lấy phản hồi mới.
- Trên từng tài khoản, mở **Thao tác → SpamBot / kháng nghị** để xem chi tiết. Check thủ công có khoảng chờ tối thiểu 30 giây. FloodWait của Telegram được giữ nguyên và chặn thao tác tới hết thời gian yêu cầu.

## Kháng nghị theo hội thoại thật của SpamBot

1. Mở **SpamBot / kháng nghị**, đọc phản hồi gốc.
2. Nếu bot có nút phù hợp, bấm nút trên web, xem nội dung rồi **Xác nhận bấm nút**. Nút hiển thị lấy từ phản hồi hiện tại của bot; worker kiểm tra lại nút trước khi bấm.
3. Khi bot hỏi nội dung, nhập thông tin thực tế vào **Nội dung kháng nghị / trả lời SpamBot**, bấm **Xem trước và gửi kháng nghị**.
4. Kiểm tra nội dung và đúng tài khoản/đích **@SpamBot**, rồi bấm **Xác nhận gửi nội dung**.
5. Dùng **Lấy phản hồi mới** để đọc tiếp mà không gửi lại `/start`. Kết quả xét duyệt do Telegram trả về trong hội thoại.

Không dùng một kịch bản kháng nghị cố định tự bấm mọi nút. Các câu hỏi của SpamBot có thể thay đổi theo tài khoản. Nếu bot yêu cầu CAPTCHA, chia sẻ thông tin hoặc mở liên kết, hoàn tất phần đó trong ứng dụng Telegram; web chỉ hỗ trợ nút văn bản/callback phù hợp, không tự chia sẻ số điện thoại/vị trí hoặc mở URL.

Trạng thái **đã gửi** xác nhận tương tác đã gửi tới bot, không xác nhận Telegram duyệt hay gỡ hạn chế. Khi mất phản hồi có thể hiện **chưa xác nhận**; dùng Lấy phản hồi mới trước khi quyết định gửi tiếp. Ứng dụng không tự phát lại yêu cầu kháng nghị. Mã yêu cầu giúp thử lại một HTTP request mà không tạo một lệnh gửi thứ hai.

## Ý nghĩa kết quả spam

- **SpamBot: không hạn chế**: nhận diện thông báo chính thức rõ ràng rằng hiện không áp dụng hạn chế.
- **SpamBot: bị hạn chế**: nhận diện thông báo rõ ràng về hạn chế tài khoản.
- **Cần đọc phản hồi**: ngôn ngữ/cấu trúc mới hoặc thông báo đang chờ xét duyệt; xem nội dung gốc, không tự kết luận đã hết hạn chế.
- **Lỗi check spam**: lỗi bot/mạng/worker, xem nguyên nhân và thời gian chờ.

Bộ nhận diện tự động bảo thủ, có mẫu tiếng Anh và một số mẫu tiếng Nga; không đảm bảo mọi ngôn ngữ/cách diễn đạt. Hạn chế spam, đóng băng và session Die là các tình trạng khác nhau. Check spam không kiểm tra mọi quyền Telegram hay đảm bảo gửi được tới mọi nhóm/người dùng.

## Quyền và lưu trữ

Tương tác SpamBot dành cho quản trị viên. Đích gửi được cố định là @SpamBot, không nhận địa chỉ tùy ý. Nội dung lệnh kháng nghị và phản hồi bot được mã hóa; payload gửi cho worker được xóa khỏi hàng đợi khi giao. Audit chỉ ghi loại thao tác, không ghi nội dung kháng nghị hoặc phản hồi gốc. Kiểm tra/xoay khóa bao gồm phản hồi SpamBot.

Kiểm thử của bản phát hành dùng session/bot giả. File session người dùng gửi trong chat không được dùng để gửi tin Telegram hoặc đưa vào ZIP/GitHub.
