## 1. Callback
### a. Callback?

Callback là kĩ thuật truyền một function (nó là callback) vào một function khác làm tham số, và khi function kia thực thi xong nó sẽ gọi lại thằng callback được truyền vào.

Có hai dạng callback:
- Callback bình thường: callback truyền cho hàm đồng bộ
- Async callback: là callback được truyền cho một hàm bất đồng bộ

Callback đảm bảo một function (callback là nó) phải được thực thi sau khi một function khác hoàn thành (function nhận callback).

Callback bình thường có thể thay thế bằng một đoạn code đồng bộ ngay phía sau, nên nó không cần thiết. Do đó, thường thì nhắc tới callback là nói tới async callback, được truyền cho hàm bất đồng bộ.

```js
setTimeout(function () {
    console.log('Done');
}, 1000);
```

### b. Error handling
Thường thì các WebAPIs hay C++ API bất đồng bộ khi sử dụng với callback, thì chúng thường tự mình xử lý lỗi và báo lỗi cho callback bằng một hoặc hai tham số.

Ví dụ như method `$.get` của [[jQuery]], thì callback truyền vào sẽ có thêm tham số thứ 2 là `status`, là chuỗi báo kết quả request.

```js
$.get('index.html', function (data, status) {
    if (status === 'success')
        // Xử lý data
    else
        console.log('Error');
});
```
Do đó, cần kiểm tra request có thành công hay không, chỉ khi không có lỗi thì callback mới thực hiện xử lý data nhận được.

### c. Callback hell

Khi bạn muốn thực hiện nhiều công việc bất đồng bộ liên tiếp nhau, thì sẽ dẫn tới callback hell. Về cơ bản, callback hell chỉ là những callback lồng vào nhau, nhưng vì quá nhiều nên sẽ làm code khó đọc, khó hiểu.

Ví dụ sau sẽ tải liên tiếp 3 file theo thứ tự `index.html`, `style.css`, `script.js` 

```js
$.get('index.html', function (data) {
    console.log('Got index.html');
    $.get('style.css', function (data) {
        console.log('Got style.css');
        $.get('script.js', function (data) {
            console.log('Got script.js');
            ...
        }
    }
}
```

Thử tưởng tượng cần phải tải nhiều file hơn nữa thì sẽ dẫn tới một đống callback lồng nhau. Do đó, nó sẽ sinh ra vấn đề là code siêu khó đọc,đó là chưa kể tới việc bắt lỗi cho từng callback. Từ đó, người ta tạo ra Promise để giải quyết vấn đề callback hell như trên.

## 2. Promise
### a. Promise?

Promise là đối tượng đại diện cho kết quả của hành động nào đó sẽ hoàn thành trong tương lai, kết quả trả về sẽ là `resolve` nếu thành công và `reject` nếu thất bại.

Chúng ta sẽ thực hiện một hành động bất đồng bộ (trong hàm gọi là executor), và gắn thêm callback vào từng kết quả, từng trường hợp thành công hay thất bại. Ví dụ khi thành công, thì những callback gắn với trường hợp `resolve` sẽ được gọi, tương tự khi thất bại thì callback của `reject` được gọi.

```none
B1. Gọi hàm execution, chứa lệnh bất đồng bộ
B2. Thêm callback cho trường hợp resolve, reject
B3. Khi executor thực hiện xong sẽ trả về kết quả
B4. Callback tương ứng khi resolve, reject sẽ được gọi
```

Bên trên là sơ đồ siêu đơn giản mô tả các promise hoạt động.
 
Một promise từ khi tạo ra tới khi kết thúc sẽ có các trạng thái (state) sau:

- Pending: promise đang thực hiện chưa xong
- Full filled: trạng thái đã thực hiện xong, kết quả thành công
- Rejected: trạng thái đã thực hiện xong, kết quả thất bại

Ngoài ra còn một trạng thái nữa là settled, là chỉ chung cho full filled và rejected. Khi đó promise thực hiện xong, không quan tâm kết quả.

### b. Promise workflow

**Executor**
Promise về bản chất là một object. Constructor của nó nhận vào một hàm gọi là executor (thường là hàm ẩn danh), có cấu trúc như sau.

```js
function (resolve, reject) {
    // Thực hiện lệnh
    if (success)
        resolve();
    else
        reject();
}
```

Executor function gồm 2 tham số là `resolve` và `reject` được xem như function. Executor sẽ:

- Thực hiện một số lệnh, thường có một lệnh bất đồng bộ
- Gọi `resolve()` để báo kết quả thành công, gọi `reject` để báo thất bại

Thường thì phần gọi `resolve()` hoặc `reject()` sẽ đặt trong lệnh bất đồng bộ, chứ không đặt bên ngoài, vì các lệnh bên ngoài sẽ chạy đồng bộ nên promise sẽ kết thúc rất nhanh, trước khi lệnh bất đồng bộ thực hiện xong.

**Promise object**

Executor sẽ được truyền vào cho Promise constructor khi tạo một promise object.

```js
let p = new Promise(function (resolve, reject) {
    // Thực hiện lệnh
    if (success)
        resolve();
    else
        reject();
});
```

Lúc này, một promise object được tạo ra. Khi nó vừa tạo ra, nó thực thi lệnh ngay lập tức. Các lệnh trong executor sẽ lần lượt được thực hiện cho tới phần gọi `resolve()` hoặc `reject()`. Khi gọi một trong hai, thì promise sẽ đẩy một callback tương ứng vào job queue, và thực hiện nốt những lệnh còn lại (nếu có, nhưng thường là không).

Callback ở trong job queue sẽ chờ

**Then & catch**

Khi lệnh bất đồng bộ thực hiện, luồng chạy sẽ tiếp tục các lệnh sau khi tạo object promise. Lúc này promise object có thể thuộc hai trường hợp:

- Đang pending, chưa gọi `resolve()` hoặc `reject()`, nên chưa có callback trong job queue
- Đã settled, `resolve()` hoặc `reject()` đã gọi rồi, và có một callback đang chờ trong job queue.

Dù trường hợp nào đi nữa, thì chắc chắn callback trong job queue chưa thực hiện ngay, hoặc là nó chưa có, hoặc job queue đang chờ chưa được thực thi (vì job queue phải chờ stack rỗng, là không còn lệnh nào sẽ chạy nữa). Do đó, có thể nói rằng callback trong job queue luôn thực thi sau cùng.

Luồng chạy vẫn tiếp tục các lệnh tiếp theo. Luồng chạy đi qua phần tạo object promise và tiến tới phần `then()` hoặc `catch()` (hai phần này thường nằm ngay sau khi tạo promise object). Cả `then()` và `catch()` thực ra đều là method của promise object.

```js
...
p.then(function () {
    console.log('Success');
})
p.catch(function () {
    console.log('Failed');
})
```

Method `then()` sẽ nhận vào callback, và gắn nó cho trường hợp thành công. `catch()` cũng thế nhưng callback sẽ gắn cho trường hợp thất bại. Và những callback sẽ được gọi bởi thằng callback bên trong job queue (có thể chưa tạo ra hay đang chờ).