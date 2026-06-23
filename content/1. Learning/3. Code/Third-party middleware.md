Sử dụng Third-party sẽ giúp ta thêm các chức năng cho vào web app của mình mà không cần mất công triển khai. Ta sẽ cần cài đặt module thông qua **npm**, sau đó khai báo sử dụng trong đối tượng `app` nếu dùng ở **Application-level**, hoặc qua đối tượng `router` nếu dùng ở **Router-level**.
```bash
$ npm install cookie-parser
```

```js
const express = require('express')
const app = express()
const cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```
