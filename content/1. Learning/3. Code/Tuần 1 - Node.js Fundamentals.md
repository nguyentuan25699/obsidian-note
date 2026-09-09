---
date: 2026-09-09
tags:
  - backend
  - code
  - learning
draft: false
related:
---
> [!info] Bối cảnh
> Xuất phát điểm: frontend (React/Next). Tuần này học các khái niệm nền tảng của **runtime Node.js** trước khi đụng vào framework (Express/Nest) ở Tuần 2 — vì Express/Nest chỉ là lớp áo khoác bên ngoài, bên dưới vẫn chạy trên đúng những cơ chế này.

## 1. Event Loop

### Vì sao cần hiểu cái này

Node.js chạy JavaScript trên **1 thread duy nhất** (single-threaded) — không có chuyện code của bạn chạy song song ở 2 chỗ cùng lúc như đa luồng trong Java/Go. Nhưng Node vẫn xử lý được hàng nghìn request cùng lúc mà không bị "đứng hình" chờ I/O (đọc file, gọi DB, gọi API khác...). Bí quyết nằm ở **event loop**: một vòng lặp chạy nền, liên tục kiểm tra "có việc gì cần làm tiếp không" và điều phối code bất đồng bộ chạy đúng lúc, đúng thứ tự.

Ở frontend, bạn cũng có microtask (Promise) và macrotask (`setTimeout`) y hệt vậy — vì trình duyệt và Node đều xây trên cùng triết lý event loop của JavaScript. Khác biệt chính: Node có thêm `process.nextTick()` (trình duyệt không có), và Node không có DOM/window nên không có các API như `requestAnimationFrame`.

### Thứ tự ưu tiên

Khi có nhiều loại "code chờ chạy" cùng lúc, Node xử lý theo đúng thứ tự này:

```
1. Synchronous code (call stack)        — chạy ngay lập tức, chạy cho tới hết
2. process.nextTick() queue             — ưu tiên cao nhất trong các hàng đợi async
3. Promise microtask queue              — .then/.catch/.finally, async/await
4. Timer phase (setTimeout/setInterval) — thuộc nhóm "macrotask"
```

Cơ chế **dọn hàng đợi**: Node chạy hết code đồng bộ trước (đây luôn là ưu tiên số 1, bất kể async ở đâu). Sau đó, trước khi được phép bước sang phase tiếp theo của event loop (như timer phase), Node bắt buộc phải **dọn sạch hoàn toàn** hàng đợi `nextTick`, rồi tới hàng đợi microtask (Promise) — kể cả khi trong lúc dọn, code lại tự sinh thêm task mới vào chính hàng đợi đó (ví dụ 1 `.then()` lại gọi tiếp 1 `.then()` khác), Node vẫn dọn tiếp cho tới khi hàng đợi trống hẳn rồi mới chuyển phase. Đây là lý do vì sao gọi `process.nextTick()` liên tục trong lúc dev có thể khiến app "đói" I/O (starvation) — event loop mãi kẹt ở bước dọn hàng đợi, không bao giờ tới được phase xử lý I/O/timer.

> [!example] Ví dụ thứ tự chạy
> ```js
> setTimeout(() => console.log('fn'), 0)
> Promise.resolve().then(() => console.log('fn2'))
> console.log('sync')
> ```
> Output: `sync` → `fn2` → `fn`.
>
> - `sync` chạy ngay vì là code đồng bộ, nằm thẳng trên call stack.
> - `fn2` chạy trước `fn` dù cả hai đều "delay 0ms" — vì callback của `.then()` được đẩy vào **microtask queue**, và microtask queue luôn được dọn sạch hoàn toàn *trước khi* event loop bước sang **timer phase** (nơi `setTimeout` nằm chờ), dù `setTimeout(..., 0)` nghĩa là "chạy sớm nhất có thể", nó vẫn phải đợi microtask xong trước.

> [!tip] Ứng dụng thực tế
> Hiểu đúng thứ tự này quan trọng khi debug những bug kiểu "tại sao giá trị này chưa được cập nhật kịp lúc tôi đọc nó" — thường là do code đọc giá trị đó nằm trong 1 tầng ưu tiên thấp hơn (vd đọc trong `setTimeout`) trong khi giá trị được set trong 1 tầng ưu tiên cao hơn (vd set trong `.then()`) tưởng là đã chạy trước nhưng thực ra ngược lại tuỳ cách viết code.

## 2. CommonJS (CJS) vs ES Modules (ESM)

### Vì sao Node có tận 2 hệ thống module

CommonJS (`require`/`module.exports`) là hệ thống module **gốc** của Node từ những ngày đầu (trước khi JavaScript có chuẩn module chính thức). ESM (`import`/`export`) là chuẩn module chính thức của ngôn ngữ JavaScript sau này (dùng chung với frontend/browser). Node giờ hỗ trợ cả hai, nhưng chúng **không tương thích 100%** với nhau — đây là nguồn gốc phần lớn các lỗi khó hiểu khi setup project Node/TypeScript.

| | CommonJS (`.cjs`) | ESM (`.mjs`) |
|---|---|---|
| Import | `require('module')` | `import x from 'module'` |
| Export | `module.exports = ...` | `export default ...` / `export { x }` |
| Biến đường dẫn file | `__dirname`, `__filename` có sẵn | Không có sẵn — dùng `import.meta.url` |
| Top-level `await` | ❌ không hỗ trợ | ✅ hỗ trợ |
| Cách load module | Đồng bộ (`require` chạy xong ngay, đọc file ngay lúc gọi) | Bất đồng bộ, được phân tích tĩnh (static analysis) trước khi chạy |
| Cách bật | mặc định, hoặc đặt file đuôi `.cjs` | `"type": "module"` trong `package.json`, hoặc đặt file đuôi `.mjs` |

Khác biệt "đồng bộ vs bất đồng bộ" ở dòng "Cách load module" không chỉ là chi tiết vặt — nó là lý do ESM hỗ trợ được top-level `await` (chờ 1 Promise ngay ở ngoài cùng file, không cần bọc trong `async function`) còn CJS thì không: cơ chế `require` được thiết kế để trả kết quả ngay lập tức, không có chỗ cho việc "chờ".

> [!warning] Lưu ý khi setup project
> Trường `"type"` trong `package.json` quyết định Node hiểu file `.js` là CJS hay ESM. Đặt sai sẽ gây lỗi `require is not defined` (nếu để `"type": "module"` mà code dùng `require`) hoặc `Cannot use import statement outside a module` (nếu ngược lại). Khi trộn TypeScript vào, `tsconfig.json` (`module: "nodenext"`) cũng phải khớp với `"type"` trong `package.json`, nếu không TypeScript sẽ biên dịch ra output sai định dạng so với những gì Node thực sự chạy được.

## 3. `process` — global object

`process` là 1 object có sẵn ở **mọi nơi** trong code Node (không cần `require`/`import` gì cả), đại diện cho chính tiến trình (process) Node đang chạy. Một số thuộc tính hay dùng nhất trong backend:

- **`process.env`** — nơi đọc biến môi trường (environment variables). Đây là cách chuẩn để truyền config/secret (connection string DB, API key, `NODE_ENV`...) vào app **mà không hardcode trong code** — quan trọng vì code thường được commit lên git công khai, còn secret thì không nên bao giờ nằm trong code.
- **`process.version`** — version Node đang chạy (vd `v26.6.0`), hữu ích khi debug lỗi liên quan tới tương thích version.
- **`process.argv`** — mảng các tham số dòng lệnh được truyền vào khi chạy script (vd `node script.js abc` → `process.argv[2]` là `"abc"`).
- **`process.exit(code)`** — thoát tiến trình thủ công. `code = 0` nghĩa là thoát thành công, khác 0 nghĩa là có lỗi — quy ước này được các tool khác (CI, shell script) dùng để biết script vừa chạy có lỗi hay không.

> [!tip] So với biến môi trường ở frontend
> Next.js cũng có `process.env.NEXT_PUBLIC_...`, nhưng đó là biến được Next **nhúng cứng vào bundle lúc build** (do chạy trên trình duyệt, không có tiến trình Node thật ở runtime phía client). Ở backend, `process.env` là biến môi trường **thật**, được đọc lại mỗi lần server khởi động, đổi giá trị không cần build lại code.

## 4. Module `http` thuần (chưa dùng framework)

Đây là những gì Express/Nest **đóng gói và làm hộ** bạn — hiểu được `http` thuần giúp hiểu rõ framework đang trừu tượng hoá cái gì, thay vì dùng như hộp đen.

```js
import { createServer } from 'node:http'

const server = createServer((req, res) => {
  // req, res ở đây là raw — không có body parser, không có router có sẵn
})

server.listen(3000)
```

`createServer` nhận vào 1 callback được gọi **mỗi khi có request mới tới**. `req` (request) và `res` (response) là 2 object Node tự tạo cho từng request — đây chính là 2 object mà Express bọc thêm 1 lớp tiện ích lên trên (`req.params`, `res.json()`...) mà bạn sẽ thấy ở Tuần 2.

### 4.1. Request là một **readable stream**

Node **không tự đọc body cho bạn** — đây là điểm khác biệt lớn nhất so với các framework "full-stack" của ngôn ngữ khác (vd Laravel/Rails tự parse sẵn). Muốn lấy dữ liệu POST/PUT, phải tự lắng nghe stream dữ liệu đổ về theo từng mẩu nhỏ (chunk):

```js
let data = ''
req.addListener('data', (chunk) => { data += chunk })
req.addListener('end', () => {
  // data đã đầy đủ ở đây — HTTP request đã nhận xong toàn bộ body
})
```

`addListener` ở đây là alias của `req.on(...)` (2 cách viết tương đương, `on` phổ biến hơn trong code thực tế). Sự kiện `'data'` bắn ra nhiều lần liên tiếp — mỗi lần 1 chunk (network chia dữ liệu lớn thành nhiều gói nhỏ), và sự kiện `'end'` chỉ bắn ra đúng 1 lần khi toàn bộ dữ liệu đã về hết. Đây chính là mô hình **stream** — thiết kế để Node có thể xử lý dữ liệu lớn (upload file vài trăm MB) mà không cần load hết vào RAM cùng lúc.

> [!bug] Lỗi hay gặp: `ERR_HTTP_HEADERS_SENT`
> Đăng ký listener `'data'`/`'end'` là **bất đồng bộ** — dòng code ngay phía dưới đoạn đăng ký listener **vẫn chạy tiếp ngay lập tức**, không đợi `'end'` bắn ra. Nếu quên `return` sau khi đăng ký xong listener, luồng thực thi sẽ "rơi" (fall through) xuống nhánh xử lý tiếp theo trong hàm (ví dụ nhánh 404 mặc định ở cuối), gọi `res.writeHead`/`res.end` ở đó **trước** — rồi vài mili-giây sau, khi `'end'` thật sự bắn ra, code trong callback lại cố gọi `res.end` **lần thứ hai** trên cùng 1 response → Node báo lỗi vì header/response đã được gửi đi rồi, không thể gửi lại.
>
> **Fix**: luôn đặt `return;` ngay sau khi đăng ký xong các listener bất đồng bộ trong 1 route, để chặn code rơi xuống các nhánh xử lý khác.

### 4.2. `res.end()` không tự serialize object

```js
res.end({ error: 'abc' })                  // ❌ TypeError [ERR_INVALID_ARG_TYPE]
res.end(JSON.stringify({ error: 'abc' }))  // ✅ đúng
```

`res.end()` là API rất thấp cấp — nó chỉ nhận `string | Buffer | Uint8Array` (dữ liệu ở dạng byte/text thô, sẵn sàng để đẩy thẳng qua network), hoàn toàn không biết gì về JSON. Object JavaScript phải được tự tay chuyển thành chuỗi (`JSON.stringify`) trước khi đưa cho `res.end`. Đây chính là việc `res.json()` của Express sẽ làm hộ bạn ở Tuần 2.

### 4.3. Set status code + headers: `res.writeHead(status, headers)`

```js
res.writeHead(200, { 'Content-Type': 'application/json' })
res.end(JSON.stringify({ status: 'ok' }))
```

`writeHead` phải được gọi **trước** `res.end()`, và chỉ được gọi **đúng 1 lần** cho mỗi response (đây chính là nguồn gốc lỗi `ERR_HTTP_HEADERS_SENT` ở trên — gọi lần 2 là lỗi). `Content-Type` báo cho client biết nên hiểu dữ liệu trả về theo định dạng gì (JSON, HTML, plain text...) để parse đúng cách.

### 4.4. try/catch — chỉ bọc đúng chỗ có thể throw

Không cần tách hàm riêng để try/catch cho "sạch" — chỉ cần bọc đúng đoạn code có khả năng throw lỗi (ở đây là `JSON.parse`, sẽ throw nếu client gửi JSON sai định dạng) ngay trong chính callback bất đồng bộ đó:

```js
req.addListener('end', () => {
  try {
    const parsed = JSON.parse(data) // chỉ dòng này có khả năng throw
    res.writeHead(200, { 'Content-Type': 'application/json' })
    res.end(JSON.stringify({ ...parsed, receivedAt: new Date().toISOString() }))
  } catch {
    res.writeHead(400, { 'Content-Type': 'application/json' })
    res.end(JSON.stringify({ error: 'Data format is not correct!' }))
  }
})
```

## 5. HTTP Status Code — chọn đúng ngữ nghĩa

Status code không chỉ là con số — nó là 1 phần của "hợp đồng" API, giúp client (frontend, mobile app, service khác) biết cách xử lý response mà không cần đọc nội dung body. Chọn sai status code khiến client xử lý sai logic (ví dụ nhầm lỗi input của chính họ thành lỗi server, rồi retry vô ích).

| Code                          | Ý nghĩa                                                             | Khi nào dùng                                                                                           |
| ----------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **400** Bad Request           | Input từ client sai định dạng/thiếu dữ liệu                         | JSON parse lỗi, thiếu field bắt buộc, sai kiểu dữ liệu                                                 |
| **401** Unauthorized          | Chưa xác thực (chưa đăng nhập / token sai, hết hạn)                 | Thiếu token, token sai/hết hạn                                                                         |
| **403** Forbidden             | Đã xác thực nhưng không đủ quyền                                    | User đã login nhưng không có quyền truy cập resource đó                                                |
| **404** Not Found             | Không tìm thấy route/resource                                       | Sai URL, id không tồn tại trong DB                                                                     |
| **500** Internal Server Error | Lỗi phía **server** (bug, crash, DB down, code throw ngoài dự tính) | **Không** dùng cho lỗi do input của client — input sai luôn là lỗi của client (400), không phải server |

> [!tip] Mẹo phân biệt 401 vs 403
> 401 = "tôi không biết anh là ai" (chưa xác thực được danh tính). 403 = "tôi biết anh là ai rồi, nhưng anh không được phép làm việc này" (đã xác thực, nhưng thiếu quyền/permission). Nhầm giữa 2 cái này là lỗi rất phổ biến kể cả với dev có kinh nghiệm.

> [!tip] Vì sao 500 không nên dùng cho lỗi input
> Về mặt thiết kế API, dải mã **4xx** luôn có nghĩa "vấn đề nằm ở phía client" (họ có thể tự sửa bằng cách gửi lại request đúng), còn dải **5xx** luôn có nghĩa "vấn đề nằm ở phía server" (client gửi đúng nhưng server tự nó lỗi, retry lại cũng vô ích, cần dev sửa code). Trả nhầm 500 cho lỗi input khiến hệ thống giám sát lỗi (error monitoring) báo động nhầm là server đang có sự cố, trong khi thực ra chỉ là 1 client gửi sai dữ liệu.

## 6. Bài tập đã hoàn thành

Server `http` thuần với `GET /health` và `POST /echo` (đọc JSON body từ stream, trả lại kèm `receivedAt`), đã qua 3 vòng review sửa lỗi thật: fallthrough thiếu `return` (→ `ERR_HTTP_HEADERS_SENT`), quên `JSON.stringify` trước khi `res.end`, và chọn sai status code (500 → sửa thành 400 đúng ngữ nghĩa). Code hoàn chỉnh xem trong `demo.mjs` ở repo.

## Liên quan
- [[Tuần 1 - Setup Project & Mẹo]]
- [[Express - Nest]]
