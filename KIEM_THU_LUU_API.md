# Kiểm thử lưu API Telegram — 12/11/2026

- **77 kiểm thử Python qua**, gồm 31 kiểm thử saved_telegram_api / telegram_api_web / session_import / session_proxy_import / migrations và 46 kiểm thử accounts_api / account_proxy / proxy_export / proxy_worker. Tổng 58 lượt integration được loại bởi marker not integration and not telegram_live.
- **80 kiểm thử frontend qua**, 8 tệp. TypeScript/Vite production build thành công.
- Migration 0011 thêm bảng application_settings; upgrade schema khớp models, downgrade sạch; nâng từ 0010 giữ API đã mã hóa và proxy của SS cũ.
- API Settings chỉ admin, ghi cần CSRF, cặp đầy đủ và định dạng hợp lệ. Hash mã hóa trong database, không xuất hiện ở response status/save/audit. Client chỉ đọc configured/api_id/updated_at. API instances mới đọc lại được cấu hình.
- Thiếu/hỏng cấu hình báo lỗi và không nhập SS. Import không gửi API trong request lấy cặp đã lưu; thêm tài khoản cũng vậy. Đổi mặc định không thay snapshot SS cũ; thao tác áp dụng cho từng SS dùng cấu hình đã lưu. Giữ tương thích client cũ gửi cặp API rõ ràng.
- Verify/rotate keys bao gồm cấu hình mặc định; verify-keys trả mã lỗi nếu không giải mã được setting. Snapshot tài khoản vẫn được kiểm tra/rotate như trước.
- Frontend tự lưu sau khi đủ cặp hợp lệ, xóa hash khỏi ô khi thành công, mở lại giữ trạng thái Đã lưu; không ghi hash vào localStorage. Chỉnh api_id đơn lẻ chưa bị coi là đã lưu. Có thông báo lỗi/thử lại, không cần gõ lại cặp sau lỗi lưu.
- Cửa sổ thêm tài khoản/nhập SS không còn input API hoặc hash trong request; chưa cấu hình thì khóa nút và liên kết tới Cài đặt. Giữ TXT/dán proxy, ghép đúng qua lô 100 + 1 và thông báo lỗi lô không bị polling xóa.
- Chromium thật: tự lưu trong Cài đặt, hash được xóa, không có hash trong localStorage; panel vừa desktop 1365px và mobile 390px. Sau đó dừng/khởi động lại tiến trình API bằng cùng database/khóa: Cài đặt vẫn hiện API ID và Đã lưu; nhập ZIP 3 SS giả + proxy TXT không cần nhập lại API; request không chứa api_id/hash. Worker thật lấy đúng cặp API đã lưu và proxy riêng trước lần connect đầu, cả 3 xác thực/check SpamBot giả thành công. Không lỗi JS/HTTP 500.

Chỉ Telegram dùng FakeBackend/session tổng hợp; không sử dụng session người dùng hay kết nối Telegram thật. Không chạy PostgreSQL integration hoặc build sạch Docker/Windows ở đợt này. Không thêm dependency. ZIP gồm source/dist, loại trừ session, .env riêng, khóa, database và runtime.
