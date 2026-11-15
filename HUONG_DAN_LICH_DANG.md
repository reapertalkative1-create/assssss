# DEVYN FORWARDER — lịch đăng theo cụm

Phiên bản: `2026.11.15-scheduled-posts`. Database vẫn `0017`.

## Cập nhật

Giữ `.env.docker`, thư mục cài hiện tại và Docker volume. Giải nén đè toàn bộ nội dung ZIP vào đúng thư mục đó, chạy `setup.cmd`, rồi `run.cmd`. Bấm Ctrl+F5 trên web; cuối trang phải hiện **Lịch đăng · 15.11.2026**. Không cần tạo lại admin, session hoặc cụm.

## Đặt lịch

1. Vào **Cụm làm việc**, bấm **Sửa** để lưu bài viết, SS, nhóm nhận và khoảng nghỉ. Cụm mới mặc định 150–180 giây; có thể sửa hai mốc.
2. Bấm **Lên lịch**, chọn ngày/giờ theo múi giờ hiển thị trong cửa sổ, rồi **Lưu lịch & kiểm tra**. Giờ gửi phải sau ít nhất 30 giây và trong 90 ngày tới.
3. Chờ kiểm tra từng SS. Chỉ những dòng hiện **Chờ lịch** đã được xếp hàng. Dòng lỗi vẫn là bản nháp, cần xem và xử lý trong **Mở lượt & tiến độ**.
4. Sau khi xếp hàng, có thể đóng trình duyệt. Máy, Docker và worker phải chạy để đăng đúng giờ. Nếu worker tắt lúc hẹn, hàng đợi được giữ và chạy khi worker hoạt động lại; giờ bắt đầu thực tế cũng có thể muộn hơn do FloodWait hoặc SS đang bận.
5. Vào **Lịch sử → Mở lượt**, tích SS rồi chọn **Tạm dừng**, **Tiếp tục** hoặc **Dừng lượt gửi → Áp dụng**. Dừng không thu hồi bài đã gửi; yêu cầu đang gửi tới Telegram có thể hoàn tất. Có thể dùng **Chi tiết SS** để xem từng nhóm và điều khiển riêng.

**Chạy** vẫn dùng bài đã lưu và bắt đầu ngay. **Sửa cụm** chỉ thay cấu hình cho lượt sau; lịch đã xếp hàng giữ bài/SS/nhóm/khoảng nghỉ lúc tạo. Chưa có sửa giờ cho lượt đã xếp hàng; có thể tạm dừng và tiếp tục thủ công khi cần. Cùng một bài và nhóm đã được xếp hàng/gửi sẽ được chống trùng, kể cả từ cụm khác; tạo lại không phải cách gửi lặp.

Ngày/giờ đang nhập được lưu tạm trên trình duyệt. Thử lại sau lỗi mất mạng dùng cùng mã yêu cầu, tránh tạo lượt trùng. Thay giờ sẽ tạo một yêu cầu mới.

## Nhóm được phép đăng

Dùng danh sách nhóm đã cho phép bạn đăng tin. SS phải **đã tham gia và có quyền gửi loại nội dung đó**. Thành viên thường có quyền gửi được hỗ trợ; không bắt buộc làm quản trị nhóm. Kênh broadcast vẫn cần quyền đăng của kênh. Worker kiểm tra lại tư cách thành viên và quyền gửi ngay trước từng bài, bao gồm sau thời gian chờ lịch.

Ứng dụng không tự tham gia nhóm/kênh và không chạy vòng lặp vô hạn. Mỗi lượt gửi hữu hạn; mỗi nhóm được giao một SS cố định. Giữ chống trùng, FloodWait, Slow Mode và chặn SS/proxy đang lỗi hoặc bị hạn chế. Khoảng nghỉ không đảm bảo tài khoản không bị Telegram hạn chế.

Lượt cũ từ bản `saved-clusters` giữ điều kiện SS quản trị đã lưu trong lượt đó. Lượt tạo mới ở bản này dùng điều kiện thành viên có quyền gửi. Không thay đổi hàng đợi cũ.
