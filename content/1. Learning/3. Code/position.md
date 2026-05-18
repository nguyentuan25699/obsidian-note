## 1. position là gì?
- position quyết định element được đặt vị trí như thế nào trong layout.

Các giá trị chính:
```
static
relative
absolute
fixed
sticky
```

## 2. position: static
Đây là mặc định.
```css
.box {
  position: static;
}
```
Đặc điểm:
- Nằm theo normal flow của document.
- top/right/bottom/left không có tác dụng.
- z-index thường không có tác dụng.

## 3. position: relative
Element vẫn nằm trong normal flow, vẫn chiếm chỗ cũ, nhưng có thể dịch chuyển bằng `top/right/bottom/left`.
```css
.box {
  position: relative;
  top: 10px;
  left: 20px;
}
```

Hiểu:
- Box vẫn chiếm vị trí ban đầu trong layout.
- Nhưng hình ảnh hiển thị bị dịch xuống 10px, sang phải 20px.

Ứng dụng quan trọng nhất: Làm mốc cho absolute child.
VD: 
```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 8px;
  right: 8px;
}
```
Ở đây `.badge` sẽ bám theo `.card`.

## 4. position: absolute
Element bị lấy ra khỏi normal flow.
```css
.badge {
  position: absolute;
  top: 8px;
  right: 8px;
}
```
Đặc điểm:
- Không chiếm chỗ trong layout bình thường.
- Định vị theo ancestor gần nhất có position khác static.
- Nếu không có ancestor phù hợp, nó bám theo initial containing block/page.

## 5. position: fixed
Element bị lấy ra khỏi normal flow và định vị theo viewport.
```css
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
}
```

Đặc diểm:
- Luôn cố định theo màn hình.
- Scroll page thì nó vẫn nằm đó.
- Không chiếm chỗ trong layout.

## 6. position: sticky
Ban đầu element nằm theo normal flow như bình thường. Khi scroll tới một ngưỡng, nó dính lại.
```css
.sidebar {
  position: sticky;
  top: 16px;
}
```
Đặc điểm:
- Kết hợp giữa relative và fixed.
- Vẫn chiếm chỗ trong layout.
- Chỉ sticky trong phạm vi parent/container của nó.
- Cần có top/bottom/left/right để hoạt động.