# Nút riêng Kiểm tra list proxy

## Cập nhật

Giữ `.env.docker` và Docker volume. Giải nén đè ZIP vào **đúng thư mục cũ**, mở Docker Desktop và chạy **setup.cmd một lần** để nâng database lên **0012** và build API/web/worker. Sau đó dùng **run.cmd**. Giữ cấu hình API đã lưu và dữ liệu SS cũ.

## Nhập → check → xuất

1. Vào **Tài khoản Telegram**, bấm nút tím viền **Kiểm tra list proxy** ở góc phải phía trên, cạnh **Nhập proxy**. Nút luôn hiện, kể cả khi chưa có SS.
2. Chọn worker Online (nếu chỉ có một worker, tự chọn). Dán vào **List proxy cần kiểm tra** hoặc tải **File list proxy .txt**.
3. Chọn loại mặc định SOCKS5 / SOCKS4 / HTTP CONNECT nếu dòng không có scheme. Dòng có scheme riêng dùng đúng scheme đó.
4. Bấm **Bắt đầu check proxy**. Xanh **Live** = kết nối thành công; đỏ **Die** = check thất bại. Có mã lỗi ngắn và thời gian ms. Chưa check/đang check/lỗi đọc cấu hình được tách riêng, không tự tính thành Die.
5. Lọc **Live / Die** để xem từng nhóm. Bấm **Xuất Live.txt (N)** hoặc **Xuất Die.txt (N)** để tải `proxy-list-live.txt` / `proxy-list-die.txt`.

Mỗi dòng một proxy, TXT UTF-8; tối đa 10.000 proxy khác nhau / 2 MB mỗi lô. Bỏ dòng trống, BOM, dòng bắt đầu bằng # và proxy trùng. Dòng sai định dạng báo lỗi trước khi tạo lô, không nhập dở.

```text
host.example:1080
host.example:1081:user:password
socks5://user:password@host.example:1082
http://user:password@host.example:8080
socks5://[::1]:1080
```

TXT xuất toàn bộ nhóm Live/Die của **lô list đang xem**, kể cả các trang khác; bộ lọc màn hình không làm đổi nhóm xuất. File giữ scheme, user/password và percent encoding để nhập lại được. Trên bảng chỉ hiện địa chỉ/cổng, không hiện user/password.

## Hoạt động độc lập

Không cần session, không cần api_id/api_hash và không tự gán proxy vào SS. Worker kiểm tra từ môi trường của máy bạn bằng cách mở tunnel qua proxy rồi xác thực TLS với api.telegram.org:443; không đăng nhập Telegram hoặc gửi tin nhắn. Live phản ánh lần check đó, không bảo đảm mọi ứng dụng/đích khác đều dùng được.

Đóng cửa sổ vẫn tiếp tục check. Mở lại nút này và chọn **Mở lại kết quả gần đây** để xem một trong 20 lô gần nhất của tài khoản quản trị đang đăng nhập. Có **Dừng check** để ngừng phần chưa hoàn tất, giữ các kết quả đã có để xuất; phản hồi muộn bị bỏ qua. **Nhập list mới** tạo lô khác, không xóa lô cũ.

Worker xử lý tối đa 10 proxy đồng thời, mỗi probe có timeout; worker gián đoạn thì phần đang check có thể được nhận lại sau khi hết lease. Lỗi worker/mất kết nối với máy chủ không bị kết luận thành proxy Die. Dữ liệu proxy được mã hóa trong database, chỉ người tạo lô (quản trị viên) đọc/xuất được; cấu hình chỉ chuyển cho worker đã chọn. Verify/rotate keys bao gồm list proxy.

**Nhập proxy** và **Xuất proxy** cũ vẫn dùng cho proxy đã gán vào SS. Luồng SS + proxy cùng lúc, API lưu tự động trong Cài đặt và nút đỏ Xóa đã chọn giữ nguyên.
