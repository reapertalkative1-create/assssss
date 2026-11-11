# Proxy riêng cho từng session

## Cập nhật

Giữ `.env.docker` và Docker volume, giải nén đè toàn bộ ZIP vào đúng thư mục cũ, mở Docker Desktop rồi chạy **setup.cmd một lần**. Bản này nâng database lên **0010**, thêm thư viện proxy cho worker và build lại API/web/worker. Những lần sau dùng **run.cmd**. Giữ giao diện gọn và tự chọn cổng web trống.

## Nhập và gán

Trong **Tài khoản Telegram → Nhập proxy**, chọn:

- **SS đã tích**: chỉ các SS được chọn, hỗ trợ chọn toàn bộ kết quả lọc rồi bỏ tích một số SS.
- **Tất cả SS theo bộ lọc**: mọi kết quả lọc, kể cả các trang khác. Muốn toàn bộ SS trong workspace, bỏ các bộ lọc trước.

Tải file `.txt` hoặc dán danh sách, mỗi dòng một proxy:

```text
127.0.0.1:1080
127.0.0.1:1081:username:password
socks5://username:password@proxy.example.com:1080
http://username:password@proxy.example.com:8080
socks4://proxy.example.com:1080
socks5://[::1]:1080
```

Dòng không có scheme dùng **Loại proxy mặc định** đang chọn. Hỗ trợ SOCKS5, SOCKS4 và HTTP CONNECT. Với ký tự đặc biệt trong username/password, dùng URL có percent encoding. File UTF-8 có/không BOM đều đọc được; bỏ qua dòng trống và dòng bắt đầu bằng `#`.

Bấm **Gán proxy**. Mỗi SS nhận một cấu hình proxy riêng theo thứ tự SS cũ đến mới. Proxy trùng cấu hình được gộp trước khi đếm. Nếu thiếu proxy hoặc proxy đang được SS ngoài lựa chọn sử dụng, toàn bộ lần gán được báo lỗi, không gán dở và không tự dùng chung. Proxy dư được báo số lượng, chưa lưu thành kho proxy; file gốc/danh sách của bạn vẫn là nguồn để nhập lần sau. Tối đa 2 MB/10.000 proxy mỗi lần.

SS đang chạy sẽ được worker tự ngắt kết nối cũ và kết nối lại với proxy mới trong các nhịp heartbeat tiếp theo; SS đang tắt vẫn tắt. Không đăng xuất session. Các SS đang nhập/đăng nhập cần hoàn tất trước khi gán. Nếu proxy lỗi, worker không tự bỏ qua proxy để nối trực tiếp.

## Kiểm tra

Cột **Proxy** ngay trên bảng SS hiển thị `protocol://host:port`, không hiển thị username/password:

- **Xanh**: lần check gần nhất kết nối thành công, có thời gian đáp ứng.
- **Đỏ**: lần check không kết nối được Telegram qua proxy.
- **Trắng**: chưa check/chưa đủ kết quả; lúc đang check ghi “Đang check”.

Bấm **Check proxy** tại dòng để kiểm tra riêng. Muốn kiểm tra nhiều SS, tích SS rồi bấm **Check proxy đã chọn**, hoặc **Check proxy tất cả theo bộ lọc**. Tiến độ/lỗi hiện ngay tại dòng, không có khung tác vụ bên dưới. Nếu worker offline, xem lỗi ở cột tiến độ; không tự kết luận proxy đã chết vì worker không chạy.

Check chạy từ worker được gán cho SS, mở đường hầm HTTP/SOCKS rồi xác minh TLS tới `api.telegram.org:443`. Không cần SS đăng nhập, không dùng tài khoản gửi tin. Kết quả này xác nhận đường tới HTTPS Telegram tại thời điểm check; không bảo đảm proxy luôn sống, địa chỉ IP duy nhất hay mọi datacenter MTProto đều truy cập được. Kết nối Telegram thực tế của SS dùng proxy qua Telethon.

Mật khẩu proxy được mã hóa bằng khóa hiện có, không ghi ra audit hoặc bảng danh sách. Worker chỉ đọc proxy của SS được gán cho nó. Đổi proxy sẽ vô hiệu kết quả check cũ, tránh ghi nhầm xanh/đỏ vào proxy mới.
