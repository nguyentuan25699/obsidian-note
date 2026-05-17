```
let / const
arrow function
template literal
destructuring
spread / rest
default parameter
class
module import/export
Promise
async/await
Map / Set
optional chaining
nullish coalescing
```

## var, let, const
```
var: function scope, có hoisting, dễ gây bug.
let: block scope, có thể gán lại.
const: block scope, không gán lại binding được.
```

```js
let count = 1;
count = 2;

const name = "Tuan";
// name = "Minh"; // lỗi
```
Lưu ý với `const` object:
```js
const user = { name: "Tuan" };

user.name = "Minh"; // được

// user = {}; // lỗi
```
`const` không cho gán lại biến, nhưng object bên trong vẫn có thể bị mutate.

## Arrow function
```js
const add = (a, b) => a + b;
```

Khác function thường ở điểm quan trọng:
```
Arrow function không có this riêng.
Nó lấy this từ scope bên ngoài.
```

Hay dùng trong callback:
```js
const names = users.map((user) => user.name);
```


## Destructuring
Lấy giá trị từ object/array nhanh hơn.
```js
const user = {
  id: 1,
  name: "Tuan",
};

const { id, name } = user;
```

Array:
```js
const numbers = [1, 2, 3];

const [first, second] = numbers;
```

## Spread / Rest
### Spread: bung dữ liệu ra
```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3];

const user = { name: "Tuan" };
const newUser = { ...user, role: "FE" };
```
Hay dùng để update state immutable trong React.

### Rest: gom phần còn lại
```js
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}
```


## Template literal (kí tự chuỗi)
Template literals là một hình thức tạo chuỗi mới trong JavaScript, bổ sung nhiều tính năng mới mạnh mẽ, chẳng hạn như tạo chuỗi nhiều dòng dễ dàng hơn và sử dụng placeholders để nhúng biểu thức vào trong chuỗi. 

Ngoài ra, một tính năng nâng cao được gọi là tagged template literals cho phép bạn thực hiện các thao tác trên các biểu thức trong một chuỗi. Tất cả các tính năng này làm tăng thêm các tùy chọn để thao tác chuỗi, cho phép bạn dễ dàng tạo các chuỗi động có thể được sử dụng cho URL hoặc các chức năng tùy chỉnh ở các thành phần HTML.

Biểu thức nội suy:
```js
const name = "Tuan";
const message = `Hello ${name}`;
```

Dễ đọc hơn nối chuỗi:
```js
"Hello " + name
```


