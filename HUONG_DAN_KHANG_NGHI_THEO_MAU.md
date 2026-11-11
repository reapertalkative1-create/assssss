# Kháng nghị hàng loạt theo mẫu điền cho từng SS

## Cập nhật

Giữ `.env.docker` và Docker volume. Giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để nâng database lên **0009** và build API/web/worker. Những lần sau dùng **run.cmd**.

## Mẫu và thông tin cá nhân

Trong danh sách tài khoản, lọc và tích các SS cần xử lý → **Kháng nghị theo mẫu đã chọn**.

Mẫu mặc định có thể sửa:

```text
Hello {name}, I am using my Telegram account on the desktop application, but I was blocked from chatting in public groups and I believe this was a mistake. I never spam messages to the group. Please check my account.

My information:
Phone Number: {phone}
Email Address: {email}

Thank you very much!
```

- `{name}`: tên hiển thị của SS trong ứng dụng; đổi tên trước khi chuẩn bị nếu cần.
- `{phone}`: worker đọc số điện thoại từ chính tài khoản đã đăng nhập qua session. Không suy ra số từ tên file. Có thể khai báo số riêng nếu không đọc được.
- `{email}`: email thực tế bạn cung cấp. Telegram không cho lấy đầy đủ email của tài khoản qua session, nên ứng dụng không tự đoán hoặc dùng email bị che một phần.

Nhập **Email liên hệ chung** nếu cùng email dùng cho các SS đã chọn. Hoặc nhập riêng theo từng dòng, tên SS/ID không phân biệt hoa thường:

```text
SS Alpha,alpha@example.com
SS Beta,beta@example.com,+15551234567
```

Dòng riêng ưu tiên hơn email chung. Số điện thoại không khai báo sẽ đọc từ session. Tên có dấu phẩy có thể dùng ID tài khoản thay thế. Nếu không dùng email, bỏ cả dòng `Email Address: {email}` khỏi mẫu. Những tài khoản thiếu dữ liệu cần thiết được báo lỗi, không điền giá trị giả.

## Chuẩn bị → xem trước → xác nhận gửi

1. Bấm **Chuẩn bị bản xem trước**. Bước này đọc thông tin tài khoản và trạng thái hội thoại SpamBot; chưa gửi kháng nghị.
2. Web hiển thị từng nội dung đã điền tên/số/email, phân trang 20 mục. Có bộ lọc Sẵn sàng/Chỉ lỗi/Đã gửi.
3. Kiểm tra mẫu và thông tin. Câu “I never spam messages” chỉ phù hợp nếu đúng sự thật với các tài khoản được chọn; sửa mẫu cho đúng trường hợp của bạn.
4. Tích **Tôi đã kiểm tra mẫu, thông tin và xác nhận nội dung đúng với tất cả tài khoản sẵn sàng gửi**.
5. Bấm **Xác nhận gửi N kháng nghị**. Chỉ những bản đã sẵn sàng và được duyệt mới xếp lệnh gửi.
6. Xem kết quả từng SS. Đóng web không làm mất tác vụ; mở lại từ **Tác vụ hàng loạt → Chi tiết** để tiếp tục xem trước/duyệt hoặc xem kết quả.

## Đúng bước SpamBot

Mẫu được gửi tới **@SpamBot** chính thức khi bot đang yêu cầu mô tả vụ việc. Bộ nhận diện chỉ cho qua các lời nhắc rõ ràng được hỗ trợ (chủ yếu tiếng Anh, một số mẫu tiếng Nga).

Nếu báo **SpamBot chưa ở bước yêu cầu mô tả**, bấm **Mở hội thoại SpamBot**, đọc và thực hiện các bước phù hợp bằng giao diện hiện có. Sau đó tạo bản xem trước mới cho nhóm cần gửi. Ứng dụng không tự bấm các câu khẳng định trong hội thoại hoặc gửi mẫu vào bước không nhận diện được.

Trước khi gửi, worker kiểm tra lại ID và nội dung câu hỏi bot. Nếu bot đã chuyển bước/chỉnh sửa câu hỏi, lệnh bị chặn với lỗi phản hồi đã thay đổi, thay vì gửi vào một ngữ cảnh khác.

CAPTCHA hoặc những bước bắt buộc thao tác trong Telegram cần người dùng hoàn tất trong ứng dụng Telegram.

## Hàng đợi và kết quả

- Lệnh chuẩn bị và gửi được xử lý theo nhóm, khoảng 30 lệnh chờ/đang chạy mỗi worker, giữ giới hạn kiểm tra đồng thời.
- Cooldown/FloodWait vẫn áp dụng. Tài khoản đang đăng nhập, worker offline hoặc thiếu session được báo riêng.
- Bấm xác nhận lại cùng tác vụ không tạo đợt gửi thứ hai. Khi gửi không rõ kết quả, ứng dụng không tự phát lại.
- Thử lại kháng nghị cần tạo bản xem trước mới; nút thử lại chung không tự gửi lại nội dung cũ.
- **Hủy phần chưa gửi** dừng phần chưa giao. Các lệnh gửi worker đã nhận có thể vẫn hoàn tất và được ghi nhận.
- **Đã gửi tin tới SpamBot** là trạng thái gửi, không bảo đảm Telegram đã tiếp nhận một phiếu hợp lệ, duyệt kháng nghị hoặc gỡ hạn chế. Theo dõi phản hồi trong cửa sổ SpamBot.

## Dữ liệu và quyền

Chỉ quản trị viên tạo/xem nội dung/duyệt các bản kháng nghị. Mẫu, email và bản đã điền số điện thoại được mã hóa với khóa hiện có. Không lưu số đầy đủ vào danh sách tài khoản công khai; chỉ hiện trong bản xem trước dành cho quản trị viên.

Bản chuẩn bị chưa duyệt được giữ mã hóa để mở lại. Khi xếp lệnh gửi, bản cá nhân trong item được xóa sau khi chuyển sang payload lệnh mã hóa; payload được xóa khỏi hàng đợi khi giao. Hủy tác vụ xóa phần nháp chưa gửi. Audit chỉ ghi loại thao tác và số lượng, không ghi nội dung hoặc email/số điện thoại đầy đủ. Kiểm tra/xoay khóa bao gồm nháp kháng nghị.

Bản này giữ nguyên nút **Xóa đã chọn** một lần bấm, không gõ tên/hộp xác nhận, và các chức năng check/import/SpamBot trước đó.
