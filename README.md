# DEVYN FORWARDER — nhập SS kèm proxy

[**Tải bản mới: SS + proxy trong cùng lần nhập**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-session-proxy-import.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ và chạy **setup.cmd một lần** để cập nhật API/web/worker. Những lần sau dùng **run.cmd**. Database head vẫn **0010**.

Trong **Tài khoản Telegram → Nhập session hàng loạt**, chọn SS/ZIP, nhập API Telegram và tải TXT hoặc dán danh sách proxy. **Nhập SS kèm proxy** bật sẵn. Mỗi SS một proxy theo thứ tự; proxy được mã hóa/lưu trước khi worker kết nối hoặc check session/SpamBot lần đầu. Thiếu proxy sẽ báo trước khi tải; proxy lỗi không tự chuyển sang kết nối trực tiếp. SS trùng giữ proxy cũ. Có thể chủ động tắt tùy chọn để nhập không proxy.

Web tự chia lô, giữ đúng proxy qua lô 100 + 1. Có cột Proxy trong tiến độ, không hiện password. Giữ nút đỏ **Xóa đã chọn**, check/lọc/xuất proxy sống/die và launcher tự chọn cổng trống. Proxy không bảo đảm Telegram sẽ không hạn chế/khóa tài khoản.

[Hướng dẫn](HUONG_DAN_NHAP_SS_KEM_PROXY.md) · [Kiểm thử](KIEM_THU_NHAP_SS_KEM_PROXY.md) · [Windows](HUONG_DAN_WINDOWS.md)

38 kiểm thử Python liên quan, 76 frontend và production build qua. Chromium thật nhập ZIP + TXT với API/worker thật, Telegram giả: 3 kết nối đầu khớp proxy từng SS, không lộ mật khẩu, form vừa mobile/desktop. Không dùng session người dùng hoặc gửi Telegram thật; không chạy PostgreSQL integration hoặc build sạch Docker/Windows ở đợt này.

ZIP gồm source và dist, không chứa session, khóa, .env riêng hoặc database. SHA256: `14e0f030a7abf7b8e56953fd50985f6e5386c1cac6d90dfc293941576f35fbec`.

## Bản trước

- [Xóa trực tiếp + lọc/xuất proxy](devyn-forwarder-proxy-export-delete.zip)
- [Thanh điều khiển gọn](devyn-forwarder-streamlined-controls.zip)
- [Proxy riêng từng SS](devyn-forwarder-session-proxies.zip)
