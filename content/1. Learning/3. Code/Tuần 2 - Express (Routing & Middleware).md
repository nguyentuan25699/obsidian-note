
> [!info] Về file này
> Gộp kiến thức + bài tập phía **Express** cho chủ đề Routing & Middleware, cập nhật thêm sau mỗi buổi (1 → 3). Phần Nest tương ứng: [[Tuần 2 - Nest (Routing & Middleware)]] *(sẽ xuất hiện ở buổi 4)*. Bảng so sánh 2 bên: [[Tuần 2 - So sánh Express vs Nest]] *(sẽ xuất hiện ở buổi 5)*.

## Buổi 1 — Routing cơ bản

### Khái niệm

Ở Tuần 1, server `http` thuần phải tự so sánh `req.method` và `req.url` bằng if/else để quyết định xử lý request nào — cách này không scale được khi có hàng chục/hàng trăm route. Express giải quyết bằng 1 hệ thống **routing khai báo**: đăng ký sẵn "URL này + method này thì chạy hàm nào", Express tự lo phần so khớp (matching) bên trong.

```js
app.get('/products', (req, res) => { ... })       // đọc danh sách
app.post('/products', (req, res) => { ... })      // tạo mới
app.put('/products/:id', (req, res) => { ... })   // cập nhật toàn bộ
app.delete('/products/:id', (req, res) => { ... }) // xoá
```

Mỗi HTTP method tương ứng với 1 "ý định" khác nhau theo quy ước REST — đây là lý do vì sao không gộp hết vào 1 route rồi tự if/else theo `req.method` như hồi Tuần 1: khai báo tách theo method giúp code tự mô tả rõ ràng "route này dùng để làm gì" chỉ qua việc đọc tên hàm (`app.get` vs `app.post`), không cần đọc vào bên trong logic mới hiểu.

**Route param** — phần đường dẫn có thể thay đổi theo từng request, khai báo bằng dấu `:` (vd `:id` trong `/products/:id`), đọc giá trị thực tế qua `req.params.id`. Về bản chất tương tự dynamic route `[id].tsx` của Next.js — khác biệt chính là ở Next bạn đọc qua `useRouter().query` (client-side) hoặc tham số hàm `getServerSideProps` (server-side), còn ở Express luôn đọc qua `req.params` vì toàn bộ logic đều chạy trên server, không có khái niệm "client re-render lại route" như SPA.

**Query string** — phần sau dấu `?` trong URL (vd `/products?category=shoes&sort=price`), dùng để truyền tham số **không bắt buộc**, thường cho việc lọc/sắp xếp/phân trang. Đọc qua `req.query`, Express tự parse thành object (`req.query.category` → `"shoes"`). Khác với route param (`:id` — bắt buộc phải có, thiếu là route không khớp), query string luôn optional — route vẫn khớp bình thường dù có hay không có query.

**`res.json(data)`** — hàm tiện ích của Express, làm hộ 2 việc: tự set header `Content-Type: application/json`, và tự gọi `JSON.stringify(data)` trước khi gửi đi. Đây chính là phần thay thế cho `res.writeHead(...) + res.end(JSON.stringify(...))` phải tự viết tay ở Tuần 1 — Express không phát minh ra cơ chế mới, chỉ đóng gói lại đúng những gì `http` thuần đã làm thành 1 lệnh gọn hơn.

> [!tip] So với module `http` thuần (Tuần 1)
> Những thứ Express làm hộ ở buổi này: (1) tự so khớp `req.url`/`req.method` với route đã đăng ký thay vì tự viết if/else, (2) tự parse route param và query string thành object thay vì tự cắt chuỗi `req.url`, (3) tự `JSON.stringify` + set header qua `res.json()`. Bản chất bên dưới vẫn là request/response object của Node `http` — Express chỉ bọc thêm property và method tiện lợi lên trên (`req.params`, `req.query`, `res.json` không tồn tại trong Node gốc).

### Bài tập
CRUD (phần đọc) cho resource `products` in-memory:
- `GET /products` — toàn bộ danh sách
- `GET /products?category=xxx` — lọc theo category qua query string
- `GET /products/:id` — 1 sản phẩm theo id, `404` nếu không có

Qua 2 vòng review, sửa 4 lỗi thật:
- Đặt route số ít `/product/:id` thay vì `/products/:id` — sai theo quy ước REST (route số ít/nhiều luôn cùng 1 resource, `:id` chỉ là cách chọn ra 1 phần tử trong collection, không đổi tên resource — giống `products[3]` vẫn là mảng `products`).
- Dùng `res.writeHead + res.end(JSON.stringify(...))` kiểu Tuần 1 thay vì `res.json()`/`res.status()` của Express.
- Typo `'application.json'` (phải là `application/json`) và `"Page note found"` (phải là "not found").
- (kiến thức thêm, không phải lỗi) `res.status(200).json(...)` — gọi `.json()` một mình đã mặc định trả `200` rồi, chỉ cần `.status()` khi muốn đổi khác mặc định.

> [!bug] Ngã rẽ thú vị: `import type e = require('express')`
> Ban đầu nghi ngờ cách import này "vòng vo", đề xuất đổi sang `import express, { Request, Response } from 'express'` — nhưng test thật bằng `tsc --noEmit` thì cú pháp đề xuất **lỗi biên dịch**: `TS1295: ECMAScript imports and exports cannot be written in a CommonJS file under 'verbatimModuleSyntax'`.
>
> Lý do: project có `"type": "commonjs"` (package.json) + `verbatimModuleSyntax: true` (tsconfig) → TypeScript cấm cú pháp `import` ESM thật trong file bản chất CommonJS. Cách lấy **type** (không phải giá trị) từ 1 package CJS trong hoàn cảnh này là cú pháp `import type X = require('...')` — chính là cách ban đầu đã viết. Bài học: đừng chỉ tin theo cảm giác "trông không quen mắt" — luôn verify bằng compiler khi nghi ngờ.

## Buổi 2 — Middleware

### Khái niệm

Middleware là 1 hàm chạy **xen giữa** lúc request tới và lúc route handler xử lý, chữ ký `(req, res, next)`. Dùng cho logic lặp lại ở nhiều/tất cả route (log, parse body, auth...) thay vì copy-paste vào từng handler.

```js
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`)
  next() // bắt buộc — quên hoặc gọi sai chỗ đều khiến request bị treo
})
```

- `app.use(...)` không path → chạy cho mọi request. Middleware phải đăng ký **trước** route mới có tác dụng (Express chạy theo đúng thứ tự khai báo).
- `express.json()` — middleware có sẵn của Express để parse JSON body vào `req.body`, không có nó `req.body` sẽ `undefined`.
- Tương đương interceptor của axios hoặc `middleware.ts` của Next.js — 1 lớp xử lý chung xen vào giữa pipeline.

### Bài tập
Thêm logging middleware (log method/url/status/thời gian xử lý) + `express.json()` + route `POST /products` (tạo mới, trả `201` kèm object vừa tạo).

Qua 2 vòng review, sửa 3 lỗi thật:
- **Bug nghiêm trọng — request treo vĩnh viễn**: đặt `next()` bên trong callback của `res.on('finish', ...)` thay vì gọi trực tiếp trong thân middleware. Deadlock vòng tròn: response cần route handler chạy để gửi (mà route handler cần `next()` được gọi trước), còn `'finish'` (nơi gọi `next()`) chỉ bắn ra sau khi response đã gửi xong — không bao giờ tới lượt. Test bằng `curl` xác nhận: request treo, timeout, không có response (`HTTP_CODE:000`). Fix: gọi `next()` ngay trong thân middleware, tách riêng khỏi việc log thời gian (vẫn dùng `res.on('finish', ...)` để log, nhưng không đặt `next()` trong đó).
- Import thừa không dùng tới: `import type NextFunction = require('express')` và `import type Request = require('express')` — dead code, chỉ cần đúng 1 import `e` là đủ vì đã có `e.Request`, `e.NextFunction`.
- `POST /products` ban đầu trả `res.json(items)` (cả mảng) — sửa lại trả đúng object vừa tạo (`res.status(201).json(newItem)`).

> [!tip] Ngã rẽ: `req.body as unknown as {...}`
> Nghi ngờ double-cast qua `unknown` là thừa (vì `req.body` mặc định type `any`, từ `any` luôn assert trực tiếp được) — verify bằng cách đọc thẳng definition file trong `node_modules/@types/express-serve-static-core`: `ReqBody = any` đúng như dự đoán, và compile thử `req.body as {...}` (không qua `unknown`) không hề báo lỗi. Không tìm được lỗi gốc để tái hiện — có thể tới từ ngữ cảnh code khác lúc đó. Kết luận: `as {...}` (assertion đơn) là đủ, không cần đường vòng qua `unknown`.

## Buổi 3 — Router & hoàn thiện CRUD
🔜 Chưa học.

## Liên quan
- [[00 - Lộ trình Backend (Master Plan)]]
- [[Tuần 2 - Nest (Routing & Middleware)]]
- [[Tuần 1 - Node.js Fundamentals]]