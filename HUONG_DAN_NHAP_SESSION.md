> API chuyển sang **Cài đặt → API Telegram**, nhập một lần rồi tự dùng lại. Cập nhật bằng setup.cmd (head **0011**), giữ .env.docker/volume. [Hướng dẫn](HUONG_DAN_LUU_API.md).

> Nhập SS kèm proxy ngay cùng cửa sổ, lưu proxy trước lần check đầu tiên. [Hướng dẫn](HUONG_DAN_NHAP_SS_KEM_PROXY.md). Bản hiện tại giữ migration head 0010. Ghi chú migration bên dưới mô tả bản cũ.

# Nhập và quản lý nhiều session

Bản mới không có trần tổng 100 session; web tự đọc ZIP và chia lô. Xem [HUONG_DAN_QUAN_LY_SESSION.md](HUONG_DAN_QUAN_LY_SESSION.md) để cập nhật và sử dụng. Giữ .env.docker và volume, chạy setup.cmd một lần để nâng migration 0008, sau đó run.cmd.
