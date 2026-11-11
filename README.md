# DEVYN FORWARDER — bảng SS gọn

[**Tải ZIP mới: hàng thấp, nhãn ngắn**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-compact-ui.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần**; sau đó dùng **run.cmd**. Giữ tự chọn cổng trống, head vẫn **0009**.

- Bỏ khung trạng thái lớn và đoạn giải thích Lý do.
- Chỉ nhãn ngắn: **Bình thường / Bị spam / Đóng băng / Bị chặn / Bị khóa / Hết phiên / Chưa rõ / Lỗi check**.
- Gộp xác thực/kết nối, thu kỹ thuật vào **Thông tin** ngay tại dòng.
- Tiến độ gọn, không thẻ lớn hoặc mô tả lặp; vẫn mở được các kháng nghị đang dở từ dòng.
- Giữ check/bật/tắt/xóa nhiều SS, không khung Tác vụ hàng loạt phía dưới.

[Hướng dẫn](HUONG_DAN_GIAO_DIEN_GON.md) · [Kiểm thử](KIEM_THU_GIAO_DIEN_GON.md) · [Windows](HUONG_DAN_WINDOWS.md)

62 kiểm thử giao diện và production build qua. Chromium: dòng mẫu khoảng 107px, nhãn xanh/đỏ, không có nguyên văn bot/Lý do, sáng/tối và mobile bằng dữ liệu giả. Không dùng session người dùng/gửi Telegram thật. ZIP không chứa session, khóa, .env.docker hoặc database cá nhân.

SHA256: `035ef82f4f48edb8dfc3f0afe6525118b95e715f9865ef18ad049990954aba55`.

## Bản trước

- [Trạng thái màu](devyn-forwarder-status-colors.zip)
- [Tự chọn cổng web](devyn-forwarder-auto-port-fix.zip)
- [Thông tin trực tiếp trên bảng SS](devyn-forwarder-inline-session-details.zip)
- [Nút check spam / đóng băng](devyn-forwarder-spam-frozen-check.zip)
- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
