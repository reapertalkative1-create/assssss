# Chạy bản khôi phục

Yêu cầu Python >=3.11 và Node.js >=18. Chạy các lệnh từ thư mục chứa README.md.

1. `python -m venv .venv`
2. Kích hoạt môi trường: Linux/macOS `source .venv/bin/activate`; Windows PowerShell `.venv\Scripts\Activate.ps1`; Windows CMD `.venv\Scripts\activate.bat`.
3. `python -m pip install -e "apps/api[dev]" -e "workers/telegram-worker[dev]"`
4. Với cài đặt mới: `python scripts/init_local.py`
5. `python -m alembic upgrade head`
6. `python -m app.cli create-admin admin` — nhập mật khẩu riêng, ít nhất 12 ký tự, không chứa tên đăng nhập.
7. Terminal thứ nhất: `python -m uvicorn app.main:app --app-dir apps/api --host 127.0.0.1 --port 8000`
8. Terminal thứ hai: `cd apps/web`, chạy `npm ci`, rồi `npm run dev -- --host 127.0.0.1`.
9. Mở http://127.0.0.1:5173 và đăng nhập.

Script local dùng SQLite và tự tạo khóa riêng, không ghi đè .env có sẵn. Nếu cập nhật cài đặt cũ, giữ nguyên .env, khóa mã hóa và database; không tạo khóa mới cho dữ liệu cũ.

Trong UI tạo worker và lưu credential; lấy api_id/api_hash tại https://my.telegram.org. Thêm vào .env trên máy worker:

```dotenv
TFCC_WORKER_CONTROL_PLANE_URL=http://localhost:8000
TFCC_WORKER_CREDENTIAL=credential-cua-ban
TFCC_WORKER_TELEGRAM_API_ID=123456
TFCC_WORKER_TELEGRAM_API_HASH=api-hash-cua-ban
```

Điền giá trị thật. Không để dòng API_ID rỗng; bỏ dòng khi chưa cấu hình. Chạy worker từ thư mục gốc đã kích hoạt .venv:

```sh
python -m worker.main check-config
python -m worker.main run
```

Trong UI: tạo tài khoản Telegram → gán worker → đăng nhập OTP/2FA → bật tài khoản → tạo tuyến → verify → start. Máy worker ở xa cần HTTPS; không chuyển khóa mã hóa của API sang worker.

SQLite/Vite chỉ dùng cho local. Triển khai thực tế cần PostgreSQL, HTTPS, TFCC_ENV=production và cookie_secure=true. Chưa kiểm thử Telegram thật. At-least-once có thể gửi trùng nếu worker chết đúng lúc Telegram đã nhận tin nhưng API chưa nhận kết quả.

Kiểm thử: `python -m pytest -m "not integration and not telegram_live"`; trong apps/web chạy `npm test` và `npm run build`. Không đặt TFCC_TEST_DATABASE_URL trỏ vào database thật vì kiểm thử sẽ xóa/tạo lại bảng.

Bản này được khôi phục từ ZIP gốc và các thay đổi đã ghi trong cuộc trò chuyện; không phải bản sao bit-for-bit của ZIP trước đã mất. Không thay đổi schema/migration.
