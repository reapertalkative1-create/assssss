# Telegram Forwarder Control Center — tự check sau nhập và SpamBot / kháng nghị

[**Tải ZIP bản mới: tự check + spam + kháng nghị**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-spam-check-appeal.zip)

Giữ nguyên **.env.docker và Docker volume**, giải nén đè mã nguồn vào thư mục cũ, chạy **setup.cmd một lần** để nâng migration **0008** và build API/web/worker. Sau đó dùng **run.cmd**.

## Chức năng mới

- Sau nhập có tùy chọn mặc định tự check phiên/API và hạn chế spam, gửi /start tới @SpamBot chính thức.
- Kết quả phiên và spam hiển thị riêng; lọc chưa check, không hạn chế, bị hạn chế, cần đọc phản hồi, lỗi.
- **Check phiên + spam** hàng loạt, có cooldown/FloodWait và dùng lại kết quả mới.
- **Thao tác → SpamBot / kháng nghị**: đọc phản hồi thật, xem nút bot, nhập nội dung, xem trước rồi xác nhận gửi.
- **Lấy phản hồi mới** chỉ đọc, không khởi động lại /start; không tự phát lại kháng nghị khi mất phản hồi.
- Nội dung báo cáo/appeal được mã hóa; audit không giữ nội dung gốc.

Kết quả gửi tin là trạng thái tương tác; quyết định xét duyệt do Telegram trả về trong hội thoại. Thông báo không nhận diện được sẽ giữ trạng thái cần đọc phản hồi. CAPTCHA/liên kết và các bước yêu cầu thao tác trong Telegram vẫn cần người dùng hoàn tất ở đó.

Xem [hướng dẫn SpamBot / kháng nghị](HUONG_DAN_SPAM_KHANG_NGHI.md), [kiểm thử](KIEM_THU_SPAM_KHANG_NGHI.md), [quản lý nhiều session](HUONG_DAN_QUAN_LY_SESSION.md), [Windows](HUONG_DAN_WINDOWS.md).

Đã thử Chromium với 3 session/bot giả: tự check clear/limited/unknown, lọc limited, xác nhận bấm nút, xem trước/gửi nội dung và đọc phản hồi. Chưa dùng session người dùng để gửi tin Telegram thật. ZIP không chứa session người dùng, .env.docker hoặc database cá nhân.

SHA256: `21144c8b98d26384a666ddabff22bb93b094497cff796ce39cfb90a65caac2aa`.

## Bản trước

- [Quản lý nhiều session](telegram-forwarder-control-center-session-manager.zip)
- [Nhập session](telegram-forwarder-control-center-session-import.zip)
- [Đăng nhập/API credentials trên web](telegram-forwarder-control-center-web-login.zip)
- [BOM fix](telegram-forwarder-control-center-windows-autoconnect-bomfix.zip)
- [Tự kết nối worker](telegram-forwarder-control-center-windows-autoconnect.zip)
- [Windows cách ly](telegram-forwarder-control-center-windows-isolated.zip)
- [Khôi phục](telegram-forwarder-control-center-phase6-fixed-v2-recovered.zip)
