# DELTA FORCE — Website tìm hiểu (HTML5 + CSS3 thuần)

Website giới thiệu game bắn súng chiến thuật **Delta Force**, làm bằng **HTML5 + CSS3 thuần**,
**không dùng JavaScript**. Toàn bộ hiệu ứng tương tác (menu trượt, slideshow, lightbox) được làm
bằng kỹ thuật CSS (`:target`, `:checked ~`, `:hover`).

> Đây là website **làm để học**, không phải trang chính thức của nhà phát hành.
> Fan-made website for study purposes. Delta Force and related assets are property of TiMi Studio Group / Tencent.

---

## 1. Cấu trúc thư mục

```
Source/
├── index.html              # Trang chủ (9 khối nội dung)
├── modes.html              # Trang chi tiết 3 chế độ chơi + bảng so sánh
├── README.md               # File này
├── css/
│   ├── style.css           # Toàn bộ style desktop + kỹ thuật CSS thuần
│   └── responsive.css      # Media queries: 992px / 768px / 480px
└── images/
    ├── hero-1.svg          # Ảnh banner 1 (1600×900)
    ├── hero-2.svg          # Ảnh banner 2 (1600×900)
    ├── hero-3.svg          # Ảnh banner 3 (1600×900)
    ├── about-main.svg      # Ảnh lớn phần Giới thiệu (1200×900)
    ├── about-detail.svg    # Ảnh nhỏ kèm khối màu nhấn (600×600)
    ├── class-assault.svg   # Ảnh lớp Điều phương (800×1000)
    ├── class-engineer.svg  # Ảnh lớp Kỹ sư (800×1000)
    ├── class-support.svg   # Ảnh lớp Hỗ trợ (800×1000)
    ├── class-recon.svg     # Ảnh lớp Trinh sát (800×1000)
    ├── mode-warfare.svg    # Ảnh chế độ Warfare (900×600)
    ├── mode-operations.svg # Ảnh chế độ Operations (900×600)
    ├── mode-campaign.svg   # Ảnh chế độ Black Hawk Down (900×600)
    ├── gallery-1.svg       # Ảnh thư viện 1 (900×675)
    ├── gallery-2.svg       # Ảnh thư viện 2 (900×675)
    ├── gallery-3.svg       # Ảnh thư viện 3 (900×675)
    ├── gallery-4.svg       # Ảnh thư viện 4 (900×675)
    ├── gallery-5.svg       # Ảnh thư viện 5 (900×675)
    ├── gallery-6.svg       # Ảnh thư viện 6 (900×675)
    └── map-mogadishu.svg   # Bản đồ tĩnh vùng Mogadishu (900×560)
```

**Không có thư mục `js/`** — đây là chủ ý, vì đề bài lập trình web cơ bản không yêu cầu JavaScript.

---

## 2. Cách chạy

1. Mở thư mục `Source/`.
2. Nhấp đúp vào **`index.html`** để mở bằng trình duyệt (Chrome, Edge, Cốc Cốc...).

Không cần máy chủ web, không cần cài đặt, không cần mạng (ngoại trừ Google Fonts — nếu mất mạng
thì chữ sẽ tự dùng font dự phòng có sẵn trong máy, trang vẫn hiển thị bình thường).

Có thể dùng VS Code cài extension **Live Server** rồi mở `index.html` để thấy hiệu ứng chuyển
slide mượt hơn.

---

## 3. Ánh xạ yêu cầu Y1 – Y4

### Y1 — Nhúng nội dung, liên kết tệp, nền tảng

| Yêu cầu | Thực hiện ở đâu |
|---|---|
| Nhúng nội dung văn bản, hình ảnh, âm thanh/video | `index.html` (28 thẻ `<img>`), `modes.html` (3 thẻ `<img>`) |
| Liên kết tới tệp ngoài | `<a href="modes.html#che-do-1">` … `<a href="index.html#tinh-nang">` |
| Liên kết trong trang (neo `#`) | Nội dung: `#tinh-nang`, `#gioi-thieu`, `#lop-nhan-vat`, `#che-do`, `#thu-vien`, `#lien-he`, `#ban-do` |
| **CSS ngoài (external)** | `index.html` + `modes.html` gọi `css/style.css` và `css/responsive.css` qua thẻ `<link>` |
| **CSS nội tuyến (internal)** | Thẻ `<style>` nằm trong `<head>` của **`modes.html`** (khoảng 200 dòng) |
| **CSS nội tuyến trực tiếp (inline)** | Thuộc tính `style="border-left-color: #7d8f3a;"` trên thẻ `<p class="note">` của `modes.html` — có chú thích `<!-- Y1: ví dụ INLINE CSS -->` ngay phía trên |
| Nhúng bản đồ Google / video YouTube | Không dùng iframe (cần mạng). Thay bằng bản đồ SVG tĩnh tự vẽ `images/map-mogadishu.svg` |

### Y2 — Định dạng nội dung

| Yêu cầu | Thực hiện ở đâu |
|---|---|
| Định dạng chữ, định dạng đoạn, tiêu đề | `h1`–`h3`, `<p>`, `.hero__title`, `.section__title`, `.about__subtitle` |
| Định dạng ảnh | `.class-card__media img`, `.gallery__item img`, `width` + `height` + `alt` cho mọi ảnh |
| Tạo khung / đường viền | `.btn` viền kép (`border` + `outline` + `outline-offset: 4px`), `.lightbox`, `.features__item` |
| Mô hình hộp (Box Model) | Chú thích `/* Y2: box model — content / padding / border / margin */` trong `.hero__slide`, `.class-card`, `.btn` |
| Nền, màu chữ | Biến CSS trong `:root` của `style.css` |
| Hộp chứa, đơn vị tương đối | `px`, `rem`, `%`, `vw/vh`, `clamp()` cho `.hero__title` |
| Float | `modes.html` — `.mode-detail__float { float: left; width: 300px; }` |
| Clearfix | `modes.html` — `.mode-detail__prose::after { content: ""; display: block; clear: both; }` |
| Vị trí: `position` | `fixed` (nút hamburger), `absolute` (radio ẩn của slideshow, các icon trong hero), `sticky` (thanh nhảy nhanh `.jump-nav` ở `modes.html`) |
| Hiệu ứng chuyển động | `transition` trong `.btn`, `.card`, `.gallery__item`, `.lightbox` (0.25s – 0.5s) |
| Keyframes | `@keyframes fade-in`, `rise-in`, `hero-zoom`, `pulse-dot` trong `style.css` |
| Hover ảnh phóng to | `.class-card__media { overflow: hidden; }` + `.class-card__media img:hover { transform: scale(1.08); }` (áp dụng cả cho `.gallery__item`, `.hero__slide`) |

### Y3 – Cấu trúc bố cục

| Yêu cầu | Thực hiện ở đâu |
|---|---|
| Flexbox | Menu điều hướng (`.nav__list`), khối **Tính năng** (`.features__list` dùng `display: flex`), Footer (`.footer__social`), căn giữa nội dung |
| CSS Grid | Khối **Lớp nhân vật** (`.classes__list` — 4 cột), **Chế độ chơi** (`.modes__list` — 3 cột), **Thư viện** (`.gallery__list` — 3 cột) |
| Float + clearfix | `modes.html` — ảnh nổi bên trái đoạn văn bản, `::after { clear: both }` |
| `position` | `fixed` / `absolute` / `sticky` — xem bảng Y2 |

### Y4 — Nâng cao

| Yêu cầu | Thực hiện ở đâu |
|---|---|
| Menu (hamburger) trượt vào | `.site-nav:target { transform: translateX(0); }` — `:target` thay cho JavaScript |
| Slideshow ảnh tự chuyển | 3 radio `name="hero-slide"` + `#s1:checked ~ .hero__slides .hero__slide--2` (đổi slide bằng nút `<label>`) |
| Zoom ảnh khi rê chuột | `overflow: hidden` + `transform: scale()` |
| Lightbox (xem ảnh phóng to) | `.lightbox:target` — 4 lightbox cho **Lớp nhân vật**, 6 lightbox cho **Thư viện** (có nút *Ảnh trước / Ảnh sau*) |
| Bản đồ | `images/map-mogadishu.svg` — bản đồ SVG tĩnh, có điểm Mogadishu, hướng bắc, tỷ lệ |
| Biểu mẫu (form) | `index.html` — `<label for>`, `required`, `type="email"`, `placeholder`, `:focus-visible` |
| Hiệu ứng xuất hiện khi tải trang | `@keyframes` + `animation-delay` tăng dần theo `:nth-child` |
| Responsive (mobile-first) | `css/responsive.css`: `@media (max-width: 992px / 768px / 480px)`. Ở ≤768px: Tính năng / Lớp nhân vật / Chế độ chơi / Thư viện về **1 cột**, phần Giới thiệu xếp dọc, bảng so sánh cuộn ngang trong `.table-wrap` |

---

## 4. Cách làm các hiệu ứng "tương tác" mà không dùng JavaScript

Đây là phần kỹ thuật đáng chú ý nhất của bài:

| Hiệu ứng | Kỹ thuật |
|---|---|
| Mở/đóng menu | `<a href="#menu">` mở, `.site-nav:target` → trượt vào. Bấm bất kỳ link menu nào cũng đổi `#target` nên **menu tự đóng** |
| Chuyển slide | 3 `<input type="radio" name="hero-slide">` ẩn, đặt **trước** khối slide; nút bấm là `<label for="sN">`; CSS `#sN:checked ~ .hero__slides .hero__slide--N { opacity: 1 }` |
| Chấm (dots) | `<label for="sN">` + `#sN:checked ~ .hero__dots .hero__dot--N { background: var(--accent) }` |
| Lightbox | `<a href="#anh-1">` mở, `.lightbox:target { opacity: 1; visibility: visible }`, nút đóng `href="#thu-vien"` |
| Ảnh trước / ảnh sau | Mỗi lightbox có 2 `<a href="#anh-N">` trỏ tới lightbox kế tiếp/lùi, vòng tròn 1 → 6 → 1 |

**Lưu ý về bàn phím (accessibility):** các nút `<label>` (chấm slideshow, mũi tên trước/sau)
bấm bằng chuột được. Người dùng bàn phím sử dụng được nhóm radio ẩn bằng cách nhấn **Tab**
đến vùng banner rồi dùng **phím mũi tên ← →**. Trang cũng có `:focus-visible` cho mọi phần tử
nhận focus và tuân thủ `prefers-reduced-motion`.

---

## 5. Ảnh và nội dung cần sinh viên TỰ THAY

### 5.1. Ảnh — toàn bộ đang là **placeholder SVG tự vẽ**

Cả 19 file trong `images/` là **ảnh SVG phong cách quân sự do tôi tự vẽ bằng code** (nền tối,
lưới, đường đồng mức, khung góc, chữ stencil), **không phải ảnh chụp hay ảnh chính thức của game**.
Mục đích: tránh vi phạm bản quyền và tránh ảnh có watermark của bên thứ ba.

| Cần thay | File | Kích thước nên dùng |
|---|---|---|
| Ảnh banner | `hero-1.svg`, `hero-2.svg`, `hero-3.svg` | 1600 × 900 |
| Ảnh phần Giới thiệu | `about-main.svg`, `about-detail.svg` | 1200 × 900 / 600 × 600 |
| Ảnh lớp nhân vật | `class-assault.svg`, `class-engineer.svg`, `class-support.svg`, `class-recon.svg` | 800 × 1000 |
| Ảnh chế độ chơi | `mode-warfare.svg`, `mode-operations.svg`, `mode-campaign.svg` | 900 × 600 |
| Ảnh thư viện | `gallery-1.svg` … `gallery-6.svg` | 900 × 675 |
| Bản đồ | `map-mogadishu.svg` | 900 × 560 |

**Cách thay:** đặt ảnh mới (`.jpg` hoặc `.webp`) vào `images/` với **tên viết thường, không dấu,
không khoảng trắng** (ví dụ `hero-1.jpg`), rồi sửa đường dẫn `src` trong HTML và **giữ nguyên**
thuộc tính `width`/`height` (hoặc dùng đúng tỉ lệ) để trang không bị nhảy layout.

### 5.2. Ảnh SVG không cần sửa mã

`map-mogadishu.svg` có sẵn `<title>` và `<desc>` (mô tả cho screen reader). Nếu thay bằng
Leaflet ở phần mở rộng (mục 8) thì xoá `<img id="ban-do-anh">` và thêm `<div id="ban-do-nhung">`.

### 5.3. Nội dung chữ nên bổ sung/thay

| Vị trí | Trong file | Ghi chú |
|---|---|---|
| Họ tên, MSSV, lớp ở chân trang | `index.html`, khối `.footer__bottom` | **Sinh viên tự điền** — hiện để chữ `TODO` |
| Email / số điện thoại / địa chỉ liên hệ | `index.html`, khối `.contact__list` | Đang là dữ liệu giả (vd `hoangvan.a1234@fpt.edu.vn`, `0901 234 567`) — thay bằng thông tin thật hoặc thông tin trường |
| Tên chiến binh (operator) | `index.html` khối **Lớp nhân vật**; `modes.html` | **Cố ý không ghi tên operator** vì danh sách tên thay đổi theo từng đợt cập nhật. Nếu muốn thêm, phải tra cứu trang chính thức hoặc Steam rồi ghi rõ nguồn |
| Tên vũ khí cụ thể | `index.html`, `modes.html` | **Không ghi** — tương tự lý do trên |
| Thống kê người chơi, giá, ngày phát hành cụ thể | — | **Không ghi** vì số liệu thay đổi liên tục. Nếu cần, ghi kèm ngày cập nhật |

---

## 6. Giả định và những gì CHƯA được kiểm chứng

### 6.1. Thông tin game đã kiểm chứng (dùng trong trang)

| Thông tin | Nguồn kiểm chứng |
|---|---|
| Nhà phát triển **Team Jade**, nhà xuất bản **TiMi Studio Group** (Tencent) | Trang Steam (App 2507950), Wikipedia *Delta Force (2025 video game)* |
| Game bắn súng chiến thuật **miễn phí** (free-to-play) | Steam, trang chính thức playdeltaforce.com |
| Thuộc dòng game Delta Force nổi tiếng của **NovaLogic (1998–2003)** | Wikipedia |
| Chế độ **Warfare**: 32 vs 32, bản đồ trải rộng trên cạn/biển/trời, xe tăng – trực thăng Black Hawk – tàu đổ bộ, có luật **Tấn công/Phòng thủ (A/D)** và **Chiếm đỉnh (King of the Hill)** | Bài giới thiệu của Epic Games (21/02/2025), trang chính thức |
| Chế độ **Operations**: mang vật phẩm vào, nhặt đồ lợi, sống sót để rút; PvE và PvP; tiểu đội 3 người | Trang chính thức, Epic Games |
| Chế độ **Black Hawk Down**: làm lại chiến dịch đồng đội, **7 nhiệm vụ**, tối đa **4 người chơi**, chọn vai trò chuyên môn (vật tư/y tế), bối cảnh **Mogadishu năm 1993** (Operation Gothic Serpent), có dòng truyện mới về **GTI (Global Threat Initiative)**, ra mắt tháng 2/2025 dưới dạng bổ sung miễn phí | Epic Games, Wikipedia, trang chính thức, Steam (App 2918370) |
| Chế độ phụ **Hot Zone**: 3 vs 3 vs 3, thắng bằng cách hạ hết đội địch hoặc tải **MandelCell**, đội nào thắng 3 ván là thắng | Trang chính thức playdeltaforce.com |
| 4 lớp nhân vật: **Điều phương (Assault)**, **Kỹ sư (Engineer)**, **Hỗ trợ (Support)**, **Trinh sát (Recon)** | Trang chính thức |
| Nền tảng **PC, PlayStation 5, Xbox Series X\|S** (thêm iOS/Android) | Steam, trang chính thức |
| Mốc thời gian: mở đá thử **PC tháng 12/2024**; ra mắt đầy đủ **PC/iOS/Android 21/04/2025**; **PS5 + Xbox 19/08/2025** | Wikipedia, thông báo của nhà phát hành |
| Bản đồ trên trang web dùng toạ độ **Mogadishu 2.0469, 45.3182** | Bối cảnh truyện *Black Hawk Down* (Mogadishu, Somalia) |

### 6.2. Những gì **CHƯA xác minh** / **cố ý không ghi**

- **Tên các operator cụ thể** và **tên vũ khí**: danh sách thay đổi theo từng đợt cập nhật, không
  ghi vào trang để tránh sai. Nếu bài cần, hãy tra **playdeltaforce.com** hoặc trang Steam rồi ghi kèm nguồn.
- **Nội dung hình ảnh trong ảnh placeholder**: vì ảnh là SVG tự vẽ, nội dung bên trong chỉ là hình học
  trang trí, **không mô tả thật** game.
- **Bản đồ `map-mogadishu.svg`** là sơ đồ minh hoạ tự vẽ, **không phải bản đồ địa lý chính xác**.
- **Ảnh chụp thật của game**: không dùng vì không tải được từ nguồn công khai và có rủi ro bản quyền.
- Thông tin "gần đây nhất" (số người chơi trực tuyến, đánh giá trên Steam, giá DLC): **không ghi** vì
  số liệu thay đổi theo ngày.
- **Không kiểm tra được phần hiển thị hình ảnh** trên máy khác: kiểm thử bằng Chrome headless ở các
  bề rộng 360 / 480 / 820 / 1024 / 1440 px, đều không tràn ngang và ảnh tải đủ; tuy nhiên **máy ảnh thực**
  không kiểm tra được nên nên mở thử trên máy tính và điện thoại thật trước khi nộp.

---

## 7. Bảng màu và font

Tất cả biến nằm trong `:root` của `css/style.css`:

| Biến | Giá trị | Ý nghĩa |
|---|---|---|
| `--bg-dark` | `#0b0e10` | Nền tối chính |
| `--panel` | `#171d21` | Khối nền tối phụ |
| `--panel-2` | `#1f262b` | Bảng màu khối tối |
| `--light-bg` | `#e9edf0` | Nền sáng (phần Liên hệ) |
| `--accent` | `#f2a900` | **Màu nhấn duy nhất** (hổ phách – quân sự) |
| `--accent-dark` | `#b87f00` | Nhấn khi rê chuột |
| `--accent-ink` | `#8a5f00` | Chữ màu nhấn trên nền sáng (đảm bảo tương phản) |
| `--olive` | `#7d8f3a` | Màu phụ (viền, sọc kẻ) |
| `--text` | `#e8ecef` | Chữ trên nền tối |
| `--text-muted` | `#a9b6bf` | Chữ phụ trên nền tối |
| `--text-dark` | `#14181a` | Chữ trên nền sáng |
| `--radius` / `--radius-sm` | `16px` / `12px` | Bo góc |

Font (tải từ Google Fonts):
- Tiêu đề: **Rajdhani**
- Chữ thân: **Barlow**
- Dòng chữ "script"/stencil: **Black Ops One**

Đều có font dự phòng `system-ui, 'Segoe UI', sans-serif` nên không vỡ khi offline.

---

## 8. Mở rộng nâng cao (giai đoạn tiếp theo — cần JavaScript)

Bài này dừng ở HTML + CSS. Khi học tới phần **Lập trình web nâng cao**, có thể thêm:

1. **Slideshow tự động chạy** — hiện tại phải bấm chấm hoặc mũi tên. Thêm `setInterval()` để tick
   radio, hoặc thêm `animation` có `animation-delay` khác nhau cho mỗi slide.
2. **Bản đồ tương tác** — thay `images/map-mogadishu.svg` bằng **Leaflet + OpenStreetMap** qua CDN,
   đặt marker tại `2.0469, 45.3182`.
3. **Lightbox nâng cao** — hiện tại mỗi ảnh là một `id` riêng. Dùng JS để gom về 1 modal duy nhất,
   thêm zoom, phím ← → và Esc.
4. **Kiểm tra biểu mẫu bằng JS** — thêm thông báo lỗi/đã gửi (hiện dùng `required` và
   `type="email"` của HTML5, và có dòng `.form__hint` giải thích đây là biểu mẫu demo).
5. **Khung chat trôi (chatbox)** — gợi ý từ khóa: `free, modes, platform, warfare, operations,
   campaign, classes`.
6. **Menu hamburger** — chuyển từ `:target` sang JS để thêm hiệu ứng mở/đóng mượt hơn, khóa
   cuộn trang và trả focus về nút.
7. **Menu di chuyển theo cuộn trang** — thay `fixed` bằng `sticky` + JS điều chỉnh.

---

## 9. Ghi chú kỹ thuật

- **Không dùng `!important`** ở bất kỳ đâu.
- Tên lớp theo kiểu **BEM** đơn giản: `.mode-card__title`, `.class-card__media`, `.hero__slide--2`.
- Đường dẫn tương đối (`css/style.css`, `images/hero-1.svg`), tên tệp viết thường, không dấu, không khoảng trắng.
- Mỗi trang có **đúng 1 thẻ `<h1>`**, thứ tự tiêu đề không nhảy cấp.
- Mọi `<img>` đều có `alt` mô tả + `width` + `height`.
- Mọi `<input>` trong form đều có `<label for>` trỏ đúng `id`.
- Có `<meta name="viewport">` và `<meta name="description">` trên cả hai trang.
- Nhúng video/iframe bên ngoài đã bị loại bỏ hoàn toàn để trang chạy được khi **mở trực tiếp từ ổ đĩa**
  (một số trình duyệt chặn iframe khi tải qua `file://`).

---

## 10. Bản quyền

- Toàn bộ mã HTML/CSS trong bài này do sinh viên viết, dùng để học và nộp bài.
- **Delta Force** là thương hiệu của **TiMi Studio Group / Tencent**. Tên và các tài sản liên quan
  thuộc về chủ sở hữu của họ; website này **không** do họ bảo trợ hay liên kết với họ.
- Ảnh trong `images/` là **hình vẽ SVG tự tạo**, không phải tài sản của nhà phát hành.

> Fan-made website for study purposes. Delta Force and related assets are property of TiMi Studio Group / Tencent.