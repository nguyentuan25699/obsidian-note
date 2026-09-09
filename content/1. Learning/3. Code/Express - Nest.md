---
date: 2026-09-09
tags:
  - code
  - learning
  - backend
draft: false
related:
---

> [!info] Cách dùng file này
> Trang mục lục (MOC) cho toàn bộ lộ trình 8 tuần — mỗi tuần có 1 bảng riêng bên dưới. Bảng chỉ để tra nội dung + link ghi chú (Markdown table không hỗ trợ checkbox thật bên trong ô, nên tracking "xong hay chưa" nằm ở phần **Mục lục** và **Trạng thái dự án** — 2 chỗ đó là checkbox thật, bấm tick được).
>
> Dự án xuyên suốt: **Ecommerce API**, build song song 2 bản `express-api/` (thủ công) và `nest-api/` (Nest CLI), cùng 1 repo git.

> [!tip] Quy ước note — học song song = 2 file sống + 1 file so sánh
> Mỗi tuần có tối đa 3 file kiến thức, không phải 1 file/buổi:
> - `Tuần N - Express (chủ đề).md` — 1 file duy nhất, có section riêng cho từng buổi Express, nối dài thêm sau mỗi buổi thay vì tạo file mới.
> - `Tuần N - Nest (chủ đề).md` — tương tự, xuất hiện lần đầu ở buổi Nest đầu tiên trong tuần.
> - `Tuần N - So sánh Express vs Nest.md` — chỉ tạo ở buổi cuối tuần.
>
> Note trong bảng dưới trỏ về 1 trong 3 file trên. Link chưa có file thật (đỏ trong Obsidian) = chưa học tới phần đó.

## Mục lục

- [x] [[#Tuần 1 — Nền tảng Node.js]]
- [ ] [[#Tuần 2 — Routing & Middleware]]
- [ ] [[#Tuần 3 — Kiến trúc & Dependency Injection]]
- [ ] [[#Tuần 4 — Database quan hệ (SQL)]]
- [ ] [[#Tuần 5 — Database phi quan hệ (NoSQL)]]
- [ ] [[#Tuần 6 — Auth, Validation & Testing]]
- [ ] [[#Tuần 7 — Docker & chuẩn bị deploy]]
- [ ] [[#Tuần 8 — Deploy thật & tổng kết]]

---

## Tuần 1 — Nền tảng Node.js

| Nội dung | Note |
|---|---|
| Event loop, CJS vs ESM, `process` global | [[Tuần 1 - Node.js Fundamentals]] |
| Server module `http` thuần (hiểu Express/Nest làm gì bên dưới) | [[Tuần 1 - Node.js Fundamentals]] |
| Setup TypeScript cơ bản cho dự án Node | [[Tuần 1 - Setup Project & Mẹo]] |
| Dự án: khởi tạo repo + cấu trúc thư mục Express/Nest | [[Tuần 1 - Setup Project & Mẹo]] |

## Tuần 2 — Routing & Middleware

Tách thành 5 buổi, mỗi buổi 1 ý, tránh dồn routing + middleware + Nest vào 1 lần.

- [ ] Buổi 1 — Express routing cơ bản (`app.get/post/...`, route params, query string)
- [ ] Buổi 2 — Express middleware (`app.use`, custom middleware, thứ tự chạy, `next()`)
- [ ] Buổi 3 — Express `Router` — tách route ra file riêng, hoàn thiện CRUD `products`
- [ ] Buổi 4 — Nest Controllers & decorator (`@Controller`, `@Get/@Post`, `@Param/@Body`)
- [ ] Buổi 5 — DTO cơ bản + so sánh Middleware vs Guards/Interceptors/Pipes + tổng kết tuần

| Buổi | Nội dung | Note |
|---|---|---|
| 1-3 | Xem chi tiết từng buổi ở trên | [[Tuần 2 - Express (Routing & Middleware)]] |
| 4-5 | Xem chi tiết từng buổi ở trên | [[Tuần 2 - Nest (Routing & Middleware)]] |
| 5 | So sánh Middleware vs Guards/Interceptors/Pipes | [[Tuần 2 - So sánh Express vs Nest]] |

## Tuần 3 — Kiến trúc & Dependency Injection

| Nội dung | Note |
|---|---|
| Nest: Modules, Providers, Services, DI | [[Tuần 3 - Nest (Kiến trúc & DI)]] |
| Express: tự tổ chức service/controller layer tương đương | [[Tuần 3 - Express (Kiến trúc & DI)]] |
| So sánh độ linh hoạt vs độ chặt chẽ | [[Tuần 3 - So sánh Express vs Nest]] |
| Dự án: refactor code Tuần 2 theo layer controller/service/repository | [[Tuần 3 - Express (Kiến trúc & DI)]] · [[Tuần 3 - Nest (Kiến trúc & DI)]] |

## Tuần 4 — Database quan hệ (SQL)

| Nội dung | Note |
|---|---|
| PostgreSQL/MySQL cơ bản, chạy local qua Docker | [[Tuần 4 - Express (SQL & Prisma)]] · [[Tuần 4 - Nest (SQL & Prisma)]] |
| ORM Prisma: schema, migration, query cơ bản | [[Tuần 4 - Express (SQL & Prisma)]] · [[Tuần 4 - Nest (SQL & Prisma)]] |
| Kết nối DB vào cả Express và Nest | [[Tuần 4 - Express (SQL & Prisma)]] · [[Tuần 4 - Nest (SQL & Prisma)]] |
| Dự án: `products` lưu DB thật + migration, thêm `orders` liên kết | [[Tuần 4 - Express (SQL & Prisma)]] · [[Tuần 4 - Nest (SQL & Prisma)]] |

## Tuần 5 — Database phi quan hệ (NoSQL)

| Nội dung | Note |
|---|---|
| MongoDB + Mongoose: document/collection, khi nào nên dùng NoSQL | [[Tuần 5 - Express (MongoDB)]] · [[Tuần 5 - Nest (MongoDB)]] |
| So sánh Mongoose (Express) vs `@nestjs/mongoose` (Nest) | [[Tuần 5 - So sánh Express vs Nest]] |
| Dự án: thêm `reviews` dùng MongoDB (dùng chung SQL + NoSQL) | [[Tuần 5 - Express (MongoDB)]] · [[Tuần 5 - Nest (MongoDB)]] |

## Tuần 6 — Auth, Validation & Testing

| Nội dung | Note |
|---|---|
| JWT: đăng ký/đăng nhập, hash password (bcrypt), guard/middleware bảo vệ route | [[Tuần 6 - Express (Auth & Validation)]] · [[Tuần 6 - Nest (Auth & Validation)]] |
| Validation: `express-validator`/Joi vs `class-validator` + DTO | [[Tuần 6 - So sánh Express vs Nest]] |
| Testing cơ bản với Jest cho service layer | [[Tuần 6 - Express (Auth & Validation)]] · [[Tuần 6 - Nest (Auth & Validation)]] |
| Dự án: auth (user chỉ thấy đơn của mình), validate input, viết 2-3 test | [[Tuần 6 - Express (Auth & Validation)]] · [[Tuần 6 - Nest (Auth & Validation)]] |

## Tuần 7 — Docker & chuẩn bị deploy

| Nội dung | Note |
|---|---|
| Dockerfile cho app Node, docker-compose (app + DB) | [[Tuần 7 - Express (Docker)]] · [[Tuần 7 - Nest (Docker)]] |
| Biến môi trường `.env`, tách config dev/production | [[Tuần 7 - Express (Docker)]] · [[Tuần 7 - Nest (Docker)]] |
| CI cơ bản (GitHub Actions): lint/test khi push | [[Tuần 7 - Express (Docker)]] · [[Tuần 7 - Nest (Docker)]] |
| Dự án: dockerize cả 2 bản, chạy thử `docker-compose up` | [[Tuần 7 - Express (Docker)]] · [[Tuần 7 - Nest (Docker)]] |

## Tuần 8 — Deploy thật & tổng kết

| Nội dung | Note |
|---|---|
| Deploy 1 bản (Express hoặc Nest) lên Render/Railway/VPS | [[Tuần 8 - Express (Deploy)]] · [[Tuần 8 - Nest (Deploy)]] |
| Domain/HTTPS cơ bản nếu deploy VPS | [[Tuần 8 - Express (Deploy)]] · [[Tuần 8 - Nest (Deploy)]] |
| Tổng kết ưu/nhược điểm Express vs Nest từ trải nghiệm thực tế | [[Tuần 8 - So sánh Express vs Nest]] |
| Dự án: Ecommerce API hoàn chỉnh chạy online + hướng học tiếp | [[Tuần 8 - Express (Deploy)]] · [[Tuần 8 - Nest (Deploy)]] |

---

## Trạng thái dự án Ecommerce API

- [x] Repo + cấu trúc thư mục (`express-api/`, `nest-api/`) khởi tạo, cả 2 chạy "Hello World"
- [ ] CRUD in-memory `products` — Express
- [ ] CRUD in-memory `products` — Nest
- [ ] Refactor theo layer controller/service/repository (Tuần 3)
- [ ] Kết nối DB thật SQL — resource `products` + `orders` (Tuần 4)
- [ ] Kết nối MongoDB — resource `reviews` (Tuần 5)
- [ ] Auth (JWT) + validation + test cơ bản (Tuần 6)
- [ ] Dockerize cả 2 bản (Tuần 7)
- [ ] Deploy thật 1 bản lên hosting (Tuần 8)

## Ghi chú tổng hợp theo chủ đề

*(sẽ điền dần khi có đủ nội dung so sánh xuyên suốt nhiều tuần)*

- So sánh Express vs Nest: *(chưa tạo)*
- Auth & bảo mật: *(chưa tạo)*
- Database & ORM: *(chưa tạo)*