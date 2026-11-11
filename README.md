# Telegram Forwarder Control Center — xóa các tài khoản đã tích

[**Tải ZIP mới: xóa hàng loạt không gõ xác nhận**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-bulk-delete.zip)

Giữ nguyên **.env.docker và Docker volume**, giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để build API/web mới. Sau đó dùng **run.cmd**. Không thêm migration mới (head 0008).

## Cách dùng

Vào **Tài khoản Telegram → lọc → tích các dòng hoặc Chọn toàn bộ kết quả lọc → Xóa đã chọn**. Có thể bỏ tích một vài dòng để giữ lại. Nút Xóa đã chọn xếp hàng ngay, **không mở hộp xác nhận và không bắt gõ tên**.

Xóa khỏi ứng dụng, gồm session/tuyến/tác vụ liên quan; tài khoản Telegram vẫn tồn tại và phiên không bị đăng xuất trên Telegram. Tài khoản đang chạy được yêu cầu dừng và đợi lease kết thúc trước khi dọn. Xem tiến độ trong Tác vụ hàng loạt.

[Hướng dẫn xóa](HUONG_DAN_XOA_HANG_LOAT.md) · [Kiểm thử](KIEM_THU_XOA_HANG_LOAT.md) · [Windows](HUONG_DAN_WINDOWS.md) · [Quản lý nhiều session](HUONG_DAN_QUAN_LY_SESSION.md)

Đã kiểm thử 303 Python, 49 giao diện. Chromium thật: lọc 84 tài khoản demo, bỏ tích 1, xóa đúng 83 bằng một lần bấm; giữ tài khoản ngoài lựa chọn. Không dùng tài khoản/session thật của người dùng trong kiểm thử.

Giữ các chức năng nhập tự chia lô, quản lý nhiều session, tự check SpamBot và tương tác kháng nghị từ bản trước. ZIP không chứa session người dùng, .env.docker hoặc database cá nhân.

SHA256: `cb28f32e81c6f84edce25b311dd0a68942d94bee0be6e68980372decba500eb8`.

## Bản trước

- [SpamBot / kháng nghị](telegram-forwarder-control-center-spam-check-appeal.zip)
- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
- [Đăng nhập/API credentials trên web](telegram-forwarder-control-center-web-login.zip)
- [BOM fix](telegram-forwarder-control-center-windows-autoconnect-bomfix.zip)
- [Tự kết nối worker](telegram-forwarder-control-center-windows-autoconnect.zip)
- [Windows cách ly](telegram-forwarder-control-center-windows-isolated.zip)
- [Khôi phục](telegram-forwarder-control-center-phase6-fixed-v2-recovered.zip)
