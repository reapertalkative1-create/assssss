# Hiện nhóm lỗi và tự lưu tạm

Giữ `.env.docker` và Docker volume, giải nén đè đúng thư mục cũ, chạy **setup.cmd** một lần rồi **run.cmd**, nhấn **Ctrl+F5** trên web. Database vẫn **0015**.

## Nhóm nào bị lỗi

Trong **Gửi bài từ liên kết**, tải TXT hoặc dán danh sách rồi bấm **Kiểm tra danh sách**. Tool chỉ kiểm tra định dạng, không kết nối Telegram và không gửi bài.

Nếu sai định dạng, thông báo hiện ngay nội dung đã nhập — tên hoặc link — cùng số dòng. Ví dụ **Dòng 81: Nhóm lỗi cần sửa**. Bấm **Sửa dòng 81** để chọn đúng dòng đó trong ô nhập, rồi sửa/dán giá trị đúng. Các dòng còn lại giữ nguyên.

Danh sách hiển thị nhiều dòng lỗi cùng lúc, tối đa 100 dòng đầu tiên. Dòng dài được rút gọn trong thông báo, còn nội dung đầy đủ vẫn nằm trong ô nhập và bản tạm. Dòng trống và dòng bắt đầu bằng `#` vẫn được tính khi báo số dòng để khớp file gốc.

**Lưu đợt gửi** cũng trả về danh sách lỗi này; nếu còn dòng lỗi thì không tạo đợt dở dang. Link đúng định dạng chưa khẳng định nhóm tồn tại hay SS có quyền gửi; bước **Kiểm tra nhóm/Kiểm tra tất cả** sau khi lưu nháp vẫn cần thiết. Với dòng sai định dạng, tên hiển thị là nội dung bạn đã nhập, chưa phải tên lấy từ Telegram.

## Tự lưu tạm

Tool tự lưu link bài, danh sách nhóm (kể cả dòng đang sai), các SS đã chọn, thời gian nghỉ và chế độ gửi. Đóng cửa sổ, chuyển sang trang khác để sao chép thông tin, tải lại web hoặc mở lại trình duyệt rồi quay về biểu mẫu sẽ khôi phục bản tạm.

- **Lưu tạm:** lưu ngay vào trình duyệt, không tạo đợt gửi và không gửi Telegram.
- **Xóa bản tạm:** bỏ nội dung tạm. Với biểu mẫu sửa/nhân bản, quay về dữ liệu gốc của đợt đang mở.
- Lưu đợt thành công: bỏ bản tạm trên trình duyệt; bản nháp trên máy chủ vẫn nằm ở danh sách tuyến/cụm gửi.
- Lưu đợt thất bại: giữ bản tạm để sửa hoặc thử lại. Thử lại nội dung không đổi sau khi tải lại giữ mã yêu cầu cũ để tránh tạo bản nháp lặp khi phản hồi trước bị mất.

Bản tạm giữ **7 ngày từ lần lưu cuối**, theo tài khoản đăng nhập và biểu mẫu tạo/sửa/nhân bản. Chỉ lưu trong **cùng trình duyệt và cùng địa chỉ web**; không đồng bộ sang máy, trình duyệt hoặc cổng web khác. Không lưu session Telegram, API hash, mật khẩu hay thông tin proxy. Khi trình duyệt chặn/hết dung lượng lưu trữ, tool báo lỗi; giữ cửa sổ mở hoặc sao chép nội dung trước khi rời trang.
