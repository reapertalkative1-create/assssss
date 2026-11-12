# DEVYN FORWARDER — Gửi bài từ liên kết

## Cập nhật

Giải nén đè vào **đúng thư mục ứng dụng đang dùng**, giữ `.env.docker` và Docker volume. Mở Docker Desktop, chạy **setup.cmd một lần** để nâng database lên **0013** và build API/web/worker; các lần sau chạy **run.cmd**. Không xóa database hoặc tạo bộ khóa mới khi còn dữ liệu cũ.

## Cách gửi

1. Vào **Cài đặt → API Telegram** để lưu API một lần. Tại **Tài khoản Telegram**, đăng nhập/nhập SS, cấu hình proxy nếu cần, kiểm tra tài khoản và bảo đảm worker Online.
2. Mở **Tuyến chuyển tiếp → Gửi bài từ liên kết**. Đặt tên và chọn một SS đã xác thực từ danh sách tài khoản. Có ô tìm tên/username và phân trang.
3. Trong Telegram, bấm **Sao chép liên kết tin nhắn**, dán vào ô **Liên kết bài viết Telegram**. Hỗ trợ bài công khai `https://t.me/tenkenh/123` và bài riêng `https://t.me/c/123456789/123` mà SS có quyền đọc.
4. Chọn **Chuyển tiếp · giữ nguồn** hoặc **Sao chép nội dung**. Mỗi đợt lấy đúng một tin nhắn ở liên kết, không tự lấy bài tiếp theo hoặc cả album.
5. Tải file `.txt` UTF-8 hoặc dán nhóm, mỗi dòng một nhóm. Tối đa **1.000 nhóm duy nhất / đợt**, file tối đa **500 KB**. Tự bỏ dòng trống, dòng bắt đầu `#` và nhóm trùng. File mới thay nội dung ô nhập; bạn có thể sửa/dán thêm trước khi lưu.
6. Chỉnh **Nghỉ giữa hai nhóm** (mặc định 60 giây, từ 5 đến 86.400 giây). Có thể đặt **Bắt đầu từ** theo giờ trên máy; để trống để chạy sau khi bấm bắt đầu.
7. **Lưu đợt gửi** chỉ tạo bản nháp. Bấm **Kiểm tra nhóm**, xem quyền từng nhóm. Chỉ khi bài nguồn và toàn bộ nhóm hợp lệ mới có nút **Bắt đầu gửi**. Muốn bỏ nhóm lỗi: sửa bản nháp → **Chỉ giữ nhóm hợp lệ** → lưu → kiểm tra lại.
8. Bấm **Bắt đầu gửi** để tạo hàng đợi một lượt. SS đang tắt sẽ được bật. Xem **Tiến độ từng nhóm** để biết đã gửi, đang chờ hoặc lỗi. **Tạm dừng / Tiếp tục / Dừng / Chạy tiếp** giữ hàng đợi, không tạo thêm bản gửi trùng.

Ví dụ file nhóm:

```text
# Các nhóm bạn có quyền đăng
@nhom_cua_ban
https://t.me/nhom_cua_ban_2
-1001234567890
```

Link mời `https://t.me/+...` chỉ dùng để tra nhóm mà SS **đã tham gia**. Ứng dụng không tự tham gia nhóm. Bài nguồn bảo vệ chuyển tiếp không được sao chép để vượt bảo vệ.

## Thời gian và trạng thái

- Khoảng nghỉ áp dụng cho cả SS khi SS có đợt gửi từ liên kết đang chạy, kể cả khi nhiều tuyến dùng cùng SS. Chỉ một tác vụ được nhận tại một thời điểm; các nhóm quá hạn sau tạm dừng vẫn chờ đủ khoảng nghỉ.
- Thời gian **Sớm nhất** là mốc sớm nhất có thể gửi. Tình trạng worker, quyền nhóm, giới hạn phút, khoảng nghỉ và FloodWait có thể làm thời gian thực tế muộn hơn.
- Khi Telegram trả **FloodWait**, chờ trên toàn SS. Khi trả **PeerFlood/hạn chế spam hoặc đóng băng**, dừng SS và tạm dừng các tuyến đang chạy của SS; giữ các việc còn lại để kiểm tra trước khi chạy tiếp. Không tự đổi SS để tiếp tục gửi.
- Khoảng nghỉ không bảo đảm tránh hạn chế của Telegram. Chỉ gửi vào nhóm/kênh bạn được phép đăng.
- Chỉ sửa/xác minh lại đợt chưa tạo hàng đợi. Đợt đã gửi có thể **Tạo bản mới** để chủ động gửi lại. Không lặp vô hạn hoặc luân phiên tài khoản tự động.
- Khóa hàng đợi chống tạo trùng khi bấm bắt đầu/chạy tiếp nhiều lần. Nếu worker hỏng ngay sau khi Telegram nhận bài nhưng trước khi báo kết quả, cơ chế khôi phục có thể gửi lại; không cam kết exactly-once khi mất kết nối.

Tuyến tự theo dõi bài mới trước đây vẫn có tại **Theo dõi nguồn**. Các chức năng tài khoản, proxy, check và xuất TXT vẫn được giữ.
