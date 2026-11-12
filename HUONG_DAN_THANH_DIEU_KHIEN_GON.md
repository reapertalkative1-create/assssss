# Trang tài khoản tinh gọn

Giữ `.env.docker` và Docker volume, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để build giao diện. Sau đó dùng **run.cmd**. Head vẫn **0010**; backend, proxy, worker và launcher không thay đổi.

## Bố cục

Đã bỏ khung Kiểm tra spam & đóng băng, dãy nút lọc nhanh lặp với thống kê/bộ lọc, dòng check proxy riêng và các đoạn giải thích dài. Trang còn:

1. Tiêu đề + Nhập session / Nhập proxy / Thêm tài khoản.
2. Sáu ô thống kê nhỏ.
3. Một thanh lọc và thao tác.
4. Bảng SS, tiến độ/lỗi ngay trên từng dòng như trước.

Bộ lọc chính có tìm tên, spam, worker và số dòng. **Lọc thêm** mở các bộ lọc xác thực, tình trạng session và bật/tắt; số trên nút báo bộ lọc phụ đang dùng. **Bỏ lọc** đặt lại các điều kiện. Các ô thống kê vẫn bấm để lọc nhanh.

## Check và thao tác

**Chưa tích SS:** chọn Check session / Check spam & đóng băng / Check proxy trong **Thao tác session**, bấm **Check (N)** để áp dụng cho mọi kết quả lọc, kể cả trang khác.

**Đã tích SS:** menu có thêm bật, tắt, xóa, kháng nghị và nhãn đóng băng thủ công. Chọn thao tác rồi bấm **Áp dụng (N)**. Chỉ áp dụng cho SS đã tích. **Chọn cả N** xuất hiện khi kết quả trải qua nhiều trang; có thể bỏ tích từng dòng để loại trừ.

Riêng **Xóa** hiện nút đỏ **Xóa đã chọn**, xếp hàng ngay, không thêm hộp xác nhận hoặc bắt gõ tên. Khi bỏ chọn hết, thao tác xóa/quản lý không được giữ sang lần chọn mới.

Nhập proxy trên tiêu đề vẫn tự dùng phạm vi SS đã tích nếu đang chọn. Kháng nghị đã lưu vẫn mở lại tại dòng SS. Các nút check riêng từng dòng giữ nguyên.

Khi danh sách rỗng, không hiện checkbox/chọn cả/nút thao tác hàng loạt vô dụng hoặc nút thêm tài khoản trùng. Các chức năng ít dùng được gom vào menu, không bị xóa khỏi ứng dụng.
