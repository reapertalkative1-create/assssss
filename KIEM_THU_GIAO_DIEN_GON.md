# Kiểm thử bảng SS gọn — 12/11/2026

- Frontend: 62 kiểm thử qua trong 7 tệp; TypeScript/Vite build thành công.
- Chromium với dữ liệu giả: nhãn đỏ Bị chặn và xanh Bình thường; không có Lý do hoặc nguyên văn bot trên bảng. Kiểm tra màu CSS, sáng/tối và 390px không tràn ngang toàn trang; không lỗi JavaScript.
- Dòng mẫu desktop dưới 145px (ảnh chụp khoảng 107px), thay cho khung cao của bản trước. Dòng có nhiều thao tác/kháng nghị đang chạy hoặc mở Thông tin có thể cao hơn.
- Giữ kiểm thử xóa ngay, check theo bộ lọc, mở kháng nghị và dừng đợt. Backend/worker/launcher không thay đổi trong bản này, không chạy lại Python/Docker.

Không dùng session người dùng hoặc gửi Telegram thật. ZIP loại trừ .env riêng, khóa, session, database và runtime; giữ launcher tự chọn cổng.
