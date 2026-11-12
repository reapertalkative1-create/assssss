# Thời hạn hạn chế ngay trên dòng SS

Giữ `.env.docker` và Docker volume. Giải nén đè ZIP vào đúng thư mục cũ rồi chạy **setup.cmd một lần** để build API/web/worker mới; những lần sau dùng **run.cmd**. Không thêm migration, head vẫn **0012**.

Cột **Trạng thái** giữ nhãn Bị chặn / Bị spam / Đóng băng và thêm một dòng gọn:

- **Vĩnh viễn**: chỉ khi phản hồi Telegram nói rõ permanent / forever / vĩnh viễn cho tài khoản đó.
- **Còn 2 ngày 3 giờ** hoặc **Còn 5 giờ 20 phút**: khi có mốc mở hạn chế rõ ràng. Dưới một giờ hiện số phút. Đồng hồ cập nhật mỗi phút, không khởi động lại khi tải lại trang.
- **Chưa rõ thời hạn**: Telegram không cung cấp ngày giờ rõ ràng hoặc nội dung không đủ chắc chắn. Bị chặn do vi phạm điều khoản, PHONE_NUMBER_BANNED hoặc FROZEN tự chúng không xác định được số ngày/vĩnh viễn.
- **Đã đến hạn · check lại**: thời hạn Telegram từng báo đã tới. Ứng dụng vẫn giữ nhãn hạn chế cho đến khi check lại có kết quả mới, không tự chuyển sang Live.

Rê chuột vào dòng đếm ngược để xem mốc hết hạn theo giờ Việt Nam. Ngày giờ UTC/offset được đổi về cùng một mốc tuyệt đối trước khi tính. Số ngày/giờ tương đối chỉ được tính khi có thời gian của tin nhắn SpamBot làm gốc; không lấy thời điểm mở trang để bắt đầu đếm lại.

Sau cập nhật, dữ liệu đã lưu có phản hồi và trạng thái phù hợp được hiển thị ngay. Nếu chưa có thông tin đủ rõ, bấm **Check spam / đóng băng** tại dòng để lấy kết quả mới. Nếu có kháng nghị đang dở, giữ luồng kháng nghị và dùng Lấy phản hồi mới khi thích hợp, tránh khởi động lại cuộc hội thoại.

Không dùng thời gian FloodWait làm thời hạn cấm; không dùng hạn gửi kháng nghị hoặc ngày tài khoản sẽ bị xóa làm ngày mở khóa; không lấy hạn spam cũ áp vào một lỗi đóng băng/khóa đăng nhập mới. Nhãn đóng băng thủ công không được coi là Telegram xác nhận thời hạn. Lời cảnh báo giả định như “may/if” không được coi là tài khoản bị khóa vĩnh viễn. Nội dung mâu thuẫn hoặc ngày giờ mơ hồ được để Chưa rõ thời hạn.

Dòng Live phụ được bỏ khỏi các dòng bị hạn chế để tránh hiểu nhầm. Session đăng nhập được và quyền gửi tin vẫn là các trạng thái riêng; không đổi dữ liệu sức khỏe/session vì chỉ đếm ngược trên giao diện. Khi check mới báo không hạn chế, dòng thời hạn được bỏ. Không chép nguyên chat SpamBot vào bảng. Người vận hành chỉ nhận loại thời hạn và mốc ngày giờ, không nhận nội dung chat riêng.

Giữ nút riêng Kiểm tra list proxy, xuất Live/Die, SS+proxy cùng lúc, API lưu tự động trong Cài đặt và nút đỏ Xóa đã chọn. Không bảo đảm Telegram luôn cung cấp thời hạn cho mọi loại hạn chế.
