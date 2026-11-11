# DEVYN FORWARDER — check spam / đóng băng

[**Tải ZIP mới: nút check trực tiếp và hàng loạt**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-spam-frozen-check.zip)

Giữ **.env.docker và Docker volume**, giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để build API/web/worker, sau đó dùng **run.cmd**. Không thêm migration; head vẫn **0009**. Ctrl+F5 nếu trình duyệt còn giao diện cũ.

## Cách dùng

Vào **Tài khoản Telegram**:

- **Check spam / đóng băng** ngay mỗi dòng tài khoản.
- **Check tất cả theo bộ lọc (N)** kiểm tra mọi kết quả lọc, kể cả trang khác.
- Hoặc tích các SS và dùng **Check spam / đóng băng đã chọn**.
- Bộ lọc nhanh **Bị spam / Đóng băng / Chưa check spam / Lỗi check spam**.
- Kết quả tự cập nhật trong bảng; tiến độ từng SS tại **Tác vụ hàng loạt → Chi tiết**.

Check gửi /start tới @SpamBot chính thức. Kết quả mới trong 10 phút có thể được dùng lại; giữ cuộc hội thoại của tài khoản vừa kháng nghị. “Live” chỉ nghĩa là đăng nhập được. SpamBot không hạn chế không bảo đảm quyền gửi trong mọi nhóm. Đóng băng được nhận diện từ lỗi FROZEN hoặc thông báo rõ ràng được hỗ trợ; không suy đoán từ lỗi mạng.

Đã sửa lỗi ghi Live khi get_me thành công nhưng SpamBot trả account_frozen. Giữ nhận diện DEVYN FORWARDER, sáng/tối, bố cục điện thoại và các chức năng bản trước.

[Hướng dẫn](HUONG_DAN_CHECK_HAN_CHE.md) · [Kiểm thử](KIEM_THU_CHECK_HAN_CHE.md) · [Windows](HUONG_DAN_WINDOWS.md)

67 kiểm thử Python liên quan và 54 frontend qua; production build thành công. Browser kiểm tra nút từng dòng, check theo bộ lọc và mobile bằng dữ liệu giả. Không dùng session người dùng/gửi Telegram thật; ZIP không chứa session, .env.docker, khóa hoặc database cá nhân.

SHA256: `457895818d5db906bb1ee70a6fe5c36f330ea766171af0be0d4942e51d9608ba`.

## Bản trước

- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
- [SpamBot / kháng nghị](telegram-forwarder-control-center-spam-check-appeal.zip)
- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
