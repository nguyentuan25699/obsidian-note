## 1. z-index là gì?
`z-index` quyết định **thứ tự chồng lớp** trên trục Z, tức là element nào nằm trên element nào, số lớn hơn thường nằm trên.
```css
.modal {
  position: fixed;
  z-index: 1000;
}
```

Thường `z-index` cần element có `position` khác `static`.

Vì sao z-index: 9999 vẫn không nổi lên?
Vì có khái niệm stacking context.

Hiểu đơn giản:
Stacking context là một “thế giới xếp lớp riêng”.
Con bên trong không thể vượt ra ngoài thứ tự của parent context.