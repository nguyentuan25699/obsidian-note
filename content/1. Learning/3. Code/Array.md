---
date: 2026-05-20
tags:
  - js
  - code
draft: false
---
## **1. Array trong JavaScript thực chất là gì?**
- Ở mức cơ bản, array là danh sách có thứ tự, ex: 
```js
const numbers = [1, 2, 3, 4];
```

- Array là 1 object đặc biệt
- Key là số bắt đầu từ 0.
- Có property length.
- Có prototype chứa các method như map, filter, reduce, forEach, find...
Check array:
```js
Array.isArray(value);
```

## **2. Array là reference type**
```js
const arr1 = [1, 2, 3];
const arr2 = arr1;
arr2.push(4);
console.log(arr1); // [1, 2, 3, 4]
console.log(arr2); // [1, 2, 3, 4]
```
Vì arr1 và arr2 cùng trỏ đến một vùng nhớ.
Trong React, nếu mutate trực tiếp state array:
```js
users.push(newUser);
setUsers(users);
```
Có thể gây bug vì reference không đổi. React khó biết state đã thay đổi.

Cách đúng
```js
setUsers((prevUsers) => [...prevUsers, newUser]);
```
*(spread array)*

