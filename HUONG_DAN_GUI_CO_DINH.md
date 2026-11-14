# Gửi bài với SS cố định và lịch sử chống trùng

## Cập nhật

Giữ `.env.docker` và Docker volume, giải nén đè đúng thư mục đang dùng. Mở Docker Desktop, chạy **setup.cmd** một lần, sau đó **run.cmd**, bấm **Ctrl+F5** trên web.

Setup build bản mới, dừng worker để hoàn tất tác vụ đang xử lý, dừng API/web rồi nâng database lên **0015**. Sau đó ứng dụng và worker tự kết nối lại. Session, proxy, API Telegram và tài khoản quản trị được giữ nguyên. Lịch sử gửi hiện có được đưa vào cơ chế chống trùng. Không xóa volume khi cập nhật.

## Cách dùng

1. Vào **Tuyến chuyển tiếp → Gửi bài từ liên kết**. Chọn SS hoặc nhóm SS từ **Tài khoản Telegram**.
2. Dán link bài viết, tải TXT/dán các nhóm được phép đăng, đặt khoảng nghỉ giữa các nhóm.
3. **Lưu đợt gửi** để xem phân công. Chọn 1.000 SS cho 200 nhóm mới chỉ phân công tối đa 200 SS; SS dư không nhận tác vụ gửi.
4. Trong **Cụm tài khoản gửi**, bấm **Kiểm tra tất cả**, sau đó **Bắt đầu SS đã đạt**. Việc lưu nháp hoặc kiểm tra quyền không gửi bài.
5. Xem **Chi tiết SS → Tiến độ từng nhóm** để theo dõi thành công, lỗi và thời gian chờ.

Các nguyên tắc dưới đây được bật sẵn, không cần nhập thêm cấu hình.

| Trường hợp | Tool xử lý |
| --- | --- |
| Nhóm chưa có phân công | Chia cho SS đã chọn; ghi nhớ SS phụ trách khi bắt đầu đợt đầu tiên đã kiểm tra quyền. |
| Nhóm đã có SS phụ trách | Giữ SS đó giữa các đợt, kể cả đổi tên SS hoặc đổi thứ tự danh sách. Nếu chưa chọn SS phụ trách, báo tên SS cần chọn. |
| SS bị hạn chế, đóng băng, hết phiên hoặc proxy die | Giữ nguyên phân công và dừng cấp việc; không tự chuyển sang SS khác. |
| Bài đã có trong đợt trước | Bỏ qua nhóm đó; hiển thị số lượng bỏ qua. Dùng ID nguồn, ID bài và ID nhóm Telegram, không phụ thuộc cách viết link hay forward/copy. |
| FloodWait | Chờ theo số giây Telegram trả về, kể cả nhiều ngày. Áp dụng cho toàn SS; không chuyển phần việc sang tài khoản khác. |
| Nhóm cấm gửi | Ghi lỗi cho tác vụ của nhóm, không tự lặp lại lỗi quyền gửi. |
| Proxy đang lỗi | Dừng gửi, giữ proxy đã gán. Kiểm tra hoặc sửa proxy rồi tiếp tục; không tự kết nối trực tiếp thay proxy. |
| Mất kết nối lúc chưa rõ đã gửi hay chưa | Tạm dừng đợt, báo **Cần đối chiếu kết quả**, không tự gửi lại. |

**Live không đồng nghĩa có quyền đăng ở mọi nhóm.** Bộ lọc Có thể chạy dựa trên trạng thái hiện có; vẫn cần kiểm tra nhóm trước khi bắt đầu. Nếu SS phụ trách đang lỗi, chọn SS đó để kiểm tra/sửa lỗi; bộ chọn vẫn cho tích SS lỗi. SS khác không tự nhận phần việc này.

## Khi cần đối chiếu kết quả

Mở trực tiếp nhóm Telegram để kiểm tra bài. Trong **Tiến độ từng nhóm**:

- **Đã gửi:** ghi nhận hoàn tất, không gửi thêm.
- **Chưa gửi · thử lại:** chỉ dùng sau khi xác định bài chưa được gửi. Tác vụ trở về hàng chờ trên SS cũ; đợt vẫn tạm dừng cho đến khi bấm Tiếp tục.

Nút thử lại thông thường và thử lại hàng loạt không bỏ qua bước này. Ghi nhận nhầm “Chưa gửi” có thể làm bài được gửi thêm lần nữa. Nếu không muốn tiếp tục, có thể hủy tác vụ ở hàng đợi; lịch sử chống trùng vẫn được giữ.

## Phạm vi và dữ liệu

- Áp dụng phân công cố định/chống trùng giữa các đợt cho **Gửi bài từ liên kết**. Tuyến **Theo dõi nguồn** cũ giữ cơ chế riêng.
- Lịch sử chống trùng vẫn còn khi xóa đợt, tác vụ hoặc SS. Tạo bản mới không phải cách gửi lại cùng bài vào cùng nhóm. Xử lý lỗi trên tác vụ gốc nếu còn tồn tại và đủ điều kiện thử lại.
- Xóa SS sẽ xóa phân công gắn với SS đó; không tự xóa lịch sử chống trùng. Tool không tự xóa SS hay thay tài khoản khi bị hạn chế.
- Proxy/session không tự xoay. Mỗi session chỉ có một worker giữ lease tại một thời điểm.
- Chỉ đăng nội dung được các nhóm chấp nhận. Các cơ chế này giảm gửi trùng và tuân thủ thời gian chờ; không bảo đảm tài khoản không bao giờ bị Telegram hạn chế.
