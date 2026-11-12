# Lưu API Telegram trong Cài đặt

## Cập nhật

Giữ `.env.docker` và Docker volume. Giải nén đè ZIP vào **đúng thư mục cũ**, mở Docker Desktop rồi chạy **setup.cmd một lần** để nâng database lên **0012** và build API/web/worker. Những lần sau dùng **run.cmd**. Không tạo thư mục cài mới nếu muốn giữ dữ liệu cũ.

## Nhập một lần

1. Vào **Cài đặt → API Telegram** bằng tài khoản quản trị.
2. Nhập `api_id`, sau đó `api_hash` lấy tại my.telegram.org → API development tools.
3. Sau khi đủ cặp hợp lệ, ứng dụng tự lưu sau khoảng 0,8 giây. Đợi nhãn xanh **Đã lưu** trước khi rời trang. Nếu lỗi sẽ báo **Chưa lưu được** và có **Thử lưu lại**.
4. Những lần sau thêm tài khoản hoặc **Nhập session hàng loạt** sẽ dùng API đã lưu. Không còn ô nhập API ở các cửa sổ này.

Cấu hình nằm trong database của ứng dụng, được mã hóa bằng khóa phiên Telegram; không lưu hash trong localStorage/trình duyệt. Đóng web, đổi trình duyệt hoặc khởi động lại vẫn còn nếu giữ database và khóa trong `.env.docker`. `api_hash` không được trả lại cho web; ô trống sau lưu là chủ đích, không phải mất cấu hình. Trang Cài đặt vẫn hiện `api_id` và trạng thái Đã lưu. Muốn thay đổi, nhập đủ cặp mới.

Nếu chưa lưu API, cửa sổ nhập SS/thêm tài khoản có liên kết tới Cài đặt và chưa cho nhập. Lưu cấu hình chỉ kiểm tra định dạng; Telegram sẽ kiểm tra API khi worker xác thực session/đăng nhập.

## Tài khoản đã có

API mới tự dùng cho các tài khoản/SS được thêm sau khi lưu. Mỗi tài khoản giữ bản cấu hình riêng đã mã hóa; đổi API trong Cài đặt không tự sửa API của các SS cũ hoặc SS đang chạy. Muốn áp dụng API đã lưu cho một SS cũ: tắt SS, mở **Thao tác → API Telegram → Dùng API đã lưu**. Không phải nhập lại hash. Trạng thái đang đăng nhập/đang chạy vẫn được bảo vệ như trước.

Giữ luồng **SS + proxy cùng lúc**, mỗi SS một proxy trước lần kết nối đầu tiên; proxy lỗi không tự chuyển sang kết nối trực tiếp. Nút đỏ Xóa đã chọn và launcher tự chọn cổng giữ nguyên.

## Check list proxy

Dùng nút riêng **Kiểm tra list proxy** ở đầu trang để tải TXT/dán list, check và xuất Live/Die độc lập, không cần SS hoặc API. [Hướng dẫn](HUONG_DAN_CHECK_LIST_PROXY.md). Cách check proxy đã gán cho SS vẫn giữ bên dưới. Trong **Nhập proxy**, dán list/tải TXT và gán cho SS đã tích hoặc tất cả SS theo bộ lọc; nếu nhập SS kèm proxy thì đã gán sẵn. Worker cần Online (chạy run.cmd).

Chọn **Thao tác session → Check proxy**: chưa tích SS thì bấm **Check (N)** theo bộ lọc; đã tích thì bấm **Áp dụng (N)**. Xanh = check thành công, đỏ = check thất bại, trắng = chưa check. **Xuất proxy → Đang chạy → .txt** hoặc **Die → .txt** tải hai nhóm riêng.
