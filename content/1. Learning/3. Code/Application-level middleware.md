Ở đây ta xây dựng application-level middleware của ứng dụng bằng cách sử dụng `app.use()` và `app.METHOD` trong đó METHOD là phương thức HTTP của request mà middleware xử lý như (GET, PUT hoặc POST).

Ví dụ dưới đây mô tả một hàm ko khai báo đường dẫn cụ thể, do đó nó sẽ được thực hiện mỗi lần request:
```js
const express = require('express')
const app = express()

app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})
```

Ví dụ dưới đây dùng hàm use đến đường dẫn `/user/:id`. Hàm này sẽ được thực hiện mỗi khi request đến đường dẫn `/user/:id` bất kể phương thức HTTP nào:
```js
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```

Tiếp theo là một ví dụ cho hàm được thực hiện mỗi khi truy cập đến đường dẫn `/user/:id` bằng phương thức GET:
```js
app.get('/user/:id', function (req, res, next) {
  res.send('USER')
})
```

Khi muốn gọi một loạt hàm middleware cho một đường dẫn cụ thể, chúng ta có thể thực hiện như ví dụ dưới đây, bằng cách khai báo liên tiếp các tham số là các hàm sau tham số đường dẫn:
```js
app.use('/user/:id', function (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}, function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```

Hoặc ta có thể tách ra thành 2 lần khai báo `app.use`, gọi là multiple routes, tuy nhiên ở các hàm phía trước cần gọi hàm `next()` khi kết thúc mỗi hàm, nếu không như ví dụ dưới đây, route thứ 2 sẽ không bao giờ được thực hiện do hàm thứ 2 trong route thứ nhất không gọi đến hàm `next()`:
```js
app.get('/user/:id', function (req, res, next) {
  console.log('ID:', req.params.id)
  next()
}, function (req, res, next) {
  res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', function (req, res, next) {
  res.end(req.params.id)
})
```

_Lưu ý_: Khi muốn bỏ qua các hàm middleware tiếp theo không thực hiện nữa, chúng ta sẽ sử dụng lệnh `next('route')`, tuy nhiên việc này chỉ tác dụng với các hàm middleware được load thông qua hàm `app.METHOD` hoặc `router.METHOD`.

Ví dụ dưới đây mô tả một hàm middleware sẽ kết thúc ngạy lập tức khi tham số `id=0`:
```js
app.get('/user/:id', function (req, res, next) {
  // if the user ID is 0, skip to the next route
  if (req.params.id === '0') next('route')
  // otherwise pass the control to the next middleware function in this stack
  else next()
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
app.get('/user/:id', function (req, res, next) {
  res.render('special')
})
```
