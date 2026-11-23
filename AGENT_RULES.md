# AGENT_RULES.md — Tiêu Chuẩn Bắt Buộc Của Dự Án

> **Tên dự án:** Gia Khiêm English (Học tiếng Anh tương tác hàng ngày)  
> **Đối tượng sử dụng:** Học sinh lớp 2 — Gia Khiêm (7–8 tuổi)  
> **Thời lượng mục tiêu:** 30 phút / ngày  
> **Giáo trình nền tảng:** Oxford *Family and Friends 2* (bắt đầu từ **Unit 7**, mở rộng hết quyển 2 và thiết kế cấu trúc dữ liệu sẵn sàng cho các quyển tiếp theo: *Family and Friends 3, 4, 5*).

Mọi AI Agent hoặc lập trình viên tham gia xây dựng và mở rộng dự án này **bắt buộc** phải tuân thủ toàn bộ các quy tắc dưới đây.

---

## 1. Giao Diện Thân Thiện Với Trẻ 7–8 Tuổi (Kid-First UI/UX)

- **Phong cách thị giác:** Tươi sáng, ấm áp, nhiều năng lượng tích cực (màu sắc chủ đạo gợi ý: vàng nắng, xanh dương nhạt, xanh lá cây, cam san hô), tránh màu tối u ám hoặc giao diện quá phức tạp.
- **Typography:**
  - Bắt buộc dùng font chữ tròn, nét rõ, dễ đọc cho trẻ nhỏ: **`Nunito`** hoặc **`Quicksand`** (ưu tiên `Nunito` cho tiêu đề/nút bấm và `Quicksand` hoặc `Nunito` cho nội dung), có fallback `sans-serif`.
  - Kích thước chữ lớn, khoảng cách dòng thoáng (`line-height >= 1.5`), phân biệt rõ chữ tiếng Anh cần học và chữ hướng dẫn tiếng Việt.
- **Tương tác & Nút bấm:**
  - Mọi nút bấm tương tác phải có kích thước lớn (tối thiểu `48x48px`, khuyến khích `56px+` cho các nút chính), bo góc mềm mại (`border-radius >= 16px`), có hiệu ứng phản hồi khi chạm/hover/nhấn (animation nhẹ, âm thanh/phản hồi trực quan).
  - Bố cục 1 màn hình = 1 nhiệm vụ chính, tránh nhồi nhét quá nhiều chữ hoặc quá nhiều lựa chọn cùng lúc.
- **Ngôn ngữ hướng dẫn:**
  - **Hạn chế tối đa chữ tiếng Anh dài dòng ở phần hướng dẫn.**
  - Toàn bộ nhãn điều hướng, hướng dẫn làm bài, thông báo khen ngợi/khuyến khích phải dùng **tiếng Việt ngắn gọn, gần gũi** kết hợp với **icon/emoji trực quan** (ví dụ: 🔊 *Nghe*, 🎤 *Nói*, ⭐ *Sao*, 📖 *Từ mới*).

---

## 2. Âm Thanh Chuẩn & Luyện Phát Âm (Web Speech API)

### 2.1. Đọc tiếng Anh (`window.speechSynthesis`)
- Mọi từ vựng, cụm từ, câu mẫu, đoạn hội thoại tiếng Anh đều phải có khả năng phát âm bằng `speechSynthesis`.
- **Cấu hình bắt buộc:**
  - Ngôn ngữ: ưu tiên giọng đọc tiếng Anh chuẩn (`en-US` hoặc `en-GB`, chọn giọng tự nhiên nhất có sẵn trên trình duyệt).
  - **Tốc độ mặc định: `rate = 0.85`** (0.85x) để trẻ 7–8 tuổi nghe rõ từng âm tiết. Có thể cung cấp tùy chọn nghe chậm hơn (`0.7x`) nếu cần, nhưng mặc định khi bấm nghe phải là `0.85`.
  - Xử lý an toàn: luôn gọi `speechSynthesis.cancel()` trước khi phát câu mới để tránh chồng âm hoặc kẹt hàng đợi; có cơ chế fallback/thông báo nhẹ nhàng bằng tiếng Việt nếu trình duyệt không hỗ trợ.

### 2.2. Chấm điểm phát âm (`SpeechRecognition` / `webkitSpeechRecognition`)
- Tích hợp nhận diện giọng nói cho các bài luyện nói / lặp lại câu / đọc từ.
- **Cấu hình & Trải nghiệm:**
  - Thiết lập `lang = 'en-US'` (hoặc `'en-GB'` đồng bộ với giọng đọc), `interimResults = false`, `maxAlternatives = 3`.
  - So sánh kết quả nhận diện với từ/câu mục tiêu (chuẩn hóa chữ thường, bỏ dấu câu) để tính điểm tương đồng và đưa ra phản hồi tích cực cho trẻ (ví dụ: hiển thị số sao đạt được, tô xanh các từ đọc đúng, gợi ý nghe lại & thử lại nhẹ nhàng nếu chưa chuẩn — không phê bình gay gắt).
  - **Xử lý fallback:** Nếu trình duyệt không hỗ trợ `SpeechRecognition` hoặc chưa cấp quyền micro, phải hiển thị hướng dẫn tiếng Việt ngắn gọn, dễ hiểu và cho phép bé bỏ qua/chuyển sang chế độ nghe & tự đọc để không bị kẹt bài học.

---

## 3. Tính Năng Từ Điển Chạm (Tap-to-Translate) — BẮT BUỘC TOÀN CỤC

- **Phạm vi áp dụng:** **MỌI từ tiếng Anh** hiển thị trong đoạn hội thoại, câu mẫu, câu hỏi, hoặc thẻ đọc hiểu đều **bắt buộc phải bấm/chạm vào được** (không render chuỗi văn bản tiếng Anh thuần túy không có tương tác ở các phần nội dung học).
- **Cơ chế hoạt động:**
  - Tạo một component dùng chung (ví dụ: `TappableText` / `InteractiveWord`) tách từng từ tiếng Anh (giữ nguyên dấu câu đi kèm nhưng tách phần từ gốc để tra cứu, ví dụ: `"apples."` -> tra từ `"apples"` / `"apple"`).
  - Khi bé bấm vào **bất kỳ từ nào**, phải **hiển thị ngay một hộp thoại nhỏ (popover / modal / bottom sheet)** chứa đầy đủ 5 thông tin sau:
    1. **Từ gốc** (Word — kèm dạng nguyên thể nếu là số nhiều/chia động từ).
    2. **Phiên âm IPA** (ví dụ: `/ˈæp.əl/`).
    3. **Loại từ** bằng tiếng Việt dễ hiểu (ví dụ: *Danh từ*, *Động từ*, *Tính từ*, *Trạng từ*, *Giới từ*, *Đại từ*...).
    4. **Nghĩa tiếng Việt dễ hiểu cho trẻ em** (ngắn gọn, sát ngữ cảnh bài học).
    5. **Nút nghe phát âm từ đó** (🔊 gọi `speechSynthesis` với `rate = 0.85`).
- **Dữ liệu từ điển:**
  - Mọi từ xuất hiện trong các Unit phải được khai báo đầy đủ trong từ điển cục bộ của ứng dụng (kèm cơ chế tra cứu fallback thông minh cho dạng số nhiều/chia thì cơ bản) để đảm bảo **không bao giờ** bấm vào một từ mà bị trống thông tin.

---

## 4. Lưu Trữ Thông Minh (`localStorage`) & Spaced Repetition

Mọi dữ liệu tiến trình của bé Gia Khiêm phải được lưu bền vững trên trình duyệt bằng `localStorage` (có namespace rõ ràng, ví dụ: `gk_english_v1_*` và kiểm soát lỗi `try/catch` khi đọc/ghi JSON).

Bắt buộc lưu trữ và quản lý 3 nhóm dữ liệu sau:
1. **Lịch sử học theo ngày (`YYYY-MM-DD`):**
   - Thời gian đã học trong ngày (để theo dõi mục tiêu 30 phút/ngày).
   - Các Unit / bài tập đã hoàn thành, chuỗi ngày học liên tiếp (streak).
2. **Danh sách từ hay sai & Lặp lại ngắt quãng (Spaced Repetition System - SRS):**
   - Ghi nhận các từ/câu bé làm sai hoặc phát âm chưa đạt.
   - Lưu trạng thái ôn tập (ví dụ: số lần sai, mức độ thành thạo `box/level`, thời điểm cần ôn lại `nextReviewDate`).
   - Ưu tiên đưa các từ hay sai quay lại vào phần ôn tập đầu buổi học ngày hôm sau.
3. **Điểm thưởng (Sao & Huy hiệu) theo từng ngày:**
   - Tổng số sao kiếm được trong ngày và tích lũy toàn bộ.
   - Danh sách huy hiệu (Badges) đã mở khóa (ví dụ: *Chăm chỉ 3 ngày*, *Siêu sao Unit 7*, *Thợ săn từ vựng*).

---

## 5. Cấu Trúc Giáo Trình & Lộ Trình 30 Phút/Ngày

- **Cấu trúc dữ liệu giáo trình mở rộng được:**
  - Tổ chức dữ liệu theo cấp bậc: `Book` (Quyển 2, 3, 4...) → `Unit` (Unit 7, Unit 8, ..., Unit 15) → `Lesson / Activity`.
  - Nội dung khởi đầu bám sát **Oxford *Family and Friends 2* từ Unit 7 trở đi** (từ vựng, ngữ pháp, phonics, hội thoại, bài tập nghe–nói–đọc–viết ngắn) và có bài mở rộng nâng cao nhẹ phù hợp học sinh lớp 2.
- **Nhịp học 30 phút/ngày:**
  - Có bộ đếm/thanh tiến trình thời gian học trong ngày nhẹ nhàng (không gây áp lực, mang tính đồng hành).
  - Chia buổi học thành các chặng nhỏ (ví dụ: *Khởi động & Ôn từ hay sai SRS* → *Từ vựng mới* → *Hội thoại & Tap-to-Translate* → *Luyện nói* → *Trò chơi/Thử thách tổng kết & Nhận sao*).

---

## 6. Quy Chuẩn Kỹ Thuật Chung

- **Chạy mượt offline-first (trừ Web Speech API nếu trình duyệt dùng dịch vụ đám mây):** Không phụ thuộc backend bắt buộc để bé có thể mở web học ngay.
- **Responsive:** Hoạt động tốt trên cả máy tính bảng (iPad/Tablet), laptop và điện thoại; vùng chạm đủ lớn cho ngón tay trẻ em.
- **Kiểm thử trước khi bàn giao:** Mọi tính năng mới thêm vào phải được kiểm tra hoạt động thực tế của: (1) Tap-to-Translate trên mọi từ, (2) `speechSynthesis` ở tốc độ `0.85`, (3) `SpeechRecognition` + fallback, và (4) lưu/đọc `localStorage` chính xác.
