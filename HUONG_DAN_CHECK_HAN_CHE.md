# Check Telegram bị spam hoặc đóng băng

## Cập nhật

Giữ `.env.docker` và Docker volume, giải nén đè ZIP mới vào đúng thư mục cũ. Mở Docker Desktop, chạy **setup.cmd một lần** để build lại API/web/worker, sau đó dùng **run.cmd**. Không thêm migration; head vẫn **0009**. Nếu giao diện còn cũ, nhấn Ctrl+F5.

## Cách dùng

Vào **Tài khoản Telegram**:

- Bấm **Check spam / đóng băng** ngay tại dòng tài khoản cần kiểm tra, không cần mở menu Thao tác.
- Muốn kiểm tra nhiều tài khoản: lọc rồi bấm **Check tất cả theo bộ lọc (N)**. Thao tác này áp dụng cho toàn bộ kết quả lọc, kể cả các trang khác, không phụ thuộc các dòng đã tích.
- Hoặc tích các SS cần kiểm tra và bấm **Check spam / đóng băng đã chọn**.
- Dùng **Bị spam**, **Đóng băng**, **Chưa check spam**, **Lỗi check spam** để lọc nhanh. Số trên nút là tổng trong workspace; các bộ lọc tên, worker và bật/tắt khác vẫn áp dụng. Bấm lại bộ lọc nhanh đang chọn để bỏ lọc đó.
- Xem **Tác vụ hàng loạt → Chi tiết** để biết tài khoản nào hoàn tất, lỗi hoặc đang chờ. Kết quả spam và tình trạng session trong bảng tự cập nhật mỗi 5 giây.

Worker cần Online, session và API Telegram cần hợp lệ. Không cần bật chuyển tiếp để check; worker dùng phiên đang chạy hoặc kết nối tạm có lease. Không mở đồng thời hai kết nối cùng session.

## Đọc kết quả

| Kết quả | Ý nghĩa |
| --- | --- |
| SpamBot: bị hạn chế | SpamBot xác nhận hạn chế cấp tài khoản. Đọc phản hồi trong **Thao tác → SpamBot / kháng nghị**. |
| SpamBot: không hạn chế | SpamBot trả lời không áp dụng hạn chế cấp tài khoản lúc kiểm tra. Không bảo đảm gửi được trong mọi nhóm. |
| Đóng băng | Telegram trả lỗi FROZEN hoặc SpamBot có thông báo đóng băng rõ ràng được nhận diện. Tài khoản được yêu cầu dừng. Dòng “Bạn đánh dấu” là nhãn do người dùng đặt thủ công, không phải phát hiện tự động. |
| Live | Session đăng nhập/đọc tài khoản được; vẫn có thể bị spam hoặc không được gửi trong một nhóm. |
| Cần đọc phản hồi | Nội dung bot chưa được nhận diện chắc chắn; mở cửa sổ SpamBot để đọc. |
| Lỗi check spam / FloodWait | Không đủ kết quả để kết luận bị spam/đóng băng. Xem lỗi, đợi thời gian Telegram yêu cầu hoặc đưa worker Online. |

Check gửi `/start` tới **@SpamBot chính thức**, không gửi thử tin vào nhóm hoặc tới người khác. Kết quả mới trong 10 phút có thể được dùng lại; tài khoản vừa tương tác kháng nghị được bỏ qua để tránh làm mất bước hội thoại. Tác vụ tiếp tục trên máy chủ khi đóng web.

Không có phép kiểm tra chỉ đọc bảo đảm phát hiện mọi loại cấm gửi tin. Cấm riêng một nhóm, quyền thành viên/admin, chế độ chỉ đọc của nhóm hoặc cách diễn đạt/ngôn ngữ SpamBot chưa hỗ trợ có thể cần đọc lỗi chuyển tiếp/phản hồi thật. Ứng dụng không suy đoán “đóng băng” từ lỗi mạng hoặc từ việc session còn đăng nhập được.

Bản này sửa lỗi kết quả get_me thành công ghi Live dù bước ghi tới SpamBot sau đó nhận lỗi account_frozen. Phản hồi đóng băng được giữ ngay cả khi bot gửi tiếp một tin hướng dẫn.
