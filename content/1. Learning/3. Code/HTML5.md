## **1. HTML5 là gì?

**HTML5** là phiên bản hiện đại của HTML, dùng để xây dựng cấu trúc trang web. So với HTML cũ, HTML5 thêm nhiều thẻ semantic, API media/form/canvas/storage tốt hơn, giúp web app hiện đại hơn.

```text
HTML5 là phiên bản mới của HTML, bổ sung semantic tags như header, nav, main, section, article, footer; hỗ trợ media như video/audio; form input type mới; canvas/SVG; và nhiều API hỗ trợ web app hiện đại. HTML5 giúp code rõ nghĩa hơn, tốt hơn cho SEO, accessibility và maintainability.
```

## 2. Điểm quan trọng nhất của HTML5: Semantic HTML
Semantic nghĩa là **thẻ có ý nghĩa**.

Thay vì viết toàn div: 
```html
<div class="header">Header</div>
<div class="menu">Menu</div>
<div class="content">Content</div>
<div class="footer">Footer</div>
```

HTML5 khuyến khích viết:
```html
<header>Header</header>
<nav>Menu</nav>
<main>Main content</main>
<footer>Footer</footer>
```

## 3. Vì sao semantic HTML quan trọng?
1. Code dễ đọc, dễ maintain
2. SEO tốt hơn vì crawler hiểu cấu trúc page
3. Accessibility tốt hơn vì screen reader hiểu vai trò từng vùng
4. Giảm việc phải dùng div + role quá nhiều

## 4. HTML5 form improvements
HTML5 thêm nhiều input type hữu ích:
```html
<input type="email" />
<input type="number" />
<input type="date" />
<input type="url" />
<input type="tel" />
<input type="search" />
```

```text
HTML5 form cung cấp nhiều input type và validation attribute giúp cải thiện UX và giảm bớt validation đơn giản phía client, nhưng vẫn cần validate lại ở server.
```



*Note:*
`<section>` dùng khi bạn muốn đánh dấu **một vùng nội dung có cùng chủ đề / cùng ý nghĩa** trong trang.
section = một “khu vực nội dung” có chủ đề riêng

```html
<main>
  <section>
    <h2>Giới thiệu sản phẩm</h2>
    <p>Sản phẩm giúp quản lý công việc hiệu quả hơn.</p>
  </section>

  <section>
    <h2>Tính năng nổi bật</h2>
    <p>Quản lý task, báo cáo, phân quyền...</p>
  </section>

  <section>
    <h2>Bảng giá</h2>
    <p>Gói Basic, Pro, Enterprise...</p>
  </section>
</main>
```

### Lợi ích của section
- Code có ý nghĩa hơn div
- Tốt hơn cho accessibility: Screen reader và các công cụ hỗ trợ có thể hiểu trang có các vùng nội dung riêng biệt.
- Tốt hơn cho SEO / document structure: Search engine/crawler có thể hiểu cấu trúc nội dung rõ hơn.
Lưu ý:
```text
section không tự động làm SEO tăng mạnh.
Nó chỉ giúp cấu trúc HTML rõ nghĩa hơn.
Quan trọng vẫn là content, heading, accessibility và semantic tổng thể.
```

- Dễ maintain hơn
- 