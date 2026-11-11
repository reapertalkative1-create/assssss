# Chạy riêng trên Windows: setup.cmd và run.cmd

## Cách dùng

1. Cài **Docker Desktop cho Windows** từ https://www.docker.com/products/docker-desktop/ nếu máy chưa có. Dùng chế độ **Linux containers** và mở Docker Desktop, đợi engine chạy. Không cần cài Python, Node.js hay PostgreSQL trên Windows.
2. Giải nén toàn bộ ZIP vào một thư mục riêng, ví dụ `Documents\TelegramForwarder` trong thư mục người dùng. Không chạy CMD ngay bên trong ZIP.
3. Bấm đúp **setup.cmd** một lần. Script tải image, tạo database, hỏi tên/mật khẩu quản trị và tự tạo/lưu worker cho máy này. Mật khẩu tối thiểu 12 ký tự, không chứa tên đăng nhập. Không có mật khẩu mặc định.
4. Khi hoàn tất, trình duyệt mở **http://127.0.0.1:8787**. Lần sau chỉ cần mở Docker Desktop rồi bấm đúp **run.cmd**: worker tự kết nối, script đợi máy Online rồi mở web. Không phải chép credential hoặc URL kết nối.

Lần setup đầu cần internet và có thể mất vài phút. Script không cài Python/Node/PostgreSQL toàn hệ thống và không sửa biến PATH. Hai CMD gọi PowerShell có sẵn trên Windows; ExecutionPolicy Bypass chỉ áp dụng cho tiến trình chạy script đó.

## Phạm vi cách ly

- Python/API, Node build giao diện, Nginx và PostgreSQL đều ở các container/image riêng của ứng dụng.
- Mỗi cài đặt mới có tên project Docker ngẫu nhiên, mạng riêng, database volume riêng và khóa riêng trong **.env.docker**. Không dùng `.env` của bản chạy Python cũ.
- Docker vẫn sử dụng CPU/RAM/ổ đĩa của máy Windows. Đây là cách ly bằng container, không phải một máy vật lý khác.
- Chỉ cổng giao diện `127.0.0.1:8787` được mở trên máy; database/API không mở cổng trực tiếp ra Windows/LAN.
- Dữ liệu PostgreSQL nằm trong volume của Docker Desktop, không nằm trong ZIP. Dừng container hoặc chạy lại setup không xóa dữ liệu. Không xóa volume hay `.env.docker` nếu cần giữ dữ liệu.

## Máy tự kết nối với web

Worker được tạo tự động dưới dạng Linux container, có tên máy của bạn trong danh sách **Worker & máy chủ**. Lúc chạy, bạn sẽ thấy `Computer connected: ...`. Credential, worker ID và hostname được lưu tự động trong `.env.docker`, không in ra màn hình. Những lần run sau dùng lại worker đó.

Nếu bạn đang dùng bản cũ: giải nén đè các tệp mã nguồn vào đúng thư mục cũ, **giữ nguyên `.env.docker` và Docker volume**, rồi chạy **setup.cmd lại một lần** để build image mới. Tài khoản quản trị có sẵn được giữ lại. Credential Linux hợp lệ đã cấu hình trước đó được dùng lại.

Worker có thể Online trước khi cấu hình Telegram. Online chỉ chứng minh máy kết nối được với web, chưa có nghĩa là đã đăng nhập tài khoản Telegram.

## Bật chuyển tiếp Telegram

1. Lấy `api_id`/`api_hash` tại https://my.telegram.org.
2. Mở **.env.docker**, chỉ điền hai trường sau bằng thông tin thật:

```dotenv
TFCC_WORKER_TELEGRAM_API_ID=123456
TFCC_WORKER_TELEGRAM_API_HASH=api-hash-cua-ban
```

3. Lưu rồi bấm **run.cmd**. Không sửa `TFCC_WORKER_CREDENTIAL`, `TFCC_WORKER_ID` hoặc URL; các giá trị kết nối do ứng dụng quản lý.
4. Trong giao diện: tạo tài khoản Telegram → gán vào worker của máy này → đăng nhập OTP/2FA → bật tài khoản → tạo tuyến → verify → start.

Nếu đã cấu hình API ID/hash ở bản cũ thì hai giá trị đó được giữ nguyên. Không đưa `.env.docker` lên GitHub và không đổi khóa mã hóa/database password khi đang dùng dữ liệu cũ.

## Dừng hoặc thay cổng

Đóng cửa sổ CMD không dừng ứng dụng, vì container chạy nền. Trong Docker Desktop → Containers, chọn project bắt đầu bằng `tfcc-` tương ứng và bấm Stop. Hoặc mở CMD tại thư mục ứng dụng, chạy:

```cmd
docker compose --env-file .env.docker --profile telegram stop
```

Để chạy lại, bấm **run.cmd**. Nếu cổng 8787 bị ứng dụng khác dùng, sửa `TFCC_HTTP_PORT=8788` trong `.env.docker` rồi chạy lại **run.cmd**; trình duyệt sẽ mở cổng mới.

## Khi có lỗi

- Không thấy lệnh Docker: cài Docker Desktop rồi mở lại CMD.
- Engine chưa sẵn sàng: mở Docker Desktop, đợi Engine running; đảm bảo đang dùng Linux containers.
- Setup bị ngắt: chạy lại **setup.cmd**; cấu hình, khóa và tài khoản hiện có được giữ nguyên.
- Chưa chạy setup thành công: **run.cmd** sẽ nhắc chạy setup trước.
- Nếu worker bị bạn thu hồi hoặc credential đã bị xoay thủ công, script sẽ báo lỗi và không tự kích hoạt lại worker bị thu hồi. Giữ thông báo lỗi để kiểm tra cấu hình hiện có.
- Không bấm đồng thời hai setup/run: ứng dụng dùng khóa để tránh tạo hai worker hoặc ghi đè cấu hình.

Đây là cấu hình local trên máy cá nhân, không phải bộ triển khai công khai qua internet. Telegram thật vẫn cần credential/tài khoản của bạn.
