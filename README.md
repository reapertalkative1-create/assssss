# DEVYN FORWARDER — chọn nhiều SS gửi bài

[**Tải ZIP bản mới tại đây**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-multi-sender-groups.zip)

**Tài khoản Telegram → tích SS → Gửi bài (N)** mở biểu mẫu với các SS đã chọn. Trong biểu mẫu có tìm kiếm, lọc nhóm tài khoản, chọn trang/toàn bộ kết quả, **SS đã tích**, chỉ xem đã chọn và bỏ chọn. Có thể lấy nhiều nhóm SS, giữ các SS đã bỏ tích.

Danh sách nhóm nhận được chia giữa các tài khoản; mỗi nhóm giao cho một SS. **Lưu đợt gửi** chỉ tạo bản nháp, mở **Cụm tài khoản gửi** để xem phân công, kiểm tra tất cả, bắt đầu các SS đã đạt, tạm dừng/tiếp tục/dừng và theo dõi từng SS. Tối đa 1.000 SS/1.000 nhóm nhận mỗi cụm. Trạng thái và FloodWait vẫn theo tài khoản.

**Cập nhật:** giải nén đè đúng thư mục cũ, giữ `.env.docker` và Docker volume. Chạy **setup.cmd** một lần rồi **run.cmd**, Ctrl+F5. Database vẫn 0014; bao gồm các bản sửa nhóm/import/proxy trước.

[Hướng dẫn](HUONG_DAN_CHON_NHIEU_SS_GUI.md) · [Kiểm thử](KIEM_THU_CHON_NHIEU_SS_GUI.md) · [Windows](HUONG_DAN_WINDOWS.md)

18 kiểm thử SQLite, 15 PostgreSQL và 106 frontend đạt; production build đạt. Kiểm thử 105 SS vượt trang đầu. Chromium + API/worker giả lập xác nhận chọn từ bảng/chọn nhóm/loại SS, chia bốn nhóm cho hai SS, kiểm tra trước gửi, gửi đúng một lần và mở lại tiến độ. Không dùng Telegram thật hoặc Windows thật.

SHA256 ZIP: `77ca37897a48d670c9704ad616fdf260641bdf6ee7ec3bb7ad3f915643509e7d`.

## Bản trước

- [Sửa nhập SS vào đúng nhóm](devyn-forwarder-import-group-fix.zip)
- [Sửa danh sách thành viên](devyn-forwarder-fix-group-members.zip)
- [Nhóm tài khoản và nhóm Telegram](devyn-forwarder-account-telegram-groups.zip)
- [Biểu mẫu gửi bài gọn](devyn-forwarder-compact-send.zip)
- [Gửi bài từ liên kết](devyn-forwarder-post-link-routes.zip)
- [Check list proxy](devyn-forwarder-proxy-list-checker.zip)
- [API lưu một lần](devyn-forwarder-saved-api-settings.zip)
- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
