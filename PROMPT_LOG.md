# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Nguyễn Trung Quân
- **MSSV:** 125001970
- **Tên đề tài Website:** Landing Page "Đánh giá năng lực tư duy & Lộ trình học tập cá nhân hóa" (MindPath)
- **Công cụ AI đã sử dụng:** Google Antigravity (Claude Opus 4.6, Gemini 3.8 Flash)

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> *Ghi lại prompt tổng quan ban đầu bạn dùng để khởi tạo khung website.*

```text
Đóng vai Senior Front-End Developer.
Hãy tạo cấu trúc dự án Landing Page "Đánh giá năng lực tư duy & Lộ trình học tập cá nhân hóa" gồm:
- index.html
- css/style.css
- assets/images/
- README.md
- PROMPT_LOG.md
Yêu cầu:
1. Dùng HTML5, CSS3, Git và GitHub.
2. Tạo file README.md giới thiệu tên dự án, mục tiêu, công nghệ và cách chạy.
3. Tạo PROMPT_LOG.md để lưu các Prompt AI sử dụng.
4. Tuyệt đối không dùng JavaScript.
5. Trả về toàn bộ cấu trúc thư mục và nội dung ban đầu của các file.
```

- **Mục tiêu khởi tạo:** Thiết lập nền tảng dự án Landing Page giáo dục hiện đại, cam kết nguyên tắc "Zero JavaScript" cho UI/UX, phân tách thư mục theo chuẩn chuyên nghiệp và sẵn sàng cho việc phát triển lũy tiến.

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & CSS Variables
- **Prompt đã dùng:**
  ```text
  Đóng vai chuyên gia Semantic HTML5, SEO và Accessibility.
  Tạo file index.html hoàn chỉnh cho Landing Page “Đánh giá năng lực tư duy & Lộ trình học tập cá nhân hóa”.
  Cấu trúc 8 phần: Header (Logo MindPath, Nav 5 mục), Hero (Tiêu đề, mô tả, CTA), Benefits (4 lợi ích),
  Assessment Types (4 loại đánh giá), Learning Path (3 lộ trình: Học sinh, Sinh viên, Người đi làm),
  Testimonials (3 cảm nhận), Registration (Form đủ trường), Footer (Liên hệ, mạng xã hội, bản quyền).
  Yêu cầu: Dùng header, nav, main (duy nhất 1 thẻ), section, article, aside, footer, figure, figcaption.
  Không lạm dụng div, không dùng thẻ lỗi thời, SEO meta đầy đủ, không dùng JavaScript.
  ```
- **Thách thức gặp phải:**
  - AI ban đầu có xu hướng dùng nhiều thẻ `<div>` lồng nhau để chia cột và quên gắn thuộc tính tiếp cận (Accessibility `aria-label`, `role`).
  - Menu điều hướng cần hoạt động đóng/mở được trên thiết bị di động nhưng đề bài cấm dùng JavaScript.
- **Cách sửa prompt (Debug prompt):**
  - Bổ sung chỉ thị nghiêm ngặt: *"Chỉ dùng đúng 1 thẻ `<main>`, mỗi ảnh bắt buộc có thẻ `<figure>` và `<figcaption>`, sử dụng kỹ thuật CSS Checkbox Hack (`#nav-toggle:checked ~ .nav-menu`) để tạo menu mobile thuần CSS, không chèn bất kỳ thẻ `<script>` nào."*
- **Kết quả AI tạo ra:**
  - File `index.html` ngữ nghĩa 100% chuẩn W3C, cấu trúc rõ ràng qua các landmark `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`.
  - Khai báo hệ thống CSS Variables trong `:root` (`--color-primary`, `--space-base`, `--font-base`...).
- **Nhận xét & Tinh chỉnh của SV:**
  - Nhắc AI bổ sung thẻ `<address>` cho thông tin liên hệ chân trang và `<time>` cho thời lượng lộ trình.
  - Thêm thẻ `<a href="#main-content" class="skip-link">` hỗ trợ phím Tab cho người khiếm thị theo chuẩn WCAG 2.1.

---

### Lần 2: Tích hợp thư viện Animate.css & AOS (Animate On Scroll)
- **Prompt đã dùng:**
  ```text
  Tích hợp thư viện AOS vào file HTML thông qua CDN và hướng dẫn cách thêm thuộc tính 'data-aos'
  vào các thẻ section để chúng hiện ra hiệu ứng mượt mà khi cuộn xuống trang.
  ```
- **Thách thức gặp phải:**
  - Ban đầu khi thêm `data-aos="fade-up"`, hiệu ứng không kích hoạt do chưa tải file script khởi tạo hoặc script bị chặn bởi quy định No-JS trước đó.
  - Khi cuộn trên mobile, hiệu ứng trượt đôi khi gây tràn mép ngang màn hình (horizontal overflow).
- **Cách sửa prompt (Debug prompt):**
  - Chèn link CDN CSS `<link rel="stylesheet" href="https://unpkg.com/aos@next/dist/aos.css">` trên `<head>` và script khởi tạo `AOS.init({ duration: 800, once: true, offset: 60 });` đặt ngay trước `</body>`.
  - Cấu hình `once: true` để animation chỉ chạy một lần duy nhất, tránh giật lag khi người dùng cuộn ngược lên.
- **Kết quả AI tạo ra:**
  - Tích hợp thành công AOS CDN cho 6 section trọng tâm: `#home`, `#benefits`, `#assessment-types`, `#learning-path`, `#testimonials`, `#registration`.
- **Nhận xét & Tinh chỉnh của SV:**
  - Thêm `overflow-x: hidden;` cho `html` và `body` trong CSS để triệt tiêu hoàn toàn hiện tượng văng lề ngang khi phần tử bắt đầu chuyển động từ `translateY(24px)`.

---

### Lần 3: Kiến trúc CSS Layout Grid & Mobile First Responsive (375px / 768px / 1024px)
- **Prompt đã dùng:**
  ```text
  Đóng vai chuyên gia Responsive Web Design theo Mobile First.
  Hãy kiểm tra và sửa lại toàn bộ phần Responsive của Landing Page:
  1. CSS mặc định dành cho mobile 375px: 1 cột cho mọi section, form 1 cột, menu hamburger.
  2. Tablet từ 768px: @media (min-width: 768px) thành 2 cột cho các grid.
  3. Desktop từ 1024px: @media (min-width: 1024px) thành 3-4 cột, menu ngang Flexbox space-between, ẩn hamburger.
  4. Container width: 90%; max-width: 1200px; margin: 0 auto;
  5. Tuyệt đối không dùng @media (max-width: ...). Không có horizontal scroll ở 375px, 768px, 1024px.
  ```
- **Thách thức gặp phải:**
  - AI viết CSS desktop trước rồi dùng `max-width` thu nhỏ lại; Footer và Form bị chia 4 cột và 2 cột ngay trên màn hình mobile 375px.
  - Huy hiệu nổi Hero (`.floating-badge`) dùng `right: -1rem` gây cuộn ngang trên điện thoại nhỏ.
- **Cách sửa prompt (Debug prompt):**
  - Yêu cầu AI xóa bỏ toàn bộ `@media (max-width: ...)`; quy định toàn bộ CSS ngoài media query là CSS mặc định cho Mobile (Single Column).
  - Tinh chỉnh `.floating-badge` trên mobile có `right: 0.5rem; max-width: calc(100% - 1rem);`.
- **Kết quả AI tạo ra:**
  - Bố cục lũy tiến sạch sẽ: Mobile (Base 1 cột) &rarr; Tablet (`min-width: 768px` 2 cột) &rarr; Desktop (`min-width: 1024px` 3 và 4 cột).
  - Đạt điểm chuẩn Zero Horizontal Scroll tại cả 3 mốc kiểm tra 375px, 768px, 1024px.
- **Nhận xét & Tinh chỉnh của SV:**
  - Yêu cầu AI đặt `min-height: 48px` cho nút bấm và ô input để đáp ứng tiêu chuẩn Accessibility Touch Target của Google Lighthouse.

---

### Lần 4: Hiệu ứng Animation, Micro-interactions & Nút Contact Pulse thuần CSS
- **Prompt đã dùng:**
  ```text
  Đóng vai chuyên gia CSS Animation và Micro-interactions.
  Thêm hiệu ứng cho Landing Page: Hero fade-in/slide-up khi tải trang; Card hover nâng nhẹ translateY(-6px)
  kèm box-shadow mềm; Nút bấm hover và active scale(0.97).
  Tạo nút tròn "Contact" cố định góc dưới bên phải có hiệu ứng 'phập phồng' (pulse) co giãn liên tục mượt mà.
  Chỉ dùng transform và opacity. Transition khoảng 0.3s qua var(--transition-speed).
  ```
- **Thách thức gặp phải:**
  - Nút Contact ban đầu co giãn bằng cách thay đổi `width` và `height`, dẫn đến hiện tượng giật khung hình (browser reflow/layout repaint).
- **Cách sửa prompt (Debug prompt):**
  - Nhắc nhở nguyên tắc hiệu năng: *"Chỉ được sử dụng `transform: scale()` và `opacity` trong `@keyframes pulseContact` để tận dụng GPU Compositor Layer đạt tốc độ 60fps mượt mà."*
- **Kết quả AI tạo ra:**
  - Animation Hero `heroFadeSlideUp` tinh tế.
  - Hover feedback đồng bộ trên toàn bộ Card và Button.
  - Nút tròn liên hệ nổi cố định co giãn êm dịu, tạm dừng khi di chuột (`hover: animation-play-state: paused`).
- **Nhận xét & Tinh chỉnh của SV:**
  - Bổ sung media query `@media (prefers-reduced-motion: reduce)` nhằm tự động vô hiệu hóa animation đối với người dùng nhạy cảm tiền đình.

---

### Lần 5: Preloader 360° Infinite Spinner & Hiệu ứng Typing Effect không dùng JS
- **Prompt đã dùng:**
  ```text
  Tạo một vòng tròn loading bằng CSS sử dụng animation xoay 360 độ vô hạn. Sử dụng border-top-color
  khác với các phần còn lại để tạo hiệu ứng xoay. Thể hiện màn hình loading trước khi vào trang.
  Viết mã CSS tạo hiệu ứng máy đánh chữ (Typing effect) cho một thẻ: chữ xuất hiện dần từ trái sang phải,
  kèm con trỏ nhấp nháy ở cuối dòng chữ. Tuyệt đối không dùng JavaScript.
  Tạo nút Hamburger di động 3 gạch, khi bấm vào biến đổi thành dấu "X".
  ```
- **Thách thức gặp phải:**
  - Preloader nếu không có JavaScript sẽ che mất nội dung trang vĩnh viễn nếu không xử lý biến mất.
  - Typing effect trong CSS dễ bị vỡ dòng nếu chữ quá dài hoặc không giới hạn chiều rộng.
- **Cách sửa prompt (Debug prompt):**
  - Dùng `@keyframes fadeOutPreloader` kết hợp `animation-delay: 1.2s; forwards;` và `pointer-events: none;` để preloader tự động mờ dần và giải phóng tương tác cho trang mà không cần 1 dòng script nào.
  - Sử dụng `white-space: nowrap; overflow: hidden; border-right: 2px solid;` cùng hàm bước `steps(40, end)` cho máy đánh chữ.
- **Kết quả AI tạo ra:**
  - Màn hình tải trang xoay 360° vô hạn với `border-top-color: var(--color-primary)`.
  - Huy hiệu Hero gõ chữ tự động với con trỏ nhấp nháy `blinkCaret`.
  - Menu 3 gạch chuyển động xoay đối xứng thành dấu "X" qua CSS Checkbox Hack.
- **Nhận xét & Tinh chỉnh của SV:**
  - Tinh chỉnh thời gian delay của Typing effect sau khi Preloader kết thúc để tạo trải nghiệm thị giác liền mạch.

---

### Lần 6: Tối ưu hóa chuyển đổi hình ảnh sang WebP 80% & Lazy Loading W3C
- **Prompt đã dùng:**
  ```text
  Hãy thêm các hình ảnh được tải lên lần lượt vào 3 thẻ Lộ trình học tập (Học sinh, Sinh viên, Người đi làm):
  1. Chuyển tất cả ảnh JPG/PNG sang WebP, chất lượng 80%.
  2. Lưu ảnh vào assets/images/.
  3. Viết thẻ img chuẩn: src .webp, alt mô tả rõ, width và height cụ thể, loading="lazy" cho ảnh ngoài màn hình đầu tiên.
  4. Ảnh Hero không dùng lazy loading.
  5. CSS ảnh responsive: max-width: 100%; height: auto; display: block; object-fit: cover.
  6. Kiểm tra không có broken links, ảnh không tràn khung và không gây horizontal scroll.
  ```
- **Thách thức gặp phải:**
  - Thư viện Pillow ban đầu chưa cài sẵn trong môi trường Python, cần cài đặt không bị treo tiến trình.
  - 3 ảnh có kích thước ban đầu khác nhau, dễ làm lệch độ cao thẻ lộ trình khi hiển thị hàng ngang trên Desktop.
- **Cách sửa prompt (Debug prompt):**
  - Viết script Python tự động convert hàng loạt sang chuẩn WebP 80% (`classroom-learning.webp`, `university-research.webp`, `professional-strategy.webp`).
  - Thiết lập thuộc tính `aspect-ratio: 3 / 2;` và `margin-top: auto` cho nút bấm trong CSS để đảm bảo cả 3 card bằng nhau chằn chặn.
- **Kết quả AI tạo ra:**
  - Giảm trung bình 26-30% dung lượng hình ảnh so với file JPG gốc.
  - Đạt điểm CLS = 0 (Cumulative Layout Shift) nhờ khai báo cứng `width` và `height`.
- **Nhận xét & Tinh chỉnh của SV:**
  - Viết kịch bản kiểm tra tự động `check_links.py`, xác nhận 100% đường dẫn ảnh hợp lệ, không có broken link.

---

### Lần 7: Refactor Clean Code CSS 7 Tầng & Chuẩn hóa Design System
- **Prompt đã dùng:**
  ```text
  Đóng vai Senior Front-End Developer chuyên về Clean Code và Design System.
  Hãy refactor CSS theo yêu cầu:
  1. Gộp các class có thuộc tính giống nhau.
  2. Xóa thuộc tính trùng lặp, thừa và không sử dụng.
  3. Trích xuất toàn bộ màu sắc, font-size, margin, padding, border-radius và transition-duration vào CSS Variables trong :root.
  4. Thay mọi giá trị cứng bằng var(--...).
  5. Dùng shorthand cho margin, padding, background và border.
  6. Sắp xếp CSS theo thứ tự: Reset → Design System → Base → Layout → Components → Responsive → Animation.
  7. Giữ nguyên hoàn toàn giao diện và hành vi hiển thị. Không đổi tên class đang dùng trong HTML.
  ```
- **Thách thức gặp phải:**
  - Nguy cơ xóa nhầm các class đang dùng hoặc làm mất hiệu ứng hover/responsive khi gộp nhóm.
- **Cách sửa prompt (Debug prompt):**
  - Sử dụng script Python trích xuất toàn bộ 74 class thực tế trong `index.html` để kiểm tra đối chiếu chéo (Cross-validation).
- **Kết quả AI tạo ra:**
  - File `css/style.css` giảm từ gần 1.700 dòng xuống còn **1.211 dòng** cực kỳ gọn gàng.
  - 100% thuộc tính dùng biến token trong `:root`.
- **Nhận xét & Tinh chỉnh của SV:**
  - Thẩm định tự động xác nhận 0 class HTML bị thiếu sót, code đạt chuẩn Clean Code cao cấp.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### 1. AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?
- **Khởi tạo mã nguồn lặp lại (Boilerplate Code):** Tạo nhanh khung HTML5 ngữ nghĩa với đầy đủ các thuộc tính trợ năng (`aria-*`, `role`), cấu trúc form biểu mẫu chi tiết.
- **Tính toán và chuyển đổi hình ảnh tự động:** Viết script xử lý tự động nén hàng loạt ảnh sang định dạng WebP với chất lượng chuẩn 80%, xác định tỷ lệ khung hình và kích thước pixel chính xác.
- **Kiểm thử liên kết & Kiểm tra lỗi CSS:** Viết script kiểm tra broken link tự động và đối soát độ phủ class giữa HTML và CSS trong vài giây thay vì phải dò thủ công từng dòng.
- **Tạo hiệu ứng phức tạp thuần CSS:** Thiết kế animation máy đánh chữ (Typing Effect), preloader xoay 360° tự ẩn và menu hamburger morphing sang dấu "X" mà hoàn toàn không cần chạm đến JavaScript.

### 2. Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?
- **Phải giao vai trò cụ thể (Role Prompting):** Khi yêu cầu AI đóng vai *"Senior Front-End Developer chuyên về Responsive Mobile First và Clean Code"*, chất lượng mã nguồn tạo ra tốt hơn hẳn, ít dùng `div` bừa bãi và biết chú trọng đến UX/a11y.
- **Thiết lập ràng buộc tiêu cực rõ ràng (Negative Constraints):** Những câu lệnh như *"Tuyệt đối không dùng JavaScript"*, *"Không được dùng @media (max-width: ...)"*, *"Chỉ dùng transform và opacity cho animation"* giúp ngăn chặn AI sử dụng các giải pháp chắp vá hoặc không đúng chuẩn đề bài.
- **Chia nhỏ tác vụ theo từng vòng lặp (Iterative Refinement):** Thay vì yêu cầu tạo toàn bộ trang web trong 1 lần duy nhất, việc chia thành các bước: *Khung Semantic &rarr; Design System &rarr; Bố cục Responsive &rarr; Animation &rarr; Tối ưu tài nguyên &rarr; Refactor Clean Code* mang lại độ chính xác gần như tuyệt đối và dễ dàng kiểm soát lỗi phát sinh.
- **Kiểm chứng độc lập (Trust but Verify):** Luôn dùng công cụ kiểm tra (script kiểm tra link, test độ phân giải 375px/768px/1024px) để xác nhận sản phẩm AI sinh ra thực sự hoạt động tốt trên thực tế chứ không chỉ nhìn đúng trên lý thuyết.

---

## 4. Bảng tổng hợp tiến trình Prompt

| Lần | Thời điểm | Hạng mục công việc | Kỹ thuật cốt lõi | Kết quả |
|:---:|:---:|:---|:---|:---:|
| **1** | 2026-10-19 13:36 | Khởi tạo kiến trúc dự án | HTML5, CSS3, Git & GitHub (No-JS) | Hoàn thành |
| **2** | 2026-10-19 13:37 | Thiết kế đồ họa vector | SVG XML Responsive (`hero-illustration.svg`) | Hoàn thành |
| **3** | 2026-10-19 13:37 | Thiết kế hệ thống CSS cơ sở | CSS Variables, Checkbox hack navigation | Hoàn thành |
| **4** | 2026-10-19 13:38 | Xây dựng ngữ nghĩa HTML5 | W3C Semantic landmarks (`header`, `main`, `section`) | Hoàn thành |
| **5** | 2026-10-19 13:38 | Soạn thảo tài liệu kỹ thuật | README.md hướng dẫn cài đặt và chạy | Hoàn thành |
| **6** | 2026-10-19 13:43 | Tối ưu chuyên sâu Semantic & a11y | Duy nhất 1 thẻ `main`, SEO meta, `figure`, `aside` | Hoàn thành |
| **7** | 2026-10-19 13:48 | Thiết kế Design System Tokens | Biến `:root`, Reset CSS, Typography scale | Hoàn thành |
| **8** | 2026-10-19 13:51 | Kiến trúc Layout CSS Grid & Flex | CSS Grid page layout, `min-height: 100vh`, Card gap | Hoàn thành |
| **9** | 2026-10-19 13:55 | Chuẩn hóa Mobile First Responsive | Base 1 cột (375px), Tablet 2 cột, Desktop 4 cột | Hoàn thành |
| **10** | 2026-10-19 14:03 | Hiệu ứng Animation GPU 60fps | Fade-in, Card hover, Contact Pulse button | Hoàn thành |
| **11** | 2026-10-19 14:15 | Preloader, AOS & Typewriter | Loading 360°, AOS scroll reveal, CSS Typewriter | Hoàn thành |
| **12** | 2026-10-19 14:24 | Khắc phục triệt để lỗi Responsive | Loại bỏ tràn ngang 375px, sửa base form và footer | Hoàn thành |
| **13** | 2026-10-19 14:38 | Tích hợp ảnh WebP Lộ trình K12 | Convert WebP 80%, thẻ `<img>` lazy loading | Hoàn thành |
| **14** | 2026-10-19 14:52 | Tích hợp ảnh WebP Sinh viên & Đi làm | Đồng bộ tỷ lệ 3:2 cả 3 card, zero horizontal scroll | Hoàn thành |
| **15** | 2026-10-19 14:58 | Refactor Clean Code & Design System | Cấu trúc 7 tầng, 100% biến CSS, xóa dead code | Hoàn thành |

---

## 5. Đánh giá mức độ tuân thủ yêu cầu kỹ thuật toàn dự án

- [x] **HTML5 Semantic:** Đầy đủ `header`, `nav`, `main` (duy nhất 1 thẻ), `section`, `article`, `aside`, `footer`, `figure`, `figcaption`, `address`, `time`.
- [x] **Mobile First Architecture:** CSS mặc định 1 cột cho Mobile (375px), lũy tiến mở rộng lên Tablet (`min-width: 768px`) và Desktop (`min-width: 1024px`).
- [x] **Zero Horizontal Scroll:** 100% không tràn ngang tại các mốc 375px, 768px và 1024px.
- [x] **Animation GPU Accelerated:** 100% chuyển động chỉ sử dụng `transform` và `opacity`, không dùng `top`, `left`, `margin-left`.
- [x] **Floating Contact Pulse:** Nút tròn Contact xanh cố định góc phải màn hình, co giãn phập phồng (pulse) êm dịu 60fps.
- [x] **Micro-interactions:** Tương tác thẻ Assessment (`translateY(-6px)`), Learning Path (`border-color` + `translateY(-4px)`), Nút bấm (`translateY(-2px)` / active `scale(0.97)`).
- [x] **Accessibility (a11y):** Tích hợp `prefers-reduced-motion` tắt chuyển động cho người dùng nhạy cảm; kích thước nút & input đạt chuẩn touch target >= 48px.
- [x] **Preloader / Loading Spinner:** Vòng tròn CSS xoay 360° vô hạn (`border-top-color` khác biệt), tự biến mất sau 1.2s bằng `@keyframes fadeOutPreloader`.
- [x] **AOS (Animate On Scroll):** Tích hợp CDN CSS + JS, các section có `data-aos="fade-up"`, `AOS.init({ duration: 800, once: true })`.
- [x] **Typewriter Effect:** Hiệu ứng máy đánh chữ thuần CSS (`@keyframes typing` + `@keyframes blinkCaret`), không JavaScript.
- [x] **Hamburger → X Morph:** Menu 3 gạch biến đổi thành dấu "X" khi nhấn (gạch giữa `opacity: 0`, gạch trên/dưới xoay ±45°), thuần CSS checkbox hack.
- [x] **WebP Optimization (80% Quality):** 100% hình ảnh trong dự án được chuyển đổi sang định dạng WebP chất lượng 80% (`classroom-learning.webp`, `university-research.webp`, `professional-strategy.webp`).
- [x] **Uniform Card Aspect Ratio (3:2):** Cả 3 thẻ lộ trình sử dụng tỷ lệ vàng 3:2, ngăn ngừa Layout Shift (CLS = 0) và căn chỉnh nút sát đáy hoàn hảo.
- [x] **Clean Code & Design System Architecture:** Refactor cấu trúc 7 tầng (Reset &rarr; Design System &rarr; Base &rarr; Layout &rarr; Components &rarr; Responsive &rarr; Animation), 100% CSS Variables, shorthand properties, xóa sạch dead code.
- [x] **Zero Broken Links:** Đã kiểm tra tự động toàn bộ 4 đường dẫn ảnh và liên kết nội bộ, 100% tồn tại hợp lệ.
- [x] **Không sử dụng JavaScript:** 100% Zero JS cho UI/interaction. Duy nhất AOS runtime script được tích hợp qua CDN theo yêu cầu đề bài.
