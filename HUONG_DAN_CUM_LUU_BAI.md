# Cụm làm việc: lưu bài, chạy lại và khoảng nghỉ

Phiên bản `2026.11.15-saved-clusters`, database **0017**.

## Cập nhật

Giữ `.env.docker` và Docker volume. Giải nén đè toàn bộ nội dung ZIP vào đúng thư mục đang dùng, chạy **setup.cmd** một lần để cập nhật API/web/worker và nâng database, rồi **run.cmd**. Trên web nhấn Ctrl+F5. Cuối trang ghi **Cụm đã lưu · 15.11.2026**.

## Sử dụng

1. Mở **Cụm làm việc → Tạo cụm làm việc** hoặc bấm **Sửa** trên cụm có sẵn.
2. Đặt tên, chọn SS, nhập nhóm nhận và **Liên kết bài viết Telegram**.
3. Nhập **Nghỉ giữa hai nhóm (giây) → Từ / Đến**. Cụm mới mặc định **150 / 180**. Hai mốc bằng nhau tương đương khoảng nghỉ cố định.
4. Bấm **Lưu cụm**. Link và hai mốc nghỉ nằm trong database; tắt trình duyệt/máy rồi mở lại vẫn còn.
5. Bấm **Chạy** ngay trên thẻ cụm. Tool dùng cấu hình đã lưu, kiểm tra nhóm rồi bắt đầu những SS đủ điều kiện. Không yêu cầu dán lại link. Cửa sổ hiện tiến độ và lỗi từng SS; bấm **Mở lượt & tiến độ** để điều khiển tiếp.
6. Muốn đổi bài hoặc khoảng nghỉ, bấm **Sửa → Lưu cụm**. Thay đổi chỉ áp dụng cho lượt mới. Lịch sử giữ bài và cấu hình tại thời điểm tạo.

**Lịch sử** nằm ngay trên thẻ cụm. Menu/trang riêng **Tuyến chuyển tiếp** đã bỏ; đường dẫn cũ chuyển tới Cụm làm việc. Dữ liệu lượt gửi và hàng đợi được giữ, không xóa SS hay lịch sử.

## Cụm đã tạo trước đây

Khi nâng lên 0017, cụm cũ giữ khoảng nghỉ đã đặt (ví dụ 90 giây trở thành 90–90). Link được lấy từ lượt gần nhất của cụm nếu có. Cụm chưa từng có lượt gửi cần lưu link một lần bằng **Sửa**. Bấm Sửa để đổi khoảng nghỉ sang 150–180 hoặc khoảng khác.

## Phạm vi chạy

Chức năng chạy cụm dành cho nhóm/kênh SS có quyền quản trị và quyền đăng bài. Kiểm tra quyền trước khi bắt đầu và kiểm tra lại trước từng lần gửi. Nhóm chưa tham gia/thiếu quyền sẽ có lỗi, không tự tham gia rồi gửi. Không bổ sung xoay SS/proxy để vượt hạn chế.

Khoảng nghỉ được lấy ngẫu nhiên trong giới hạn đã lưu và giữ cùng từng tác vụ, không lấy lại mỗi lần kiểm tra hàng đợi. Khoảng nghỉ áp dụng giữa các lần xử lý của SS. FloodWait, giới hạn tần suất, proxy lỗi, tài khoản bị hạn chế và kết quả gửi chưa rõ vẫn được giữ; vì vậy thực tế có thể chờ lâu hơn mốc Đến.

Chạy lại cùng bài không tạo thêm tin nhắn trùng ở nhóm đã có trong lịch sử. Dùng **Lịch sử → Mở lượt** để tiếp tục lượt đang dừng/tạm dừng. **Dừng thao tác** trong cửa sổ Chạy dừng xử lý các SS kế tiếp; các lượt đã bắt đầu tiếp tục và có thể dừng trong phần tiến độ.
