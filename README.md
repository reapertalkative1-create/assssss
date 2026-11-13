# DEVYN FORWARDER — nhập SS đúng nhóm và đổi nhóm

[**Tải ZIP bản sửa tại đây**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-import-group-fix.zip)

Đã sửa nguyên nhân: nhóm đang chọn trước đây chỉ dùng để lọc bảng, chưa được lưu khi nhập SS hoặc tạo tài khoản. Bản này lưu nhóm ngay khi tải lên, giữ nhóm ở mọi lô nhập và hiển thị ngay sau khi đóng cửa sổ.

- Chọn nhóm → Nhập session: ô Nhóm tài khoản tự điền. Có thể nhập SS mới trực tiếp trong nhóm.
- Nút **Đổi nhóm** trên từng SS và **Đổi nhóm (N)** cho các SS đã tích; có **Bỏ khỏi nhóm**.
- Trong nhóm: tìm kiếm, chọn trang/chọn qua nhiều trang, chuyển sang nhóm khác, bỏ nhóm; giữ tạo/đổi tên/xóa nhóm.
- Nhập lại SS trùng vào nhóm đích sẽ đổi nhóm, giữ session/proxy cũ. Không chọn nhóm đích thì giữ nhóm hiện tại.
- SS vào sai nhóm ở bản cũ: lọc **Chưa có nhóm** → tích SS → **Đổi nhóm (N)**, không cần nhập lại file.

**Cập nhật:** giải nén đè đúng thư mục đang dùng; giữ `.env.docker` và Docker volume. Chạy **setup.cmd** một lần rồi **run.cmd**, làm mới web bằng Ctrl+F5. Database vẫn 0014.

[Hướng dẫn](HUONG_DAN_NHAP_SS_VAO_NHOM.md) · [Kiểm thử](KIEM_THU_NHAP_SS_VAO_NHOM.md) · [Windows](HUONG_DAN_WINDOWS.md)

Kiểm thử: 39 SQLite, 9 PostgreSQL, 102 frontend đạt; production build đạt. Chromium + API thật xác nhận nhập vào nhóm, tải lại, đổi nhóm từng/nhiều SS, nhập trùng giữ proxy và giao diện desktop/mobile. Session kiểm thử tổng hợp; không Telegram thật hoặc Windows thật.

ZIP chứa source/dist, không chứa dữ liệu hay khóa của người dùng. SHA256: `ebe28234cc7fb48b9901c159c8d1bd7948de523289eb5aad5f6e66c0d431d8f8`.

## Bản trước

- [Sửa danh sách thành viên](devyn-forwarder-fix-group-members.zip)
- [Nhóm tài khoản và nhóm Telegram](devyn-forwarder-account-telegram-groups.zip)
- [Biểu mẫu gửi bài gọn](devyn-forwarder-compact-send.zip)
- [Gửi bài từ liên kết + TXT nhóm](devyn-forwarder-post-link-routes.zip)
- [Thời hạn hạn chế SS](devyn-forwarder-restriction-expiry.zip)
- [Check list proxy](devyn-forwarder-proxy-list-checker.zip)
- [API lưu một lần](devyn-forwarder-saved-api-settings.zip)
- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
