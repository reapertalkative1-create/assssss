# Mỗi SS đi hết danh sách nhóm — bản fix3

Phiên bản: `2026.11.18-full-list-fix3`. Database vẫn là `0022`.

## Cách gửi mới

Mỗi SS nhận **toàn bộ danh sách nhóm** đã lưu trong cụm. Ví dụ, 3 SS và 100 nhóm: mỗi SS có 100 nhóm trong một vòng, tổng cộng 300 lượt gửi.

- Mỗi SS chọn thứ tự ngẫu nhiên riêng, xử lý mỗi nhóm một lần trong vòng đó.
- Chỉ khi SS đã xử lý hết danh sách mới bắt đầu vòng tiếp theo, tiếp tục đến khi bạn bấm **Dừng** trên thẻ cụm.
- Nhiều SS có thể cùng dùng danh sách nhóm, nhưng hàng đợi không cấp cùng một nhóm đang được gửi cho SS khác trong cùng cụm. SS chọn nhóm còn trống hoặc chờ nếu mọi lựa chọn còn lại đang bận.
- Khi SS nhiều hơn nhóm, SS phải chờ được luân phiên xử lý; không bị bỏ khỏi lượt chạy hoặc bị gán mãi một nhóm.
- Danh sách nhóm còn lại và tác vụ đã xử lý được lưu trong database. Khởi động lại API/worker không xáo lại vòng đang chạy hoặc gửi lại các nhóm đã hoàn tất trong vòng đó.
- Lỗi một nhóm được ghi lại rồi SS tiếp tục các nhóm khác; các SS còn lại tiếp tục độc lập. Khoảng nghỉ giữa hai lần gửi, FloodWait, quyền gửi của Telegram, hạn chế tài khoản và tình trạng proxy vẫn được giữ.
- Tài khoản bị dừng riêng cần được bật lại sau khi xử lý nguyên nhân. Cụm chỉ tắt vòng lặp khi bạn bấm Dừng.
- Thẻ cụm đếm **lượt gửi theo từng SS**, kèm tên SS trong kết quả; không gộp kết quả của nhiều SS vào cùng một nhóm.

Danh sách được chuẩn hóa theo tên nhóm/link/ID đã nhập. Hãy dùng một định danh duy nhất cho mỗi nhóm, tránh nhập cùng một nhóm vừa bằng username vừa bằng ID/link mời khác. Mỗi cụm kiểm soát nhóm đang bận trong phạm vi của cụm đó.

Bản fix2 đã chia nhóm cố định giữa các SS. Bản fix3 sửa chính cách phân phối này. Cụm gửi tin nhắn và chức năng tạo đợt gửi một lần trong Lịch sử vẫn là luồng riêng.

## Cập nhật từ bản cũ

1. Bấm **Dừng** cụm đang chạy. Sao lưu ứng dụng/database theo cách bạn đang dùng.
2. Giải nén ZIP đè vào đúng thư mục cũ. Giữ `.env.docker`, `.docker-ready`, cấu hình worker, session và Docker volume; giữ `.env` nếu có cấu hình riêng.
3. Bật Docker Desktop rồi chạy `run.cmd` để build lại container. Nếu worker chạy riêng, cập nhật và khởi động lại worker theo cách triển khai hiện tại.
4. Nhấn **Ctrl+F5** và kiểm tra phiên bản `2026.11.18-full-list-fix3`.
5. Bấm **Chạy** trên thẻ cụm để tạo phiên mới. Không bấm Thử lại hàng loạt tác vụ cũ: phiên cũ giữ nguyên lịch sử và cách chia nhóm cũ.

Không cần tạo lại SS, nhập lại session hoặc xóa database. Cài mới: chạy `setup.cmd` trước `run.cmd`.

Bấm **Dừng** hủy công việc chưa bắt đầu và ngăn vòng tiếp theo. Tin đã bắt đầu gửi tới Telegram có thể hoàn tất.

## Kiểm thử

Kiểm thử tự động dùng tài khoản/worker giả: mỗi SS đi hết danh sách qua nhiều vòng; khởi động lại giữa vòng; SS nhiều hơn nhóm; hai worker cùng xin nhóm; lỗi nhóm, FloodWait và Dừng. Không gửi bài tới Telegram thật. Docker/Windows và PostgreSQL thật chưa được chạy trong môi trường kiểm thử này.
