# Chọn nhiều SS gửi bài — DEVYN FORWARDER

## Cách 1: chọn tại Tài khoản Telegram

Tích các SS cần dùng (có thể chọn toàn bộ kết quả lọc và bỏ tích vài SS), bấm **Gửi bài (N)**. Biểu mẫu mở với đúng phạm vi đã chọn; SS chưa đủ điều kiện được loại và báo số lượng. Nếu chuyển qua trang Tuyến chuyển tiếp bằng menu, mở Gửi bài từ liên kết rồi bấm **SS đã tích (N)** để lấy lựa chọn đó.

Lựa chọn đã tích được giữ trong bộ nhớ của tab trong phiên mở ứng dụng; tải lại trang hoặc đăng xuất sẽ xóa lựa chọn này. Bản nháp đã lưu và phân công trong cụm được lưu ở database, vẫn còn sau khi tải lại.

## Cách 2: chọn ngay trong Tài khoản gửi

- Ô tìm tên/username và **Nhóm tài khoản gửi** lấy dữ liệu từ Tài khoản Telegram.
- Tích từng SS, **Chọn trang này**, hoặc **Chọn toàn bộ kết quả** để lấy cả các trang khác.
- Chọn một nhóm rồi bấm Chọn toàn bộ kết quả để lấy nhóm đó. Có thể tiếp tục chọn nhóm khác; SS trùng chỉ tính một lần.
- **Chỉ xem đã chọn**, bỏ tích từng SS hoặc **Bỏ chọn hết** để chỉnh lại.
- SS chưa xác thực, đang xóa, die, đóng băng, bị spam/chặn hoặc chưa gán worker không được chọn. Worker có thể đang offline khi lưu nháp; cần online khi kiểm tra và gửi.

## Phân công và gửi

1. Dán liên kết bài viết, dán/tải TXT nhóm nhận, chọn cách gửi và thời gian nghỉ theo SS.
2. Bấm **Lưu đợt gửi**: chỉ lưu bản nháp. Hệ thống bỏ các dòng nhóm trùng và chia danh sách nhóm nhận giữa các SS đã chọn theo thứ tự tên tài khoản. Mỗi nhóm giao cho một SS; không nhân toàn bộ danh sách cho mọi SS. Tối đa 1.000 SS và 1.000 nhóm nhận trong một cụm; nếu số SS nhiều hơn nhóm nhận, chỉ các SS được phân công tạo tuyến và phần còn lại được báo rõ.
3. **Cụm tài khoản gửi** hiển thị từng SS và danh sách nhóm được giao. Bấm **Kiểm tra tất cả** để kiểm tra quyền trên từng tài khoản.
4. **Bắt đầu SS đã đạt (N)** chỉ chạy các SS đã kiểm tra đạt và không bị hạn chế. Theo dõi kết quả, **Tạm dừng / Tiếp tục / Dừng** chung hoặc mở **Chi tiết SS**.
5. Ở danh sách tuyến, nút **Cụm gửi** mở lại phân công và tiến độ đã lưu.

SS không có quyền ở nhóm được giao cần sửa danh sách và kiểm tra lại. Hệ thống giữ giới hạn FloodWait theo tài khoản, không tự chuyển nhóm sang SS khác khi tài khoản bị hạn chế. Nếu hai dạng link/ID khác nhau cùng trỏ tới một nhóm Telegram trong cụm, hệ thống chặn bắt đầu để sửa trùng. Sửa một tuyến đã lưu chỉ sửa phân công của SS đó; tạo bản mới để chọn lại nhiều SS.

## Cập nhật

Giải nén đè vào đúng thư mục cũ, giữ `.env.docker` và Docker volume. Chạy **setup.cmd** một lần rồi **run.cmd**, làm mới web bằng **Ctrl+F5**. Database vẫn 0014. Bao gồm các bản sửa nhập SS đúng nhóm, chuyển nhóm và proxy trước đây.
