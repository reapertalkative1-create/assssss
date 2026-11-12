# DEVYN FORWARDER — ô thống kê gọn

[**Tải ZIP mới: 6 ô thống kê gọn**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-compact-counters.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để build API/web/worker; sau đó dùng **run.cmd**. Head vẫn **0010**, giữ proxy và tự chọn cổng trống.

## Thay đổi

**Tất cả · Chưa check · Live · Die / hết phiên · Đóng băng · Bị chặn**

- Bỏ ô **FloodWait** và **Lỗi kiểm tra**.
- Mỗi ô chỉ có tên và số lượng, bỏ chú thích; cao khoảng **48px** trên desktop, mobile chia 2 cột.
- **Đóng băng** và **Bị chặn** có đếm/lọc riêng. **Tất cả** bỏ lọc hai loại trạng thái; các bộ lọc tên/worker khác vẫn giữ.
- Tách trạng thái blocked khỏi generic spam; khi API khởi động tự cập nhật các thông báo bị chặn đã lưu mã hóa ở bản cũ. Không cần liên hệ Telegram. Số đếm/lọc sau đó dùng trạng thái lưu trong DB.

Số đếm là toàn workspace, không chỉ trang hiện tại. Live và Bị chặn có thể đồng thời trên một SS vì Live chỉ phản ánh khả năng đăng nhập.

[Hướng dẫn](HUONG_DAN_O_THONG_KE_GON.md) · [Kiểm thử](KIEM_THU_O_THONG_KE_GON.md) · [Windows](HUONG_DAN_WINDOWS.md)

49 kiểm thử Python liên quan, 66 frontend và production build qua. Chromium thật: khôi phục dữ liệu blocked cũ, đếm/lọc/reset đúng, kích thước 48px, sáng/tối/mobile bằng dữ liệu giả; không lỗi JS/HTTP 500. Không dùng session người dùng/gửi Telegram thật, không thêm migration/dependency. ZIP không chứa session, khóa, .env.docker hoặc database cá nhân.

SHA256: `759a78133c2d5db18c4662a06733d6e6a5a93d3ef40a0f54b3e3fa2698fe45f7`.

## Bản trước

- [Proxy riêng từng SS](devyn-forwarder-session-proxies.zip)
- [Bảng SS gọn](devyn-forwarder-compact-ui.zip)
- [Trạng thái màu](devyn-forwarder-status-colors.zip)
- [Tự chọn cổng web](devyn-forwarder-auto-port-fix.zip)
- [Thông tin trực tiếp trên bảng SS](devyn-forwarder-inline-session-details.zip)
- [Nút check spam / đóng băng](devyn-forwarder-spam-frozen-check.zip)
- [DEVYN FORWARDER — giao diện chuyên nghiệp](devyn-forwarder-professional-ui.zip)
- [Kháng nghị hàng loạt theo mẫu](telegram-forwarder-control-center-bulk-appeal-template.zip)
- [Xóa hàng loạt](telegram-forwarder-control-center-bulk-delete.zip)
