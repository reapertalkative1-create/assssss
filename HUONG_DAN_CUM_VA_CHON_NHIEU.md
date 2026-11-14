# Cụm làm việc và chọn nhiều SS

## Cập nhật đúng bản

Giữ `.env.docker` và Docker volume. Giải nén đè đúng thư mục đang dùng, không tạo một bản cài đặt riêng trong thư mục khác. Chạy **setup.cmd** một lần rồi **run.cmd**, mở đúng địa chỉ launcher in ra và nhấn **Ctrl+F5**.

Bản mới có **Cụm làm việc** riêng trên menu trái; cuối trang ghi **Cụm & chọn nhiều · 14.11.2026**. Nếu vẫn thấy giao diện không có mục này, kiểm tra lại thư mục giải nén và địa chỉ web đang mở.

Từ bản này, `run.cmd` so sánh `APP_VERSION` với dấu cài đặt `.docker-version`. Thiếu dấu hoặc khác phiên bản sẽ tự build, dừng worker/API trước khi nâng dữ liệu, rồi mở bản mới. Phiên bản không đổi không build lại. Launcher kiểm tra `/version.json` của web, không báo thành công nếu web còn bản cũ. Nginx yêu cầu tải lại HTML/version thay vì giữ cache. Dữ liệu vẫn dùng database **0016**.

## Tạo và tìm cụm

- **Menu Cụm làm việc → Tạo cụm làm việc**: đặt tên, chọn SS, nhập TXT/dán nhóm và lưu. Mỗi ngày chọn **Bài mới**, dán link khác.
- **Tài khoản Telegram → tích SS → Tạo cụm (N)**: giữ lựa chọn SS để đặt tên và thêm nhóm nhận.
- **Tuyến chuyển tiếp → tích các dòng gửi bài từ liên kết → Lưu thành cụm**: gộp các SS/nhóm đã chọn, tự bỏ trùng. Đặt tên rồi lưu. Các lượt cũ giữ nguyên.

Nếu các dòng cũ có cách gửi/thời gian nghỉ khác nhau, biểu mẫu báo rõ để bạn kiểm tra lại. Giá trị nghỉ mặc định là thời gian dài nhất trong lựa chọn. Không thể nhập tuyến theo dõi nguồn vào cụm gửi bài từ link; dùng bộ lọc **Bài từ liên kết** trước khi chọn.

## Tích và thao tác nhiều dòng

Trong **Tuyến chuyển tiếp** có checkbox từng dòng, checkbox đầu bảng, **Chọn trang này**, **Chọn tất cả kết quả** và **Bỏ chọn**. Lựa chọn giữ nguyên khi đổi trang danh sách hoặc bộ lọc; số dòng và số SS riêng biệt hiển thị trên thanh thao tác. Bộ lọc tìm tên SS, tên cụm hoặc tên tuyến. Chọn tất cả lấy danh sách tại thời điểm bấm; dòng mới phát sinh sau đó không tự được thêm. Giới hạn mỗi lựa chọn toàn bộ là 10.000 dòng; cụm vẫn tối đa 1.000 SS/1.000 nhóm.

Chọn thao tác trong ô bên trái rồi bấm **Áp dụng (N)**:

- **Kiểm tra nhóm**: gửi yêu cầu xác minh bài/nhóm cho các dòng chưa tạo hàng chờ.
- **Bắt đầu gửi**: chỉ các dòng đang dừng, đã xác minh và SS không bị hạn chế.
- **Tạm dừng / Tiếp tục / Dừng lượt gửi**: chỉ các dòng đã tích đủ điều kiện; giữ SS phụ trách và hàng chờ theo cơ chế hiện có.
- **Xóa tuyến / lượt**: xóa dòng đang dừng và tác vụ liên quan; giữ tài khoản Telegram. Bấm nút xác nhận xóa, không phải gõ tên. Dòng đang chạy hoặc đang được worker xử lý sẽ bị bỏ qua/báo lỗi.
- **Kiểm tra SS**: kiểm tra phiên, spam/đóng băng hoặc proxy cho các SS của dòng đã chọn. Một SS xuất hiện nhiều dòng chỉ được đưa vào lượt kiểm tra một lần.

Kết quả hiển thị số đã xử lý, bỏ qua, lỗi và tên SS kèm lý do. Xác minh mới được chấp nhận chưa có nghĩa đã xác minh đạt; xem trạng thái cập nhật trước khi bắt đầu. Tool đọc lại trạng thái hiện tại trước từng thao tác, server tiếp tục áp dụng quyền, giới hạn Telegram, chống gửi trùng và các chặn lỗi hiện có.

**Ngừng thao tác** dừng các yêu cầu chưa thực hiện; yêu cầu đang gửi tới server vẫn có thể hoàn tất. Rời màn hình cũng ngừng phần chưa thực hiện. Các tác vụ kiểm tra SS đã tạo trên server tiếp tục như trước.

Trong **Mở lượt** cũng có checkbox, lọc SS, chọn cả trang/kết quả lọc và cùng thanh thao tác. Mặc định chưa chọn dòng nào. Chỉ SS đã tích được xử lý. Bảng chia trang 50 SS để giao diện nhẹ hơn.

Quản trị viên có thêm tạo cụm, kiểm tra SS và xóa; tài khoản vận hành dùng các thao tác tuyến theo quyền hiện có. Các nút quản lý tài khoản gốc vẫn ở **Tài khoản Telegram**.
