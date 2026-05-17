- Theo định nghĩa [ở đây](https://github.com/css-modules/css-modules), CSS module là những file css bao gồm tất cả các **class names** và **animation names**.
- Vì vậy, cũng gần giống như một số ngôn ngữ css mở rộng như sass hay scss, **css module** không thể thực thi trực tiếp trên trình duyệt mà cần thông qua các trình biên dịch ( Webpack hoặc Browserify)
- CSS Module hiểu đơn giản là: **Cách viết CSS sao cho class chỉ có tác dụng trong đúng component đang import nó**, không bị “đụng tên class” với component khác.
![[Pasted image 20260513223111.png]]

- Bây giờ chúng ta xét một ví dụ cụ thể cho dễ hiểu. Đầu tiên chúng ta cần 1 file html và css thông thường như sau:

```HTML
  <h1 class="title">An example heading</h1>
```

```CSS
  .title {
     background-color: red;
  }
```

- Khi áp dụng đoạn code trên, chúng ta sẽ có được thẻ H1 màu đỏ, Browser sẽ hiểu cả 2 file và không cần xử lý gì cả.
- Nhưng css module thì khác, thay vì viết code html , chúng ta cần viết code bằng javascript, ví dụ như sau:

```JS
    import styles from "./styles.css";

    element.innerHTML = 
      `<h1 class="${styles.title}">
         An example heading
       </h1>`;
```

```css
  .title {
     background-color: red;
  }
```

- Trong quá trình build, trình biên dịch sẽ duyệt tìm qua file "./styles.css" . Và sau đó sẽ tìm qua file Javascript mà chúng ta đã viết. Tạo class ".title" có thể truy cập qua {styles.title}. Tiếp đó compiler sẽ xử lý để tạo 2 file html và css mới, với một chuỗi ký tự mới thay thế cho cả html và css selector

```html
<h1 class="_styles__title_309571057">
  An example heading
</h1>
```

```CSS
._styles__title_309571057 {
  background-color: red;
}
```

- Thuộc tính class và selector .title đã hoàn toàn biến mất, được thay thế hoàn toàn bằng một chuỗi mới. File CSS ban đầu của chúng ta không hề được sử dụng trên browser.
![[Pasted image 20260513223405.png]]

Ví dụ trong React:
```css
/* UserCard.module.css */

.card {
  padding: 16px;
  border: 1px solid #ddd;
}

.title {
  font-size: 20px;
  font-weight: bold;
}
```
Trong component:
```ts
import styles from "./UserCard.module.css";

function UserCard() {
  return (
    <div className={styles.card}>
      <h2 className={styles.title}>Nguyễn Tuấn</h2>
    </div>
  );
}
```


- Tại sao chúng ta lại muốn xáo trộn css và html để làm điều này? Tại sao chúng ta lại muốn style theo cách này?
___

## Tại sao chúng ta nên sử dụng CSS Module

CSS Module đảm bảo rằng tất cả style cho một component:

- Chỉ tồn tại ở 1 nơi
- Chỉ được sử dụng cho riêng component đó mà không sử dụng ở bất kỳ chỗ nào khác
- Thêm vào đó bất kỳ component nào đều có một sự phụ thuộc, Ví dụ:

```JS
    import buttons from "./buttons.css";
    import padding from "./padding.css";

    element.innerHTML = `<div class="${buttons.red} ${padding.large}">`;
```

- Với cách này chúng ta khắc phục được vấn đề phạm vi global trong css.


### **Ví dụ so sánh CSS thường vs CSS Module**
#### **CSS thường**
```css
.title {
  color: red;
}
```

```ts
<h1 className="title">Hello</h1>
```
Class `.title` là global. Ai dùng `.title` cũng bị ảnh hưởng.

#### CSS Module
```css
/* Header.module.css */
.title {
  color: red;
}
```

```ts
import styles from "./Header.module.css";

<h1 className={styles.title}>Hello</h1>
```
Class `.title` chỉ scoped trong file/component import nó.

___

## Từ khoá composes

- Giả sử chúng ta có một module và được style bằng file type.css. Như ví dụ dưới đây:

```CSS
    .serif-font {
      font-family: Georgia, serif;
    }

    .display {
      composes: serif-font;
      font-size: 30px;
      line-height: 35px;
    }

```

- Chúng ta có thể khai báo một trong các class trong template như sau:

```JS
    import type from "./type.css";

    element.innerHTML = 
      `<h1 class="${type.display}">
        This is a heading
      </h1>`;
```

- Chúng ta sẽ được kết quả như sau:

```none
    <h1 class="_type__display_0980340 _type__serif_404840">
      Heading title
    </h1>
```

- Cả 2 class đều được rằng buộc vào phần tử bằng cách sử dụng từ khoá composes, từ đó tránh được một số vấn đề không hay của [các giải pháp #](https://www.sitepoint.com/avoid-sass-extend/) , như Sass’ [@extend](https://viblo.asia/u/extend).
- Chúng ta thậm chí có thể biên soạn từ một class cụ thể trong từng file css riêng biệt.

Ví dụ:
```CSS
    .element {
      composes: dark-red from "./colors.css";
      font-size: 30px;
      line-height: 1.2;
    }

```
___

## Ưu nhược điểm của CSS Module
Ưu điểm:
- Tránh conflict class name
- Style scoped theo component
- Dễ maintain trong project lớn
- Dễ xoá component thì xoá luôn style đi kèm
- Dùng tốt với React/Next.js
- Vẫn viết CSS/SCSS bình thường

Nhược điểm:
- Không tiện cho style global/theme toàn app
- Muốn dùng nhiều class phải combine qua template string hoặc clsx
- Không tự giải quyết design system, spacing, color token
- Override thư viện bên ngoài đôi khi phải dùng :global()
- Class name trong DevTools bị hash nên đôi lúc khó nhìn hơn CSS thường

___
## Khi nào nên dùng CSS Module?

Nên dùng cho:
- Component style riêng
- Button/Card/Header/Form
- Page-specific style
- Style không muốn ảnh hưởng global
- Project React/Next.js vừa và lớn

Không nên dùng cho:
- CSS reset
- Global font
- Global CSS variables
- Theme root variables
- Style thư viện global
