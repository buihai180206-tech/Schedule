# Dayflow — lịch làm việc theo buổi trong ngày

## Cài đặt (giống hệt quy trình bạn đã làm với Vocab Alarm)

1. Vào https://app.netlify.com/drop, kéo thả cả thư mục này (6 file: `index.html`, `manifest.json`, `sw.js`, `README.md`, 2 icon) vào — sẽ có ngay 1 link. (Hoặc dùng GitHub Pages như trước nếu muốn ổn định lâu dài.)
2. Mở link đó bằng **Safari** trên iPhone.
3. Bấm nút Chia sẻ → **"Thêm vào MH chính"**.
4. Icon "Dayflow" sẽ xuất hiện trên màn hình chính, mở lên chạy full màn hình như app thật.

## Cách dùng

1. Mở app → bấm icon bút **✎** → vào "Chỉnh lịch tuần".
2. Mỗi buổi (Sáng/Trưa/Chiều/Tối) của từng ngày, bấm **"+ Thêm hoạt động"** để thêm bao nhiêu hoạt động tuỳ ý, mỗi hoạt động có giờ riêng (không bắt buộc) + mô tả. Bấm ✕ để xoá.
3. **Giờ phải nằm trong đúng khung của buổi đó** — Sáng: 00:00–10:59, Trưa: 11:00–12:59, Chiều: 13:00–18:59, Tối: 19:00–23:59. Ví dụ hoạt động lúc 00:30 (12 giờ rưỡi đêm) phải điền vào buổi **Sáng**, không điền được vào buổi Tối — app sẽ báo lỗi và không lưu nếu bạn chọn giờ lệch buổi.
4. Bấm **←** để quay lại — màn hình chính tự nhận diện hôm nay, các hoạt động trong buổi được sắp theo giờ tăng dần.
5. Bấm **"Bật thông báo nhắc giờ hoạt động"** để cho phép thông báo ngay trong trình duyệt — dùng được khi app đang mở, tiện cho lúc đang dùng điện thoại.

## Tích hoàn thành & thống kê

- Mỗi hoạt động ở màn hình chính có 1 ô tích bên trái. Làm xong thì bấm tích — chữ sẽ gạch ngang, và **đẩy lên Gist ngay lập tức** (không chờ như khi sửa lịch) nếu bạn đã bật Đồng bộ.
- **Khi buổi đó (sáng/trưa/chiều/tối) đã trôi qua trong ngày mà bạn chưa tích**, ô tích tự **khoá lại** (hiện dấu ✕ đỏ, không bấm được nữa) và hoạt động đó bị tính là **chưa hoàn thành** — không tích bù được sau đó; hoạt động đã tích rồi cũng không gỡ tích lại được sau khi buổi khoá, để số liệu không bị sửa ngược.
- Mốc khoá theo từng buổi: Sáng khoá lúc 11:00, Trưa lúc 13:00, Chiều lúc 19:00, Tối khoá khi sang ngày mới (00:00). Ngày đã qua thì toàn bộ ô tích của ngày đó luôn ở trạng thái khoá.
- Dưới danh sách hoạt động ở màn hình chính có 1 thẻ gồm 2 dòng:
  - **Hôm nay: x/y hoàn thành** — đếm sống ngay khi bạn tích, trên tổng số hoạt động đặt cho hôm nay.
  - **Tuần này: z% hoàn thành** — tính từ **Thứ Hai của tuần hiện tại** đến hết hôm nay (không tính trước các ngày chưa tới). Sang **Thứ Hai tuần mới** (tức đêm Chủ Nhật vừa qua), số % này **tự bắt đầu lại từ 0** vì lúc đó tuần mới chỉ mới có 1 ngày (hôm đó) để tính.
- Bấm vào thẻ để xem chi tiết theo từng ngày trong tuần ("Thống kê tuần"). Chỉ hoạt động đã "tới hạn" (buổi đã khoá) mới được tính vào %; hoạt động của buổi chưa tới thì chưa tính, tránh làm giảm ảo tỉ lệ trước khi bạn có cơ hội thực hiện. Dòng "Hôm nay" thì không chờ khoá — đếm mọi hoạt động trong ngày ngay khi tích, để bạn thấy tiến độ tức thời.
- Nếu bạn xoá hoặc thêm hoạt động, số liệu các ngày trước tính lại theo lịch mẫu hiện tại (không lưu ảnh chụp lịch cũ) — nên số liệu tuần có thể đổi nhẹ nếu bạn sửa lịch giữa tuần.

## Vì sao thông báo trong app không đáng tin cậy khi app đóng — và cách khắc phục bằng Shortcuts

Thông báo tích hợp sẵn (nút "Bật thông báo") chỉ hoạt động khi **app đang mở trên màn hình** — đây là giới hạn của mọi web app trên iOS, không phải lỗi riêng của Dayflow. Khi bạn khoá máy hoặc chuyển app khác, iOS tạm dừng code nên có thể lỡ thông báo.

Để có thông báo đáng tin cậy kể cả khi app đã đóng, dùng **Shortcuts** (Personal Automation của iOS) — nó chạy độc lập với web app. Bản này thêm một lớp **đồng bộ qua GitHub Gist** để dữ liệu lịch của bạn (điền trong app Web) và nội dung Shortcuts đọc luôn khớp nhau, không cần gõ 2 nơi.

### Vì sao không "tự đồng bộ 100%" được

Mỗi hoạt động trong Dayflow có **giờ cụ thể riêng** (không cố định theo 4 buổi như trước). Nhưng Shortcuts không đọc được giờ "động" từ dữ liệu — một Automation luôn phải khai báo sẵn **giờ kích hoạt cố định** ngay trong app Shortcuts. Vì vậy:

- **Nội dung & việc bạn gán cho ngày nào** → đồng bộ tự động qua Gist, sửa trong app Web là Shortcuts đọc được, không cần đụng vào Shortcuts.
- **Giờ kích hoạt** → mỗi **mốc giờ khác nhau** bạn từng dùng trong tuần cần đúng **1 Automation** tương ứng (không phải theo từng buổi, từng ngày, hay từng hoạt động — chỉ theo giờ). Ví dụ cả tuần bạn chỉ dùng 3 mốc giờ: 07:00, 12:30, 20:00 → chỉ cần 3 Automation, dù có 10 hoạt động khác nhau nằm rải ở các ngày khác nhau lúc 07:00. Khi nào bạn thêm một **giờ hoàn toàn mới** (ví dụ 15:45) chưa từng dùng, lúc đó mới cần tạo thêm 1 Automation mới cho giờ đó — việc này làm thủ công trong Shortcuts, không tự động được vì iOS không cho app tạo Automation hộ bạn.

## Vì sao xoá app khỏi màn hình chính làm mất hết lịch & tick đã làm

Khi bạn **xoá icon app khỏi màn hình chính**, iOS coi như xoá hẳn app đó — toàn bộ dữ liệu lưu trên máy (`localStorage`, gồm cả lịch và các lượt tích hoàn thành) bị xoá theo, giống hệt xoá 1 app thường. Đây là hành vi mặc định của iOS, không phải lỗi của Dayflow, và không có cách nào giữ lại dữ liệu cũ nếu bạn chưa từng bật đồng bộ trước khi xoá.

Cách duy nhất để không mất dữ liệu khi lỡ xoá app (hoặc đổi máy): **bật "Đồng bộ" ở mục cuối màn hình "Chỉnh lịch tuần" trước**. Từ bản này, mục Đồng bộ sao lưu cả 2 phần lên cùng 1 Gist:
- `dayflow-schedule.json` — lịch tuần (hoạt động, giờ).
- `dayflow-completions.json` — toàn bộ lượt tích hoàn thành 60 ngày gần nhất (dữ liệu cũ hơn tự dọn bớt để file không phình to).

Nếu chẳng may xoá app: cài lại theo hướng dẫn ở trên → vào mục Đồng bộ → dán lại đúng token + Gist ID cũ → bấm "Lưu & đồng bộ ngay" → lịch và các lượt tích sẽ được kéo về lại đầy đủ.

> **Vuốt tắt app trong đa nhiệm** (như đóng app YouTube bình thường) khác hẳn xoá icon — bản thân thao tác này **không** xoá dữ liệu trên máy. Nếu trước đây bạn vẫn thấy mất tick ngay sau khi vuốt tắt dù chưa xoá icon, đó là do lượt đẩy lên Gist bị cắt ngang giữa chừng. Bản này đã sửa: tích xong là **đẩy lên Gist ngay lập tức** (không còn chờ ~1 giây như trước), và app còn tự đẩy nốt phần đang chờ (khi sửa lịch) ngay khi bạn rời/ẩn app (bắt cả 2 tín hiệu `visibilitychange` lẫn `pagehide` để chắc ăn hơn trên Safari). Trường hợp cực hiếm còn sót: vuốt tắt trong tích tắc (vài phần nghìn giây) ngay sau khi tích, trước khi trình duyệt kịp gửi được request nào — đây là giới hạn phần cứng/hệ điều hành, không có cách nào chặn 100% từ phía web app.

> Lưu ý: vuốt tắt app trong đa nhiệm (App Switcher) — như đóng app YouTube bình thường — **không** xoá dữ liệu trên máy, khác hẳn với xoá icon. App cũng tự đẩy ngay dữ liệu lên Gist nếu bạn thoát/khoá máy trong lúc đang chờ đồng bộ (thay vì chờ đủ ~1 giây), và khi kéo dữ liệu về app **gộp** thay vì ghi đè — nên tick vừa làm sẽ không bao giờ bị 1 bản cũ trên Gist ghi đè mất.



Mục "Đồng bộ" nằm cuối màn hình "Chỉnh lịch tuần".

1. Tạo GitHub Personal Access Token: **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token** → quyền **Gists: Read and write**. (Token "classic" thì tick scope `gist`.) Copy token (chỉ hiện 1 lần).
2. Dán token vào ô **"GitHub token (quyền: gist)"** trong app.
3. Bấm **"Tạo Gist mới"** — app tạo 1 Gist secret chứa lịch hiện tại, tự điền Gist ID và hiện ra **URL Raw**.
4. Copy URL Raw đó — dùng ở bước 5 bên dưới.
5. Từ giờ mỗi lần sửa hoạt động (thêm/sửa/xoá/đổi giờ) trong app, app tự đẩy lên Gist sau ~1 giây; trạng thái hiện ngay dưới 2 nút.

> Token lưu trong trình duyệt của máy bạn (localStorage) — coi như mật khẩu, không chia sẻ URL Raw/token cho người khác vì ai có token sửa được Gist. Dùng lại trên máy khác: dán đúng token + Gist ID cũ rồi bấm "Lưu & đồng bộ ngay", không cần tạo Gist mới.

## Nếu thấy app vẫn hành xử "kiểu cũ" dù mình đã báo đã sửa lỗi

PWA trên iOS đôi khi vẫn giữ 1 bản cache cũ của app dù bạn đã cài lại từ file mới — do trình duyệt cache riêng file `sw.js` (service worker) nên không nhận ra có bản cập nhật để tải bản mới về. Bản này thêm file `_headers` để Netlify ngừng cache `sw.js`, giúp việc cập nhật đáng tin cậy hơn cho các lần sau — nhưng nếu bạn đang thấy hành vi cũ ngay bây giờ, làm theo các bước sau để chắc chắn có đúng bản mới nhất:

1. **Bật Đồng bộ trước** (nếu chưa) để không mất lịch/tick khi làm bước tiếp theo — xem mục "Thiết lập đồng bộ" bên dưới.
2. Xoá icon app khỏi màn hình chính (chấp nhận mất dữ liệu local, sẽ khôi phục lại qua Gist).
3. Kéo thả **lại toàn bộ 7 file** (gồm cả `_headers`) vào https://app.netlify.com/drop để có 1 link/deploy hoàn toàn mới — dùng đúng link mới này, không dùng lại link cũ đã lưu trước đó vì link cũ có thể vẫn trỏ tới bản deploy cũ.
4. Mở link mới bằng Safari → Thêm vào MH chính lại.
5. Vào mục Đồng bộ, dán lại token + Gist ID cũ → "Lưu & đồng bộ ngay" để kéo lịch/tick về.

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
