# Chọn SS và lọc trạng thái gửi

## Cập nhật bản đang dùng

Giữ nguyên `.env.docker` và Docker volume. Giải nén đè vào đúng thư mục ứng dụng cũ, mở Docker Desktop, chạy **setup.cmd** một lần, rồi **run.cmd**. Trên web bấm **Ctrl+F5**. Không cần tạo lại tài khoản quản trị, worker hay nhập lại SS. Database vẫn ở migration **0014**.

## Chọn tài khoản gửi

1. Mở **Tuyến chuyển tiếp → Gửi bài từ liên kết**, hoặc tích SS trong **Tài khoản Telegram → Gửi bài (N)**.
2. Bấm **Có thể chạy** để xem SS đang có đủ điều kiện đã biết. **Tất cả**, **Live**, **Die** và bộ lọc trạng thái giúp xem các SS khác.
3. Tìm tên, chọn nhóm tài khoản, tích từng SS/chọn cả trang hoặc **Chọn toàn bộ kết quả**. SS lỗi vẫn tích được và lưu vào bản nháp. SS đã chọn được giữ khi đổi trang, nhóm hoặc bộ lọc.
4. Bấm **Chỉ xem đã chọn** để rà lại lựa chọn. Các nhãn được làm mới tự động, kể cả SS không nằm trên trang hiện tại.
5. Chọn **Kiểm tra phiên**, **Check spam / đóng băng** hoặc **Check proxy**, rồi bấm **Kiểm tra SS (N)**. Xem tiến độ và lỗi ngay trong bộ chọn. Kiểm tra spam hỏi @SpamBot, có thể dùng lại kết quả mới trong 10 phút.
6. Dán link bài viết, tải TXT/dán các nhóm được phép đăng, rồi **Lưu đợt gửi**. Màn hình cụm có nút kiểm tra SS, kiểm tra quyền nhóm và bắt đầu các SS đã đạt.

Mỗi nhóm nhận giao cho một SS. Chọn thêm tài khoản không tự gửi; bản nháp cần được kiểm tra và bắt đầu. Tối đa 1.000 SS và 1.000 nhóm nhận mỗi cụm. SS đang xóa không nhận thêm vào lựa chọn; nếu SS bị xóa trước lúc lưu, ứng dụng yêu cầu chọn lại để không tạo bản nháp thiếu dữ liệu.

## Ý nghĩa trạng thái

| Nhãn | Ý nghĩa |
| --- | --- |
| Có thể chạy | Đã xác thực, có session, worker online và chưa ghi nhận lỗi chặn, thời gian chờ hoặc proxy die. Vẫn cần kiểm tra quyền đăng vào nhóm đích. |
| Live | Phiên đăng nhập hoạt động. Tài khoản vẫn có thể đồng thời bị spam/bị chặn; nhãn hạn chế hiển thị riêng. |
| Die / hết phiên | Session không còn đăng nhập hợp lệ. Cần đăng nhập lại hoặc thay session hợp lệ. |
| Bị spam / Bị chặn / Đóng băng | Hạn chế đã ghi nhận từ Telegram hoặc dấu đóng băng thủ công. Kiểm tra lại sau khi vấn đề được giải quyết. |
| Cần kiểm tra lại | Có lỗi kiểm tra, kết nối hoặc proxy. Có thể tích và chạy kiểm tra lại; nếu lỗi tạm thời đã hết thì trạng thái sẽ cập nhật. |
| Worker offline / Chưa xác thực / Đang chờ Telegram | Cần khởi động worker, hoàn tất đăng nhập hoặc chờ hết thời hạn tương ứng. |

Số đếm tính trên toàn bộ kết quả tìm kiếm/nhóm, không chỉ 50 SS của trang hiện tại. Các nhóm trạng thái có thể giao nhau; chẳng hạn một SS vừa Live vừa bị chặn. Việc cho tích SS lỗi không bỏ qua lỗi hết phiên, giới hạn Telegram hay quyền đăng bài. Ứng dụng không tự chuyển phần việc của SS bị hạn chế sang SS khác.

Lựa chọn ở bảng Tài khoản Telegram dùng trong phiên mở web hiện tại; tải lại trang sẽ xóa lựa chọn chưa lưu. Bản nháp và tiến độ đã lưu vẫn ở database.
