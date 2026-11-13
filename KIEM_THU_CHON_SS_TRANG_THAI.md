# Kiểm thử bộ chọn SS — 14/11/2026

- SQLite: **22** kiểm thử trạng thái/bộ chọn/gửi bài đạt.
- PostgreSQL 16: **19** kiểm thử tương ứng đạt, dùng database và role riêng; đã xóa sau kiểm thử.
- Frontend: **109** kiểm thử đạt; TypeScript và Vite production build đạt.
- Quy mô 240 SS trên 5 trang: 80 bị chặn, 40 Die, 40 đóng băng, 40 lỗi và 40 sẵn sàng; số đếm/lọc theo nhóm và tìm kiếm đúng. Chọn toàn bộ vượt trang đầu, loại trừ SS, chọn lỗi và lưu nháp đều được kiểm tra.
- Kiểm tra điều kiện worker online, session tồn tại, proxy die, FloodWait, trạng thái NULL cũ, tài khoản đang xóa và yêu cầu sai. Giữ các chốt kiểm tra thực tế trước gửi.
- Chromium + API/worker thật với FakeBackend: chọn cả 4 SS lỗi kết nối/bị chặn/Die/sẵn sàng qua nhiều bộ lọc, giữ đủ 4 trong bản nháp. Chạy kiểm tra lại SS lỗi kết nối, chuyển về sẵn sàng, kiểm tra quyền nhóm và gửi giả lập thành công hai nhóm.
- Không lỗi JavaScript hoặc HTTP 500 trong luồng trình duyệt. Kiểm tra desktop 1600px và mobile 390px không tràn ngang.
- Kiểm thử frontend bao gồm chạy kiểm tra lần thứ hai sau khi tác vụ đầu hoàn tất, chọn qua bộ lọc, số đếm toàn bộ kết quả và lựa chọn từ bảng tài khoản.

Session và backend kiểm thử đều giả lập; không kết nối hoặc gửi Telegram thật. Chưa kiểm thử trực tiếp Docker Desktop trên Windows. Launcher và migration 0014 được giữ nguyên. ZIP loại dữ liệu, session, mật khẩu và khóa riêng của người dùng.
