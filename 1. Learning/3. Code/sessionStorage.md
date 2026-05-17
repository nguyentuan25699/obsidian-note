sessionStorage khá giống với localStorage. Vì chúng đều thuộc về web storage API.

- Lưu data theo cặp key/value ở local browser và phía server không access được các data này.
- Có cùng APIs: setItem, getItem, removeItem, clear.
- Cho phép lưu trữ nhiều data(khoảng 10MB).

Một khuyết điểm của cả localStorage và sessionStorage là có thể bị đọc bởi Javascript. Do đó dễ bị đánh cắp thông tin thông qua một cross-site scripting. Vì vậy, chúng ta không nên lưu trữ những thông tin nhạy cảm như token ID, password, username, email của người dùng vào localStorage hay sessionStorage.

Ví dụ về các hàm:

```none
// Save data to sessionStorage
sessionStorage.setItem('key', 'value');

// Get saved data from sessionStorage
var data = sessionStorage.getItem('key');

// Remove saved data from sessionStorage
sessionStorage.removeItem('key');

// Remove all saved data from sessionStorage
sessionStorage.clear();
```

Khi close tab hay close browser thì data ở localStorage vẫn tồn tại, và chỉ bị mất khi user xoá cache hoặc clear web data. Còn đối với sessionStorage thì data sẽ bị mất ngay khi close tab hoặc close browser.