Bất kì element nào trên một trang web, đều được trình duyệt (browser) thể hiện dưới dạng một hình chữ nhật. Điều đó có nghĩa là, nếu bạn chèn một tấm hình tròn, mình oval, hay cố gắng bo góc tròn các element, thì browser vẫn xem nó là một hình chữ nhật. Và với một hình chữ nhật, sẽ có các thông số đi kèm với nó như chiều rộng `width` và chiều cao `height`, các cạnh biên `border`... Nhưng bấy nhiêu đó thôi thì chưa đủ, browser còn cần phải biết được các thông tin khác như độ dày của border, độ rộng của content bên trong... để có thể render layout được chính xác như mình mong muốn.

![[Pasted image 20260512234009.png]]

Hình bên trên sẽ hơi khó hiểu và khó nhớ nếu ít làm việc với box model, nhưng thật ra nó chả có gì phức tạp cả. Có thể nhớ đơn giản thế này: mình có phần content trong cùng, bọc lấy nó là `padding` (nếu có), bọc tiếp tầng nữa là `border`, bọc tiếp tầng cuối là `margin` (nếu có). Nó giống như một cái bánh hamburger kẹp nhiều tầng vậy. Có một điều quan trọng là thứ tự của chúng chính xác và luôn là như vậy, không có cách nào thay đổi thứ tự được.

Các thuật ngữ trên có thể tạm giải thích như sau:
- **content** (hay content area): là vùng chứa nội dung của một element, với chiều rộng/cao được xác định qua thuộc tính width và height. Vùng này thường chứa text, hình ảnh, video…
- **padding** (hay padding area): cho biết độ rộng của vùng padding bao quanh vùng content.
- **border** (hay border area): cho biết độ rộng (và style) của border bao quanh vùng padding.
- **margin** (hay margin area): cho biết độ rộng của vùng margin bao quanh vùng border.
- **edge**: là biên bên ngoài của từng vùng, thuật ngữ này không thật sự nằm trong box model mà chỉ được đưa ra để giải thích cho dễ hiểu hơn thôi. Bạn có thể bỏ qua nó mà không cần phải lo lắng gì.


## Các thuộc tính CSS

![[Pasted image 20260512234430.png]]

#### Thuộc tính Margin: `margin-top`, `margin-right`, `margin-bottom`, `margin-left`, và `margin`

Các thuộc tính này xác định độ rộng của vùng margin bao quanh element. Giá trị của nó thường được dùng là px (pixel), % (percentage), [[em]], [[rem]], auto... Một điều đặc biệt của margin (so với padding) là margin có thể nhận giá trị âm.

```css
.element {
  margin-top: 15px;
  margin-right: 20px;
  margin-bottom: 30px;
  margin-left: 20px;

  /* Margin có thể nhận cả giá trị âm:
  margin-top: -10px;
  */
}
```

Thông thường, ta sẽ dùng thuộc tính `margin` để định nghĩa nhanh cho cả 4 hướng, thay vì phải định nghĩa riêng lẻ 4 hướng top, right, bottom, left. Tuy nhiên trong một số trường hợp thì bạn sẽ chỉ muốn dùng 1 hướng mà thôi.

```css
/* top, right, bottom, left đều là 15px */
.element { margin: 15px; }

/* top &amp; bottom: 10px, left &amp; right: 15px */
.element { margin: 10px 15px; }

/* top: 10px, left &amp; right: 15px, bottom: 30px */
.element { margin: 10px 15px 30px; }

/* top: 10px, right: 15px, bottom: 30px, left: 40px */
.element { margin: 10px 15px 30px 40px; }
```

Nếu bạn thấy khó nhớ thứ tự của các giá trị tương ứng với hướng nào, thì hãy nhớ 2 quy tắc sau:

1. Quy tắc chiều kim đồng hồ, bắt đầu từ đỉnh 12h (top): với `margin: 10px 15px 30px 40px;`, các giá trị sẽ tương ứng là top, right, bottom, left.
2. Quy tắc đối xứng, top đối xứng với bottom, left đối xứng với right: với `margin: 10px 15px;`, top và bottom cùng là 10px, còn left và right là 15px.

Lưu ý là quy tắc số 1 cũng áp dụng được cho cả padding, border, border-radius... nữa nhé.

#### Thuộc tính Padding: `padding-top`, `padding-right,` `padding-bottom`, `padding-left`, và `padding`

Các thuộc tính này xác định độ rộng của vùng padding bao quanh element. Giá trị của nó thường được dùng là px (pixel), % (percentage), em. Khác với margin, padding không nhận giá trị âm hay auto nhé.

```css
.element {
  padding-top: 15px;
  padding-right: 20px;
  padding-bottom: 30px;
  padding-left: 20px;

  /* padding KHÔNG nhận giá trị âm và auto, 2 dòng CSS sau sẽ không chạy:
  padding-top: -10px;
  padding-left: auto;
  */
}
```

Tương tự padding cũng có thể được viết tắt:

```css
/* top, right, bottom, left đều là 15px */
.element { padding: 15px; }

/* top &amp; bottom: 10px, left & right: 15px */
.element { padding: 10px 15px; }

/* top: 10px, left & right: 15px, bottom: 30px */
.element { padding: 10px 15px 30px; }

/* top: 10px, right: 15px, bottom: 30px, left: 40px */
.element { padding: 10px 15px 30px 40px; }
```

#### Thuộc tính Border:

Border đặc biệt có rất nhiều thuộc tính nhưng cũng khá dễ hiểu và dễ nhớ:

Các thuộc tính thường dùng là các thuộc tính viết tắt: `border-top`, `border-right,` `border-bottom`, `border-left`, và `border`

```css
.element {
  border-top: 1px solid #ccc;
  border-right: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
  border-left: 1px solid #ccc;

  /* hoặc viết tắt */
  border: 1px solid #ccc;
}
```

Như ví dụ trên, để khai báo border, bạn cần cung cấp 3 thông tin cần thiết, tuy nhiên bạn vẫn có thể bỏ qua color mà không cần khai báo, giá trị mặc định của nó sẽ là `initial`, và sẽ được kế thừa từ color của chính element hoặc cha của nó (CSS Inheritance):

- width: độ dày của border (1px...)
- style: loại border ví dụ như `solid`, `dashed`, `dotted`, `double`, `none`...
- color: màu của border ví dụ như `#ccc`, `black`, `rgba(100, 100, 100, 1)`...

Ngoài các thuộc tính thông dụng trên, bạn có thể khai báo cụ thể cho width, style và color bằng các thuộc tính sau: `border-width`, `border-style`, `border-color`, `border-top-width`, `border-top-style`, `border-top-color`... và cứ thế cho các hướng right, bottom, left.