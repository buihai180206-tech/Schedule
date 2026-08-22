# Nhịp Tuần — lịch làm việc theo buổi trong ngày

## Vì sao bản Web không tự bật thông báo, còn Shortcuts thì được?

Đây không phải lỗi code. App web (PWA) cài qua "Thêm vào MH chính" trên iOS **không có cách nào chạy nền và tự bật thông báo hẹn giờ khi app đã tắt hẳn** — đó là giới hạn của iOS/Safari, không riêng app này. Bản Shortcuts làm được vì nó chạy qua Personal Automation của hệ thống, độc lập với app.

Vì vậy hướng xử lý ở bản này: **giữ nguyên Shortcuts lo việc bắn thông báo**, còn app Web chỉ lo việc **lưu & đồng bộ lịch** — qua một GitHub Gist — để cả hai bên luôn đọc chung một nguồn dữ liệu, không lệch nhau nữa.

## 1. Cài đặt app (như cũ)

1. Vào https://app.netlify.com/drop, kéo thả cả thư mục này (6 file: `index.html`, `manifest.json`, `sw.js`, `README.md`, 2 icon) vào — sẽ có ngay 1 link. (Hoặc GitHub Pages nếu muốn ổn định lâu dài.)
2. Mở link đó bằng **Safari** trên iPhone.
3. Bấm nút Chia sẻ → **"Thêm vào MH chính"**.
4. Icon "Nhịp Tuần" sẽ xuất hiện trên màn hình chính.

## 2. Cách dùng màn hình chính & chỉnh lịch (như cũ)

- Bấm icon bút **✎** để vào "Chỉnh lịch tuần", điền công việc cho từng buổi (Sáng/Trưa/Chiều/Tối) của từng ngày. Ô nào trống thì buổi đó hiện "Không có công việc nào".
- Bấm **←** để quay lại — màn hình chính tự nhận diện hôm nay và chỉ hiện đúng lịch hôm đó.
- Dữ liệu vẫn lưu trên máy (localStorage) trước tiên, không cần mạng vẫn dùng bình thường.

## 3. Thiết lập đồng bộ (Gist) — chỉ làm 1 lần

Mục "Đồng bộ" nằm cuối màn hình "Chỉnh lịch tuần".

1. Tạo GitHub Personal Access Token:
   - Vào github.com → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
   - Đặt quyền (Permissions) → **Gists: Read and write**. Không cần cấp thêm quyền nào khác.
   - (Nếu dùng token dạng cũ "classic": chỉ cần tick scope `gist`.)
   - Copy token vừa tạo (chỉ hiện 1 lần).
2. Dán token vào ô **"GitHub token (quyền: gist)"** trong app.
3. Bấm **"Tạo Gist mới"** — app sẽ tạo 1 Gist riêng (ở chế độ secret, không công khai tìm kiếm được) chứa lịch hiện tại, đồng thời tự điền Gist ID và hiện ra **URL Raw**.
4. Copy URL Raw đó lại — sẽ cần dán vào Shortcuts ở bước 4.
5. Từ giờ, mỗi lần sửa lịch trong app, app tự đẩy (push) bản mới lên Gist sau ~1 giây. Trạng thái đồng bộ hiện ngay dưới 2 nút bấm.

> Lưu ý: token này lưu trong trình duyệt của máy bạn (localStorage), không gửi đi đâu khác ngoài GitHub. Vẫn nên coi nó như mật khẩu — không chia sẻ URL Raw hay token cho người khác, vì ai có token có thể sửa được Gist.
>
> Nếu dùng lại app trên máy khác (hoặc cài lại), chỉ cần dán đúng token + Gist ID cũ vào rồi bấm "Lưu & đồng bộ ngay" — không cần tạo Gist mới.

## 4. Thiết lập thông báo trong Shortcuts (làm 1 lần, 4 Automation)

Mở app **Shortcuts** → tab **Automation** → **"+"** → **"Tạo Automation cá nhân"**. Lặp lại toàn bộ các bước dưới đây **4 lần**, mỗi lần cho 1 buổi (Sáng/Trưa/Chiều/Tối) — chỉ khác giờ kích hoạt và 1 chữ khoá ở bước 9.

| Buổi | Giờ gợi ý | Khoá dùng ở bước 9 |
|---|---|---|
| Sáng | 06:00 | `sang` |
| Trưa | 11:00 | `trua` |
| Chiều | 13:00 | `chieu` |
| Tối | 18:00 | `toi` |

Các bước cho mỗi Automation:

1. Chọn trigger **"Thời gian trong ngày"** → đặt giờ theo bảng trên → Lặp lại **Hằng ngày** → Tiếp.
2. Ở màn tiếp theo, **tắt "Hỏi trước khi chạy"** (chọn "Không hỏi") để tự chạy im lặng.
3. Thêm hành động **"Lấy nội dung của URL"** (Get Contents of URL) → dán **URL Raw** đã copy ở bước 3 phần trên.
4. Thêm **"Lấy từ điển từ input"** (Get Dictionary from Input), Input = kết quả bước 3.
5. Thêm **"Ngày giờ hiện tại"** (Current Date).
6. Thêm **"Định dạng ngày"** (Format Date) → chọn định dạng tuỳ chỉnh **`EEEE`** → nếu action có tuỳ chọn ngôn ngữ/locale, chọn **English (US)** để chắc chắn ra tên thứ tiếng Anh (vd "Monday").
7. Thêm **"Đổi chữ hoa/thường"** (Change Case) → chọn **chữ thường** (lowercase) để có "monday", "tuesday"...
8. Thêm **"Lấy giá trị trong từ điển"** (Get Dictionary Value): Từ điển = kết quả bước 4, Khoá = kết quả bước 7.
9. Thêm tiếp **"Lấy giá trị trong từ điển"** lần 2: Từ điển = kết quả bước 8, Khoá = gõ tay theo bảng trên (`sang`/`trua`/`chieu`/`toi`).
10. Thêm **"Nếu"** (If): Input = kết quả bước 9, điều kiện **"có giá trị bất kỳ"** (has any value):
    - Bên trong If: thêm **"Văn bản"** (Text), nội dung gõ: `[kết quả bước 9] đi nhé!` (chèn biến kết quả bước 9 vào trước, gõ thêm chữ " đi nhé!" phía sau).
    - Thêm **"Hiện thông báo"** (Show Notification), nội dung = văn bản vừa tạo.
11. Lưu Automation.

Kết quả: buổi nào có việc, ví dụ ô "Sáng" của hôm đó ghi "Học tiếng Anh", đến giờ sẽ hiện thông báo **"Học tiếng Anh đi nhé!"**. Buổi nào để trống trong lịch thì im lặng, không bắn thông báo (giống đúng cách màn hình chính hiển thị).

> Ghi chú nhỏ: GitHub cache nội dung Gist Raw vài phút, nên nếu vừa sửa lịch trong app xong bấm chạy thử Automation ngay có thể chưa thấy thay đổi mới nhất — đợi vài phút là đồng bộ.

Dữ liệu vẫn lưu trên máy trước (localStorage) như bản gốc; Gist chỉ là lớp đồng bộ ở giữa Web và Shortcuts, không đồng bộ với thiết bị khác nếu bạn không dùng chung 1 Gist/token.
