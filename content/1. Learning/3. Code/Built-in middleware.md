Kể từ phiên bản 4.x, Express đã không còn phụ thuộc vào thư viện [Connect](https://github.com/senchalabs/connect). Tất cả các hàm middleware trước đây đều đã được tách ra thành các modules riêng biệt. Điều này cung cấp cách tối ưu hóa và tùy chỉnh ứng dụng Express một cách linh hoạt nhất, giúp tạo ra một ứng dụng Web Application phù hợp với nhu cầu, không bị thừa những thứ không cần thiết. Có thể tham khảo các modules middlware đã được tách ra ở [đây](https://github.com/senchalabs/connect#middleware).

Express có các hàm built-in middleware sau:
- [express.static](https://expressjs.com/en/4x/api.html#express.static) các file tĩnh như hình ảnh, HTML, ....
- [express.json](https://expressjs.com/en/4x/api.html#express.json) phân tích cú pháp request đến với JSON payload. _Lưu ý_: Chỉ khả dụng từ Express 4.16.0+
- [express.urlencoded](https://expressjs.com/en/api.html#express.urlencoded) phân tích cú pháp request đến với URL-encoded payloads. _Lưu ý_: Chỉ khả dụng từ Express 4.16.0+
