# Bảng SS gọn

Giữ `.env.docker` và Docker volume, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần**; sau đó dùng **run.cmd**. Giữ tự chọn cổng trống, không thêm migration (head 0009).

- Bỏ khung trạng thái lớn và toàn bộ đoạn giải thích “Lý do”.
- Chỉ hiện nhãn ngắn: **Bình thường**, **Bị spam**, **Đóng băng**, **Bị chặn**, **Bị khóa**, **Hết phiên**, **Chưa rõ**, **Lỗi check**, **Chưa check**.
- Màu xanh/đỏ/vàng/xám giữ đúng kết quả cũ, không đổi cách kiểm tra.
- Gộp xác thực/kết nối trên một hàng. Worker, ID và cấu hình kỹ thuật nằm trong **Thông tin** mở ngay tại dòng khi cần.
- Giảm padding và khoảng cách, thu hẹp cột trạng thái. Tiến độ bỏ khung và mô tả lặp; mặc định hiện thao tác ưu tiên cùng các đợt kháng nghị đang dở để vẫn mở/duyệt được từ dòng.
- Không có chat SpamBot hay khung Tác vụ hàng loạt trên bảng.

Cửa sổ SpamBot/kháng nghị và các nút check/bật/tắt/xóa nhiều SS giữ nguyên. Dừng cả đợt vẫn áp dụng mọi SS cùng đợt.
