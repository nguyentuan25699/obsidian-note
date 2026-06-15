Đây là các middleware phục vụ cho việc xử lý lỗi. Một lưu ý là các hàm cho việc này luôn nhận bốn tham số (_err, req, res, next_). Khi muốn khai báo một middlware cho việc xử lý lỗi, cần phải tạo một hàm có 4 tham số đầu vào. Mặc dù ta có thể không cần sử dụng đối tượng next, nhưng hàm vẫn cần format với bốn tham số như vậy. Nếu không Express sẽ không thể xác định đó là hàm xử lý lỗi, và sẽ không chạy khi có lỗi xảy ra, chỉ hoạt động giống như các hàm middlware khác.

Đoạn code dưới đây mô tả một hàm xử lý lỗi truyền về cho client lỗi 500 khi có lỗi xảy ra từ server:
```js
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

