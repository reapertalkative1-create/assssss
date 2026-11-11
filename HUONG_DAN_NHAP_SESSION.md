# Nhập tối đa 100 session Telethon trên web

## Cập nhật

Giữ nguyên `.env.docker` và Docker volume. Giải nén đè mã nguồn vào thư mục ứng dụng cũ, chạy **setup.cmd một lần** để build API/web/worker và nâng database lên migration 0006. Những lần sau dùng **run.cmd**.

## Nhập hàng loạt

1. Đóng ứng dụng khác đang dùng những session này để tránh cùng một phiên chạy ở hai nơi.
2. Đăng nhập web bằng quản trị viên. Vào **Tài khoản Telegram → Nhập session hàng loạt**.
3. Chọn worker đang Online. Chọn nhiều file `.session` bằng Ctrl+A hoặc chọn một ZIP chứa chúng, tối đa **100 session/lần**.
4. Nhập `api_id/api_hash` cho lô này và bấm **Nhập và kiểm tra session**. File session không chứa sẵn cặp API này. Nếu dùng nhiều cặp API, chia thành nhiều lô.
5. Xem kết quả từng file: đang chờ, đang kiểm tra, thành công, trùng hoặc lỗi. Worker kiểm tra tối đa **3 session cùng lúc**; tổng thời gian phụ thuộc mạng/Telegram. Session hợp lệ không cần OTP/2FA lại.

Không đăng nhập Telegram ngay trong setup. Việc kết nối xảy ra khi người dùng chủ động bấm Nhập trên web của họ.

Tài khoản thành công được đặt tên tạm `Session ...`, có username/Telegram ID nếu worker nhận được. Bạn có thể Đổi tên rồi Bật tài khoản để chạy tuyến. Nhập thành công không tự bật chuyển tiếp.

## Giới hạn và xử lý lỗi

- Hỗ trợ SQLite session của Telethon; chưa hỗ trợ Pyrogram hoặc tdata.
- Tổng file tải lên tối đa **10 MiB**, mỗi session tối đa **1 MiB**, tổng dữ liệu session giải nén tối đa **32 MiB**. ZIP không đặt mật khẩu. Các tệp không kết thúc bằng `.session` trong ZIP được bỏ qua.
- Session trùng trong cùng lô hoặc những lô đã nhập trước đó được bỏ qua, không tạo tài khoản thứ hai hoặc ghi đè cấu hình cũ.
- Session bị thu hồi/hết hiệu lực cần đăng nhập lại bằng số điện thoại, OTP và 2FA nếu có.
- Lỗi mạng/thời gian chờ có thể dùng **Kiểm tra lại**; nếu Telegram trả FloodWait, đợi hết thời gian yêu cầu. Không tự thử dồn dập.
- Đóng hộp thoại không hủy hàng đợi. Sau khi mở lại trang, danh sách tài khoản giữ trạng thái. Có thể bấm **Kiểm tra session** để lấy lại kết quả hoặc thử lại lệnh hết hạn. Worker khởi động lại giữa một lần kiểm tra có thể để lệnh ở trạng thái đang xử lý tới khi hết hạn (tối đa 1 giờ), sau đó thử lại.
- Đổi worker trong lúc lệnh kiểm tra còn chờ/đang xử lý sẽ bị chặn; đợi hoàn tất hoặc hết hạn rồi đổi.

## Lưu trữ

Session được chuyển sang StringSession tương thích Telethon và lưu mã hóa với khóa hiện có. ZIP và file SQLite gốc không lưu vào database; chỉ đọc trong bộ nhớ. API ID/hash cũng được mã hóa. Worker chỉ nhận phiên của tài khoản được gán và chỉ lấy session khi giữ lease. Log/audit không ghi session gốc.

Bản ZIP mã nguồn công khai không chứa session đã tải lên của người dùng. Không đưa file `.session` hoặc `.env.docker` lên GitHub.
