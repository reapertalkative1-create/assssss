# Kiểm thử trạng thái màu — 12/11/2026

- Frontend: **62 passed**, 7 tệp; TypeScript/Vite production build thành công.
- Python test_spambot: **30 passed, 10 deselected** với marker not integration and not telegram_live.
- Nhận đúng thông báo tài khoản bị chặn trong ảnh thành đỏ và lý do tiếng Việt. Dữ liệu cũ unknown vẫn trình bày đúng. Không kết luận chặn từ câu điều kiện, “may be blocked” hoặc phủ định.
- Xanh chỉ từ kết quả clear; limited/frozen/dead dùng đỏ; unknown/lỗi kiểm tra dùng vàng. Nhãn đóng băng thủ công ghi rõ nguồn.
- Kiểm thử trang xác nhận nguyên văn bot không được render trên bảng SS; tiến độ/lỗi và quyền mở kháng nghị còn giữ nguyên.
- Chromium thật với API và dữ liệu hiển thị giả: nhãn đỏ bị chặn, nhãn xanh không hạn chế và lý do tiếng Việt; không còn nguyên văn bot trên bảng. Kiểm tra CSS màu thực, sáng/tối và viewport 390px không tràn ngang toàn trang. Không lỗi JavaScript.

Không dùng session người dùng, không gửi Telegram thật. Browser dùng fixture giả cho tình trạng tài khoản. Không kiểm thử mọi ngôn ngữ/cách diễn đạt bot hoặc xét duyệt hạn chế Telegram. Không thêm dependency/migration; chưa build sạch Docker Windows trong đợt sửa này. Các báo cáo cũ mô tả phiên bản giao diện cũ.

ZIP loại trừ session, khóa, database, .env riêng và runtime; giữ launcher tự chọn cổng và giao diện tiến độ trên dòng SS.
