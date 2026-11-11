# DEVYN FORWARDER — thông tin ngay trên bảng SS

## Cập nhật

Giữ `.env.docker` và Docker volume. Giải nén đè ZIP mới vào đúng thư mục cũ, mở Docker Desktop rồi chạy **setup.cmd một lần** để build API/web/worker; sau đó dùng **run.cmd**. Không thêm migration, head vẫn **0009**. Ctrl+F5 nếu trình duyệt còn giao diện cũ.

## Bảng session

Đã xóa khung **Tác vụ hàng loạt** và phần tải danh sách tác vụ phía dưới. Bảng chính được gom thành các cột:

- **Tài khoản & kết nối**: tên SS, username/số đã che (nếu có), Telegram ID, xác thực, kết nối, worker, bật/tắt, API và session đã cấu hình hay chưa. SS đã xác thực nhưng chưa có username/số không còn bị ghi nhầm “Chưa đăng nhập”.
- **Tình trạng & phản hồi**: spam, session/đóng băng, thời điểm check, lỗi và FloodWait, cùng toàn bộ nội dung phản hồi SpamBot hiện lưu. Nội dung tự xuống dòng, không cần chuyển đến khung tác vụ. Phản hồi vẫn giữ giới hạn 8.000 ký tự từ bản trước. Chỉ quản trị viên được xem nội dung bot; vận hành viên vẫn xem trạng thái theo quyền cũ.
- **Tiến độ & kết quả**: đang chờ, worker xử lý, chờ duyệt, hoàn tất, thất bại, hết hạn, đã hủy; ghi rõ lỗi và thời điểm. Hiển thị tối đa 5 thao tác hàng loạt gần nhất, ưu tiên đang xử lý/chờ duyệt, cùng lệnh trực tiếp gần nhất không trùng với thao tác đó.
- **Kiểm tra / thao tác**: nút check tại dòng và các thao tác tài khoản như trước.

Kết quả tự cập nhật mỗi 5 giây và vẫn còn sau khi tải lại/đóng mở web. Check nhiều SS vẫn chạy trên máy chủ; không cần giữ trình duyệt mở. Các nút chọn nhiều SS, bật/tắt/xóa/check/kháng nghị giữ nguyên.

## Kháng nghị và dừng đợt

Bấm **Xem / duyệt kháng nghị** ngay trên dòng SS để mở lại bản đã chuẩn bị và xem/duyệt kết quả của đợt kháng nghị đó. Việc duyệt vẫn yêu cầu kiểm tra nội dung chính xác trước khi gửi.

Nút **Dừng cả đợt** trên dòng áp dụng cho tất cả SS trong cùng đợt, không chỉ dòng đang bấm. Chỉ dừng phần chưa gửi; lệnh worker đã nhận có thể vẫn hoàn tất. Có thể check lại riêng từng SS bằng nút check tại dòng.

Sau khi xóa hoàn tất, dòng SS được xóa khỏi bảng; lúc đang đợi dừng phiên sẽ hiện trạng thái chờ xóa trên chính dòng đó. Không thêm hộp xác nhận cho Xóa đã chọn.

“Cần đọc phản hồi” nghĩa là hệ thống chưa phân loại chắc nội dung SpamBot; đọc nguyên văn ngay trong cột Tình trạng & phản hồi. “Live” chỉ nghĩa là session đăng nhập được, không phải kết luận không bị cấm gửi tin.
