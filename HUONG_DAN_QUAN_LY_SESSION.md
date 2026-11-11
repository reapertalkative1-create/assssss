# Quản lý nhiều session

## Cập nhật

Giải nén đè vào thư mục đang dùng, **giữ nguyên .env.docker và Docker volume**. Chạy **setup.cmd một lần** để nâng database lên migration **0007** và build lại API/web/worker. Sau đó dùng **run.cmd** như trước.

## Nhập không có trần tổng 100 session

- Chọn nhiều file Telethon `.session` hoặc một ZIP lớn. Web đọc ZIP từng thành viên, tự chia thành nhiều yêu cầu tối đa 100 file và khoảng 8 MiB dữ liệu mỗi lô. Không cần tự chia ZIP thành từng gói 100.
- ZIP Store/Deflate được hỗ trợ; có xử lý metadata ZIP64. Không hỗ trợ ZIP có mật khẩu/nhiều phần, Pyrogram hoặc tdata.
- Mỗi file session vẫn tối đa **1 MiB**; đây là giới hạn cho một file, không phải số tài khoản. Không áp dụng trần 100 cho tổng danh sách, tổng lần nhập hoặc chọn toàn bộ kết quả lọc. Khả năng chạy đồng thời thực tế phụ thuộc RAM/CPU, mạng, Telegram và số worker.
- Chọn worker Online, nhập API ID/hash rồi bấm Nhập. Nếu nhiều cặp API khác nhau, chia thành từng lô tương ứng.
- Worker check tối đa 3 session cùng lúc và hạn chế số lệnh đang giữ trong RAM. Session hợp lệ không cần OTP; session trùng trong các lô đã nhập được bỏ qua.
- Có **Dừng tải thêm**. Những lô đã gửi vẫn xử lý; file chưa gửi không bị nhập. Khi lỗi/đóng trình duyệt giữa chừng, chọn lại ZIP/file: session đã nhập được bỏ qua, không tạo bản sao.
- Tiến độ trong hộp nhập được phân trang. Khi đóng hộp, các tài khoản và lệnh đã gửi vẫn còn trên máy chủ.

## Chọn và thao tác hàng loạt

1. Lọc theo tình trạng session, trạng thái xác thực, worker, bật/tắt hoặc tìm tên/username.
2. Chọn từng dòng, **Chọn trang hiện tại** hoặc **Chọn toàn bộ N kết quả lọc**. Có thể bỏ chọn một vài dòng sau khi chọn toàn bộ. Chọn theo trang được giữ khi chuyển trang; đổi bộ lọc sẽ bỏ lựa chọn cũ.
3. Chọn **Bật**, **Tắt**, **Check session**, **Đánh dấu đóng băng** hoặc **Bỏ dấu đóng băng**, rồi xác nhận số lượng.
4. Mục **Tác vụ hàng loạt** hiển thị tổng số, xong, lỗi và đang chờ. Có phân trang/lọc lịch sử; tác vụ đang chạy được ưu tiên hiển thị.
5. Mở **Chi tiết → Chỉ lỗi**, hoặc bấm **Thử lại các mục lỗi** để tạo tác vụ mới đúng những tài khoản lỗi.

Tắt chỉ yêu cầu worker dừng sử dụng phiên; không đăng xuất Telegram hoặc xóa session. Bật/Tắt ghi trạng thái mong muốn: worker áp dụng khi kết nối. Bật cần tài khoản đã xác thực và không bị đánh dấu đóng băng/Die.

Danh sách tài khoản hiển thị 20/50/100 dòng mỗi trang, menu Thao tác trên từng dòng và bộ đếm tình trạng. Không nạp toàn bộ danh sách vào bảng.

## Ý nghĩa tình trạng

| Tình trạng | Ý nghĩa |
|---|---|
| Chưa check | Chưa có kết quả xác thực gần đây; dữ liệu cũ sau nâng cấp bắt đầu ở đây. |
| Live — đăng nhập được | Lần kiểm tra gần nhất đăng nhập/đọc thông tin tài khoản thành công. Không khẳng định có mọi quyền gửi tin hoặc không bị hạn chế. |
| Die / phiên hết hiệu lực | Telegram từ chối auth key, thu hồi phiên, vô hiệu hóa tài khoản hoặc phiên bị dùng trùng từ nhiều nơi. Có thể cần đăng nhập lại. |
| Đóng băng | Telegram trả lỗi có mã FROZEN, hoặc người dùng tự đánh dấu. Nhãn thủ công hiển thị rõ **Bạn đánh dấu**. |
| FloodWait — cần chờ | Telegram yêu cầu chờ. Hiển thị thời điểm được thử lại; không tự coi là Die. |
| Lỗi kiểm tra | Lỗi mạng/timeout/API/worker. Không tự vô hiệu hóa session vì lỗi mạng. |

Telegram có thể cho tài khoản bị hạn chế đọc thông tin bình thường; check không gửi tin thử và không đảm bảo phát hiện mọi hình thức đóng băng. Chỉ ghi nhận kết luận Telegram thực sự trả về. Bạn có thể đánh dấu thủ công để quản lý, tắt hàng loạt nhóm này. Bỏ nhãn thủ công không xóa lỗi đóng băng Telegram đã xác nhận; check thành công sau đó mới cập nhật kết quả tự động.

Tình trạng có thời gian check và nguyên nhân; đây là kết quả lần gần nhất, không phải giám sát liên tục mọi quyền Telegram.

## Tác vụ bền vững và tài nguyên

Mỗi tác vụ chụp danh sách ID được chọn vào database, không phụ thuộc trang web đang mở. API xử lý theo lô, tự tiếp tục phần còn lại khi khởi động lại với cùng database. Đóng web không hủy tác vụ. Tắt máy/API thì dừng xử lý tới khi chạy lại.

Check hàng loạt chỉ xếp tối đa khoảng 30 lệnh chờ/đang chạy mỗi worker, phần còn lại ở database. Worker đọc từng nhóm và check có giới hạn đồng thời, tránh tạo hàng nghìn kết nối cùng lúc. Các lần Bật cũng khởi tạo kết nối theo nhóm nhỏ. Không bỏ qua thời gian chờ Telegram.

**Dừng xếp hàng** hủy phần chưa gửi, không rút lại lệnh worker đã nhận. Những lệnh đó vẫn hoàn tất và được ghi kết quả. Lệnh đã giao bị mất khi worker chết có thể cần chờ hết hạn rồi Check lại; không hứa hoàn tất vô hạn trong một thời gian cố định.

API quản lý theo database, không có trần số session toàn hệ thống trong mã. Các giới hạn mỗi yêu cầu/file, phân trang và hàng đợi vẫn được giữ để kiểm soát bộ nhớ. Chọn thủ công hoặc bỏ chọn tối đa 10.000 ID trong một yêu cầu; dùng **Chọn toàn bộ kết quả lọc** cho tập lớn hơn.

Session/API pair vẫn được mã hóa. ZIP nguồn công khai không chứa session người dùng, `.env.docker` hoặc database cá nhân.
