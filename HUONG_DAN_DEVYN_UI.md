# DEVYN FORWARDER — giao diện mới

## Cập nhật trên Windows

Giữ nguyên `.env.docker` và Docker volume trong thư mục cài đặt cũ. Giải nén đè toàn bộ mã nguồn từ ZIP vào đúng thư mục đó, mở Docker Desktop rồi chạy **setup.cmd một lần** để build giao diện mới. Sau đó dùng **run.cmd** như trước. Không cần nhập lại tài khoản Telegram hoặc credential worker. Không xóa volume hoặc dùng lệnh `down -v`.

Bản giao diện không thêm migration; database head vẫn là **0009**. Nếu cập nhật từ bản cũ hơn, setup sẽ tự chạy những migration còn thiếu. Không chạy chỉ run.cmd ngay sau khi chép mã nguồn vì image web cũ có thể vẫn đang được dùng. Nếu trình duyệt còn giao diện cũ, dùng Ctrl+F5.

## Giao diện

- Thương hiệu **DEVYN FORWARDER**, logo riêng, favicon và tiêu đề trình duyệt mới.
- Trang đăng nhập hai cột, có nút hiện/ẩn mật khẩu.
- Sidebar tối, điều hướng theo nhóm; tên người dùng và quyền lấy từ tài khoản đăng nhập.
- Tổng quan có thẻ chỉ số, biểu đồ tác vụ và hoạt động thực tế từ máy chủ.
- Quản lý session có thẻ lọc tình trạng, bộ lọc và nhóm thao tác hàng loạt rõ ràng.
- Đồng bộ bảng, biểu mẫu, cửa sổ, nút, trạng thái tải/rỗng/lỗi trên cả 9 trang.
- Bấm biểu tượng mặt trời ở góc phải để đổi sáng/tối. Trong **Cài đặt → Giao diện** có thêm tùy chọn theo hệ thống. Lựa chọn lưu trên trình duyệt.
- Màn hình nhỏ có nút menu góc trái; đóng bằng nút X, chạm ngoài menu hoặc Escape. Bảng rộng cuộn ngang trong khung bảng.

Giữ các tính năng nhập nhiều session, API Telegram trên web, check session/spam, SpamBot, kháng nghị theo mẫu, quản lý worker/tuyến/hàng đợi và **Xóa đã chọn** một lần bấm. Số liệu trong ứng dụng lấy từ máy chủ; bộ dữ liệu demo dùng kiểm thử không nằm trong ZIP.
