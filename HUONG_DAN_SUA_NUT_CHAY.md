# Bản sửa nút Chạy cụm chuyển tiếp

Phiên bản: `2026.11.17-cluster-start-fix1`. Giữ nguyên phiên bản database `0022`.

## Cập nhật trên máy đang dùng

1. Sao lưu thư mục ứng dụng hiện tại và database theo cách bạn đang dùng.
2. Chép nội dung ZIP này đè vào **đúng thư mục ứng dụng cũ**, nơi đang có `run.cmd` và `.env.docker`. Giữ nguyên `.env.docker`, `.docker-ready`, thông tin worker và dữ liệu Docker hiện có; giữ cả `.env` nếu bạn có cấu hình riêng trong file này.
3. Bật Docker Desktop rồi chạy `run.cmd`. Launcher nhận phiên bản mới, build lại container và giữ cấu hình/session cũ. Chờ hoàn tất rồi mở lại địa chỉ ứng dụng do launcher hiển thị.
4. Nhấn `Ctrl+F5` trong trình duyệt để nạp giao diện mới.
5. Mở cụm và bấm **Chạy**. Chỉ thực hiện bước này khi bạn muốn bắt đầu gửi bài thật.

Không cần tạo lại tài khoản, nhập lại session hoặc xóa database để áp dụng bản sửa.

Nếu cài lần đầu trong thư mục mới, chạy `setup.cmd` thành công trước rồi mới chạy `run.cmd`.

## Khi mở lại cụm

- **Đang chạy / 132 nhóm:** đã có công việc trong hàng đợi. Gửi từng nhóm theo thời gian nghỉ cấu hình; không phải gửi cả 132 nhóm tức thì.
- **Không thể bắt đầu:** đọc nguyên nhân cạnh từng nhóm. Worker offline, tài khoản bị hạn chế hoặc proxy lỗi cần được xử lý trước khi thử lại.
- **Chưa xếp hàng:** lượt chưa tạo công việc gửi; không được tính là hoàn tất.
- **Đã có lượt trước:** cơ chế chống trùng đã giữ bài trong hàng đợi/lịch sử. Mở **Hàng đợi tác vụ**, chọn tác vụ lỗi và dùng chức năng thử lại có sẵn sau khi xử lý nguyên nhân. Nếu kết quả gửi chưa xác định, dùng chức năng đối chiếu kết quả trước; bản sửa không tự gửi lại các bài đã gửi hoặc chưa rõ kết quả.

## Nội dung sửa

- Giữ `source_peer` và `dest_peer` trong phản hồi API giao job để worker phân giải được nguồn/đích dạng username.
- Hiển thị đúng số nhóm và lý do chưa chạy khi không có job; bỏ trạng thái “Hoàn tất 0/0” cho trường hợp này.
- Lưu lỗi khởi chạy để vẫn xem được sau khi tải lại trang.
- Hoàn tác riêng thao tác khởi chạy của tài khoản bị lỗi, giữ công việc của tài khoản khởi chạy thành công.
- Nút Chạy/Dừng dùng trạng thái thực do API trả về, không báo đang chạy khi không có công việc.

Bản này tập trung vào nút Chạy cụm chuyển tiếp; chưa sửa toàn bộ các vấn đề vòng lặp tin nhắn trong báo cáo review trước.

Kiểm thử dùng dữ liệu giả và worker giả; không gửi tin nhắn tới Telegram thật. Chưa kiểm thử Docker/Windows hoặc PostgreSQL thật trong môi trường này.
