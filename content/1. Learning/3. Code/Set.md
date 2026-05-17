
### SET
Set là tập hợp các **giá trị duy nhất**. Không giống như Map, Set về mặt khái niệm tương tự như Array hơn là Object, vì đây là danh sách các giá trị chứ không phải cặp key / value. Tuy nhiên, Set không phải là sự thay thế cho array , mà là phần bổ sung để cung cấp hỗ trợ bổ sung để làm việc với dữ liệu trùng lặp. Có thể khởi tạo Set với cú pháp sau :

```js
const set = new Set()

tạo ra một Set rỗng :
Set(0) {}
```

Các phần tử có thể được thêm vào Set với add() method. (không bị nhầm lẫn với set() trong Map dù chúng tương tự nhau)
```js
// Add items to a Set
set.add('Beethoven')
set.add('Mozart')
set.add('Chopin')
```

Vì Set chỉ có thể chứa các giá trị duy nhất, mọi nỗ lực thêm giá trị đã tồn tại sẽ bị bỏ qua. `set.add('Chopin') // Set will still contain 3 unique values` 
Lưu ý : So sánh bằng nhau tương tự áp dụng cho các key của Map và các phần tử Set . Hai đối tượng có cùng giá trị nhưng không chia sẻ cùng một tham chiếu sẽ không được coi là bằng nhau. Bạn cũng có thể khởi tạo Set với một mảng các giá trị. Nếu có các giá trị trùng lặp trong mảng, chúng sẽ bị xóa khỏi Tập hợp.
```js
// Initialize a Set from an Array
const set = new Set(['Beethoven', 'Mozart', 'Chopin', 'Chopin'])
Set(3) {"Beethoven", "Mozart", "Chopin"}
```
Ngược lại, một Set có thể được chuyển đổi thành một Mảng :
```js
const arr = [...set]
(3) ["Beethoven", "Mozart", "Chopin"]
```
Set có nhiều phương thức và thuộc tính giống như Map, bao gồm `delete (), has (), clear ()` và `size.`
```js
set.delete('Beethoven') // true

// Check for the existence of an item
set.has('Beethoven') // false

// Clear a Set
set.clear()

// Check the size of a Set
set.size // 0
```
Lưu ý rằng Set không phải là cách để truy cập đến value qua key hoặc index, giống như Map.get(key) hoặc arr\[index]

#### Khi nào sử dụng Set?
Set là một bổ sung hữu ích cho bộ công cụ JavaScript của bạn, đặc biệt để làm việc với các giá trị trùng lặp trong dữ liệu. Trong một dòng duy nhất, chúng ta có thể tạo một Mảng mới mà không cần các giá trị trùng lặp từ một Mảng có các giá trị trùng lặp.

```none
const uniqueArray = [...new Set([1, 1, 2, 2, 2, 3])] // (3) [1, 2, 3]
=> (3) [1, 2, 3]
```

Set có thể được dùng để tìm kiếm liên kết, điểm chung, sự khác biệt giữa hai bộ dữ liệu. tuy nhiên, arrays có một lợi thế đáng kể so với Set để thao tác bổ sung dữ liệu do các phương thức sort (), map (), filter () và less (), cũng như tương thích trực tiếp với các phương thức JSON.