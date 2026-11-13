# DEVYN FORWARDER — sửa hiển thị SS trong nhóm

[**Tải ZIP mới tại đây**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-fix-group-members.zip)

Mở **Tài khoản Telegram → Nhóm tài khoản → Xem SS → Thêm SS**. Chọn SS (có thể qua nhiều trang), bấm **Thêm vào nhóm**; danh sách thành viên tự hiện và vẫn còn khi tải lại trang. Chọn SS từ bảng chính cũng được, cần chọn rõ nhóm đích. Xóa nhóm vẫn giữ SS; mỗi SS thuộc tối đa một nhóm.

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ, chạy **setup.cmd một lần** để build API/web/worker, sau đó **run.cmd**. Không thêm migration, database vẫn **0014**.

[Hướng dẫn](HUONG_DAN_SUA_NHOM_SS.md) · [Kiểm thử](KIEM_THU_SUA_NHOM_SS.md) · [Windows](HUONG_DAN_WINDOWS.md)

Kiểm thử API nhóm trên PostgreSQL 16 (database test riêng đã xóa), frontend và build qua. Chromium + SQLite kiểm tra thêm, xem, mở lại/tải lại, chọn ở hai trang và giao diện desktop/mobile. Không dùng session người dùng hoặc Telegram thật, không thử Windows thực.

ZIP gồm source/dist, loại session, khóa, database và .env riêng. SHA256: `caca2b5337b048bc276c3dc0c3f552679008ad7a6e577113e6174fcfc6967f2d`.

## Bản trước

- [Nhóm tài khoản và nhóm Telegram](devyn-forwarder-account-telegram-groups.zip)
- [Biểu mẫu gửi bài gọn](devyn-forwarder-compact-send.zip)
- [Gửi bài từ liên kết + TXT nhóm](devyn-forwarder-post-link-routes.zip)
- [Thời hạn hạn chế ngay trên dòng SS](devyn-forwarder-restriction-expiry.zip)
- [Check list proxy độc lập](devyn-forwarder-proxy-list-checker.zip)
- [API lưu một lần](devyn-forwarder-saved-api-settings.zip)
- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
