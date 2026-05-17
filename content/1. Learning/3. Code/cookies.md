___
Cookies là các tệp được trang web người dùng truy cập tạo ra. Cookie giúp trải nghiệm trực tuyến của bạn dễ dàng hơn bằng cách lưu thông tin duyệt web. Với Cookies, các trang web có thể duy trì trạng thái đăng nhập của bạn, ghi nhớ tùy chọn trang web và cung cấp nội dung phù hợp với vị trí của người dùng. Và bản chất lưu trữ Cookie cũng là một bản ghi đơn giản gồm key, value.

### Một số điểm nổi bật của cookie đó là:

- localStorage chỉ access được trên browser client; còn cookies thì có thể access được ở browser client và cả phía server (khi tạo một http request thì cookies của browser sẽ được attach vào header Cookie, từ đó phía server có thể parse header này và get được data cookie).
- cookies có thời gian hết hạn expires, sau thời gian này thì cookies sẽ biến mất khỏi browser.
- cookies chỉ cho phép lưu tối đa khoảng 4 KB, vì vậy ta nên sử dụng cookies với mục đích save những loại data simple ví dụ như token cho authentication,...

Ví dụ hàm set-cookie trong Javascript:

```js 
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";
```

Cookie thường được dùng để đăng nhập, lưu vài giá trị cơ bản và đơn giản. Cookie không bị giới hạn bởi độ dài dung lượng hay ký tự. Tuy nhiên vì nó chuyển từ Client tới Server và ngược lại theo Header Request. Nên chúng càng nhẹ càng tốt. Trong các cách tăng tốc website thì giảm bớt Cookie là một ý kiến hay ho…

### Một số lưu ý khi dùng cookie:

- Nên xác định thời gian expire/max-age. Thông thường chỉ nên cho phép một cookie chứa thông tin để authenticate trong khoảng 3-4 tháng. Để tránh người dùng phải đăng nhập nhiều lần, chúng ta cung cấp một option lưu trữ thông tin để lần sau user không cần đăng nhập nữa.
- Nếu cookie dùng để authenticate nên set httpOnly bằng true. Dùng cờ này để không cho phép đọc được cookie từ Javascript. Tránh được sự tấn công từ bên ngoài bằng thủ thuật scripting.
- Dễ bị đánh cắp thông tin người dùng. Cho nên đừng bao giờ lưu password nguyên gốc của user mà hãy mã hoá nó, hay dùng token-based authentication.