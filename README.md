# Dayflow — lịch làm việc theo buổi trong ngày

## Cài đặt (giống hệt quy trình bạn đã làm với Vocab Alarm)

1. Vào https://app.netlify.com/drop, kéo thả cả thư mục này (6 file: `index.html`, `manifest.json`, `sw.js`, `README.md`, 2 icon) vào — sẽ có ngay 1 link. (Hoặc dùng GitHub Pages như trước nếu muốn ổn định lâu dài.)
2. Mở link đó bằng **Safari** trên iPhone.
3. Bấm nút Chia sẻ → **"Thêm vào MH chính"**.
4. Icon "Dayflow" sẽ xuất hiện trên màn hình chính, mở lên chạy full màn hình như app thật.

## Cách dùng

1. Mở app → bấm icon bút **✎** → vào "Chỉnh lịch tuần".
2. Mỗi buổi (Sáng/Trưa/Chiều/Tối) của từng ngày, bấm **"+ Thêm hoạt động"** để thêm bao nhiêu hoạt động tuỳ ý, mỗi hoạt động có giờ riêng (không bắt buộc) + mô tả. Bấm ✕ để xoá.
3. Bấm **←** để quay lại — màn hình chính tự nhận diện hôm nay, các hoạt động trong buổi được sắp theo giờ tăng dần.
4. Bấm **"Bật thông báo nhắc giờ hoạt động"** để cho phép thông báo ngay trong trình duyệt — dùng được khi app đang mở, tiện cho lúc đang dùng điện thoại.

## Vì sao thông báo trong app không đáng tin cậy khi app đóng — và cách khắc phục bằng Shortcuts

Thông báo tích hợp sẵn (nút "Bật thông báo") chỉ hoạt động khi **app đang mở trên màn hình** — đây là giới hạn của mọi web app trên iOS, không phải lỗi riêng của Dayflow. Khi bạn khoá máy hoặc chuyển app khác, iOS tạm dừng code nên có thể lỡ thông báo.

Để có thông báo đáng tin cậy kể cả khi app đã đóng, dùng **Shortcuts** (Personal Automation của iOS) — nó chạy độc lập với web app. Bản này thêm một lớp **đồng bộ qua GitHub Gist** để dữ liệu lịch của bạn (điền trong app Web) và nội dung Shortcuts đọc luôn khớp nhau, không cần gõ 2 nơi.

### Vì sao không "tự đồng bộ 100%" được

Mỗi hoạt động trong Dayflow có **giờ cụ thể riêng** (không cố định theo 4 buổi như trước). Nhưng Shortcuts không đọc được giờ "động" từ dữ liệu — một Automation luôn phải khai báo sẵn **giờ kích hoạt cố định** ngay trong app Shortcuts. Vì vậy:

- **Nội dung & việc bạn gán cho ngày nào** → đồng bộ tự động qua Gist, sửa trong app Web là Shortcuts đọc được, không cần đụng vào Shortcuts.
- **Giờ kích hoạt** → mỗi **mốc giờ khác nhau** bạn từng dùng trong tuần cần đúng **1 Automation** tương ứng (không phải theo từng buổi, từng ngày, hay từng hoạt động — chỉ theo giờ). Ví dụ cả tuần bạn chỉ dùng 3 mốc giờ: 07:00, 12:30, 20:00 → chỉ cần 3 Automation, dù có 10 hoạt động khác nhau nằm rải ở các ngày khác nhau lúc 07:00. Khi nào bạn thêm một **giờ hoàn toàn mới** (ví dụ 15:45) chưa từng dùng, lúc đó mới cần tạo thêm 1 Automation mới cho giờ đó — việc này làm thủ công trong Shortcuts, không tự động được vì iOS không cho app tạo Automation hộ bạn.

## Thiết lập đồng bộ (Gist) — chỉ làm 1 lần

Mục "Đồng bộ" nằm cuối màn hình "Chỉnh lịch tuần".

1. Tạo GitHub Personal Access Token: **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token** → quyền **Gists: Read and write**. (Token "classic" thì tick scope `gist`.) Copy token (chỉ hiện 1 lần).
2. Dán token vào ô **"GitHub token (quyền: gist)"** trong app.
3. Bấm **"Tạo Gist mới"** — app tạo 1 Gist secret chứa lịch hiện tại, tự điền Gist ID và hiện ra **URL Raw**.
4. Copy URL Raw đó — dùng ở bước 5 bên dưới.
5. Từ giờ mỗi lần sửa hoạt động (thêm/sửa/xoá/đổi giờ) trong app, app tự đẩy lên Gist sau ~1 giây; trạng thái hiện ngay dưới 2 nút.

> Token lưu trong trình duyệt của máy bạn (localStorage) — coi như mật khẩu, không chia sẻ URL Raw/token cho người khác vì ai có token sửa được Gist. Dùng lại trên máy khác: dán đúng token + Gist ID cũ rồi bấm "Lưu & đồng bộ ngay", không cần tạo Gist mới.

## Tạo Automation trong Shortcuts — 1 lần cho mỗi mốc giờ

Mở **Shortcuts → Automation → "+" → "Tạo Automation cá nhân"**. Lặp lại các bước sau cho **từng mốc giờ khác nhau** bạn dùng trong tuần:

1. Trigger **"Thời gian trong ngày"** → đặt đúng giờ (vd 07:00) → Lặp lại **Hằng ngày** → Tiếp.
2. **Tắt "Hỏi trước khi chạy"** (chọn "Không hỏi") để chạy im lặng.
3. Thêm **"Lấy nội dung của URL"** (Get Contents of URL) → dán URL Raw ở bước 4 phần trên.
4. Thêm **"Lấy từ điển từ input"** (Get Dictionary from Input), Input = kết quả bước 3.
5. Thêm **"Ngày giờ hiện tại"** (Current Date).
6. Thêm **"Định dạng ngày"** (Format Date) → định dạng tuỳ chỉnh **`EEEE`** → nếu có tuỳ chọn ngôn ngữ, chọn **English (US)** (để ra "Monday" chứ không phải "Thứ Hai").
7. Thêm **"Đổi chữ hoa/thường"** (Change Case) → **chữ thường** → ra "monday", "tuesday"...
8. Thêm **"Lấy giá trị trong từ điển"**: Từ điển = kết quả bước 4, Khoá = kết quả bước 7. (Kết quả là từ điển các hoạt động trong ngày, dạng giờ → mô tả.)
9. Thêm **"Lấy giá trị trong từ điển"** lần 2: Từ điển = kết quả bước 8, Khoá = gõ tay đúng giờ của Automation này, định dạng `HH:mm` (vd `07:00`, phải khớp chính xác với giờ bạn đặt trong app Web).
10. Thêm **"Nếu"** (If): Input = kết quả bước 9, điều kiện **"có giá trị bất kỳ"**:
    - Bên trong: thêm **"Văn bản"** (Text) → chèn kết quả bước 9, gõ thêm " đi nhé!" phía sau.
    - Thêm **"Hiện thông báo"** (Show Notification), nội dung = văn bản vừa tạo.
11. Lưu Automation.

Kết quả: đúng 07:00 mỗi ngày, Automation tự kiểm tra hôm nay có hoạt động nào đặt giờ 07:00 không — có thì bắn "Học tiếng Anh đi nhé!" (hoặc bất kỳ nội dung nào bạn điền cho giờ đó ở ngày đó), không có thì im lặng. Sửa nội dung/ngày trong app Web sẽ tự phản ánh vào lần thông báo tiếp theo, không cần sửa lại Shortcuts.

> Ghi chú: GitHub cache nội dung Gist Raw vài phút, nên vừa sửa lịch xong chạy thử Automation ngay có thể chưa thấy thay đổi mới nhất. Nếu 2 hoạt động khác ngày/khác buổi nhưng trùng đúng giờ HH:mm, Gist chỉ giữ được nội dung thêm sau cùng cho giờ đó trong cùng 1 ngày — 2 hoạt động khác ngày thì không ảnh hưởng nhau.

Dữ liệu vẫn lưu trên máy trước (localStorage); Gist chỉ là lớp đồng bộ ở giữa Web và Shortcuts.
