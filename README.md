# Telegram Forwarder Control Center — quản lý nhiều session

[**Tải ZIP quản lý session bản mới**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/telegram-forwarder-control-center-session-manager.zip)

Giải nén đè vào thư mục cũ, **giữ nguyên .env.docker và Docker volume**, chạy **setup.cmd một lần** để nâng migration 0007 và build API/web/worker. Sau đó dùng **run.cmd**.

## Quản lý trên web

- Bỏ trần tổng 100 session: ZIP đọc từng file và tự chia lô; không cần tự tách gói 100.
- Chọn từng dòng, theo trang hoặc toàn bộ kết quả lọc; có thể bỏ chọn một vài dòng trong toàn bộ.
- Bật/Tắt/Check hàng loạt, đánh dấu hoặc bỏ dấu đóng băng thủ công.
- Lọc Live, Die, lỗi mạng, FloodWait, đóng băng, worker, bật/tắt; tìm tên hoặc username.
- Tác vụ lưu trong database, có tiến độ, lịch sử phân trang, lọc lỗi, thử lại riêng các mục lỗi và dừng xếp hàng. Đóng web không hủy tác vụ.

Không có trần số session toàn catalog; giới hạn từng file/yêu cầu và tài nguyên máy vẫn áp dụng. Check đăng nhập không chứng minh mọi quyền Telegram đều bình thường. Đóng băng chỉ tự ghi khi Telegram trả lỗi FROZEN; nhãn thủ công được ghi rõ.

Xem [hướng dẫn quản lý](HUONG_DAN_QUAN_LY_SESSION.md), [hướng dẫn Windows](HUONG_DAN_WINDOWS.md), [kết quả kiểm thử](KIEM_THU_QUAN_LY_SESSION.md).

Đã thử Chromium: ZIP 205 session giả tự chia 100+100+5 và xác thực đủ; Tắt toàn bộ 251 tài khoản, bỏ/chọn lại từng dòng, lọc Die và giữ tác vụ khi tải lại trang. Chưa thử Telegram thật. ZIP không chứa session người dùng hoặc .env.docker.

SHA256: `44db73c102260b39b5bffd53c43da0aa24b242e35ca4edc1ed41815585beef94`.

## Bản trước

- [Nhập 100 session](telegram-forwarder-control-center-session-import.zip)
- [Đăng nhập/API credentials trên web](telegram-forwarder-control-center-web-login.zip)
- [BOM fix](telegram-forwarder-control-center-windows-autoconnect-bomfix.zip)
- [Tự kết nối worker](telegram-forwarder-control-center-windows-autoconnect.zip)
- [Windows cách ly](telegram-forwarder-control-center-windows-isolated.zip)
- [Khôi phục](telegram-forwarder-control-center-phase6-fixed-v2-recovered.zip)
