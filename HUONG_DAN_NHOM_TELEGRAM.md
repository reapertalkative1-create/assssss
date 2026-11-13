# Nhóm tài khoản và nhóm chat Telegram

## Cập nhật Windows

Giải nén đè vào đúng thư mục cũ, giữ `.env.docker` và Docker volume. Mở Docker Desktop, chạy **setup.cmd một lần** để nâng cơ sở dữ liệu lên **0014** và build API/web/worker; những lần sau dùng **run.cmd**. Các mục phiên bản bên dưới trong README và hướng dẫn Windows là lịch sử.

## Nhóm các session trong ứng dụng

1. Mở **Tài khoản Telegram → Nhóm tài khoản** để tạo hoặc đổi tên nhóm. Danh sách hiển thị số SS mỗi nhóm.
2. Tích các SS trên bảng (có thể chọn toàn bộ kết quả lọc, kể cả nhiều trang), mở **Nhóm tài khoản**, chọn nhóm đích và bấm **Áp dụng**. Chọn **Bỏ khỏi nhóm** để bỏ phân loại. Mỗi SS thuộc tối đa một nhóm.
3. Dùng **Mọi nhóm / Chưa có nhóm / tên nhóm** trên thanh lọc. Khi chọn tất cả theo bộ lọc, check, xóa, gán/xuất proxy và kháng nghị chỉ áp dụng trong nhóm đang lọc. Đổi bộ lọc sẽ bỏ lựa chọn cũ.
4. **Xóa nhóm** chỉ xóa nhãn nhóm, giữ nguyên các tài khoản và session. Xóa SS sẽ bỏ SS khỏi nhóm.

## Nhóm chat Telegram của từng SS

Ở dòng SS đã xác thực chọn **Thao tác → Nhóm Telegram**. Worker Online sẽ đọc danh sách nhóm mà SS đó đã tham gia. Bạn có thể tìm theo tên, username hoặc ID, bấm **Làm mới** và **Xuất TXT** theo kết quả đang lọc. TXT dùng username công khai khi có, hoặc ID nhóm riêng tư. Dùng tài khoản có quyền truy cập khi nhập lại ID. Danh sách tối đa 2.000 nhóm mỗi lần, giao diện sẽ báo nếu còn dữ liệu chưa tải.

Đây là danh sách nhóm chat, không bao gồm hội thoại cá nhân hoặc kênh phát tin. Danh sách không tự kiểm tra quyền đăng; kiểm tra quyền tại tuyến gửi trước khi bắt đầu. Tính năng chỉ đọc danh sách, không tự tham gia hay rời nhóm. Nếu Telegram yêu cầu FloodWait, hãy đợi theo thông báo rồi làm mới.

Bạn có thể tải TXT đó vào **Tuyến chuyển tiếp → Gửi bài từ liên kết**. Mỗi đợt hỗ trợ tối đa 1.000 nhóm hợp lệ, vì vậy cần chia file nếu danh sách lớn hơn.
