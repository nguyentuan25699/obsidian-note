Một framework được dùng cho xây dựng server backend trền nền tảng node.js

Express là một framework được xây dựng trên nền tảng của Nodejs. Nó cung cấp các tính năng mạnh mẽ để phát triển web hoặc mobile. Express hỗ trợ các method HTTP và middleware tạo ra API vô cùng mạnh mẽ và dễ sử dụng.

Các tính năng nổi bật của Express:
- Thiết lập router cho phép sử dụng với các hành động khác nhau dựa trên phương thức HTTP và URL.
- Hỗ trợ xây dựng theo mô hình MVC
- Cho phép định nghĩa middleware giúp tổ chức và tái sử dụng code
- Hỗ trợ RESTful API

Cài đặt: với [[npm]]
```bash
npm install express
```
Hoặc: 
```bash
yarn add express
```

Init:
```bash
npm init -y
```

Sau khi đã có file package.json rồi ta tạo file index.js.
Tại đây, ta khai báo module express và tạo ứng dụng. Ứng dụng được đặt tên `app`, sau khi được khởi tạo `app` sẽ có các phương thức để định tuyến HTTP, cấu hình middleware, hiển thị chế độ xem HTML, đăng ký template engine và sửa đổi cài đặt để kiểm soát ứng dụng hoạt động,...
```js
const express = require('express'); 
const app = express(); 
```

Phần định tuyến bởi phương thức `app.get()` sẽ chỉ định một hàm callback bất cứ khi nào có một yêu cầu HTTP GET với một đường dẫn ('/'). Hàm callback nhận vào hai đối số là request và response, và trả về phản hồi bằng gọi hàm send để trả về chuỗi Hello World.
```js
app.get('/', (req, res) => {   
    res.send('Hello World!') 
});
```

Phần cuối chương trình chạy ứng dụng trên `port` được chỉ định là 3000, với máy chủ đang chạy có thể truy cập `localhost:3000` trên trình duyệt để xem kết quả.
```js
const port = 3000;  

app.listen(port, () => {   
    console.log(`Example app listening on port ${port}!`) 
});
```


## Routing
Routing/định tuyến đề cập đến cách các endpoint(URI) của ứng dụng phản hồi các yêu cầu từ client.

Ta xác định định tuyến bằng các phương thức của đối tượng trong ứng dụng Express tương ứng với các phương thức HTTP. Ví dụ: `app.get()` để xử lý yêu cầu **GET** và `app.post` để xử lý yêu cầu **POST**. Tương tự với các phương thức khác như PUT, PATH, DELETE,... Ta cũng có thể sử dụng `app.all()` để xử lý tất cả các phương thức HTTP và `app.use` để chi định middleware cần thiết.

Các phương thức định tuyến này chỉ định một hàm callback (đôi khi được gọi là "handler function"), chúng được gọi khi ứng dụng nhận được yêu cầu đến tuyến được chỉ định (endpoint) và phương thức HTTP. Nói cách khác, nó sẽ "lắng nghe" các yêu cầu ứng với (các) tuyến và (các) phương thức được chỉ định, và khi thấy trùng, ứng dụng sẽ gọi hàm callback được chỉ định.

VD: 
```js
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.send('hello world')
})
```

Về hai tham số là req và res ta sẽ tìm hiểu như sau:

### Request
Request viết tắt là req là các yêu cầu từ phía client đến server. Như ở ví dụ trên thì request có vẻ không cần thiết, nhưng thực tế ta sẽ cần rất nhiều thông tin từ request, như **body** từ phương thức POST, thông tin từ đường dẫn, các yêu cầu xác thực,... Vì thế có rất rất nhiều loại request, nhưng ở đây ta chỉ cần quan tâm đến những loại thường dùng là:

#### req.body
Lấy phần thông tin từ body của request. Sau phiên bản Express.4x để lấy thông tin từ phương thức POST của HTTP. Ta phải sử dụng body-parser.
```js
const app = require('express')()
const bodyParser = require('body-parser')

app.use(bodyParser.json()) // for parsing application/json
app.use(bodyParser.urlencoded({ extended: true })) // for parsing application/x-www-form-urlencoded

app.post('/profile', function (req, res) {
  console.log(req.body)
  res.json(req.body)
})
```

#### req.params
Lấy tham số từ parameter của đường dẫn. Ví dụ như ta có link là:
	GET /api/users/:name
```js
console.dir(req.params.name)
```

#### req.query
Tương tự như `req.params` nhưng là lấy query từ link
	GET /api/users?name="Bob"
```js
console.dir(req.query.name)
```

#### req.header
Lấy thông tin từ header của HTTP. Chủ yếu dùng để xác thực người dùng
```js
const token = req.headers.authorization;
```

### Response
Response viết tắt là res. Là phản hồi từ phía server đến client. Có thể là gửi về dữ liệu mà client yêu cầu, hoặc thực hiện các thao tác mà client mong muốn, như chuyển hướng, render đến template,... Ta có bảng tóm tắt các res thường dùng như sau.

| Method         | Description                         |
|----------------|-------------------------------------|
| res.download() | Tệp được tải xuống                  |
| res.end()      | Kết thúc quá trình response         |
| res.json()     | Gửi về file json                    |
| res.jsonp()    | Gửi về file json hỗ trợ JSONP       |
| res.redirect() | Chuyển hướng request                |
| res.render()   | Render ra giao diện theo template   |
| res.send()     | Gửi về nhiều loại tệp khác nhau     |
| res.sendFile() | Gửi về dưới dạng luồng octet        |
| res.status()   | Gửi về trạng thái của HTTP phản hồi |
Như đã nói ở trên khi tạo `app` với Express, ta sẽ có tất cả tính năng mà Express cung cấp và đôi khi nó sẽ trở nên thừa thải khi ta chỉ cần tính năng định tuyến, lúc này để tối ưu ta làm như sau:
```js
const express = require('express')
const router = express.Router()

router.get('/', function (req, res) {
  res.send('Home page')
})

module.exports = router
```

Sau đấy tại file index.js ta xuất nó ra:
```js
const routes = require('./routes')

// ...

app.use('/api', routes)
```


## Middleware
Middleware là các hàm được dùng để tiền xử lý, lọc các request trước khi đưa vào xử lý logic hoặc điều chỉnh các response trước khi gửi về cho người dùng.

Ta sẽ tìm hiểu cách Express sử dụng middleware:
![[Pasted image 20260609235341.png]]

Hình trên mô tả khi một request gửi đến Express sẽ được xử lý qua 5 bước như sau :
- Tìm định tuyến tương ứng với request
- Dùng [[CORS]] Middleware để kiểm tra cross-origin Resource sharing của request
- Dùng [[CSRF]] Middleware để xác thực CSRF của request, chống fake request
- Dùng Auth Middleware để xác thực request có được truy cập hay không
- Xử lý công việc được yêu cầu bởi request (Main Task)

Bất kỳ bước nào trong các bước 2,3,4 nếu xảy ra lỗi sẽ trả về response thông báo cho người dùng, có thể là lỗi CORS, lỗi CSRF hay lỗi auth tùy thuộc vào request bị dừng ở bước nào.

Hàm middleware thường có dạng như sau:
```js
async function name(req, res, next) {
    await something
    next();
}
```

Ta thấy hàm middleware sử dụng 3 tham số `req`, `res` và `next`, hai tham số trước ta đã biết còn `next` được dùng để chuyển tiếp sang hành động kế tiếp. Trong một vài trường hợp ta sẽ sử dụng tham số `err`, đối tượng lỗi. Các chức năng middleware có thể thực hiện các tác vụ sau:
- Thực hiện bất cứ đoạn code nào
- Thay đổi các đối tượng request và response
- Kết thúc một quá trình request-response
- Gọi hàm middleware tiếp theo trong stack

Trong Express, có 5 kiểu middleware có thể sử dụng :
- [[Application-level middleware]] (middleware cấp ứng dụng)
- [[Router-level middleware]] (middlware cấp điều hướng - router)
- [[Error-handling middleware]] (middleware xử lý lỗi)
- [[Built-in middleware]] (middleware sẵn có)
- [[Third-party middleware]] (middleware của bên thứ ba)

