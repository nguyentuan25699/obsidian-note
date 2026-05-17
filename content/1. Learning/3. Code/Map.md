### Map
Map là một tập hợp các cặp key/value có thể sử dụng mọi kiểu dữ liệu làm key và có thể duy trì thứ tự các phần tử của nó. 
Map có các yếu tố của Object (bộ key/value duy nhất ) và Array (một tập hợp được sắp xếp ), nhưng tượng tự như khái niệm object. Điều này là vì mặc dù kích thước và thứ tự của các phần tử được lưu trữ như một array, các phần tử vẫn là các cặp key/value như object. Map có thể được khởi tạo với cú pháp và điều này sinh ra một map rỗng. :

```js
const map = new Map()
=> Map(0) {}
```

Có thể thêm giá trị vào map với phương thức`set()`. Tham số đầu tiên có thể là 1 key, và thứ hai là value. Ở đây chúng ta bắt đầu thấy Map có các yếu tố của object và array. Giống array, chúng ta có một bộ các phần tử với chỉ mục (index) từ 0, và chúng ta có thể thấy có bao nhiêu phần tử mặc định trong Map. Map sử dụng cú pháp `=>` để biểu thị key/value `key => value`
```js
map.set('firstName', 'Luke')
map.set('lastName', 'Skywalker')
map.set('occupation', 'Jedi Knight')

=>
Map(3)
0: {"firstName" => "Luke"}
1: {"lastName" => "Skywalker"}
2: {"occupation" => "Jedi Knight"}

```

Map chấp nhận bất kì kiểu dữ liệu nào key, và không cho phép trùng lặp key value. Chúng ta có thể chứng minh điều này bằng cách tạo 1 map và sử dụng giá trị không phải chuỗi, như cài đặt 2 giá trị cùng 1 key:
```js
const map = new Map()

map.set('1', 'String one')
map.set(1, 'This will be overwritten')
map.set(1, 'Number one')
map.set(true, 'A Boolean')
```
Ví dụ trên sẽ ghi đè key đầu tiên là 1 bằng khóa tiếp theo, nó sẽ coi '1' và 1 là các khóa duy nhất.
```js
0: {"1" => "String one"}
1: {1 => "Number one"}
2: {true => "A Boolean"}
```

#### Khi nào sử dụng Map?

Tóm lại, Maps giống với Object khi chúng cũng có các cặp key/value. Nhưng Map có các lợi ích hơn Object như :

- size : có thuộc tính size, Objects không có tích hợp để lấy ra size của nó.
- vòng lặp : Map có thể lặp lại trực tiếp, còn Object thì không.
- tính linh hoạt : Maps có thể có bất kì kiểu dữ liệu nào làm key cho 1 value, còn Object thì chỉ là chuỗi.
- sắp xếp : Map giữ lại thứ tự chèn của chúng, trong khi objects không có thứ tự bảo đảm. Do những yếu tố này, Map là một cấu trúc dữ liệu mạnh. 
 
Tuy nhiên, object cũng có một số lợi ích quan trọng
- json : object làm việc hoàn hảo với JSON.parse() và JSON.stringify(), hai hàm thiết yếu khi làm việc với JSON, một kiểu data phổ biến mà nhiều REST API sử dụng.
- làm việc với một element : làm việc với một giá trị đã biết trong object, ban có thể truy cập trực tiếp bằng key mà không cần sử dụng phương thức, chẳng hạn như get() của Map.

Danh sách này sẽ giúp bạn quyết định nếu Map hoặc Object sẽ là kiểu dữ liệu phù hợp cho bạn.
