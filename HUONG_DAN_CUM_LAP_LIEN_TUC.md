# Sửa admin_required và chạy cụm chuyển tiếp liên tục

Phiên bản: `2026.11.17-cluster-loop-fix2`. Database vẫn là `0022`; không cần xóa hoặc tạo lại dữ liệu.

## Cập nhật

1. Bấm **Dừng** các cụm đang chạy trên bản cũ. Sao lưu thư mục ứng dụng và database theo cách bạn đang dùng.
2. Giải nén ZIP này đè vào đúng thư mục ứng dụng cũ. Giữ nguyên `.env.docker`, `.docker-ready`, cấu hình worker, session và các Docker volume; giữ cả `.env` nếu bạn có cấu hình riêng.
3. Bật Docker Desktop và chạy `run.cmd` để build lại container bằng mã mới. Worker chạy riêng cũng cần được cập nhật/khởi động lại theo cách triển khai hiện tại.
4. Nhấn **Ctrl+F5**, kiểm tra phiên bản mới rồi mở **Cụm chuyển tiếp** và bấm **Chạy** trên thẻ cụm.
5. Bấm **Dừng** trên thẻ khi muốn kết thúc. Tin đã bắt đầu gửi tới Telegram có thể hoàn tất; tác vụ chưa bắt đầu sẽ không được gửi tiếp.

Nếu cài mới, chạy `setup.cmd` thành công trước rồi chạy `run.cmd`.

## Hành vi mới

- Không ép thành viên thường phải là admin để chuyển tiếp. Telegram vẫn kiểm tra quyền gửi thực tế; nhóm/kênh cấm gửi hoặc bài cấm chuyển tiếp vẫn có thể trả lỗi.
- Nhóm được chuẩn hóa, chia thành các danh sách không trùng giữa những SS đã chọn. Các nhóm đã được gán cho SS từ trước giữ nguyên SS phụ trách; nhóm mới được chia ngẫu nhiên, cân bằng. Mỗi SS gửi từng nhóm một, xáo trộn thứ tự khi tạo mỗi vòng.
- Nếu số SS lớn hơn số nhóm, SS dư sẽ chờ, không cùng gửi vào một nhóm. Không chuyển nhóm của SS đang lỗi sang SS khác.
- Nút **Chạy trên thẻ cụm** bật vòng lặp liên tục. Hết danh sách riêng, SS tạo vòng tiếp theo và tiếp tục gửi lại bài đã lưu cho đến khi bấm **Dừng**. Khoảng nghỉ cấu hình áp dụng cả giữa hai vòng.
- Lỗi ở một nhóm được ghi lại; SS tiếp tục nhóm khác rồi thử trong vòng kế tiếp. Kết quả gửi chưa xác định không bị thử lại ngay trong cùng tác vụ, nhưng vòng tiếp theo vẫn là một lần gửi mới theo chế độ lặp.
- Một SS gặp lỗi không dừng các SS còn lại. Cụm vẫn bật khi mọi SS đang chờ; SS lỗi lúc khởi chạy được kiểm tra lại sau khoảng 30 giây. FloodWait, giới hạn gửi, phiên đăng nhập hỏng, tài khoản bị hạn chế và proxy lỗi vẫn được tôn trọng. Khi SS đã bị dừng riêng, cần bật lại SS sau khi xử lý nguyên nhân.
- Trạng thái vòng được lưu trong database. Sau khi API/worker khởi động lại, cụm đang bật tiếp tục từ hàng đợi đã lưu; bấm Chạy nhiều lần không tạo thêm phiên chạy song song.
- Lượt cũ và lỗi `admin_required` cũ vẫn còn trong lịch sử. Bấm **Dừng**, rồi **Chạy** trên thẻ tạo phiên mới dùng bản sửa; không cần xóa database hoặc thử lại hàng loạt tác vụ cũ.

Chức năng tạo lượt gửi một lần trong Lịch sử và API `/runs` vẫn giữ cơ chế chống gửi trùng. Chế độ lặp mới áp dụng cho nút Chạy/Dừng trên thẻ **cụm chuyển tiếp**. Cụm gửi tin nhắn là luồng riêng.

## Kiểm chứng

Có kiểm thử tự động cho thành viên không phải admin, nhiều vòng liên tiếp, nhóm riêng của từng SS, lỗi quyền gửi, FloodWait, khôi phục worker, khởi động lại scheduler, khoảng nghỉ, bấm Chạy lặp và Dừng trước khi gửi. Dùng worker giả, không gửi tới Telegram thật. Docker/Windows và PostgreSQL thật chưa được chạy trong môi trường kiểm thử này.
