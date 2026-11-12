# DEVYN FORWARDER — nút riêng Kiểm tra list proxy

[**Tải ZIP mới: check list proxy độc lập**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-proxy-list-checker.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để nâng database **0012** và build API/web/worker. Sau đó dùng **run.cmd**.

Trong **Tài khoản Telegram**, bấm nút viền tím **Kiểm tra list proxy** ở đầu trang, cạnh **Nhập proxy**. Chọn worker Online → tải TXT hoặc dán list → **Bắt đầu check proxy** → lọc Live/Die → **Xuất Live.txt / Xuất Die.txt**.

Dùng độc lập khi chưa có SS hoặc API Telegram, không gán proxy vào tài khoản. Bảng có nhãn xanh Live, đỏ Die, lỗi ngắn và ms; tách chưa check/đang check/lỗi đọc. Bỏ proxy trùng, tối đa 10.000 proxy/2 MB mỗi lô. Export lấy toàn bộ nhóm trong lô, không bị phân trang; TXT giữ username/password để nhập lại, bảng không hiện credential.

Đóng cửa sổ vẫn tiếp tục; mở lại **Mở lại kết quả gần đây** hoặc **Dừng check** để giữ phần đã có. Lô lưu trong database, ràng buộc người tạo/worker và mã hóa. Giữ cấu hình API tự lưu trong Cài đặt, nhập SS+proxy cùng lúc, nút đỏ Xóa đã chọn, check/xuất proxy đã gán cho SS và tự chọn cổng web.

[Hướng dẫn](HUONG_DAN_CHECK_LIST_PROXY.md) · [Kiểm thử](KIEM_THU_CHECK_LIST_PROXY.md) · [Windows](HUONG_DAN_WINDOWS.md)

42 kiểm thử Python liên quan, 85 frontend và production build qua. Chromium thật dùng API/worker/transport proxy thật với HTTP CONNECT, SOCKS5 và TLS cục bộ: 2 Live + 2 Die, tải thật hai file TXT đúng, lọc/mở lại lô, vừa desktop/mobile. Không có account/API Telegram, không dùng session/proxy người dùng hoặc kết nối Telegram thật. Chưa chạy PostgreSQL integration hoặc build sạch Docker/Windows ở đợt này.

ZIP gồm source/dist; không có session, khóa, .env riêng hoặc database. SHA256: `92365348b7f4b27c64dcee844495a6aaaa0ab1a67931e41761be01ef27216756`.

## Bản trước

- [API Telegram lưu một lần trong Cài đặt](devyn-forwarder-saved-api-settings.zip)
- [Nhập SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
- [Xóa trực tiếp + lọc/xuất proxy của SS](devyn-forwarder-proxy-export-delete.zip)
