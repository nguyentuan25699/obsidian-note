BEM là một convention đặt tên class CSS để code dễ đọc, dễ maintain, tránh conflict.

BEM viết tắt của:
```
B = Block
E = Element
M = Modifier
```


## 1. Block là gì?
**Block** là một component/khối độc lập.
```html
<div class="card">
  ...
</div>
```

```css
.card {
  padding: 16px;
  border: 1px solid #ddd;
}
```
`card` là block.

## 2. Element là gì?
**Element** là phần con bên trong block, không nên đứng độc lập.
Cú pháp:

```css
.block__element
```

```html
<div class="card">
  <h2 class="card__title">Product name</h2>
  <p class="card__description">Product description</p>
</div>
```

```css
.card__title {
  font-size: 20px;
}

.card__description {
  color: gray;
}
```

ở đây:
- card = block
- card__title = element của card
- card__description = element của card

## 3. Modifier là gì?
**Modifier** là biến thể/trạng thái của block hoặc element.
Cú pháp:
```css
.block--modifier
.block__element--modifier
```

Ví dụ cho button có nhiều varriant:
```html
<button class="button button--primary">Save</button>
<button class="button button--danger">Delete</button>
<button class="button button--disabled">Disabled</button>
```

```css
.button {
  padding: 8px 16px;
  border-radius: 8px;
}

.button--primary {
  background: blue;
  color: white;
}

.button--danger {
  background: red;
  color: white;
}

.button--disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

ở dây:
button = block
button--primary = modifier
button--danger = modifier
button--disabled = modifier