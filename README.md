# DEVYN FORWARDER — trang tài khoản tinh gọn

[**Tải ZIP mới: thanh điều khiển gọn**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-streamlined-controls.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để build giao diện; sau đó dùng **run.cmd**. Head vẫn **0010**, giữ proxy, đếm/lọc blocked và tự chọn cổng trống.

## Giao diện mới

- Bỏ khung check lớn, dãy lọc nhanh trùng với thống kê/bộ lọc, dòng check proxy riêng và các đoạn giải thích dài.
- Tiêu đề + 3 nút nhập/thêm, 6 ô thống kê nhỏ, một thanh lọc/thao tác rồi đến bảng SS.
- Bộ lọc chính: tên, spam, worker, số dòng. Xác thực/tình trạng/bật tắt nằm trong **Lọc thêm**; có **Bỏ lọc**.
- Chưa tích SS: menu **Thao tác session** chỉ có các loại check, **Check (N)** áp dụng toàn bộ kết quả lọc.
- Đã tích SS: thêm bật/tắt/xóa/kháng nghị/nhãn thủ công, chọn thao tác rồi **Áp dụng (N)**. **Chọn cả N** hỗ trợ nhiều trang và bỏ tích để loại trừ.
- Xóa vẫn có nút đỏ **Xóa đã chọn**, xếp hàng ngay, không modal/gõ xác nhận. Bỏ chọn hết reset thao tác phá hủy.
- Danh sách rỗng không hiện điều khiển hàng loạt vô dụng hay nút thêm tài khoản trùng.

[Hướng dẫn](HUONG_DAN_THANH_DIEU_KHIEN_GON.md) · [Kiểm thử](KIEM_THU_THANH_DIEU_KHIEN_GON.md) · [Windows](HUONG_DAN_WINDOWS.md)

69 kiểm thử giao diện và production build qua. Chromium thật: bộ lọc, check theo phạm vi, chọn 80/bỏ tích 1, mở kháng nghị/nhập proxy, danh sách rỗng, sáng/tối và mobile bằng dữ liệu giả. Desktop 1600×1000: bảng bắt đầu khoảng y=333px; không lỗi JS/HTTP 500. Backend/worker/launcher không đổi, không dùng session người dùng/gửi Telegram thật.

ZIP không chứa session, khóa, .env.docker hoặc database cá nhân. SHA256: `17bd9d8d99977d929ab5e705e31825790b22d0a23b88e4562006430b5928217c`.

## Bản trước

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
