# Ô thống kê session gọn

Bản này thu dãy thống kê còn **6 ô**:

**Tất cả · Chưa check · Live · Die / hết phiên · Đóng băng · Bị chặn**

Bỏ hai ô FloodWait và Lỗi kiểm tra. Mỗi ô chỉ có tên và số lượng; bỏ dòng chú thích, giảm chiều cao xuống khoảng 48px trên desktop. Mobile chia 2 cột, mỗi ô khoảng 44px.

Bấm **Bị chặn** để lọc các SS đã được SpamBot xác nhận chặn do vi phạm điều khoản. Đây là trạng thái riêng với hạn chế spam thông thường. Bấm **Đóng băng** để lọc SS đóng băng; bấm **Tất cả** để bỏ hai loại lọc trạng thái. Bộ lọc tên/worker khác vẫn được giữ.

Số đếm tính toàn workspace, không chỉ trang hiện tại. Live phản ánh khả năng đăng nhập, nên một SS có thể đồng thời Live và Bị chặn; các số không phải những nhóm loại trừ nhau.

API tự đọc lại các kết quả mã hóa cũ khi khởi động và tách đúng thông báo Bị chặn khỏi generic spam. Không liên hệ Telegram, không đổi session/proxy hoặc reset hội thoại. Kết quả đã thay đổi trong lúc cập nhật không bị ghi đè. Kết quả không giải mã được được giữ nguyên, không đoán trạng thái. Các lần check mới lưu trạng thái blocked trực tiếp; đếm/lọc sau đó dùng SQL trên trạng thái đã lưu.

## Cập nhật

Giữ `.env.docker` và Docker volume, giải nén đè đúng thư mục cài cũ rồi chạy **setup.cmd một lần** để build API/web/worker mới. Sau đó dùng **run.cmd**. Không thêm migration, head vẫn **0010**. Giữ toàn bộ proxy, giao diện dòng SS gọn và tự chọn cổng trống.
