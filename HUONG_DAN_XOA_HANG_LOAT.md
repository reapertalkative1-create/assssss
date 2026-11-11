# Xóa các tài khoản đã tích — không gõ xác nhận

## Cập nhật

Giữ nguyên `.env.docker` và Docker volume, giải nén đè mã nguồn vào thư mục cũ. Chạy **setup.cmd một lần** để build API/web mới, sau đó dùng **run.cmd**. Bản này không thêm migration; database hiện tại vẫn ở 0008.

## Cách dùng

1. Đăng nhập web bằng quản trị viên, vào **Tài khoản Telegram**.
2. Lọc nhóm cần xóa (Die, lỗi, spam, worker, tên…).
3. Tích từng dòng, Chọn trang hiện tại hoặc **Chọn toàn bộ N kết quả lọc**. Có thể bỏ tích những dòng muốn giữ.
4. Bấm nút đỏ **Xóa đã chọn**. Thao tác được xếp hàng ngay, **không có hộp xác nhận và không bắt gõ tên**.
5. Xem tiến độ ngay trên dòng session. Khi xóa xong, dòng session biến mất khỏi bảng.

Tập ID được chụp tại lúc tạo tác vụ. Những dòng bỏ tích và những tài khoản ngoài lựa chọn được giữ lại, kể cả khi chuyển trang. Đổi bộ lọc sẽ bỏ lựa chọn cũ, giống các thao tác hàng loạt khác.

## Dữ liệu được xóa

Xóa bản ghi tài khoản/session trong ứng dụng, API pair và báo cáo SpamBot đã lưu, tuyến chuyển tiếp, checkpoint, tác vụ chuyển tiếp và các lệnh liên quan. Lịch sử tác vụ hàng loạt và audit vẫn ghi kết quả xóa.

Đây là xóa khỏi ứng dụng, không xóa tài khoản Telegram và không gửi lệnh đăng xuất phiên lên Telegram. Các file `.session`/ZIP gốc bạn giữ trên máy cũng không bị xóa. Có thể nhập lại file gốc sau khi bản ghi cũ được dọn xong.

## Tài khoản đang chạy

Ứng dụng yêu cầu dừng, hủy các lệnh chưa hoàn tất và chặn việc lấy lease mới. Nếu worker còn giữ phiên, tiến độ hiển thị **Đang dừng phiên để xóa**, đợi worker trả lease hoặc lease hết hạn rồi mới dọn bản ghi. Cơ chế này tránh xóa dữ liệu khi worker còn đang giữ quyền dùng phiên.

Đóng web không hủy hàng đợi. **Dừng xếp hàng** chỉ hủy những mục chưa bắt đầu xử lý; các mục đã bắt đầu xóa vẫn hoàn tất. Những thao tác bên Telegram đã thực hiện trước khi yêu cầu xóa không thể rút lại bằng việc xóa bản ghi ứng dụng.

Nút Xóa riêng trong menu từng dòng vẫn là luồng cũ có tùy chọn đăng xuất Telegram và xác nhận tên. Để xóa nhiều tài khoản không gõ xác nhận, dùng **Xóa đã chọn** ở thanh thao tác hàng loạt.
