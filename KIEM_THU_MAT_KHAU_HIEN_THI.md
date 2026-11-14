# Kiểm thử bản mật khẩu hiển thị

Phiên bản `2026.11.14-visible-password`.

- **41 kiểm thử Python đạt:** tạo quản trị viên qua tiến trình helper thật, đăng nhập bằng mật khẩu chứa Unicode/ký tự đặc biệt/dấu cách; phân biệt chữ hoa/thường; từ chối xác nhận sai, tên sai, mật khẩu yếu và tên trùng; không ghi mật khẩu vào kết quả helper/audit. Kiểm thử CLI, đăng nhập và quản lý người dùng liên quan đều đạt.
- **39 kiểm thử frontend đạt:** ô tạo người dùng luôn hiện chữ, giữ nguyên mật khẩu gửi API và bỏ giá trị khi đóng sau tạo; các luồng đăng nhập/2FA và biểu mẫu liên quan vẫn đạt.
- **Production build đạt:** TypeScript + Vite; APP_VERSION trùng version.json trong dist.
- **PowerShell launcher đạt:** xác nhận phân biệt hoa/thường; sai xác nhận nhập lại tại chỗ; mật khẩu yếu/tên trùng được hỏi lại; Docker tắt TTY khi tạo admin; không có mật khẩu trong argv; tài khoản/cấu hình cũ được giữ; setup/run và khóa chống chạy trùng vẫn hoạt động.
- **PowerShell → tiến trình Python thật đạt:** stdin JSON UTF-8 không BOM, giữ nguyên Unicode, emoji, dấu cách và các ký tự `& | ^ % ! " ' \ $`; phản hồi JSON được đọc đúng.
- ZIP được kiểm tra CRC, loại trừ file cấu hình riêng/session/key/caches; giữ script PowerShell UTF-8 BOM và launcher CMD CRLF.

Môi trường kiểm thử là Linux với PowerShell 7 và Docker được mô phỏng trong kiểm thử launcher. Chưa chạy trên Windows PowerShell 5.1/Docker Desktop thật; mã launcher dùng cú pháp tương thích 5.1. 37 lượt PostgreSQL được bỏ qua vì chưa cấu hình database kiểm thử; không có thay đổi schema. Không kết nối Telegram thật.

Lệnh kiểm thử:

```sh
python -m pytest tests/unit/test_setup_admin.py tests/unit/test_cli.py tests/unit/test_security.py tests/unit/test_auth.py tests/unit/test_users_audit.py -q
cd apps/web
npm test -- src/pages/Users.test.tsx src/pages/pages.test.tsx
npm run build
```

```powershell
pwsh -NoProfile -File tests/windows_launcher.test.ps1
pwsh -NoProfile -File tests/windows_password_pipe.test.ps1 -PythonExe python
```
