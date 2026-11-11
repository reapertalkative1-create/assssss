# DEVYN FORWARDER

[**Tải DEVYN FORWARDER — giao diện mới**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-professional-ui.zip)

Giữ **.env.docker và Docker volume**, giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để build bản mới, sau đó dùng **run.cmd**. Database head vẫn **0009**. Nếu vẫn thấy giao diện cũ, dùng Ctrl+F5.

## Giao diện mới

- Nhận diện **DEVYN FORWARDER**, logo SVG riêng, favicon và tiêu đề trình duyệt.
- Trang đăng nhập hai cột; sidebar tối; màu nhấn tím; bảng, biểu mẫu, nút và cửa sổ đồng bộ.
- Tổng quan có thẻ chỉ số và biểu đồ từ dữ liệu máy chủ; quản lý session có thẻ lọc tình trạng.
- Chế độ sáng/tối, tùy chọn theo hệ thống và menu điện thoại.
- Giữ nhập nhiều session, API Telegram trên web, check session/spam, SpamBot, kháng nghị theo mẫu và **Xóa đã chọn** một lần bấm.

[Hướng dẫn giao diện](HUONG_DAN_DEVYN_UI.md) · [Kiểm thử](KIEM_THU_DEVYN_UI.md) · [Windows](HUONG_DAN_WINDOWS.md)

51 kiểm thử frontend qua, TypeScript/Vite build thành công. Chromium thật kiểm tra 9 trang trên desktop/điện thoại, sáng/tối, menu và cửa sổ thao tác bằng dữ liệu giả. Không dùng session người dùng hoặc gửi tin Telegram trong đợt kiểm tra UI. ZIP không chứa session, database cá nhân, khóa hoặc .env.docker.

SHA256: `9e63566f21bd4c8e06ca360ea4246fafdf379e9aa191e47e86c2e5215e36b03e`.

## Bản trước

- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
- [SpamBot / kháng nghị](telegram-forwarder-control-center-spam-check-appeal.zip)
- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
