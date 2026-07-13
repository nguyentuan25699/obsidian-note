## 1. Các loại biến

- var, let: có thể reassigned
- const: không thể reassigned
## 2. Các loại scope
- Global: Bao gồm biến var, const, let được khai báo ngài cùng của file javascript.
- Block code: Bao gồm biến let, const được khai báo trong block code như: if else, switch case sẽ có phạm vi trong block code, trường hợp var được khai báo trong block code sẽ có phạm vi global.
- Local: Còn được gọi phạm vi hàm, bao gồm let, const, var hoặc hàm được khai báo trong một hàm sẽ tạo ra phạm vi hàm.
## 3. Khái niệm Closure
- Closure là một function ghi nhớ biến ở phạm vi bên ngoài của nó, kể cả khi phạm vi đó đã bị giải phóng.
```js
function outer() {
  let count = 0;
  return function () {
    return ++count;
  };
}
const counter = outer();

```

## 4. Trình bày sự khác nhau giữa [[localStorage]], [[cookies]], [[sessionStorage]] ?
- **localStorage**: Dung lượng ~5MB, Tồn tại vĩnh viễn, Không được truy cập từ server.
- **sessionStorage**: Dung lượng ~5MB, Tồn tại đến khi đóng tab, Không được truy cập từ server.
- **cookies**: Dung lượng ~4KB, Tồn tại tùy thuộc vào thời gian expired, Được truy cập từ server.

## 5. [[Xử lý bất đồng bộ trong JS]] ( Cách hoạt động, cú pháp của Promise, Callback, Async await )
...
## 6. Khái niệm [[Hoisting]]
- [[Hoisting]] là cơ chế mặc định của JavaScript để di chuyển tất cả các biến và hàm khi khai báo lên đầu scope trước khi chúng được thực thi. 
(*Lưu ý đối với cơ chế này nó chỉ di chuyển khai báo, còn việc gán giá trị thì giữ nguyên.*)

- **var** được hoist nhưng khởi tạo là undefined.
- **let/const** cũng được hoist nhưng không thể truy cập trước khi khai báo.

## 7. [[Truthy, Falsy]]
- Falsy: false, 0, '', null, undefined, NaN
- Truthy: mọi thứ còn lại

## 8. [[Box model]] là gì?
- Box model gồm content, padding, border, margin.
- Kích thước thực tế của element phụ thuộc vào box-sizing.

box-sizing: content-box và border-box khác nhau thế nào?
- content-box: width chỉ tính content.
- border-box: width bao gồm content + padding + border.

Trong layout thực tế thường dùng border-box để dễ kiểm soát kích thước.

## 9.  [[Specificity]] là gì?
- MDN định nghĩa specificity là thuật toán browser dùng để quyết định CSS declaration nào áp dụng khi nhiều selector cùng target một element.

Thứ tự: 
inline style > id > class/attribute/pseudo-class > tag/pseudo-element


Làm sao tránh specificity quá cao?
- Tránh lạm dụng id selector và !important.
- Ưu tiên class rõ ràng, component-scoped styles, naming convention như [[BEM]] hoặc [[CSS Modules]].
- Nếu specificity bị phình to, CSS sẽ khó override và maintain.
## 10. CSS
- [[Box model]]
- [[Specificity]]
- [[flex vs grid]]
- [[position]] vs [[z-index]]
- responsive
- CSS variable vs SCSS variablel
- [[mixin]]
- [[nesting]]
- CSS Modules/Tailwind trade-offf
- [[Sass - SCSS]]

## 11. Thuật toán điều hòa của React hoạt động như thế nào, và React Fiber tối ưu hóa những gì?
- React reconciliation là quá trình React so sánh cây UI mới với cây UI cũ để quyết định phần nào cần update thật trên DOM.
- React không diff toàn bộ DOM thật vì rất tốn kém. Thay vào đó, React tạo virtual tree mới sau mỗi lần state/props thay đổi, rồi so sánh với tree trước đó.


- React Fiber là kiến trúc nội bộ giúp chia công việc render thành nhiều đơn vị nhỏ hơn. Nhờ Fiber, React có thể tạm dừng, tiếp tục, ưu tiên hoặc hủy một render chưa cần thiết. Đây là nền tảng cho concurrent rendering, Suspense, useTransition và rendering theo độ ưu tiên.

| Đặc điểm                                      | Stack Reconciler (React < 16)                        | Fiber Reconciler (React >= 16)                                       |
|-----------------------------------------------|------------------------------------------------------|----------------------------------------------------------------------|
| Cách xử lý                                    | Đồng bộ (Synchronous)                                | Không đồng bộ (Asynchronous) & Có thể bị ngắt                        |
| Đơn vị làm việc                               | Duyệt cây component theo cấu trúc Stack (đệ quy sâu) | Fiber (đơn vị làm việc nhỏ)                                          |
| Khả năng tạm dừng/tiếp tục                    | Không thể                                            | Có thể (ở Giai đoạn Render)                                          |
| Khả năng ưu tiên công việc                    | Không                                                | Có                                                                   |
| Hiệu năng trên thiết bị chậm/bản cập nhật lớn | Có thể gây đơ UI (blocking)                          | Mượt mà hơn (non-blocking), phân bổ thời gian linh hoạt              |
| Hỗ trợ tính năng hiện đại                     | Không (hoặc hạn chế)                                 | Có (Concurrent Mode, Suspense, Transitions)                          |
| Mục tiêu chính                                | Tìm và áp dụng thay đổi hiệu quả                     | Đảm bảo UI mượt mà, phản hồi nhanh, cho phép các tính năng tương lai |


## 12. [[useTransition]]
- Một React hook giúp bạn đánh dấu một phần update là **không gấp**, để React ưu tiên giữ UI mượt trước.

## 13. React xử lý việc render đồng thời ra sao?
- React xử lý render đồng thời (Concurrent Rendering) bằng cách cho phép tạm dừng (pause), ngắt quãng (interrupt) hoặc ưu tiên các tác vụ render. Nó chia việc render thành các phần nhỏ, xử lý ngầm trong nền và chỉ cập nhật lên màn hình (commit) khi luồng chính rảnh rỗi, giúp giao diện không bị giật lag

## 14. [[React server component]]

## 15. [[Redux]]
## 16. [[Async techniques]]

## 17. [[HTML5]]/[[CSS3]]

## 18. [[AJAX]]
```text
AJAX = kỹ thuật/gọi chung cách request bất đồng bộ không reload page.
fetch = API native của browser để làm AJAX. (fetch là Web API có sẵn trong browser để gửi HTTP request.)
axios = thư viện bên ngoài để làm HTTP/AJAX dễ hơn. (axios là thư viện HTTP client.)
```
Tức là **fetch và axios đều là cách triển khai AJAX**, còn AJAX không phải một thư viện cụ thể.

Đặc điểm của fetch():
```text
Có sẵn trong browser hiện đại
Promise-based
Không cần cài thư viện
API tương đối low-level
Cần tự check response.ok
Cần tự parse JSON bằng response.json()
Cancel request bằng AbortController
```

Đặc điểm của axios:
```text
Không phải API native, là thư viện ngoài
Promise-based
Tự parse JSON response
Tự reject khi HTTP status là 4xx/5xx
Có interceptor rất tiện
Dễ set baseURL, headers, timeout
Có thể dùng cả browser và Node.js
```

### Khác nhau quan trọng nhất: HTTP lỗi 404/500
#### **fetch**
`fetch` **không throw error** khi server trả `404`, `500`.
```js
const response = await fetch("/api/users");

console.log(response.status); // 404
console.log(response.ok); // false
```

Vẫn phải tự check:
```js
if (!response.ok) {
  throw new Error(`HTTP error: ${response.status}`);
}
```

`fetch` chỉ reject khi lỗi network kiểu:
```text
Mất mạng
DNS lỗi
Request bị block nghiêm trọng
Abort request
```

#### **axios**

`axios` mặc định **reject promise** nếu status nằm ngoài range `2xx`.
```js
try {
  const response = await axios.get("/api/users");
  console.log(response.data);
} catch (error) {
  console.log("Request failed");
}
```
Nếu API trả `404`, nó sẽ nhảy vào `catch`.
Đây là khác biệt rất hay bị hỏi.

### **Khác nhau về timeout**
`fetch` không có option `timeout` trực tiếp.
Muốn timeout phải dùng `AbortController`.

```js
async function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();

  const timer = setTimeout(() => {
    controller.abort();
  }, timeout);

  try {
    const response = await fetch(url, {
      signal: controller.signal,
    });

    return response;
  } finally {
    clearTimeout(timer);
  }
}
```

Axios có option `timeout` sẵn:
```js
axios.get("/api/users", {
  timeout: 5000,
});
```

### Khi nào dùng fetch, khi nào dùng axios?
#### Dùng fetch khi:
```
Muốn dùng native API, không thêm dependency
Project nhỏ/vừa
Đã có wrapper riêng
Đang dùng Next.js/React Query/SWR và không cần interceptor phức tạp
Muốn giảm bundle size
```

#### Dùng axios khi:
```
Cần interceptor request/response tiện
Cần baseURL/timeout/config chung
App có auth token/refresh token phức tạp
Muốn error handling 4xx/5xx mặc định vào catch
Team đã dùng axios convention
Cần chạy cùng code ở browser/Node trong một số context
```

## 19. xHTML 
xHTML hiểu đơn giản là:
**HTML nhưng được viết theo quy tắc chặt chẽ của XML.**

## 20. [[JavaScript]]

## 21. [[ES6+]] là gì?
ES6 là phiên bản JavaScript hiện đại hơn, bổ sung nhiều cú pháp/tính năng mới. ES6+ nghĩa là ES6 và các phiên bản sau đó.

## 22. [[Map]]/[[Set]]
### **Set**
Lưu giá trị unique.
```js
const ids = [1, 2, 2, 3];

const uniqueIds = [...new Set(ids)];
// [1, 2, 3]
```
Dùng khi:
```
Remove duplicate
Check exists nhanh bằng has()
```
### **Map**
Lưu key-value, key có thể là nhiều kiểu.
```js
const userMap = new Map();

userMap.set(1, "Tuan");
userMap.get(1); // "Tuan"
```
Dùng tốt cho lookup/cache.

## 23. Optional chaining / Nullish coalescing
### **Optional chaining**
Tránh lỗi khi property bị null/undefined.
```js
const city = user.address?.city;
```
Nếu address không có, không crash.

### **Nullish coalescing**
Default khi value là `null` hoặc `undefined`.
```js
const name = user.name ?? "Unknown";
```

Khác `||` ở chỗ `??` không thay thế `0`, `false`, `""`.
```js
const value = 0 || 10; // 10
const value2 = 0 ?? 10; // 0
```


## 24. [[React Context]]
Context giúp truyền dữ liệu xuống nhiều component con mà không cần truyền props qua từng tầng.

## 25. Controlled vs uncontrolled component?
### **Controlled component**
Form value được quản lý bởi React state.

```js
const [email, setEmail] = useState("");

<input
  value={email}
  onChange={(e) => setEmail(e.target.value)}
/>
```

Ưu điểm:
```
Dễ validate
Dễ control value
Dễ submit/process data
```

Nhược điểm:
```
Form lớn có thể re-render nhiều nếu quản lý không tốt
```

### Uncontrolled component
DOM tự giữ value, React lấy qua `ref`.
```js
const inputRef = useRef<HTMLInputElement>(null);

<input ref={inputRef} />
```

Dùng khi:
```
Form đơn giản
File input
Tích hợp thư viện ngoài
Muốn giảm re-render
```


## 25. useRef dùng khi nào?
`useRef` dùng để giữ một giá trị qua các lần render nhưng **thay đổi ref không làm component re-render**.
Dùng cho 2 nhóm chính:
- Truy cập DOM:
```js
const inputRef = useRef<HTMLInputElement>(null);

function focusInput() {
  inputRef.current?.focus();
}

<input ref={inputRef} />
```

- Lưu mutable value không cần render
```js
const latestValueRef = useRef(value);

useEffect(() => {
  latestValueRef.current = value;
}, [value]);
```

## 26. useMemo
Memoize kết quả tính toán.
```js
const filteredUsers = useMemo(() => {
  return users.filter((user) => user.name.includes(keyword));
}, [users, keyword]);
```


## 27. useCallback
Memoize **function reference**.
```js
const handleClick = useCallback(() => {
  onSelect(id);
}, [onSelect, id]);
```


## 28. SSR/SSG/ISR/CSR khác nhau?
```
CSR - Client-side Rendering: render ở browser, phù hợp dashboard sau login, SEO không quan trọng.
SSR - Server-side Rendering:  render trên server mỗi request, phù hợp page cần SEO và data fresh.
SSG - Static Site Generation: render sẵn lúc build, phù hợp blog/docs/landing ít đổi.
ISR là static generation nhưng có revalidate định kỳ, cân bằng performance và freshness.
```


## 29. Custom hook là gì?
Custom hook là function bắt đầu bằng `use`, dùng để tái sử dụng logic React.

```js
function useDebounce(value: string, delay: number) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => clearTimeout(timer);
  }, [value, delay]);

  return debouncedValue;
}
```

```
Custom hook giúp tách và tái sử dụng stateful logic giữa nhiều component, ví dụ useFetch, useDebounce, useLocalStorage, useAuth.
```


## 30. React.memo
`React.memo` memoize component. Nếu props không đổi theo shallow comparison, React có thể skip render component đó.

## 31. Middleware trong Next.js là gì?
Middleware là đoạn code chạy **trước khi request đi tới page/route handler**.
```
User request /dashboard
↓
Middleware chạy trước
↓
Middleware quyết định:
- cho đi tiếp
- redirect
- rewrite
- thêm/sửa headers
↓
Page/Route Handler mới chạy
```

```
Middleware trong Next.js là logic chạy trước khi request được xử lý bởi page hoặc route. Nó thường dùng cho auth guard, redirect, rewrite, i18n, A/B testing, hoặc xử lý header/cookie.
```

## 32. Github action














```
1. FE nền tảng:
HTML5, CSS3, xHTML, browser compatibility, UI/UX basic

2. JS ecosystem:
JavaScript, TypeScript, ES6+, Ajax, jQuery, jQuery UI, Bootstrap

3. Modern framework:
ReactJS, Redux, NextJS, hoặc Angular/Vue

4. Web service + backend/database awareness:
Web service, Ajax/API, MySQL, Oracle

5. Tối ưu frontend:
Performance, browser compatibility, loading speed, render optimization
```

```text
HTML5/CSS3
JavaScript ES6+
TypeScript basic
Ajax/fetch/XMLHttpRequest concept
ReactJS
Redux basic
NextJS basic
Web service/API
Browser compatibility
Frontend performance
```

```text
jQuery
Bootstrap
jQuery UI
xHTML
UI/UX basic
MySQL/Oracle basic
```

```text
Angular/Vue
Database query sâu
IE support rất cũ
jQuery UI component customization sâu
```


