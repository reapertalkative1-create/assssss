# Nhập SS và proxy cùng lúc

Giữ `.env.docker` và Docker volume. Giải nén đè vào đúng thư mục đang dùng, mở Docker Desktop và chạy **setup.cmd một lần** để build API/web/worker mới. Những lần sau dùng **run.cmd**. Không thêm migration; head vẫn **0010**.

## Cách nhập

1. Vào **Tài khoản Telegram → Nhập session hàng loạt**.
2. Chọn worker online, chọn nhiều file Telethon `.session` hoặc ZIP, nhập `api_id/api_hash`.
3. **Nhập SS kèm proxy** đã bật sẵn. Tải file proxy `.txt` UTF-8 (tối đa 2 MB) hoặc dán vào **Proxy cho session mới**. Mỗi dòng một proxy.
4. Chọn SOCKS5 / SOCKS4 / HTTP CONNECT cho dòng chưa có scheme. Dòng có `socks5://`, `socks4://`, `http://` dùng đúng scheme đó.
5. Bấm **Nhập và kiểm tra session**. Cột Proxy trong tiến độ cho biết proxy được gán, chỉ hiện địa chỉ/cổng.

```text
host1.example:1080:user:password
socks5://user:password@host2.example:1080
http://user:password@host3.example:8080
```

Dòng proxy thứ 1 ghép với file session thứ 1, dòng 2 ghép file thứ 2… theo thứ tự file được chọn và thứ tự file lưu trong ZIP. Bỏ dòng trống, BOM và dòng bắt đầu bằng `#`; proxy dư không được gán. File không đọc/giải nén được ở trình duyệt bị bỏ qua và không lấy proxy. File đã gửi nhưng không phải session hợp lệ, hoặc session trùng, vẫn giữ vị trí tương ứng; proxy ở vị trí đó không được gán sang SS kế tiếp. SS trùng giữ cấu hình/proxy cũ, không tự thay đổi.

Web đếm file trước khi tải: thiếu proxy sẽ báo số lượng và chưa tải SS nào. Web không giới hạn tổng 100 SS; tự chia lô tối đa 100 file/8 MiB dữ liệu session, cắt danh sách proxy theo đúng lô. File session tối đa 1 MiB như trước.

## Kết nối

Session, API Telegram, proxy mã hóa và lệnh kiểm tra được lưu cùng giao dịch. Worker lấy proxy trước khi mở kết nối Telegram đầu tiên; xác thực session và check SpamBot (nếu bật) dùng kết nối đó. Proxy lỗi hoặc không đọc được cấu hình sẽ làm kiểm tra thất bại, **không tự chuyển sang kết nối trực tiếp**. **Kiểm tra lại** dùng proxy đã lưu.

API từ chối lô nếu thiếu/sai/trùng proxy hoặc proxy đã thuộc SS khác. Không tạo SS nào của lô bị từ chối; các lô gửi thành công trước đó vẫn được xử lý. Nếu đã tải một phần, sửa danh sách rồi nhập lại cùng file/thứ tự; SS trùng được bỏ qua. Username/password proxy không hiện trên bảng hoặc audit. Có thể tắt **Nhập SS kèm proxy** nếu chủ động muốn nhập không có proxy.

Sau nhập, proxy hiện ngay ở bảng SS; trạng thái trắng là chưa check proxy riêng. Dùng **Check proxy**, lọc đang chạy/die và **Xuất proxy** như trước. Kiểm tra session thành công không tự coi proxy đã qua bài check TLS độc lập.

Giữ nút đỏ **Xóa đã chọn**, giao diện gọn và tự chọn cổng web. Proxy giúp chọn đường kết nối; không bảo đảm Telegram sẽ không hạn chế/khóa tài khoản.
