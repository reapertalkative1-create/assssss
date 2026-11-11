# Telegram Forwarder Control Center — kháng nghị hàng loạt theo mẫu

[**Tải ZIP mới: kháng nghị hàng loạt theo mẫu điền từng SS**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-bulk-appeal-template.zip)

Giữ nguyên **.env.docker và Docker volume**, giải nén đè mã nguồn, chạy **setup.cmd một lần** để nâng migration **0009** và build API/web/worker. Sau đó dùng **run.cmd**.

## Cách dùng

Chọn SS → **Kháng nghị theo mẫu đã chọn** → nhập email chung hoặc riêng → **Chuẩn bị bản xem trước** → kiểm tra từng nội dung đã điền → xác nhận gửi các bản sẵn sàng.

- `{name}`: tên SS trong ứng dụng.
- `{phone}`: số điện thoại đọc từ chính session, có tùy chọn khai báo riêng.
- `{email}`: email bạn cung cấp. Telegram không trả đầy đủ email qua session; ứng dụng không tự đoán.

Mẫu có thể sửa. Nội dung như “I never spam messages” cần đúng với các tài khoản đã chọn và được người dùng xác nhận trước khi gửi. Bước chuẩn bị chỉ đọc/tạo nháp, chưa gửi kháng nghị.

Chỉ gửi khi SpamBot đang ở bước yêu cầu mô tả được nhận diện và ngữ cảnh vẫn khớp lúc gửi. Tài khoản chưa đúng bước được báo riêng; dùng cửa sổ SpamBot để hoàn tất bước phù hợp rồi tạo nháp mới. Gửi tin không bảo đảm Telegram duyệt/gỡ hạn chế.

[Hướng dẫn](HUONG_DAN_KHANG_NGHI_THEO_MAU.md) · [Kiểm thử](KIEM_THU_KHANG_NGHI_THEO_MAU.md) · [Windows](HUONG_DAN_WINDOWS.md)

309 kiểm thử Python và 51 kiểm thử giao diện qua. Chromium/FakeBackend: chọn 3 SS giả, chuẩn bị 2 bản chính xác và báo 1 chưa sẵn sàng; 0 tin trước khi duyệt, đúng 2 tin sau duyệt. Chưa dùng session người dùng gửi Telegram thật. Nội dung/email/số trong nháp và payload được mã hóa.

Giữ chức năng nhập tự chia lô, quản lý/check session, SpamBot và Xóa đã chọn một lần bấm. ZIP không chứa session người dùng, .env.docker hoặc database cá nhân.

SHA256: `745ae249ceb155eee37c0cbf28e8b0aa33d746dd5232a06fc9cba975f45c0423`.

## Bản trước

- [Xóa hàng loạt không gõ xác nhận](telegram-forwarder-control-center-bulk-delete.zip)
- [SpamBot / kháng nghị](telegram-forwarder-control-center-spam-check-appeal.zip)
- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
- [Đăng nhập/API credentials trên web](telegram-forwarder-control-center-web-login.zip)
- [BOM fix](telegram-forwarder-control-center-windows-autoconnect-bomfix.zip)
- [Tự kết nối worker](telegram-forwarder-control-center-windows-autoconnect.zip)
- [Windows cách ly](telegram-forwarder-control-center-windows-isolated.zip)
- [Khôi phục](telegram-forwarder-control-center-phase6-fixed-v2-recovered.zip)
