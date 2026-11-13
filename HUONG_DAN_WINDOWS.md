> Bản hiện tại sửa hiển thị và thêm SS trực tiếp trong nhóm. Giữ `.env.docker`/volume, chạy **setup.cmd** một lần rồi **run.cmd**. [Hướng dẫn](HUONG_DAN_SUA_NHOM_SS.md). Các ghi chú dưới đây là lịch sử.

> Bản hiện tại thêm nhóm tài khoản và danh sách nhóm Telegram. Giữ `.env.docker`/volume, chạy **setup.cmd** một lần để nâng database **0014**, rồi **run.cmd**. [Hướng dẫn](HUONG_DAN_NHOM_TELEGRAM.md). Các ghi chú dưới đây là lịch sử.

> Biểu mẫu gửi bài hiện tự đặt tên và không có ô lịch. Giữ `.env.docker`/volume và chạy **setup.cmd** một lần để cập nhật. [Hướng dẫn](HUONG_DAN_GUI_BAI_TU_LINK.md).

> Bản hiện tại: **Gửi bài từ liên kết + TXT nhóm**, migration **0013**. Giữ `.env.docker`/volume, chạy **setup.cmd một lần**, sau đó **run.cmd**. [Hướng dẫn gửi bài](HUONG_DAN_GUI_BAI_TU_LINK.md). Các ghi chú cập nhật bên dưới là lịch sử.

> Bản mới hiển thị thời hạn hạn chế trên dòng SS. Giữ .env.docker/volume, chạy setup.cmd một lần để build API/web/worker; head vẫn **0012**. [Hướng dẫn](HUONG_DAN_THOI_HAN_SS.md).

> Bản mới có nút **Kiểm tra list proxy** độc lập. Giữ .env.docker/volume, chạy setup.cmd một lần để nâng database **0012** và build; sau đó run.cmd. [Hướng dẫn](HUONG_DAN_CHECK_LIST_PROXY.md).

> Bản mới lưu API một lần tại Cài đặt, tự dùng cho SS mới. Giữ .env.docker/volume, chạy setup.cmd một lần để nâng database **0011** và build; sau đó run.cmd. [Hướng dẫn](HUONG_DAN_LUU_API.md). Ghi chú phiên bản cũ nằm bên dưới.

> Nhập SS kèm proxy ngay cùng cửa sổ: giữ .env.docker/volume, chạy setup.cmd một lần để cập nhật API/web/worker; head vẫn 0010. [Hướng dẫn](HUONG_DAN_NHAP_SS_KEM_PROXY.md).

> Cập nhật nút xóa và lọc/xuất proxy: giữ .env.docker/volume, chạy setup.cmd một lần để build API/web; head vẫn 0010. [Hướng dẫn](HUONG_DAN_XUAT_PROXY.md).

> Giao diện điều khiển mới: Lọc thêm + menu Thao tác session. Giữ .env.docker/volume và chạy setup.cmd một lần để cập nhật giao diện; head vẫn 0010. [Hướng dẫn](HUONG_DAN_THANH_DIEU_KHIEN_GON.md).

> Cập nhật ô thống kê gọn: chạy setup.cmd một lần để build API/web/worker, giữ .env.docker và volume; head vẫn 0010. [Hướng dẫn](HUONG_DAN_O_THONG_KE_GON.md).

> Bản proxy mới cần setup.cmd một lần để nâng database lên 0010 và cài thư viện proxy cho worker. Giữ .env.docker và volume. [Hướng dẫn proxy](HUONG_DAN_PROXY.md).

# Chạy riêng trên Windows: setup.cmd và run.cmd

## Cách dùng

1. Cài **Docker Desktop cho Windows** từ https://www.docker.com/products/docker-desktop/ nếu máy chưa có. Dùng chế độ **Linux containers** và mở Docker Desktop, đợi engine chạy. Không cần cài Python, Node.js hay PostgreSQL trên Windows.
2. Giải nén toàn bộ ZIP vào một thư mục riêng, ví dụ `Documents\TelegramForwarder` trong thư mục người dùng. Không chạy CMD ngay bên trong ZIP.
3. Bấm đúp **setup.cmd** một lần. Script tải image, tạo database, hỏi tên/mật khẩu quản trị và tự tạo/lưu worker cho máy này. Mật khẩu tối thiểu 12 ký tự, không chứa tên đăng nhập. Không có mật khẩu mặc định.
4. Khi hoàn tất, trình duyệt mở địa chỉ được in ở dòng **Application running** (mặc định http://127.0.0.1:8787, tự chuyển cổng nếu bận). Lần sau chỉ cần mở Docker Desktop rồi bấm đúp **run.cmd**: worker tự kết nối, script đợi máy Online rồi mở web. Không phải chép credential hoặc URL kết nối.

Lần setup đầu cần internet và có thể mất vài phút. Script không cài Python/Node/PostgreSQL toàn hệ thống và không sửa biến PATH. Hai CMD gọi PowerShell có sẵn trên Windows; ExecutionPolicy Bypass chỉ áp dụng cho tiến trình chạy script đó.

## Phạm vi cách ly

- Python/API, Node build giao diện, Nginx và PostgreSQL đều ở các container/image riêng của ứng dụng.
- Mỗi cài đặt mới có tên project Docker ngẫu nhiên, mạng riêng, database volume riêng và khóa riêng trong **.env.docker**. Không dùng `.env` của bản chạy Python cũ.
- Docker vẫn sử dụng CPU/RAM/ổ đĩa của máy Windows. Đây là cách ly bằng container, không phải một máy vật lý khác.
- Chỉ cổng giao diện `127.0.0.1:8787` được mở trên máy; database/API không mở cổng trực tiếp ra Windows/LAN.
- Dữ liệu PostgreSQL nằm trong volume của Docker Desktop, không nằm trong ZIP. Dừng container hoặc chạy lại setup không xóa dữ liệu. Không xóa volume hay `.env.docker` nếu cần giữ dữ liệu.

## Máy tự kết nối với web

Worker được tạo tự động dưới dạng Linux container, có tên máy của bạn trong danh sách **Worker & máy chủ**. Lúc chạy, bạn sẽ thấy `Computer connected: ...`. Credential, worker ID và hostname được lưu tự động trong `.env.docker`, không in ra màn hình. Những lần run sau dùng lại worker đó.

Nếu bạn đang dùng bản cũ: giải nén đè các tệp mã nguồn vào đúng thư mục cũ, **giữ nguyên `.env.docker` và Docker volume**, rồi chạy **setup.cmd lại một lần** để build image mới. Tài khoản quản trị có sẵn được giữ lại. Credential Linux hợp lệ đã cấu hình trước đó được dùng lại.

Worker có thể Online trước khi cấu hình Telegram. Online chỉ chứng minh máy kết nối được với web, chưa có nghĩa là đã đăng nhập tài khoản Telegram.

## Bật chuyển tiếp Telegram

1. Đăng nhập web bằng tài khoản quản trị đã tạo khi setup.
2. Vào **Cài đặt → API Telegram**, nhập `api_id` và `api_hash` lấy tại https://my.telegram.org → API development tools; ứng dụng tự lưu. Sau đó vào **Tài khoản Telegram → Thêm tài khoản**, nhập tên và chọn worker (tự chọn khi chỉ có một máy online).
3. Bấm **Tạo và đăng nhập**, nhập số điện thoại quốc tế, mã OTP và mật khẩu 2FA nếu có. Đây là thêm tài khoản Telegram đã có; tạo số/tài khoản Telegram mới bằng ứng dụng Telegram chính thức trước.
4. Vào **Tuyến chuyển tiếp → Gửi bài từ liên kết**, chọn tài khoản, dán link bài và tải TXT/dán nhóm, đặt khoảng nghỉ/lịch. Lưu → Kiểm tra nhóm → Bắt đầu gửi. SS sẽ được bật khi bắt đầu. Xem hướng dẫn gửi bài ở đầu tài liệu.

Không cần nhập API ID/hash vào `.env.docker` hoặc nhập lại mỗi lần thêm SS. Cấu hình API đã lưu trong Cài đặt được dùng cho tài khoản mới; `api_hash` được mã hóa trong database. Cấu hình riêng đã có của tài khoản cũ vẫn được giữ.

Để cập nhật: giải nén đè vào đúng thư mục cũ, **giữ `.env.docker` và Docker volume**, chạy **setup.cmd một lần** để nâng database và build image mới; lần sau dùng **run.cmd**. Không đưa `.env.docker` lên GitHub hoặc thay khóa khi còn dữ liệu cũ.

## Dừng hoặc thay cổng

Đóng cửa sổ CMD không dừng ứng dụng, vì container chạy nền. Trong Docker Desktop → Containers, chọn project bắt đầu bằng `tfcc-` tương ứng và bấm Stop. Hoặc mở CMD tại thư mục ứng dụng, chạy:

```cmd
docker compose --env-file .env.docker --profile telegram stop
```

Để chạy lại, bấm **run.cmd**. Nếu cổng 8787 bị ứng dụng khác dùng, sửa `TFCC_HTTP_PORT=8788` trong `.env.docker` rồi chạy lại **run.cmd**; trình duyệt sẽ mở cổng mới.

## Khi có lỗi

- Không thấy lệnh Docker: cài Docker Desktop rồi mở lại CMD.
- Engine chưa sẵn sàng: mở Docker Desktop, đợi Engine running; đảm bảo đang dùng Linux containers.
- Setup bị ngắt: chạy lại **setup.cmd**; cấu hình, khóa và tài khoản hiện có được giữ nguyên.
- Chưa chạy setup thành công: **run.cmd** sẽ nhắc chạy setup trước.
- Nếu worker bị bạn thu hồi hoặc credential đã bị xoay thủ công, script sẽ báo lỗi và không tự kích hoạt lại worker bị thu hồi. Giữ thông báo lỗi để kiểm tra cấu hình hiện có.
- Không bấm đồng thời hai setup/run: ứng dụng dùng khóa để tránh tạo hai worker hoặc ghi đè cấu hình.

Đây là cấu hình local trên máy cá nhân, không phải bộ triển khai công khai qua internet. Telegram thật vẫn cần credential/tài khoản của bạn.

## Cập nhật bản sửa BOM

Nếu thấy `Unexpected UTF-8 BOM`, tải bản BOM fix, giải nén đè vào chính thư mục đang dùng, giữ `.env.docker` và volume. Chạy `setup.cmd` lại một lần để cập nhật image API. Tài khoản admin đã tạo được giữ lại; không cần cài lại Docker hay tạo lại database.

## Nhập session có sẵn

Vào **Tài khoản Telegram → Nhập session hàng loạt**. Chọn nhiều file Telethon `.session` hoặc một ZIP, chọn worker Online, thêm proxy cùng cửa sổ nếu cần và bấm Nhập. API dùng lại từ Cài đặt. Xem [HUONG_DAN_NHAP_SESSION.md](HUONG_DAN_NHAP_SESSION.md). Cập nhật bản này cần chạy setup.cmd một lần để nâng migration 0007.

## Quản lý nhiều session

Xem [HUONG_DAN_QUAN_LY_SESSION.md](HUONG_DAN_QUAN_LY_SESSION.md): bỏ trần tổng 100 session, chọn toàn bộ kết quả lọc, bật/tắt/check hàng loạt, nhãn Live/Die/đóng băng/FloodWait/lỗi và lịch sử tác vụ lưu trong database.

## Tự check và kháng nghị spam

Bản mới cần setup.cmd một lần để nâng migration 0008. Khi nhập session có tùy chọn tự check phiên/API + @SpamBot. Dùng **Thao tác → SpamBot / kháng nghị** để xem phản hồi, bấm nút bot hoặc xem trước/xác nhận nội dung kháng nghị. Xem [HUONG_DAN_SPAM_KHANG_NGHI.md](HUONG_DAN_SPAM_KHANG_NGHI.md).

## Xóa các tài khoản đã tích

Lọc và chọn các dòng, bấm **Xóa đã chọn** để xóa hàng loạt khỏi ứng dụng, không gõ tên hay mở hộp xác nhận. Xem [HUONG_DAN_XOA_HANG_LOAT.md](HUONG_DAN_XOA_HANG_LOAT.md). Cập nhật bằng setup.cmd một lần, giữ .env.docker và volume.

## Kháng nghị hàng loạt theo mẫu

Bản mới cần setup.cmd một lần để nâng migration 0009. Chọn SS → Kháng nghị theo mẫu đã chọn → nhập email chung/riêng → chuẩn bị/xem trước nội dung cá nhân hóa → xác nhận gửi các bản sẵn sàng. Xem [HUONG_DAN_KHANG_NGHI_THEO_MAU.md](HUONG_DAN_KHANG_NGHI_THEO_MAU.md).

## DEVYN FORWARDER — giao diện mới

Bản mới đổi toàn bộ giao diện, thêm logo/favicon, sáng/tối và menu điện thoại. Giữ .env.docker và volume, giải nén đè mã nguồn vào thư mục cũ rồi chạy **setup.cmd một lần**, sau đó dùng run.cmd. Head vẫn 0009. Xem [HUONG_DAN_DEVYN_UI.md](HUONG_DAN_DEVYN_UI.md).

## Nút check spam / đóng băng

Bản mới có nút check ngay từng dòng, check tất cả theo bộ lọc và các bộ lọc nhanh. Giữ .env.docker/volume và chạy setup.cmd một lần để build API/web/worker, sau đó dùng run.cmd. Xem [HUONG_DAN_CHECK_HAN_CHE.md](HUONG_DAN_CHECK_HAN_CHE.md).

## Thông tin ngay trên bảng session

Bản mới bỏ khung Tác vụ hàng loạt, đưa trạng thái/lỗi/phản hồi bot vào dòng SS. Chạy setup.cmd một lần để build API/web/worker, giữ .env.docker và volume. Xem [HUONG_DAN_BANG_SS.md](HUONG_DAN_BANG_SS.md).

## Cổng web bị chiếm

setup.cmd/run.cmd mới tự chọn cổng trống và lưu lại. Giữ .env.docker/volume, giải nén đè đúng thư mục cũ, chạy setup.cmd lại. Xem [HUONG_DAN_TU_CHON_CONG.md](HUONG_DAN_TU_CHON_CONG.md).
