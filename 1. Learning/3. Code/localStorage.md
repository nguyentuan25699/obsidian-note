___
## 1. localStorage là gì ?
- Tất cả các trình duyệt hiện đại đều hỗ trợ chức năng này. LocalStorage giúp website lưu trữ dữ liệu vĩnh viễn trên trình duyệt. Trừ khi người dùng xóa cache hoặc làm các hành động như cài lại trình duyệt.

- Về cơ bản, nó như một table trong Excel, nhưng chỉ có hai trường là: key và value. Một số ví dụ dùng localStorage như một số user preferences: ngôn ngữ, theme, danh mục sản phẩm được chọn, giao diện tuỳ chỉnh, dashboard, layout, …

Để có thể tạo ra 1 localStorage ở trên trình duyệt thì ta thực hiện như sau:
```
window.LocalStorage.setItem('name', 'value');
```

Để đọc lại giá trị, bạn gọi hàm:

```
window.LocalStorage.getItem('name');
```

Và để xóa chúng đi:

```
window.LocalStorage.clear(); //xóa tất cả
window.LocalStorage.removeItem('name'); //chỉ xóa phần tử có tên là name
```

- Có rất nhiều giá trị trong một ứng dụng website nên lưu trong LocalStorage thay vì SessionStorage.
- Tuy nhiên, nên lưu ý là LocalStorage không bảo mật. Có thể dễ dàng lưu dữ liệu, lấy dữ liệu và chỉnh sửa dữ liệu từ LocalStorage.
- Ngoài ra, điểm yếu của LocalStorage là nó chỉ lưu đơn thuần một String. Các kiểu dữ liệu phức tạp đều không phù hợp để lưu trong LocalStorage.