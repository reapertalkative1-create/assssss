# DEVYN FORWARDER — nhóm tài khoản và nhóm Telegram

[**Tải ZIP mới tại đây**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-account-telegram-groups.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ, chạy **setup.cmd một lần** để nâng database **0014** và build API/web/worker; lần sau dùng **run.cmd**.

- **Nhóm tài khoản**: tạo, đổi tên, xóa nhóm; chọn nhiều SS để chuyển hoặc bỏ nhóm, lọc và thao tác theo nhóm. Xóa nhóm giữ tài khoản/session; mỗi SS một nhóm phân loại.
- **Nhóm Telegram**: tại dòng SS đã xác thực chọn Thao tác → Nhóm Telegram. Xem, tìm, làm mới và xuất TXT nhóm chat đã tham gia. Tối đa 2.000 nhóm/lần, không tự tham gia/rời nhóm; quyền đăng cần kiểm tra tại tuyến gửi.

[Hướng dẫn](HUONG_DAN_NHOM_TELEGRAM.md) · [Kiểm thử](KIEM_THU_NHOM_TELEGRAM.md) · [Windows](HUONG_DAN_WINDOWS.md)

Kiểm thử Python chọn lọc, 98 frontend và build qua. Chromium với SQLite và dữ liệu giả kiểm tra tạo/lọc/xóa nhóm giữ SS, tìm nhóm Telegram và tải TXT ở desktop/mobile. Không dùng Telegram thật hoặc session người dùng; chưa thử Windows/Docker Desktop/PostgreSQL thực.

ZIP gồm source/dist, không có session, khóa, database hoặc .env riêng. SHA256: `560da333ebe4f2f656a4a53d055b75dab6ff246acde14750f7d6a7f548462022`.

## Bản trước

- [Biểu mẫu gửi bài gọn](devyn-forwarder-compact-send.zip)
- [Gửi bài từ liên kết + TXT nhóm](devyn-forwarder-post-link-routes.zip)
- [Thời hạn hạn chế ngay trên dòng SS](devyn-forwarder-restriction-expiry.zip)
- [Check list proxy độc lập](devyn-forwarder-proxy-list-checker.zip)
- [API lưu một lần](devyn-forwarder-saved-api-settings.zip)
- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
