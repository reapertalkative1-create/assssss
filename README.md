# DEVYN FORWARDER — thông tin ngay trên bảng SS

[**Tải ZIP mới: kết quả và tiến độ trực tiếp trên dòng session**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-inline-session-details.zip)

Giữ **.env.docker và Docker volume**, giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để build API/web/worker, sau đó dùng **run.cmd**. Không thêm migration; head vẫn **0009**. Ctrl+F5 nếu trình duyệt còn giao diện cũ.

## Thay đổi

Đã xóa khung **Tác vụ hàng loạt** phía dưới. Theo dõi ngay trên bảng SS:

- **Tài khoản & kết nối**: danh tính, xác thực, worker, kết nối, bật/tắt, cấu hình API/session.
- **Tình trạng & phản hồi**: spam, đóng băng, lỗi, FloodWait, thời gian check và nguyên văn phản hồi SpamBot hiện lưu.
- **Tiến độ & kết quả**: đang chờ, worker xử lý, chờ duyệt, hoàn tất, thất bại/hết hạn và lỗi riêng từng SS.
- **Xem / duyệt kháng nghị** mở lại bản đã chuẩn bị ngay tại dòng, kể cả sau khi đóng/mở web.
- **Dừng cả đợt** ghi rõ phạm vi áp dụng cho mọi SS cùng đợt. Các nút chọn nhiều SS, check/bật/tắt/xóa/kháng nghị giữ nguyên.

Kết quả tự cập nhật mỗi 5 giây. Hoạt động từng SS được tải gộp theo trang, tối đa 5 thao tác hàng loạt ưu tiên đang xử lý/chờ duyệt cùng lệnh trực tiếp gần nhất; không cần gọi danh sách tác vụ riêng. Phản hồi bot chỉ hiện cho quản trị viên, giữ quyền vận hành viên như trước.

[Hướng dẫn bảng SS](HUONG_DAN_BANG_SS.md) · [Kiểm thử](KIEM_THU_BANG_SS.md) · [Windows](HUONG_DAN_WINDOWS.md)

67 kiểm thử Python liên quan, 56 frontend và production build thành công. Chromium thật kiểm tra thông tin trên dòng, trạng thái check mới, mở lại kháng nghị sau reload và mobile bằng dữ liệu giả. Không sử dụng session người dùng/gửi Telegram thật. ZIP không chứa session, khóa, .env.docker hoặc database cá nhân.

SHA256: `6f521a5db0b8d7119411b04564bdcf10a30cb6e6c5d8dc63953752958d1e5815`.

## Bản trước

- [Nút check spam / đóng băng](devyn-forwarder-spam-frozen-check.zip)
- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
- [SpamBot / kháng nghị](telegram-forwarder-control-center-spam-check-appeal.zip)
- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
