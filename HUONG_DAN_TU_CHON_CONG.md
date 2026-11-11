# Sửa lỗi cổng 8787 đang bị chiếm

Lỗi `Bind for 127.0.0.1:8787 failed: port is already allocated` xảy ra sau khi build thành công: ứng dụng/container khác đang giữ cổng 8787.

## Cập nhật

Giữ nguyên `.env.docker` và Docker volume. Giải nén đè toàn bộ ZIP mới vào **đúng thư mục đang cài**, mở Docker Desktop rồi chạy **setup.cmd** lại. Sau khi setup hoàn tất, những lần sau dùng **run.cmd**.

Script mới tự chọn cổng trống, ví dụ `8788`, và lưu `TFCC_HTTP_PORT` vào `.env.docker`. Trình duyệt tự mở đúng địa chỉ; cũng có dòng:

```text
Application running: http://127.0.0.1:8788
```

Lấy địa chỉ thực tế được in trên máy bạn, không mặc định mở lại 8787. Nếu cổng đó thuộc chính web của bản cài hiện tại, run/setup giữ lại cổng cũ. Script không dừng container của bản cài khác, không xóa volume và không đổi khóa/tài khoản/session.

Script kiểm tra cả cổng Docker công bố và khả năng bind loopback của Windows. Nếu cổng bị chiếm giữa lúc kiểm tra và khởi động, script chọn cổng khác và thử lại, tối đa 3 lần khởi động. Lỗi API/database khác vẫn được báo đúng, không coi là lỗi cổng.

Nếu 100 cổng gần cổng đang cấu hình đều không dùng được, chọn một cổng khác trong `.env.docker`, ví dụ `TFCC_HTTP_PORT=8899`, rồi chạy setup/run lại. Script vẫn xác minh cổng đó trước khi dùng.

## Chạy ngay với bản cũ

Có thể sửa **chỉ dòng** `TFCC_HTTP_PORT=8787` trong `.env.docker` thành `TFCC_HTTP_PORT=8788` rồi chạy setup.cmd lại. Nếu 8788 cũng bận, dùng cổng trống khác. Không xóa `.env.docker`, không đổi tên project Docker và không xóa volume để xử lý lỗi này.

Bản này giữ giao diện bảng SS của bản trước: trạng thái, phản hồi SpamBot, tiến độ và lỗi trực tiếp trên dòng; không có khung Tác vụ hàng loạt phía dưới. Không thêm migration, head vẫn 0009.
