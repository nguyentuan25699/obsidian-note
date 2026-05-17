## Vấn đề Context giải quyết: props drilling
Context giúp truyền dữ liệu xuống nhiều component con mà không cần truyền props qua từng tầng.

## Context dùng như thế nào?
Có 3 bước:
```
1. createContext
2. Provider bọc bên ngoài
3. useContext để đọc data
```

VD:
```js
import { createContext, useContext } from "react";

type User = {
  name: string;
  role: string;
};

const UserContext = createContext<User | null>(null);

function App() {
  const user = { name: "Tuan", role: "FE" };

  return (
    <UserContext.Provider value={user}>
      <Layout />
    </UserContext.Provider>
  );
}

function Layout() {
  return <Sidebar />;
}

function Sidebar() {
  return <UserInfo />;
}

function UserInfo() {
  const user = useContext(UserContext);

  return <p>{user?.name}</p>;
}
```

Lúc này `UserInfo` lấy được `user` mà không cần truyền props qua `Layout`, `Sidebar`.


## Context phù hợp cho data gì?
Context hợp với data kiểu:

```
Theme: light/dark
Language/i18n
Current user/auth info
Permission/config
Design system settings
Global modal/toast ở mức đơn giản
```


## Context có phải thay Redux không?
Không hẳn.
```
Context giải quyết việc truyền data qua nhiều tầng component.
Redux/Zustand giải quyết quản lý state phức tạp hơn, có nhiều action, nhiều module, cần debug/devtools/convention rõ.
```
Context tốt cho:
- State đơn giản, ít thay đổi, phạm vi rõ.

Redux/Zustand tốt hơn cho:
- State phức tạp
- Nhiều nơi update
- Nhiều action/business logic
- Cần DevTools/debug
- App lớn/team đông

## Nhược điểm lớn của Context: re-render
Khi `value` của Provider thay đổi, các component dùng context đó có thể re-render.

VD:
```js
const AppContext = createContext({
  user: null,
  theme: "light",
  count: 0,
});
```

Nếu `count` thay đổi liên tục, component chỉ dùng `theme` cũng có thể bị ảnh hưởng nếu cùng một context value.