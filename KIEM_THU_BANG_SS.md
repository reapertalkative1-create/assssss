# Kiểm thử thông tin trên bảng SS — 11/11/2026

- Python: **67 passed, 48 deselected** trong test_account_rows, test_accounts_api, test_account_bulk, test_spambot, với marker `not integration and not telegram_live`.
- Frontend: **56 passed**, 6 tệp; TypeScript/Vite production build thành công.
- API list/detail trả phản hồi bot cho admin, không trả nội dung riêng/tokens/payload cho operator. Không lộ khóa/session/API hash.
- Truy vấn hoạt động gộp theo trang, giới hạn lịch sử từng SS; thao tác chờ duyệt cũ được ưu tiên trước kết quả hoàn tất mới. Không tải từng tác vụ riêng cho từng dòng.
- Lệnh worker đã gắn với thao tác hàng loạt không xuất hiện lặp; lỗi một phần SpamBot trong lệnh done vẫn hiện thất bại ở kết quả dòng.
- Frontend hiển thị phản hồi, lỗi và tiến độ ngay trên bảng; không còn heading Tác vụ hàng loạt hoặc polling GET /api/account-bulk. Giữ mở bản kháng nghị từ dòng và nút dừng đợt có phạm vi ghi rõ.
- Chromium thật + API/SQLite với dữ liệu giả: nguyên văn bot và lỗi đóng băng hiện trên dòng; tạo check mới rồi thấy trạng thái trên dòng; chuẩn bị nháp, đóng, tải lại và mở lại nháp từ dòng session. Không lỗi JavaScript/HTTP 500. Viewport 390px không tràn ngang toàn trang; bảng rộng cuộn trong khung.

Không dùng session người dùng và không gửi Telegram thật. Browser không chạy worker Telegram; dữ liệu giả dùng cho hiển thị và trạng thái chờ/lỗi worker offline. Không kiểm chứng mọi phản hồi bot, PostgreSQL integration hoặc build sạch Docker Windows trong đợt này. Không thêm dependency/migration. Các báo cáo cũ mô tả giao diện ở thời điểm của bản cũ.

ZIP gồm source, web dist, setup.cmd/run.cmd và tài liệu; loại trừ session, database, .env riêng, khóa và runtime.
