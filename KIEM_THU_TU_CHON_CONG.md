# Kiểm thử launcher tự chọn cổng — 12/11/2026

- Chạy thành công `tests/windows_ports.test.ps1` bằng PowerShell 7.4.6 trên Linux: đọc binding Docker/nhãn Compose, cổng loopback bị giữ bằng socket thật, lưu cổng mới và giữ nguyên project/khóa/credential.
- Cổng thuộc web cùng project được giữ lại; cổng của project khác và cổng bị từ chối được bỏ qua. Kiểm tra wrap ở 65535 và lỗi rõ ràng khi hết 100 ứng viên.
- Giả lập Docker báo port allocated lúc startup: chọn cổng mới và khởi động tiếp. Không thử lại lỗi API unhealthy; dừng sau tối đa 3 lần khi liên tục xung đột cổng.
- Chạy thành công bộ hồi quy `tests/windows_launcher.test.ps1`: parse cú pháp, khóa, chạy lại, Docker checks, tự nối worker, giữ admin/database, setup, run và launcher lock.
- Docker Compose config thật với cấu hình giả: published port 8788, host 127.0.0.1 và API allowed origins cùng cổng 8788.
- Script vẫn có UTF-8 BOM và dùng cú pháp tương thích mục tiêu Windows PowerShell 5.1. Chưa chạy trực tiếp trên Windows PowerShell 5.1/Docker Desktop của người dùng; Docker startup trong các ca race được giả lập. Không build lại các Docker image hoặc chạy lại Python/frontend vì thay đổi chỉ ở launcher và tài liệu.

Không dừng container khác, xóa volume hoặc thay khóa/session để giải phóng cổng. ZIP loại trừ `.env.docker`, khóa, session, database, launcher lock, runtime và công cụ PowerShell tải phục vụ kiểm thử.
