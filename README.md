# DEVYN FORWARDER — gửi bài từ liên kết + TXT nhóm

[**Tải ZIP mới: tuyến gửi bài từ liên kết**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-post-link-routes.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để nâng database **0013** và build API/web/worker. Sau đó dùng **run.cmd**.

Vào **Tuyến chuyển tiếp → Gửi bài từ liên kết**: chọn SS ở Tài khoản Telegram, dán link lấy từ Sao chép liên kết tin nhắn, tải TXT/dán danh sách nhóm, chỉnh khoảng nghỉ và lịch. **Lưu → Kiểm tra nhóm → Bắt đầu gửi**. Có tìm SS, chuyển tiếp/sao chép, tiến độ từng nhóm, tạm dừng/chạy tiếp và tạo bản mới; giao diện desktop/mobile gọn. Tối đa 1.000 nhóm duy nhất mỗi đợt; gửi một lượt đúng tin nhắn ở liên kết.

Nháp/xác minh không gửi bài. Kiểm tra quyền đăng và nguồn được phép chuyển tiếp; không tự tham gia nhóm. FloodWait chờ toàn SS, PeerFlood/đóng băng dừng SS và tạm dừng các tuyến. Khoảng nghỉ không bảo đảm tránh hạn chế Telegram. Tuyến Theo dõi nguồn cũ vẫn dùng được.

Giữ toàn bộ phần tài khoản/proxy/check/xuất, API lưu trong Cài đặt, nút đỏ Xóa đã chọn, thời hạn hạn chế SS và tự chọn cổng web.

[Hướng dẫn](HUONG_DAN_GUI_BAI_TU_LINK.md) · [Kiểm thử](KIEM_THU_GUI_BAI_TU_LINK.md) · [Windows](HUONG_DAN_WINDOWS.md)

Bộ Python chọn lọc và 96 kiểm thử frontend qua; production build qua. Chromium + API/worker/FakeBackend xác nhận TXT/link/SS, kiểm tra quyền, pause/resume và khoảng nghỉ thực tế, 3 nhóm nhận đúng message 123 trong lượt thử, desktop/mobile không tràn và không lỗi JS/HTTP 500. Không dùng session người dùng hoặc Telegram thật; chưa thử Windows/Docker Desktop/PostgreSQL trong lượt này. Chi tiết số lượt kiểm thử trong tài liệu.

ZIP gồm source/dist; không có session, khóa, .env riêng hoặc database. SHA256: `10eeade75eef7ec50c87f4b0948e669423b664e3202fbba43f1f97f5f8e15df1`.

## Bản trước

- [Thời hạn hạn chế ngay trên dòng SS](devyn-forwarder-restriction-expiry.zip)
- [Check list proxy độc lập](devyn-forwarder-proxy-list-checker.zip)
- [API lưu một lần](devyn-forwarder-saved-api-settings.zip)
- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
