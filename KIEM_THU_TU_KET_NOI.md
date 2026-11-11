# Xác minh bản tự kết nối

- 33 kiểm thử Python liên quan đã qua, 8 nhánh PostgreSQL bị bỏ qua trong lệnh pytest đó. Có kiểm thử tạo/dùng lại/khôi phục credential, không tạo trùng, không ghi credential vào audit, giữ worker Linux hiện có và không kích hoạt worker bị thu hồi.
- PowerShell: kiểm tra cú pháp, tự lưu credential theo cách ghi tệp nguyên tử, giữ các khóa cũ, không thay đổi cấu hình ở lần run sau, tự chạy khi chưa có API ID/hash, và khóa ngăn hai launcher chạy cùng lúc đều qua.
- Docker + PostgreSQL thật: cấu hình không có credential và không có Telegram API ID/hash vẫn tự tạo/khôi phục worker, lưu credential riêng, đăng ký Online và báo đúng hostname máy Windows giả lập MY-WINDOWS-PC.
- Run hai lần dùng cùng worker ID, không tăng số worker, không đổi file cấu hình sau khi đã lưu, giữ session quản trị và các khóa database/mã hóa. Console không chứa credential.
- API/web/worker được thử với dependencies của image đã build ở bản trước, cập nhật thêm mã mới trong các image kiểm thử. Chưa build lại toàn bộ dependency từ đầu trong lần sửa này vì giới hạn ổ đĩa cloud.
- Chưa thử bấm đúp CMD trực tiếp trên Windows; kiểm tra PowerShell thực hiện bằng PowerShell 7.4.6 trên Linux và các container thật. Script chỉ dùng cú pháp PowerShell 5.1 trở lên.
- Chưa đăng nhập/gửi tin qua Telegram thật. Worker Online không thay cho việc cấu hình API ID/hash và đăng nhập OTP/2FA.

Bản này không thêm migration. Giữ nguyên .env.docker và Docker volume của bản cũ, chạy setup.cmd lại một lần để cài code vào image mới. Không kèm cấu hình riêng hoặc dữ liệu thử trong ZIP.

## Sửa UTF-8 BOM trên Windows PowerShell

- Bộ đọc CLI nhận byte UTF-8 có/không BOM bằng utf-8-sig, áp dụng cho cả provision và wait-online.
- PowerShell đặt UTF-8 không BOM riêng cho lần gọi Docker JSON, sau đó khôi phục encoding của tiến trình gọi. Phản hồi JSON có BOM cũng được chấp nhận.
- Đã tái hiện lỗi cũ bằng json.loads với U+FEFF đầu chuỗi.
- 6 trường hợp CLI thực tế trên Docker/PostgreSQL đã qua: provision có/không BOM, wait-online có/không BOM, từ chối JSON không phải object có/không BOM. Worker ID và credential giữ nguyên.
- Kiểm thử PowerShell xác nhận encoding không BOM khi gửi, khôi phục encoding cũ và đọc phản hồi BOM thành công.
