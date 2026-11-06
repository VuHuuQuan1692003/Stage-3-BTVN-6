# Đặc tả thiết kế kỹ thuật: Trang web Rikkei Coffee (BTVN 6)

- **Ngày tạo**: 2026-11-06
- **Trạng thái**: Chờ phê duyệt (Pending Review)
- **Mục tiêu**: Xây dựng giao diện web Rikkei Coffee chuẩn semantic HTML5, CSS hiện đại, responsive chính xác theo ảnh mẫu 1280px & 360px với dung sai dưới 2px (0.125rem), đáp ứng trọn vẹn 9 tiêu chuẩn đầu ra.

---

## 1. Kiến trúc tổng thể & Cấu trúc tệp tin

### 1.1 Tổ chức tệp
```
Stage-3-BTVN-6/
├── index.html       # Cấu trúc HTML5 semantic, đầy đủ chú thích tiếng Việt
├── style.css        # Toàn bộ CSS ngoại bộ, CSS Variables, Responsive & Tương tác
└── docs/            # Tài liệu thiết kế & kế hoạch
```

### 1.2 Cấu trúc HTML5 Semantics & Phân cấp Tiêu đề (Yêu cầu 5 & 8)
- Cấu trúc cây DOM chuẩn:
  - `<header class="site-header">` (Chứa logo thương hiệu và thanh điều hướng `<nav>`)
  - `<main class="main-content">`:
    - `<section class="hero-section">`:
      - Phụ đề: `<p class="hero-subtitle">Khuyến mãi mùa hè</p>`
      - Tiêu đề cấp 1 duy nhất: `<h1 class="hero-title">Mùa hè sảng khoái, giảm đến 30%</h1>`
      - Mô tả thời gian áp dụng: `<p class="hero-desc">...</p>`
      - Nút hành động: `<a href="#combo" class="btn btn-hero">Nhận ưu đãi</a>`
    - `<section class="combo-section" id="combo">`:
      - Tiêu đề cấp 2: `<h2 class="section-title">Combo mùa hè</h2>`
      - Lưới combo: `<div class="combo-grid">` chứa 4 thẻ `<article class="combo-card">`:
        - Khối ảnh: `<div class="combo-image">`
        - Nhãn giảm giá: `<span class="discount-badge">-20%</span>` (nằm đè góc trên bên phải khối ảnh)
        - Tiêu đề cấp 3: `<h3 class="combo-name">Combo Sáng nhẹ</h3>`
        - Mô tả: `<p class="combo-desc">Cà phê sữa và bánh croissant</p>`
        - Giá gốc: `<p class="combo-old-price">Giá gốc 54.000 đ</p>`
        - Giá ưu đãi: `<p class="combo-price">43.200 đ</p>`
    - `<section class="register-section" id="register">`:
      - Tiêu đề cấp 2: `<h2 class="section-title">Đăng ký nhận mã ưu đãi</h2>`
      - Thẻ Form: `<form class="register-card" novalidate>`:
        - Nhóm Họ tên: `<label for="full-name">Họ tên</label>` + `<input id="full-name" name="fullName" type="text" placeholder="Nguyễn Văn An" required>`
        - Nhóm Email: `<label for="email">Email</label>` + `<input id="email" name="email" type="email" placeholder="ban@example.com" required>`
        - Nhóm Chi nhánh: `<label for="branch">Chi nhánh</label>` + `<select id="branch" name="branch">...`
        - Nút gửi: `<button type="submit" class="btn btn-submit">Nhận mã ưu đãi</button>`
  - `<footer class="site-footer">`:
    - Khung viền chứa thông tin liên hệ: `<div class="footer-card">`
      - Tên thương hiệu: `<p class="footer-brand">Rikkei Coffee</p>`
      - Địa chỉ, giờ mở cửa, hotline.
- **Chú thích mã nguồn (Yêu cầu 8)**:
  - HTML: Mỗi vùng chính đều có comment phân định rõ ràng (ví dụ: `<!-- ==================== ĐẦU TRANG (HEADER) ==================== -->`).
  - CSS: Mỗi khối CSS chính có 1 dòng chú thích tiếng Việt ngắn nêu rõ khối dựng cho phần nào của trang.

---

## 2. Hệ thống CSS Custom Properties & Thiết kế Chi tiết (Yêu cầu 6)

### 2.1 Bảng màu (Color Palette)
- `--color-header-bg`: `#793c12` (Màu nâu ấm thanh header)
- `--color-hero-bg`: `#49250f` (Màu nâu cafe đậm phần mở đầu)
- `--color-hero-tag`: `#d88439` (Màu cam sáng phụ đề hero)
- `--color-hero-desc`: `#d9c8bc` (Màu be sáng chữ mô tả)
- `--color-accent`: `#d97706` (Màu cam nút "Nhận ưu đãi" & nhãn giảm giá)
- `--color-accent-hover`: `#b45309` (Màu cam sẫm khi hover)
- `--color-combo-bg`: `#fcf9f4` (Màu nền kem nhạt của phần combo)
- `--color-card-bg`: `#ffffff` (Nền thẻ combo & thẻ form)
- `--color-card-border`: `#ece4da` (Viền thẻ combo)
- `--color-card-img`: `#e1d1be` (Màu placeholder ảnh combo)
- `--color-badge-text`: `#281508` (Màu chữ đen nâu trên nhãn giảm giá và nút hero)
- `--color-price`: `#8c3e0d` (Màu giá ưu đãi)
- `--color-price-old`: `#776c62` (Màu xám nâu giá gốc)
- `--color-register-bg`: `#e3d6c6` (Màu nền be cát của khu vực đăng ký)
- `--color-form-border`: `#dcd2c6` (Viền các ô input/select)
- `--color-btn-submit`: `#6c330c` (Màu nâu nút submit form)
- `--color-btn-submit-hover`: `#542608` (Màu nâu đậm khi hover submit)
- `--color-footer-bg`: `#1f1611` (Màu nâu đen chân trang)
- `--color-footer-border`: `#36281e` (Viền khung chân trang)
- `--color-footer-text`: `#b0a296` (Màu chữ nhạt chân trang)
- `--color-text-dark`: `#27160b` (Màu chữ tối tiêu đề và nội dung)
- `--color-text-muted`: `#685a50` (Màu chữ mô tả phụ)

### 2.2 Khoảng cách (Spacing) & Bo góc (Border Radius)
- Khoảng cách:
  - `--spacing-xs`: `0.25rem` (4px)
  - `--spacing-sm`: `0.5rem` (8px)
  - `--spacing-md`: `1rem` (16px)
  - `--spacing-lg`: `1.5rem` (24px)
  - `--spacing-xl`: `2rem` (32px)
  - `--spacing-2xl`: `3rem` (48px)
- Bo góc:
  - `--radius-sm`: `4px`
  - `--radius-md`: `8px`
  - `--radius-lg`: `12px`
  - `--radius-xl`: `16px`
  - `--radius-full`: `9999px`

---

## 3. Thiết kế Responsive & Các Hành vi Đặc thù

### 3.1 Thanh đầu trang dính & Menu linh hoạt (Yêu cầu 2 & 3)
- `position: sticky; top: 0; z-index: 1000;` đảm bảo thanh đầu trang luôn ở trên cùng màn hình khi cuộn trang, đè lên tất cả các phần tử khác, bao gồm cả nhãn giảm giá `discount-badge`.
- **Ở khung nhìn < 768px (bao gồm 360px)**:
  - Các liên kết menu `.nav-list` được ẩn (`display: none;`).
  - Biểu tượng menu ba gạch `.hamburger-btn` hiển thị ở góc phải (`display: flex;`). Nút có `aria-label="Menu"` để hỗ trợ tiếp cận (accessibility).
- **Ở khung nhìn >= 768px (bao gồm 1280px)**:
  - Biểu tượng menu ba gạch ẩn đi (`display: none;`).
  - Các liên kết menu `.nav-list` hiển thị đầy đủ (`display: flex; gap: var(--spacing-lg);`).

### 3.2 Lưới combo tự co giãn & Nhãn giảm giá đè góc (Yêu cầu 4 & 9)
- Khối ảnh `.combo-image`: `position: relative; border-radius: var(--radius-md); background: var(--color-card-img); aspect-ratio: 16 / 10;`.
- Nhãn giảm giá `.discount-badge`: `position: absolute; top: 8px; right: 8px; z-index: 2; border-radius: var(--radius-sm); padding: 4px 10px; font-weight: 700;`. Đè chính xác góc trên bên phải của khối ảnh.
- Lưới hiển thị `.combo-grid`:
  - Mobile (< 576px): `grid-template-columns: 1fr;`
  - Tablet (576px - 991px): `grid-template-columns: repeat(2, 1fr);`
  - Desktop (>= 992px): `grid-template-columns: repeat(4, 1fr);`
  - Thiết lập `align-items: stretch;` kết hợp thẻ combo `.combo-card` có `display: flex; flex-direction: column; height: 100%;`.
  - Phân bổ nội dung thẻ: Tiêu đề `.combo-name` áp dụng `overflow-wrap: break-word; word-break: break-word; line-height: 1.35;`. Phần khối giá được đẩy xuống đáy thẻ bằng `margin-top: auto;`.
  - **Đảm bảo Yêu cầu 9**:
    - Khi thêm thẻ combo thứ 5 vào HTML, thẻ thứ 5 tự động nhảy xuống hàng tiếp theo, giữ nguyên bề rộng cột (1/4 chiều rộng lưới).
    - Các thẻ trên cùng một hàng luôn có chiều cao bằng nhau tuyệt đối.
    - Dù tên combo rất dài thì chữ vẫn tự động xuống dòng mượt mà, không bị tràn khung và không bị cắt cụt.

### 3.3 Form Đăng ký & Ràng buộc Dữ liệu (Yêu cầu 5)
- Thẻ form `.register-card` là khung trắng nổi bật trên nền be cát, được căn giữa ở màn hình lớn (`max-width: 520px; margin: 0 auto;`).
- Mỗi input đều có `<label>` liên kết tường minh qua thuộc tính `for` trùng khớp `id`.
- Ô "Họ tên": `<input type="text" id="full-name" name="fullName" required placeholder="Nguyễn Văn An">`.
- Ô "Email": `<input type="email" id="email" name="email" required placeholder="ban@example.com">`.
- Ô "Chi nhánh": `<select id="branch" name="branch">` có các tùy chọn Hà Nội, TP. Hồ Chí Minh, Đà Nẵng...

### 3.4 Phản hồi Tương tác (Hover & Focus) (Yêu cầu 7)
- Nguyên tắc: **Tuyệt đối không làm đổi kích thước hoặc xô lệch bố cục**.
- Dùng `transition: background-color 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease, color 0.2s ease;`.
- Trạng thái `:focus-visible` bằng bàn phím (phím Tab):
  - Áp dụng `outline: 2px solid var(--color-accent); outline-offset: 2px;` trên các liên kết, nút và ô nhập.
  - Do `outline` và `outline-offset` nằm ngoài mô hình hộp (box model), phần tử không bao giờ bị tăng kích thước hay đẩy các phần tử xung quanh.
- Trạng thái `:hover`:
  - Nút hero & nút submit: thay đổi độ sáng màu nền (background-color).
  - Nút hamburger ba gạch: thay đổi màu nền tinh tế hoặc opacity.
  - Các input: đổi màu viền sang tông nhấn ấm.
  - Các thẻ combo: đổ bóng nhẹ (`box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);`) không thay đổi padding/margin.

---

## 4. Kế hoạch Kiểm thử & Xác minh (Verification Plan)
1. **Kiểm tra hiển thị ở 1280px & 360px**: So khớp trực tiếp với ảnh mẫu 1 và 2 (độ lệch <= 2px).
2. **Kiểm tra cuộn trang & Sticky Header**: Header luôn cố định ở top, che phủ nội dung cuộn bên dưới bao gồm cả badge giảm giá.
3. **Kiểm tra Responsive Menu**: Resize màn hình từ 320px đến 1280px, xác nhận mốc 768px chuyển đổi mượt mà giữa hamburger và menu ngang.
4. **Kiểm tra Thanh cuộn ngang**: Không có thanh cuộn ngang ở bất kỳ kích thước nào từ 320px trở lên (`overflow-x: hidden` trên wrapper nếu cần, nhưng chủ yếu là container sizing chuẩn).
5. **Kiểm tra Điều hướng Phím Tab & Hover**: Nhấn Tab lần lượt qua tất cả các liên kết, nút, input; xác nhận viền focus rõ ràng và không nhảy layout.
6. **Kiểm tra Thử nghiệm Mở rộng (Yêu cầu 9)**:
   - Thêm thẻ combo thứ 5 vào HTML.
   - Đặt tên combo thứ 5 hoặc một combo bất kỳ với độ dài lớn (ví dụ: "Combo Trà Đào Cam Sả Thượng Hạng Đặc Biệt Mùa Hè Kèm Bánh Croissant Phô Mai").
   - Xác nhận: Cùng bề rộng, các thẻ cùng hàng bằng chiều cao, không vỡ layout, không tràn chữ.

