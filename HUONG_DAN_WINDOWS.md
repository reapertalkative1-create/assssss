# Chạy riêng trên Windows: setup.cmd và run.cmd

## Cách dùng

1. Cài **Docker Desktop cho Windows** từ https://www.docker.com/products/docker-desktop/ nếu máy chưa có. Dùng chế độ **Linux containers** và mở Docker Desktop, đợi engine chạy. Không cần cài Python, Node.js hay PostgreSQL trên Windows.
2. Giải nén toàn bộ ZIP vào một thư mục riêng, ví dụ `Documents\TelegramForwarder` trong thư mục người dùng. Không chạy CMD ngay bên trong ZIP.
3. Bấm đúp **setup.cmd** một lần. Script tải image, cài thư viện trong container, tạo database và hỏi tên/mật khẩu quản trị. Mật khẩu tối thiểu 12 ký tự, không chứa tên đăng nhập. Không có mật khẩu mặc định.
4. Khi hoàn tất, trình duyệt mở **http://127.0.0.1:8787**. Lần sau chỉ cần mở Docker Desktop rồi bấm đúp **run.cmd**.

Lần setup đầu cần internet và có thể mất vài phút. Script không cài Python/Node/PostgreSQL toàn hệ thống và không sửa biến PATH. Hai CMD gọi PowerShell có sẵn trên Windows; ExecutionPolicy Bypass chỉ áp dụng cho tiến trình chạy script đó.

## Phạm vi cách ly

- Python/API, Node build giao diện, Nginx và PostgreSQL đều ở các container/image riêng của ứng dụng.
- Mỗi cài đặt mới có tên project Docker ngẫu nhiên, mạng riêng, database volume riêng và khóa riêng trong **.env.docker**. Không dùng `.env` của bản chạy Python cũ.
- Docker vẫn sử dụng CPU/RAM/ổ đĩa của máy Windows. Đây là cách ly bằng container, không phải một máy vật lý khác.
- Chỉ cổng giao diện `127.0.0.1:8787` được mở trên máy; database/API không mở cổng trực tiếp ra Windows/LAN.
- Dữ liệu PostgreSQL nằm trong volume của Docker Desktop, không nằm trong ZIP. Dừng container hoặc chạy lại setup không xóa dữ liệu. Không xóa volume hay `.env.docker` nếu cần giữ dữ liệu.

## Bật chuyển tiếp Telegram

1. Trong giao diện tạo worker với nền tảng **Linux**, dù máy bạn là Windows: worker chạy trong Linux container.
2. Lưu credential được cấp. Lấy `api_id`/`api_hash` tại https://my.telegram.org.
3. Mở **.env.docker** bằng Notepad và điền đủ ba trường (không thêm dấu ngoặc):

```dotenv
TFCC_WORKER_CREDENTIAL=credential-cua-worker-Linux
TFCC_WORKER_TELEGRAM_API_ID=123456
TFCC_WORKER_TELEGRAM_API_HASH=api-hash-cua-ban
```

4. Lưu file rồi bấm **run.cmd**. Worker sẽ tự chạy trong container khi đủ ba trường. Không cần mở thêm terminal Python.
5. Trong giao diện: tạo tài khoản Telegram → gán worker → đăng nhập số điện thoại/OTP/2FA → bật tài khoản → tạo tuyến → verify → start. Bắt đầu bằng chat thử do bạn quản lý.

Không đưa `.env.docker` lên GitHub và không sửa các khóa/DB password khi đang dùng dữ liệu cũ.

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
- Credential sai nền tảng: tạo worker **Linux** mới, cập nhật `.env.docker`, chạy lại **run.cmd**.

Đây là cấu hình local trên máy cá nhân, không phải bộ triển khai công khai qua internet. Telegram thật vẫn cần credential/tài khoản của bạn.
