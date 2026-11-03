> [!info] Về file này
> Gộp kiến thức + bài tập phía **Nest** cho chủ đề Routing & Middleware (buổi 4-5 của Tuần 2). Phần Express tương ứng: [[Tuần 2 - Express (Routing & Middleware)]]. Bảng so sánh 2 bên: [[Tuần 2 - So sánh Express vs Nest]] *(sẽ xuất hiện ở buổi 5)*.

## Buổi 4 — Nest Controllers & Decorator

### Khái niệm

Nest không dùng hàm `app.get(...)` như Express — dùng **class + decorator**:

```ts
@Controller('products')
export class ProductsController {
  @Get()
  findAll(@Query('category') category?: string) { ... }   // GET /products

  @Get(':id')
  findOne(@Param('id') id: string) { ... }                 // GET /products/:id

  @Post()
  create(@Body() body: {...}) { ... }                      // POST /products
}
```

- `@Controller('products')` — tương đương phần mount prefix (`app.use('/products', router)`) đã làm ở Buổi 3 bên Express, chỉ khác là khai báo ngay trên class thay vì gọi hàm lúc runtime.
- `@Get()`, `@Post()` — tương đương `router.get()`, `router.post()`. Ý nghĩa REST của từng method HTTP không đổi so với Buổi 1.
- **Không có `req`/`res` trực tiếp** — lấy dữ liệu qua decorator tham số: `@Param('id')` thay `req.params.id`, `@Query('category')` thay `req.query.category`, `@Body()` thay `req.body`. Route "khai báo rõ" ngay trên chữ ký hàm cần gì, thay vì đọc thủ công từ object `req`.
- **Return giá trị = response body** — không gọi `res.json()`/`res.status()` thủ công. `@Get` mặc định trả `200`, `@Post` mặc định trả `201`. Đây là khác biệt triết lý lớn nhất so với Express: Express "imperative" (tự gọi API để gửi response), Nest "declarative" (return giá trị, framework tự lo phần gửi đi).
- **Lỗi thì `throw`, không `return`** — `throw new NotFoundException('...')`, `throw new BadRequestException('...')`. Tên class ứng đúng status code đã học ở Buổi 1 (`NotFoundException` → 404, `BadRequestException` → 400, `UnauthorizedException` → 401, `ForbiddenException` → 403...). Nest bắt exception, tự dựng response `{ statusCode, message, error }`.
- Controller phải đăng ký vào `controllers: [...]` trong 1 **Module** (`app.module.ts`) thì Nest mới nhận diện được — quan trọng, thiếu bước này thì route không tồn tại dù code controller không lỗi gì. Cơ chế Module/DI đầy đủ học kỹ ở Tuần 3.

### Bài tập
CRUD (đọc + tạo) cho resource `products`, y hệt bài Express để so sánh trực tiếp: `GET /products` (+ filter category), `GET /products/:id`, `POST /products`.

Qua 5 vòng review, sửa các lỗi thật:
- **`return new NotFoundException(...)` thay vì `throw`** (3 chỗ) — return 1 exception nghĩa là Nest coi nó như giá trị bình thường, serialize thành JSON và trả **200**, không phải 404. Phải `throw` thì Nest mới bắt và biến thành đúng HTTP response.
- **`ProductsController` chưa đăng ký vào `app.module.ts`** — verify bằng cách chạy thật và đọc log Nest lúc khởi động: chỉ thấy `Mapped {/, GET}` (route của `AppController`), không có route `/products` nào. `curl /products` → `404 Cannot GET /products`. Thiếu dòng import + thêm vào mảng `controllers: [AppController, ProductsController]`.
- **`findAll` logic sai nhiều vòng liên tiếp** — ban đầu dùng `if (!category || itemsFound)` (array luôn truthy → luôn nhảy vào throw, dead code phía dưới); sửa còn `!category` → throw 404 khi không có query (sai, phải trả toàn bộ); sửa tiếp còn `!itemsFound.length` → throw 404 khi filter ra rỗng (cũng sai — tìm không ra kết quả vẫn là **200 `[]`**, không phải 404, vì `/products` vẫn tồn tại, chỉ là filter rỗng). Bản đúng cuối cùng: `findAll` **không có `throw` nào cả**, chỉ 2 nhánh return (toàn bộ / đã lọc).
- **Validation `create` bằng `Object.keys(body)`** — duyệt key **đang có sẵn** trong body rồi check falsy, nên thiếu hẳn 1 field (không có key đó) lại lọt qua. Sửa bằng danh sách field bắt buộc cố định: `const keys = ['name', 'price', 'category']`.

> [!bug] Bài học debug quan trọng nhất buổi này
> "Tìm không ra kết quả" (empty list) và "resource không tồn tại" (404) là 2 khái niệm khác nhau hoàn toàn trong REST — dễ nhầm nhất khi mới quen `NotFoundException`. Quy tắc: **list endpoint (`findAll`) không bao giờ throw 404** — luôn trả `200` kèm mảng (đầy hoặc rỗng). `404` chỉ dành cho việc tìm **1** resource cụ thể theo id/khoá chính mà không có (`findOne`).

## Buổi 5 — DTO + so sánh Middleware vs Guards/Interceptors/Pipes

### Khái niệm

**DTO (Data Transfer Object)** — tách type body ra thành class riêng (`create-product.dto.ts`) thay vì khai báo inline trong controller. Lợi ích: DTO là class thật, sau này gắn được decorator validate (`@IsString()`...) — nền cho `class-validator` ở Tuần 6.

**Middleware (Express) vs Guards/Interceptors/Pipes (Nest)** — cùng mục đích "xử lý xen giữa request và route handler", Nest chia nhỏ theo đúng việc đang làm thay vì gộp chung:

| | Vai trò | Tương đương Express |
|---|---|---|
| Middleware | Chạy sớm, chưa biết route nào xử lý | `app.use(...)` |
| Guard | Cho phép/chặn request (auth/permission) | middleware tự viết check auth |
| Pipe | Biến đổi/validate input trước route handler | code validate thủ công đầu handler |
| Interceptor | Can thiệp trước lẫn sau route handler | middleware + tự bọc logic quanh handler |

Guard/Interceptor để dành viết thật ở Tuần 6 (gắn với auth JWT thật, không viết bài tập rỗng). Pipe thì áp dụng ngay được, không cần chờ auth.

### Bài tập

1. Tách `CreateProductDto` ra `src/products/dto/create-product.dto.ts`, dùng trong `create()` thay type inline.
2. Áp dụng `ParseIntPipe` có sẵn của Nest cho `:id`: `@Param('id', ParseIntPipe) id: number` — Nest tự validate + convert, chặn input sai (`id=abc`) **trước khi** vào handler, tự trả `400` không cần code tay.

Qua review, sửa 2 lỗi thật:
- Tên file `create-product-dto.ts` (gạch ngang trước "dto") lệch quy ước Nest — đúng phải là `create-product.dto.ts` (dấu chấm, giống hệt `.controller.ts`).
- `if (!id || !itemFound)` — sau khi có `ParseIntPipe`, `id` luôn là number hợp lệ khi vào tới handler. Giữ `!id` không chỉ thừa mà còn **là bug tiềm ẩn**: nếu tồn tại sản phẩm `id: 0`, `!0` = `true` trong JS → dù `itemFound` tìm thấy đúng item, vẫn bị nhảy vào nhánh `throw 404` sai. Bỏ hẳn `!id`, chỉ giữ `!itemFound` — `.find()` đã trả đúng "có tìm thấy hay không" cho mọi giá trị `id`, kể cả 0.

> [!tip] Mẹo review code: cẩn thận với falsy check trên number
> `!x` coi cả `0`, `NaN`, `''` là "thiếu giá trị" giống `undefined`/`null`. Với number có thể hợp lệ bằng `0` (id, số lượng, giá...), luôn ưu tiên check tường minh (`x === undefined`) hoặc dựa vào kết quả đã có sẵn ý nghĩa đúng (`!itemFound` — `undefined` khi thật sự không tìm thấy) thay vì suy luận qua 1 biến trung gian dễ nhầm.

## Liên quan
- [[Express - Nest]]
- [[Tuần 2 - Express (Routing & Middleware)]]
