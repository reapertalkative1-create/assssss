> Có thêm nút **Kiểm tra list proxy** để nhập/check/xuất list rời, không cần gán vào SS. Hai nút xuất nằm ngay trong cửa sổ đó. Menu Xuất proxy mô tả bên dưới vẫn áp dụng cho proxy đã gán vào SS. [Hướng dẫn mới](HUONG_DAN_CHECK_LIST_PROXY.md).

# Lọc và xuất proxy sống / die

Giữ `.env.docker` và Docker volume, giải nén đè đúng thư mục cũ rồi chạy **setup.cmd một lần** để cập nhật API/web. Sau đó dùng **run.cmd**. Không thêm migration, head vẫn **0010**.

## Check, lọc, xuất

1. Trong bảng SS, bấm **Check proxy** tại dòng; hoặc chọn Check proxy trong **Thao tác session** rồi check theo bộ lọc/áp dụng cho SS đã tích.
2. Đợi kết quả: xanh = lần check thành công, đỏ = lần check thất bại, trắng = chưa đủ kết quả.
3. Dùng bộ lọc **Mọi proxy → Proxy đang chạy / Proxy die / Proxy chưa check / Proxy đang check**.
4. Bấm **Xuất proxy**:
   - **Đang chạy → .txt** tải `proxies-live.txt`.
   - **Die → .txt** tải `proxies-die.txt`.

Xuất proxy đã gán cho SS, theo kết quả check lưu trên máy chủ. Chưa check/đang check không được đưa vào hai file sống/die. Không có kết quả trong nhóm sẽ hiện thông báo thay vì tải file rỗng.

File xuất lấy mọi SS khớp bộ lọc tên/worker/xác thực/spam/tình trạng/bật tắt hiện tại, kể cả ngoài trang đang xem; không phụ thuộc SS đã tích. Nhóm sống/die được chọn bằng nút xuất, thay cho bộ lọc proxy đang chọn. Ví dụ đang xem sống vẫn có thể tải file die của cùng bộ lọc SS. Proxy của SS đang chờ xóa không được xuất.

Mỗi dòng là URL có scheme, ví dụ `socks5://user:password@host:port` hoặc `http://host:port`, có percent encoding cho ký tự đặc biệt và hỗ trợ IPv6. Có thể nhập lại file bằng chức năng Nhập proxy. File giữ username/password nếu proxy có, chỉ quản trị viên được tải; bảng SS và audit không hiện credential. Giải mã lỗi sẽ báo lỗi, không tải file dở.

## Nút xóa

**Xóa đã chọn** là nút đỏ riêng ngay trên thanh điều khiển, không nằm trong menu. Khi có SS, nút luôn thấy; tích SS để bật nút rồi bấm xóa trực tiếp. Không nhập tên/xác nhận thêm. Chọn cả N rồi bỏ tích một số dòng vẫn giữ đúng các dòng loại trừ. Khi chưa tích SS hoặc đang gửi thao tác, nút bị khóa.

Giữ giao diện gọn, proxy từng SS, bộ lọc blocked/frozen và tự chọn cổng web.
