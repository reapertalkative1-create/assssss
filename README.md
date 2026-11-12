# DEVYN FORWARDER — xóa trực tiếp và xuất proxy

[**Tải ZIP mới: nút Xóa + lọc/xuất proxy**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-proxy-export-delete.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để cập nhật API/web; sau đó dùng **run.cmd**. Head vẫn **0010**; giữ worker/proxy, giao diện gọn và tự chọn cổng trống.

## Nút xóa

Nút đỏ **Xóa đã chọn** được đưa riêng ra ngoài menu và luôn thấy khi có SS. Tích SS để bật nút rồi bấm xóa ngay, không cần tìm trong menu, gõ tên hoặc xác nhận thêm. Chọn cả N rồi bỏ tích vẫn giữ đúng phạm vi loại trừ. Menu không còn lựa chọn Xóa lặp.

## Proxy

- Giữ **Check proxy** từng dòng và check hàng loạt theo loại thao tác đang chọn.
- Có bộ lọc **Proxy đang chạy / Proxy die / Proxy chưa check / Proxy đang check**.
- **Xuất proxy → Đang chạy → .txt** tải `proxies-live.txt`.
- **Xuất proxy → Die → .txt** tải `proxies-die.txt`.

File lấy proxy đã gán cho SS, theo kết quả check đã lưu, không bị phân trang. Nhóm sống/die theo nút xuất, giữ các bộ lọc SS khác; không phụ thuộc SS đã tích. Chưa check/đang check không bị coi là sống/die. Nhóm rỗng được báo, không tải file rỗng.

URL trong TXT giữ username/password nếu có và nhập lại được; chỉ quản trị viên được tải. Credential không hiện trên bảng/audit. Giải mã lỗi sẽ báo trước khi trả file, không xuất dở.

[Hướng dẫn](HUONG_DAN_XUAT_PROXY.md) · [Kiểm thử](KIEM_THU_XUAT_PROXY.md) · [Windows](HUONG_DAN_WINDOWS.md)

31 kiểm thử Python liên quan, 71 frontend và production build qua. Chromium tải thật hai file từ fixture proxy có trạng thái giả, kiểm tra bộ lọc/phạm vi, xóa một SS giả bằng một lần bấm và menu vừa tablet/mobile; không lỗi JS/HTTP 500. Không sử dụng session người dùng/gửi Telegram thật. Không thêm dependency/migration.

ZIP không chứa session, khóa, .env.docker, file xuất hoặc database cá nhân. SHA256: `c5afbd3f1b713b88494dac2241d42fcf1ccec979ea4e3e4dbee6299f22d59c16`.

## Bản trước

- [Thanh điều khiển gọn](devyn-forwarder-streamlined-controls.zip)
- [6 ô thống kê gọn](devyn-forwarder-compact-counters.zip)
- [Proxy riêng từng SS](devyn-forwarder-session-proxies.zip)
- [Bảng SS gọn](devyn-forwarder-compact-ui.zip)
- [Trạng thái màu](devyn-forwarder-status-colors.zip)
- [Tự chọn cổng web](devyn-forwarder-auto-port-fix.zip)
- [Thông tin trực tiếp trên bảng SS](devyn-forwarder-inline-session-details.zip)
- [Nút check spam / đóng băng](devyn-forwarder-spam-frozen-check.zip)
- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
