## 1. **JavaScript là gì?**
**JavaScript** là một ngôn ngữ lập trình được sử dụng chủ yếu để tạo ra các trang web tương tác và động. Ban đầu, JavaScript chỉ chạy trên trình duyệt, nhưng ngày nay nó còn có thể chạy trên máy chủ, ứng dụng di động và nhiều nền tảng khác.

### **JavaScript dùng để làm gì?**
- Tạo hiệu ứng động trên website (menu, slideshow, animation…).
- Xử lý sự kiện như nhấn nút, nhập dữ liệu.
- Kiểm tra dữ liệu người dùng trước khi gửi lên máy chủ.
- Giao tiếp với máy chủ để cập nhật nội dung mà không cần tải lại trang.
- Phát triển ứng dụng web, ứng dụng di động và cả ứng dụng máy tính.

VD: 
```js
let ten = "An";
console.log("Xin chào, " + ten + "!");

// Xin chào, An!
```

### **JavaScript khác gì với HTML và CSS?**
- **HTML**: Tạo cấu trúc của trang web.
- **CSS**: Thiết kế giao diện, màu sắc và bố cục.
- **JavaScript**: Thêm chức năng và tính tương tác.

Ví dụ:
- HTML tạo nút bấm.
- CSS làm nút đẹp hơn.
- JavaScript khiến nút thực hiện hành động khi người dùng nhấn.

### **JavaScript hoạt động như thế nào?**
Khi trình duyệt đọc:
```js
<script>
console.log("Hello");
</script>
```

Nó sẽ:
```
Đọc source code
↓
Parse
↓
Biến thành AST
↓
Compile (JIT)
↓
Machine Code
↓
CPU thực thi
```

Engine phổ biến:
- Chrome → **V8**
- Edge → V8
- Node.js → V8
- Firefox → SpiderMonkey
- Safari → JavaScriptCore
___

### **JavaScript Engine là gì?**
Engine là chương trình chịu trách nhiệm đọc và chạy JavaScript.
Ví dụ:

```
JavaScript
↓
V8 Engine
↓
Machine Code
↓
CPU
```

Không có Engine thì JavaScript không chạy được.
___

### **ECMAScript là gì?**
Đây là điều rất quan trọng.
Nhiều người nghĩ:
```
JavaScript = ECMAScript
```
Không hoàn toàn đúng.

Thực tế:
```
ECMAScript
      ↑
   Specification
      ↑
JavaScript triển khai theo chuẩn đó
```

ECMAScript là bộ tiêu chuẩn quy định:
- if
- for
- function
- class
- Promise
- async/await

Tất cả đều được định nghĩa trong đặc tả ECMAScript.

Ví dụ:

**ES6 (2015)**
Thêm:
- let
- const
- class
- arrow function
- template string
- Promise

**ES2016+**
- async/await
- Optional chaining
- Nullish coalescing
- BigInt
- Modules
- …
___

### **JavaScript có những đặc điểm gì?**
#### **1. Dynamic Typing**
Không cần khai báo kiểu.
```js
let x = 10;

x = "Hello";

x = true;
```
Đều hợp lệ.
___

#### **2. Weakly Typed**
JavaScript tự chuyển kiểu.
```js
"5" + 1
```
Kết quả:
```js
"51"
```


```js
"5" - 1
```
Kết quả:
```js
4
```
___

#### **3. Single Thread**
JavaScript chỉ có **một luồng chính** để thực thi mã.
Ví dụ:

```
Task A

↓

Task B

↓

Task C
```

Nó không chạy song song trên nhiều luồng như Java hoặc C# (dù có cơ chế bất đồng bộ giúp xử lý nhiều tác vụ hiệu quả).