Sass/SCSS là **CSS preprocessor**. Browser không hiểu trực tiếp, phải compile ra CSS.
SCSS cho thêm tính năng:
- variables
- nesting
- mixins
- functions
- partials
- modules
- extend
- operators

### Sass vs SCSS khác nhau?
Sass có 2 syntax:

#### **SCSS syntax**
Giống CSS, dùng `{}` và `;`.

#### Sass indented syntax
Không dùng `{}` và `;`, dùng indentation.

```
CSS variable:
runtime, browser hiểu, đổi theme động tốt.

SCSS variable:
compile-time, browser không biết, hợp token/tính toán tĩnh.

Mixin:
tái sử dụng block CSS, có thể có tham số, nhưng lạm dụng dễ duplicate CSS.

Nesting:
viết CSS lồng nhau, dễ đọc nhưng không nên quá 2–3 cấp.

CSS Modules:
scoped CSS theo component, tránh conflict class.

Tailwind:
utility-first, build UI nhanh, className có thể dài.

SCSS/Sass:
CSS preprocessor, thêm variables/nesting/mixins/functions, phải compile ra CSS.
```
