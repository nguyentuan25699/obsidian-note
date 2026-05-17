Flexbox = layout 1 chiều: ngang hoặc dọc.
Grid = layout 2 chiều: hàng và cột cùng lúc.

Ví dụ thực tế:
- Navbar: dùng Flex
- Button icon + text: dùng Flex
- Card content align: dùng Flex

- Gallery ảnh: dùng Grid
- Dashboard nhiều ô: dùng Grid
- Layout 3 cột: dùng Grid
- Product list responsive: dùng Grid

## Flexbox
### Flexbox là gì?
Flexbox giúp sắp xếp các phần tử con theo một trục.

Ví dụ:
```html
<div class="container">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

```css
.container {
  display: flex;
}
```


### Main axis và cross axis
Đây là key để hiểu Flexbox.

Nếu: 
```css
.container {
  display: flex;
  flex-direction: row;
}
```
thì: 
- Main axis = ngang
- Cross axis = dọc

Nếu:
```css
.container {
  display: flex;
  flex-direction: column;
}
```
thì: 
- Main axis = dọc
- Cross axis = ngang

### justify-content vs align-items
- justify-content: Căn theo **main axis**.
```css
.container {
  display: flex;
  justify-content: center;
}
```
Nếu `flex-direction: row`, nó căn ngang.


- align-items: Căn theo **cross axis**.
```css
.container {
  display: flex;
  align-items: center;
}
```
Nếu `flex-direction: row`, nó căn dọc.


### Các thuộc tính Flex quan trọng
- flex-direction
```css
.container {
  flex-direction: row;
}
```
Giá trị:
- row: ngang, mặc định
- column: dọc
- row-reverse: ngang đảo chiều
- column-reverse: dọc đảo chiều

### gap
Khoảng cách giữa item.
```css
.container {
  display: flex;
  gap: 16px;
}
```


### flex-wrap
Cho item xuống dòng.
```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
```


### flex: 1 là gì?
Ví dụ:
```css
.item {
  flex: 1;
}
```

Hiểu đơn giản: Item sẽ cố gắng chia đều không gian còn lại.
Ví dụ 3 item đều `flex: 1`:

```txt
| item 1 | item 2 | item 3 |
```
Mỗi item chiếm 1 phần bằng nhau.

- flex thực ra là viết tắt của gì?
Gần tương đương:
```css
.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 0%;
}
```

### flex-grow
Cho phép item **nở ra** để chiếm phần trống.
```css
.item {
  flex-grow: 1;
}
```
Nếu item A grow 1, item B grow 2 thì B ăn nhiều phần trống hơn A.


### flex-shrink
Cho phép item **co lại** khi thiếu chỗ.
```css
.item {
  flex-shrink: 1;
}
```
Nếu không muốn item bị co:
```css
.item {
  flex-shrink: 0;
}
```

Hay dùng cho avatar, icon:
```css
.avatar {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
}
```
Nếu không, avatar có thể bị bóp méo khi container hẹp.

### flex-basis
Kích thước ban đầu của item trước khi grow/shrink.
```css
.item {
  flex-basis: 200px;
}
```
Nghĩa là item bắt đầu với width khoảng `200px`, sau đó mới grow/shrink tùy layout.

## CSS Grid
### CSS Grid là gì?
CSS Grid là layout system dùng để chia container thành **rows** và **columns**.

Ví dụ:
```html
<div class="grid">
  <div>Card 1</div>
  <div>Card 2</div>
  <div>Card 3</div>
  <div>Card 4</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
}
```

- Container này là grid.
- Chia thành 4 cột bằng nhau.
- Các item cách nhau 16px.


### grid-template-columns
Đây là thuộc tính quan trọng nhất. Nó định nghĩa số cột và kích thước mỗi cột.
- 3 cột bằng nhau
```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```

Có thể viết gọn:
```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```
1fr nghĩa là “1 phần của không gian còn lại”.

- Sidebar + content
```css
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
}
```
Cột 1 rộng 240px
Cột 2 chiếm phần còn lại

- Layout 3 cột
```css
.layout {
  display: grid;
  grid-template-columns: 240px 1fr 320px;
}
```
Left sidebar: 240px
Main: phần còn lại
Right panel: 320px

### grid-template-rows
Định nghĩa hàng.

Ví dụ layout header/main/footer:
```css
.page {
  display: grid;
  min-height: 100vh;
  grid-template-rows: auto 1fr auto;
}
```
Header: cao theo content
Main: chiếm phần còn lại
Footer: cao theo content

### fr unit là gì?
	`fr` là đơn vị riêng của Grid, viết tắt của **fraction**.
Nó chia phần không gian còn lại.