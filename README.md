# Nhịp Tuần — lịch làm việc theo buổi trong ngày

## Cài đặt (giống hệt quy trình bạn đã làm với Vocab Alarm)

1. Vào https://app.netlify.com/drop, kéo thả cả thư mục này (4 file: `index.html`, `manifest.json`, `sw.js`, và 2 icon) vào — sẽ có ngay 1 link. (Hoặc dùng GitHub Pages như trước nếu muốn ổn định lâu dài: tạo repo mới, upload các file này, bật Pages trong Settings.)
2. Mở link đó bằng **Safari** trên iPhone.
3. Bấm nút Chia sẻ → **"Thêm vào MH chính"**.
4. Icon "Nhịp Tuần" sẽ xuất hiện trên màn hình chính, mở lên chạy full màn hình như app thật.

## Cách dùng

1. Mở app → bấm icon bút **✎** ở góc trên bên phải → vào màn hình "Chỉnh lịch tuần".
2. Mỗi ngày trong tuần (Thứ Hai → Chủ Nhật) có 4 ô: **Sáng, Trưa, Chiều, Tối** — điền công việc cho từng buổi. Ô nào để trống thì buổi đó coi như không có việc gì.
3. Bấm **←** để quay lại màn hình chính — màn hình này tự nhận diện hôm nay là thứ mấy và **chỉ hiện đúng lịch của ngày hôm đó**, chia theo 4 buổi. Sang ngày mới, mở app lên sẽ tự động hiện đúng lịch của ngày mới, không cần làm gì thêm.
4. Buổi nào không có việc sẽ hiện chữ "Không có công việc nào".
5. Dải chấm tròn phía trên (Sáng — Trưa — Chiều — Tối) là thanh nhịp ngày — chấm nào đang sáng lên là buổi hiện tại theo giờ thực trên máy bạn.

Dữ liệu lưu trên máy (localStorage), không cần mạng sau khi cài, không đồng bộ với thiết bị khác (giống Vocab Alarm bản đầu — nếu sau này bạn muốn đồng bộ nhiều máy, có thể áp dụng đúng cơ chế Gist đã làm bên Vocab Alarm).
