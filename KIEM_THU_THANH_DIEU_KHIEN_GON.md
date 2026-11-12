# Kiểm thử trang tài khoản tinh gọn — 12/11/2026

- Frontend: **69 passed**, 7 tệp; TypeScript/Vite production build qua.
- Kiểm thử không còn khung check lặp/nút thêm trùng; danh sách rỗng không hiện điều khiển hàng loạt. Bộ lọc phụ mở được.
- Check toàn bộ theo bộ lọc gửi đúng phạm vi; chọn toàn bộ rồi bỏ tích vẫn giữ exclude_ids đúng khi áp dụng quản lý. Bỏ chọn hết làm reset thao tác phá hủy; xóa đã chọn vẫn xếp hàng ngay, không thêm modal/nhập tên.
- Giữ kiểm thử proxy import, kháng nghị, trạng thái màu, đếm/lọc blocked/frozen và tiến độ ngay trên dòng.
- Chromium thật + API/SQLite, 80 SS giả: check theo lọc blocked, chọn 80/bỏ tích 1/tắt đúng phạm vi 79; mở kháng nghị và nhập proxy từ phạm vi đã chọn. Kiểm tra bộ lọc phụ/bỏ lọc, check proxy toàn bộ, trạng thái rỗng.
- Desktop 1600×1000: bảng bắt đầu khoảng y=333px, hiển thị nhiều dòng ngay màn hình đầu. Kiểm tra sáng/tối và mobile 390px không tràn ngang toàn trang. Không lỗi JavaScript/HTTP 500.
- Điều khiển không bị khóa trong đợt refresh nền định kỳ; vẫn khóa khi đang gửi thao tác hoặc tải lần đầu.

Backend/worker/proxy transport/launcher không thay đổi; không chạy lại Python hoặc build sạch Docker Windows. Browser dùng dữ liệu giả, worker offline, không kết nối hay gửi Telegram thật. ZIP loại trừ .env riêng, khóa, session, database và runtime.
