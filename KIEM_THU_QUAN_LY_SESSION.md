# Kiểm thử bản quản lý nhiều session — 11/11/2026

## Phạm vi

Bỏ trần tổng 100 session ở luồng web bằng cách đọc ZIP từng thành viên và tự chia nhiều yêu cầu nhỏ. Thêm bộ lọc/tổng quan tình trạng, lựa chọn theo trang/toàn bộ kết quả lọc có ngoại lệ, thao tác Bật/Tắt/Check/đánh dấu đóng băng hàng loạt và tác vụ lưu bền trong database. Migration 0007 thêm metadata sức khỏe session và bảng tác vụ/items.

## Kết quả

- Toàn bộ Python local tại mốc tích hợp: **278 passed, 146 deselected**; `pytest -q -m 'not integration and not telegram_live'`.
- Nhóm cuối sau bổ sung lựa chọn ngoại lệ, heartbeat >200 và cải tiến cấp lại slot khởi động: **36 passed, 14 deselected** (bulk + worker accounts + account E2E). Nhóm bulk/migration riêng trước cải tiến khởi động: **12 passed, 10 deselected**. Các nhóm này có chồng lặp; không cộng thành tổng số kiểm thử.
- Frontend cuối: **46 passed** trong 6 tệp; TypeScript/Vite build thành công. Có kiểm thử UI tự chia 101 file thành yêu cầu 100 và 1, không render toàn bộ kết quả cùng lúc.
- Bộ bulk xác minh snapshot 251 tài khoản, xử lý nhiều lượt qua các transaction mới, hủy 51 mục chưa xử lý, kiểm tra đúng bộ lọc, đánh dấu/bỏ đánh dấu, phân loại network/Die/FROZEN/FloodWait, thử lại riêng lỗi, RBAC/CSRF và chọn toàn bộ trừ ID được bỏ chọn.
- Giới hạn xếp khoảng 30 lệnh kiểm tra mỗi worker được kiểm thử. Kiểm tra đồng thời tối đa 3; khởi động kết nối tối đa 3 và tiếp tục cấp slot ngay khi xong, không đợi heartbeat tiếp theo cho từng nhóm.
- Kiểm thử heartbeat **251 account reports** qua API thật: không bị trần 200 cũ, không mất lease. Đọc account reports từ DB theo nhóm thay vì truy vấn từng tài khoản.
- Migration nâng/hạ SQLite, so sánh model/schema: qua.

## Trình duyệt thật

- Chromium + Vite + API/SQLite: catalog 251, chọn toàn bộ, bỏ/chọn lại một dòng, Tắt toàn bộ 251, tải lại trang khi tác vụ đang xử lý, kết quả vẫn hoàn tất. Lọc nhóm Die cho 84 mục và mở chi tiết phân trang. Không có lỗi JavaScript. Các nhãn trong catalog này là dữ liệu demo, không phải đánh giá Telegram thật.
- Chromium + API + worker/AccountManager thật + FakeBackend: tải ZIP Deflate chứa **205 session giả**, trình duyệt tự chia **100 + 100 + 5**, worker xác thực đủ 205, không hỏi OTP và không có lỗi JavaScript.

## Giới hạn xác minh

Chưa dùng session của người dùng để kết nối Telegram thật; chưa thử mọi dạng hạn chế tài khoản/frozen, ZIP64 quy mô rất lớn, PostgreSQL integration toàn bộ hoặc build sạch Docker image bản này. Không thêm dependency. setup.cmd trên máy người dùng sẽ chạy migration và build mã mới.

Đóng băng chỉ tự ghi khi Telegram trả lỗi FROZEN; đăng nhập/get_me thành công không chứng minh mọi quyền gửi tin đều bình thường. Nhãn thủ công được phân biệt với kết quả Telegram. FloodWait/lỗi mạng không tự coi là Die.

Không có trần số session toàn catalog; vẫn có giới hạn từng file/yêu cầu, các lô/queue được kiểm soát và phân trang. Dung lượng, kết nối đồng thời và tốc độ thực tế tùy máy/mạng/Telegram. Xem HUONG_DAN_QUAN_LY_SESSION.md.

ZIP phát hành không chứa file session của người dùng, .env.docker, khóa hoặc database thử nghiệm.
