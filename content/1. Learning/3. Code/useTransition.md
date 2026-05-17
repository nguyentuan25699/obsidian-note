useTransition hiểu đơn giản là:
- Một React hook giúp bạn đánh dấu một phần update là không gấp, để React ưu tiên giữ UI mượt trước.

Ví dụ thực tế nhất: user gõ vào ô search.
- Việc hiển thị chữ user vừa gõ vào input: gấp, phải mượt.
- Việc filter/render danh sách 10.000 item: không gấp bằng, có thể chậm hơn một chút.
`useTransition` sinh ra để xử lý kiểu này.

## 1. Vấn đề trước khi có useTransition
Giả sử có input search và list lớn:
```ts
function SearchPage({ items }) {
  const [keyword, setKeyword] = useState("");

  const filteredItems = items.filter((item) =>
    item.name.toLowerCase().includes(keyword.toLowerCase())
  );

  return (
    <>
      <input
        value={keyword}
        onChange={(e) => setKeyword(e.target.value)}
      />

      {filteredItems.map((item) => (
        <div key={item.id}>{item.name}</div>
      ))}
    </>
  );
}
```
Vấn đề:
```text
Mỗi lần gõ 1 ký tự:
1. setKeyword chạy
2. component re-render
3. filter list lớn
4. render list lớn
```
Nếu list nặng, input có thể bị lag. User gõ chữ nhưng UI phản hồi chậm.

## 2. Ý tưởng của useTransition
Ta tách state thành 2 loại:
```text
Urgent state:
- Cần update ngay
- Ví dụ value trong input

Non-urgent state:
- Có thể update chậm hơn
- Ví dụ search query dùng để filter list lớn
```

Ví dụ:
```ts
import { useState, useTransition } from "react";

function SearchPage({ items }) {
  const [inputValue, setInputValue] = useState("");
  const [searchQuery, setSearchQuery] = useState("");

  const [isPending, startTransition] = useTransition();

  function handleChange(e) {
    const value = e.target.value;

    // Urgent update: input phải hiển thị ngay
    setInputValue(value);

    // Non-urgent update: filter list có thể chậm hơn
    startTransition(() => {
      setSearchQuery(value);
    });
  }

  const filteredItems = items.filter((item) =>
    item.name.toLowerCase().includes(searchQuery.toLowerCase())
  );

  return (
    <>
      <input value={inputValue} onChange={handleChange} />

      {isPending && <p>Updating results...</p>}

      {filteredItems.map((item) => (
        <div key={item.id}>{item.name}</div>
      ))}
    </>
  );
}
```

## 3. useTransition trả về gì?
```ts
const [isPending, startTransition] = useTransition();
```
Nó trả về 2 thứ:
```text
isPending:
true khi transition update đang pending.

startTransition:
function dùng để bọc update không gấp.
```
VD: 
```ts
startTransition(() => {
  setSearchQuery(value);
});
```
Nghĩa là: 
```text
React ơi, update searchQuery này không cần ưu tiên cao.
Nếu đang bận giữ input mượt thì cứ ưu tiên input trước.
```


## 4. useTransition không làm code chạy nhanh hơn
Cực kỳ quan trọng.
`useTransition` **không làm phép filter 10.000 item nhanh hơn**.
Nó chỉ giúp React xử lý độ ưu tiên tốt hơn:
```text
Không dùng useTransition:
Input update và list update cùng priority.
List nặng có thể làm input lag.

Có useTransition:
Input update urgent.
List update non-urgent.
React có thể ưu tiên input trước để cảm giác gõ mượt hơn.
```

- useTransition cải thiện độ mượt/responsiveness.
- Không giảm bản chất chi phí tính toán.

## 5. useTransition dùng khi nào?
Dùng khi có update UI nặng nhưng không cần phản hồi ngay lập tức.
VD: 
- Search/filter list lớn
- Switch tab có content nặng
- Change route/view mà render nhiều component
- Update chart/table/dashboard lớn
- Render result sau khi user nhập input

## 6. Khi nào không cần useTransition?
Không cần cho update nhẹ:
```ts
setCount(count + 1);
setIsOpen(true);
setName(value);
```


## 7. useTransition khác debounce thế nào?
### Debounce
Debounce trì hoãn việc chạy function theo thời gian cố định.
- User gõ liên tục.
- Chỉ sau khi user ngừng gõ 500ms mới chạy search.

### useTransition
Không delay theo thời gian cố định.
- React vẫn có thể bắt đầu update ngay,
- nhưng update đó có priority thấp hơn.
- Nếu có update gấp hơn, React ưu tiên cái gấp trước.

## 8. useTransition khác useDeferredValue thế nào?
