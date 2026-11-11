> Cập nhật giao diện gọn: bảng hiện chỉ dùng nhãn ngắn, đã bỏ phần Lý do và khung lớn. Xem [HUONG_DAN_GIAO_DIEN_GON.md](HUONG_DAN_GIAO_DIEN_GON.md). Phần dưới mô tả cách phân loại và giao diện trước đó.

# Trạng thái màu và lý do lỗi trên bảng SS

Giữ `.env.docker` và Docker volume, giải nén đè ZIP mới vào đúng thư mục cũ rồi chạy **setup.cmd một lần** để build API/web/worker; sau đó dùng **run.cmd**. Không thêm migration, head vẫn 0009. Ctrl+F5 nếu còn giao diện cũ. Bản sửa tự chọn cổng trống vẫn được giữ.

Bảng SS không còn chép nguyên đoạn chat SpamBot. Cột **Trạng thái & lý do** hiển thị nhãn và lời giải thích ngắn bằng tiếng Việt:

- **Xanh — Không bị hạn chế spam**: SpamBot trả kết quả không áp dụng hạn chế cấp tài khoản. Quyền gửi trong từng nhóm vẫn tùy nhóm.
- **Đỏ — Tài khoản bị chặn**: nhận đúng thông báo tài khoản bị chặn do vi phạm điều khoản Telegram. Nếu thông báo ghi các báo cáo đã được kiểm duyệt xác nhận, lý do hiển thị tương ứng; không tự kết luận chặn vĩnh viễn.
- **Đỏ — Bị hạn chế spam / Tài khoản đóng băng / Tài khoản bị khóa / Session hết hiệu lực**: phân biệt từng tình huống bằng nhãn và lý do.
- **Vàng — Chưa xác định hạn chế / Kiểm tra chưa thành công**: chưa đủ thông tin để kết luận, lỗi mạng/worker không bị biến thành tài khoản chết hoặc tự cho là an toàn.
- **Xám — Chưa kiểm tra spam**.

Nhãn do người dùng tự đánh dấu đóng băng vẫn ghi rõ chưa phải kết luận tự động của Telegram. Thời gian check, tình trạng session, FloodWait, tiến độ và lỗi thao tác vẫn hiển thị ở dòng SS.

Dữ liệu cũ có đoạn “Your account was blocked for violations of the Telegram Terms of Service…” cũng được trình bày thành nhãn đỏ ngay, kể cả khi kết quả cũ đang là unknown. Những lần check mới nhận đúng câu này được ghi thành trạng thái limited để lọc Bị spam. Với dữ liệu cũ, check lại để cập nhật trạng thái lưu/bộ đếm/bộ lọc.

Cửa sổ **Thao tác → SpamBot / kháng nghị** vẫn có hội thoại thật để đọc câu hỏi và trả lời đúng bước khi cần; nguyên văn không hiển thị trên bảng danh sách.
