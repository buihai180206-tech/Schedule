# Dayflow — lịch làm việc theo buổi trong ngày

## Cài đặt (giống hệt quy trình bạn đã làm với Vocab Alarm)

1. Vào https://app.netlify.com/drop, kéo thả cả thư mục này (4 file: `index.html`, `manifest.json`, `sw.js`, và 2 icon) vào — sẽ có ngay 1 link. (Hoặc dùng GitHub Pages như trước nếu muốn ổn định lâu dài: tạo repo mới, upload các file này, bật Pages trong Settings.)
2. Mở link đó bằng **Safari** trên iPhone.
3. Bấm nút Chia sẻ → **"Thêm vào MH chính"**.
4. Icon "Dayflow" sẽ xuất hiện trên màn hình chính, mở lên chạy full màn hình như app thật.

## Cách dùng

1. Mở app → bấm icon bút **✎** ở góc trên bên phải → vào màn hình "Chỉnh lịch tuần".
2. Mỗi ngày trong tuần (Thứ Hai → Chủ Nhật) chia thành 4 buổi: **Sáng, Trưa, Chiều, Tối**. Trong mỗi buổi, bấm **"+ Thêm hoạt động"** để thêm bao nhiêu hoạt động tuỳ ý — mỗi hoạt động có 1 ô chọn giờ cụ thể (không bắt buộc) và 1 ô mô tả công việc. Bấm ✕ để xoá hoạt động nào không cần nữa.
3. Bấm **←** để quay lại màn hình chính — tự nhận diện hôm nay là thứ mấy, chỉ hiện đúng lịch ngày đó, các hoạt động trong từng buổi được sắp theo giờ tăng dần. Buổi nào không có hoạt động nào (có mô tả) sẽ hiện "Không có công việc nào".
4. Bấm **"Bật thông báo nhắc giờ hoạt động"** một lần để cho phép app gửi thông báo — Safari sẽ hỏi xin quyền, bấm Allow.

App tự kiểm tra giờ mỗi 15 giây khi đang mở — hoạt động nào có đặt giờ, đến đúng giờ đó (trong vòng 5 phút) sẽ gửi 1 thông báo nhắc, nội dung chính là mô tả hoạt động bạn đã điền.

**Lưu ý về giới hạn của iOS** (giống hệt Vocab Alarm): thông báo chỉ hoạt động đáng tin cậy khi app đang mở trên màn hình. Nếu bạn chuyển sang app khác hoặc khoá máy, iOS tạm dừng code của app nên có thể bị lỡ thông báo — đây là giới hạn chung của mọi web app trên iOS, không phải lỗi riêng của Dayflow.

Dữ liệu lưu trên máy (localStorage), không cần mạng sau khi cài, không đồng bộ với thiết bị khác.
