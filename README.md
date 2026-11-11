# DEVYN FORWARDER — proxy riêng từng SS

[**Tải ZIP mới: nhập, gán và check proxy**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-session-proxies.zip)

Giữ **.env.docker và Docker volume**, giải nén đè toàn bộ ZIP đúng thư mục cũ, mở Docker Desktop rồi chạy **setup.cmd một lần** để nâng database **0010** và build API/web/worker với thư viện proxy. Sau đó dùng **run.cmd**. Giữ tự chọn cổng trống và giao diện gọn.

## Cách dùng

1. **Tài khoản Telegram → Nhập proxy**: tải .txt hoặc dán, mỗi dòng một proxy. Hỗ trợ host:port, host:port:user:pass và URL SOCKS5/SOCKS4/HTTP CONNECT.
2. Chọn **SS đã tích** hoặc **Tất cả SS theo bộ lọc** rồi **Gán proxy**. Mỗi SS một cấu hình riêng; thiếu proxy báo lỗi, không gán dở hoặc dùng chung. Proxy dư được báo, chưa lưu thành kho.
3. Proxy hiện ngay trên dòng: **xanh = check thành công**, **đỏ = không kết nối**, **trắng = chưa đủ kết quả/chưa check**. Không hiện username/password.
4. **Check proxy** tại dòng, **Check proxy đã chọn** hoặc **Check proxy tất cả theo bộ lọc**. Kết quả/tiến độ ở dòng SS, không có khung tác vụ bên dưới.

SS đang chạy tự kết nối lại với proxy mới; SS đang tắt vẫn tắt. Worker không bỏ proxy để nối trực tiếp khi proxy lỗi. Check proxy mở đường hầm và xác minh TLS HTTPS Telegram từ worker, không cần đăng nhập SS hay gửi tin. Kết quả không bảo đảm mọi datacenter MTProto truy cập được hoặc proxy luôn sống.

[Hướng dẫn đầy đủ](HUONG_DAN_PROXY.md) · [Kiểm thử](KIEM_THU_PROXY.md) · [Windows](HUONG_DAN_WINDOWS.md)

345 kiểm thử Python local, 65 frontend và production build qua. Migration nâng/hạ SQLite khớp model; tunnel HTTP/SOCKS5 có auth + TLS thử nghiệm cục bộ, tự reconnect không trùng auth key, mã hóa/xoay khóa/quyền worker và browser file/paste/chọn phạm vi qua. Browser dùng dữ liệu/fixture màu giả; không dùng session người dùng/gửi Telegram thật, chưa thử proxy thương mại hoặc build sạch Docker Windows.

ZIP không chứa session, khóa, .env.docker hoặc database cá nhân. SHA256: `f8f41981b0d2d977b3f72f4f4bd4d395ffacc03d55f5791c79435c0099183291`.

## Bản trước

- [Bảng SS gọn](devyn-forwarder-compact-ui.zip)
- [Trạng thái màu](devyn-forwarder-status-colors.zip)
- [Tự chọn cổng web](devyn-forwarder-auto-port-fix.zip)
- [Thông tin trực tiếp trên bảng SS](devyn-forwarder-inline-session-details.zip)
- [Nút check spam / đóng băng](devyn-forwarder-spam-frozen-check.zip)
- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
