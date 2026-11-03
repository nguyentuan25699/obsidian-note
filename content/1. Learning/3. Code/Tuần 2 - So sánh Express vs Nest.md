> [!info] Về file này
> Tổng kết đối chiếu trực tiếp sau khi làm cùng 1 bài toán (CRUD `products`) ở cả 2 framework. Chi tiết từng bên: [[Tuần 2 - Express (Routing & Middleware)]] · [[Tuần 2 - Nest (Routing & Middleware)]].

## Routing

| | Express | Nest |
|---|---|---|
| Khai báo route | Gọi hàm: `app.get('/products', handler)` | Decorator trên class: `@Controller('products')` + `@Get()` |
| Lấy route param | `req.params.id` | `@Param('id') id: string` |
| Lấy query string | `req.query.category` | `@Query('category') category?: string` |
| Lấy body | `req.body` | `@Body() body: CreateProductDto` |
| Trả response | Gọi API: `res.json(data)`, `res.status(201).json(data)` | Return giá trị, framework tự gửi + tự set status theo method (`@Get`→200, `@Post`→201) |
| Trả lỗi | Gọi API: `res.status(404).json({...})` | `throw new NotFoundException(...)` — throw, không return |

**Khác biệt triết lý cốt lõi**: Express là **imperative** (tự tay gọi API để điều khiển response), Nest là **declarative** (khai báo cấu trúc bằng decorator, return/throw giá trị, framework tự lo phần "cách gửi đi"). Không cái nào "hơn" cái nào — Express cho toàn quyền kiểm soát, Nest đánh đổi bớt quyền kiểm soát để lấy code ngắn gọn + nhất quán hơn giữa các route.

## Tách route ra file riêng

| | Express | Nest |
|---|---|---|
| Cơ chế | `express.Router()`, tự tạo file, tự `app.use(prefix, router)` | `@Controller()` tự nhiên đã là 1 class riêng, đăng ký qua `controllers: [...]` trong Module |
| Bắt buộc hay tuỳ chọn | Tuỳ chọn — Express không ép, tự quyết định khi nào tách | Nest tự nhiên đã tách theo class, không có kiểu "viết hết vào 1 file" như Express |

## Middleware / Guard / Pipe / Interceptor

| | Vai trò | Express | Nest |
|---|---|---|---|
| Middleware | Chạy sớm, chưa biết route nào xử lý | `app.use((req,res,next) => ...)` | Tương tự, nhưng khai báo qua `NestMiddleware` + `configure()` trong Module (chưa viết, sẽ gặp ở Tuần 3+) |
| Guard | Cho phép/chặn request (auth) | Middleware tự viết `if (!isAuth) return res.status(401)` | `@UseGuards(...)` — tách riêng thành khái niệm, không gộp vào middleware (viết thật ở Tuần 6) |
| Pipe | Biến đổi/validate input | Code validate thủ công đầu handler | `@Param('id', ParseIntPipe)` — validate + transform khai báo ngay trên tham số, chặn trước khi vào handler |
| Interceptor | Can thiệp trước lẫn sau handler | Middleware + tự bọc logic quanh handler | `@UseInterceptors(...)` (chưa viết, sẽ gặp ở Tuần 6) |

Nest tách 4 khái niệm rõ ràng theo đúng "thời điểm chạy" + "mục đích", trong khi Express gộp tất cả vào 1 khái niệm middleware duy nhất — linh hoạt hơn nhưng đòi hỏi tự kỷ luật để không lẫn lộn trách nhiệm giữa các middleware.

## Bug thật đã gặp — điểm chung đáng nhớ

Cả 2 bên đều dính đúng 1 dạng bug giống nhau dù cú pháp khác hẳn: **quên/đặt sai chỗ bước "chuyển tiếp xử lý"**.
- Express: đặt `next()` bên trong `res.on('finish', ...)` thay vì gọi trực tiếp → deadlock, request treo vĩnh viễn (response cần route chạy để gửi, route cần `next()` gọi trước, `next()` lại chờ response gửi xong — vòng lặp chết).
- Nest: `return new NotFoundException(...)` thay vì `throw` → exception bị coi như giá trị trả về bình thường, serialize thành JSON với status 200 thay vì 404.

Bài học chung: cả 2 framework đều có 1 "quy tắc ngầm" về cách giao quyền xử lý tiếp theo (`next()` bên Express, `throw` bên Nest) — hiểu sai cơ chế này gây lỗi khó nhận ra ngay (không crash rõ ràng, chỉ sai hành vi).

## Liên quan
- [[Express - Nest]]
- [[Tuần 2 - Express (Routing & Middleware)]]
- [[Tuần 2 - Nest (Routing & Middleware)]]
