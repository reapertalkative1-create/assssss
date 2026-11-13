# Sửa nhập SS vào nhóm và đổi nhóm

Bản 13/11/2026. Nguyên nhân: bộ lọc nhóm trước đây chỉ lọc bảng; yêu cầu nhập SS và tạo tài khoản không gửi/lưu nhóm. Bản này lưu nhóm cùng giao dịch với SS, trước khi worker kiểm tra phiên.

## Nhập SS mới đúng nhóm

1. Chọn nhóm ở bộ lọc **Lọc nhóm tài khoản**, rồi bấm **Nhập session**.
2. Cửa sổ có ô **Nhóm tài khoản** tự chọn theo nhóm đang lọc. Có thể đổi trước khi nhập.
3. Chọn SS/ZIP và proxy như trước, bấm **Nhập và kiểm tra session**. Mỗi lô đều giữ nhóm đã chọn; SS xuất hiện trong nhóm ngay khi API nhận, không phải chờ check Telegram.

Hoặc mở **Nhóm tài khoản → Nhập SS mới** ngay cạnh nhóm cần nhập. **Thêm tài khoản** cũng có ô nhóm, mặc định theo bộ lọc hiện tại.

SS đã nhập trước đó: chọn nhóm rồi nhập lại file sẽ chuyển SS trùng vào nhóm đó, giữ nguyên session và proxy cũ, không tạo bản sao hoặc check lại. Nếu không chọn nhóm, nhập trùng giữ nguyên nhóm hiện có. Nhóm bị xóa trước lúc nhập sẽ báo lỗi để chọn lại, không âm thầm đưa SS vào Chưa có nhóm.

## Chuyển SS đang có

- Từng SS: nút **Đổi nhóm** ngay cạnh nhãn nhóm trên dòng SS → chọn nhóm đích → **Lưu nhóm**.
- Nhiều SS: tích các dòng hoặc chọn toàn bộ kết quả lọc → **Đổi nhóm (N)** → chọn nhóm đích → **Lưu nhóm**. Các dòng đã bỏ tích được loại khỏi thao tác.
- Trong nhóm: **Xem SS** → tích từng SS / **Chọn trang** → chọn nhóm đích → **Chuyển (N)**. Có thể tích qua nhiều trang.
- **Bỏ khỏi nhóm** chuyển về Chưa có nhóm, giữ SS/proxy. Có nút Bỏ chọn, tìm kiếm và phân trang.
- Giữ các chức năng tạo/đổi tên/xóa nhóm. Mỗi SS một nhóm; xóa nhóm giữ tài khoản.

Các SS bị nhập sai nhóm ở bản cũ không thể tự đoán nhóm đích. Lọc **Chưa có nhóm**, tích SS rồi dùng **Đổi nhóm (N)** để sắp xếp lại; không cần nhập lại file.

## Cập nhật Windows

Giải nén đè vào đúng thư mục đang dùng; giữ `.env.docker` và Docker volume. Mở Docker Desktop, chạy **setup.cmd** một lần để build API/web/worker rồi **run.cmd**. Làm mới trình duyệt bằng Ctrl+F5. Không tạo một thư mục cài đặt mới hoặc xóa dữ liệu cũ. Database vẫn migration 0014.
