# DEVYN FORWARDER — chọn SS lỗi và lọc trạng thái

[**Tải ZIP bản mới tại đây**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-sender-status-fix.zip)

- Sửa checkbox: SS lỗi/bị chặn/Die vẫn tích được, giữ lựa chọn khi đổi trang hoặc bộ lọc, và lưu vào bản nháp.
- Bộ chọn gọn, có **Tất cả / Có thể chạy / Live / Die**, lọc spam/đóng băng/lỗi/worker/proxy, số đếm toàn bộ kết quả.
- Kiểm tra phiên/spam/proxy cho SS đã chọn ngay tại bộ chọn và màn hình cụm. SS hết phiên hoặc bị Telegram khóa vẫn cần xử lý lỗi trước khi gửi.

**Cập nhật:** giải nén đè đúng thư mục cũ, giữ `.env.docker` và Docker volume. Chạy **setup.cmd** một lần rồi **run.cmd**, Ctrl+F5. Database vẫn 0014; giữ các tính năng nhóm, nhập SS kèm proxy và chọn nhiều tài khoản gửi.

[Hướng dẫn](HUONG_DAN_CHON_SS_TRANG_THAI.md) · [Kiểm thử](KIEM_THU_CHON_SS_TRANG_THAI.md) · [Windows](HUONG_DAN_WINDOWS.md)

**Kiểm thử:** 22 SQLite, 19 PostgreSQL, 109 frontend đạt; production build đạt. Thử 240 SS qua 5 trang. Chromium + API/worker giả lập xác nhận chọn cả SS lỗi, lưu nháp, kiểm tra lại lỗi kết nối rồi gửi thành công. Không dùng Telegram thật hoặc Windows thật.

SHA256 ZIP: `ba40ef9d1241f604a95e0c6e99edea07f524ab7197b6dcaf6141c0e6bc24297a`.

---

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
