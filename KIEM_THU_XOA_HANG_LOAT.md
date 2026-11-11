# Kiểm thử xóa các dòng đã tích — 11/11/2026

- Python toàn bộ: **303 passed, 161 deselected**, `pytest -q -m 'not integration and not telegram_live'`.
- Nhóm tính năng cuối sau bổ sung khóa dòng khi xóa: **5 passed, 5 deselected**. Hồi quy ban đầu API/account import/bulk: **44 passed, 38 deselected**. Các nhóm có chồng lặp, không cộng thành tổng.
- Frontend: **49 passed** trong 6 tệp. TypeScript/Vite build cuối thành công.
- Kiểm thử UI xác nhận một lần bấm Xóa đã chọn gọi thẳng API, không có dialog, nút xác nhận hay ô nhập tên.
- Kiểm thử snapshot >100: tạo 251 tài khoản, lọc 250 dòng Die, bỏ tích 1, xóa đúng 249; giữ lại dòng bỏ tích và tài khoản ngoài bộ lọc.
- Kiểm thử dọn route/checkpoint/forward job liên quan, giữ dữ liệu tài khoản khác.
- Kiểm thử tài khoản giữ lease: chuyển draining, dừng, xóa payload lệnh đang chờ, chặn lấy lease mới; chỉ purge sau khi release/hết lease. Dừng xếp hàng không đảo ngược mục đã bắt đầu xóa.
- Kiểm thử RBAC/CSRF; bulk removal không tạo lệnh logout Telegram.
- Giữ đường lease/API credential được phép cho lệnh logout đã giao của luồng xóa một tài khoản cũ; kiểm thử tương thích này qua.

## Chromium thật

API/SQLite và Vite, catalog demo 251 tài khoản:

1. Lọc 84 dòng Die.
2. Chọn toàn bộ rồi bỏ tích một dòng, số lượng còn 83.
3. Bấm Xóa đã chọn một lần: không dialog JavaScript, không modal xác nhận, không gõ tên.
4. Đợi tác vụ máy chủ: đúng 83 dòng bị xóa, dòng bỏ tích vẫn truy cập được; tổng catalog còn 168.
5. Không có lỗi JavaScript.

Tất cả dữ liệu dùng để kiểm thử là dữ liệu giả do phiên này tạo. Không xóa dữ liệu trên máy người dùng hoặc tài khoản Telegram thật. Chưa chạy PostgreSQL integration toàn bộ hay build sạch Docker image trong lần sửa này. Khóa dòng dùng theo cơ chế PostgreSQL hiện có; SQLite bỏ qua FOR UPDATE.

Không thêm migration (head 0008). Khi cập nhật giữ .env.docker/volume và chạy setup.cmd một lần để build mã API/web mới. ZIP không chứa session người dùng hoặc database/khóa thử nghiệm.
