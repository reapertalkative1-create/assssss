# DEVYN FORWARDER — API Telegram lưu một lần trong Cài đặt

[**Tải bản mới: lưu API tự động**](https://github.com/reapertalkative1-create/assssss/raw/refs/heads/main/devyn-forwarder-saved-api-settings.zip)

Giữ **.env.docker và Docker volume**, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để nâng database **0011** và build API/web/worker. Sau đó dùng **run.cmd**.

Vào **Cài đặt → API Telegram**, nhập api_id rồi api_hash. Đủ cặp hợp lệ sẽ tự lưu sau khoảng 0,8 giây; đợi nhãn xanh **Đã lưu**. Thêm tài khoản và Nhập session hàng loạt tự dùng lại, không còn ô API trong cửa sổ nhập. Đóng web hoặc khởi động lại vẫn giữ cấu hình trong database. Hash được mã hóa, không trả lại cho web hay lưu trong localStorage.

Tài khoản cũ giữ API đang dùng; thay mặc định chỉ áp dụng cho SS mới. Có thể tắt SS cũ và chọn **Thao tác → API Telegram → Dùng API đã lưu** để áp dụng lại mà không nhập hash.

Giữ luồng SS + proxy cùng lúc, mỗi SS một proxy trước lần connect đầu; proxy lỗi không tự chạy trực tiếp. Giữ nút đỏ Xóa đã chọn, check/lọc/xuất proxy sống/die và launcher tự chọn cổng.

**Check list proxy:** proxy cần được gán cho SS trước; worker Online. Chọn Thao tác session → Check proxy; chưa tích SS thì Check (N) theo bộ lọc, đã tích thì Áp dụng (N). Xuất proxy → Đang chạy/Die → .txt tải riêng hai nhóm. Chưa có bộ kiểm tra list rời chưa gán.

[Hướng dẫn API và check proxy](HUONG_DAN_LUU_API.md) · [Kiểm thử](KIEM_THU_LUU_API.md) · [Nhập SS + proxy](HUONG_DAN_NHAP_SS_KEM_PROXY.md) · [Windows](HUONG_DAN_WINDOWS.md)

77 kiểm thử Python liên quan, 80 frontend và production build qua. Chromium thật xác nhận tự lưu, giữ API sau khi dừng/khởi động lại tiến trình API và nhập ZIP + proxy không cần hash; worker nhận đúng cặp đã lưu. Telegram/session giả, không gửi Telegram thật. Không chạy PostgreSQL integration hoặc build sạch Docker/Windows ở đợt này.

ZIP gồm source/dist, không chứa session, khóa, .env riêng hoặc database. SHA256: `e0b8be57f0429faf4ccfd625e135afeaf6625f6078ba120c558cce5d67c1d772`.

## Bản trước

- [SS + proxy cùng lúc](devyn-forwarder-session-proxy-import.zip)
- [Xóa trực tiếp + lọc/xuất proxy](devyn-forwarder-proxy-export-delete.zip)
