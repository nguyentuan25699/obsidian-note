---
date: 2026-05-20
tags:
  - code
  - js
draft: false
---
AJAX viết tắt từ Asynchronous JavaScript and XML, là bộ công nghệ giúp tạo ra các web động hay các ứng dụng giàu tính Internet, cho phép tăng tốc độ ứng dụng web bằng cách cắt nhỏ dữ liệu và chỉ hiển thị những gì cần thiết, thay vì tải đi tải lại toàn bộ trang web, làm như vậy trang của bạn sẽ muợt và đẹp hơn. AJAX không phải một công nghệ đơn lẻ mà là sự kết hợp một nhóm công nghệ với nhau. Trong đó:
- HTML (hoặc XHTML) và CSS đóng vai hiển thị thông tin, dữ liệu
- mô hình DOM (Document Object Model) được thực hiện thông qua JavaScript, nhằm hiển thị thông tin động và tương tác với những thông tin được hiển thị
- Đối tượng XMLHttpRequest để trao đổi dữ liệu một cách không đồng bộ với máy chủ web. (Mặc dù, việc trao đổi này có thể được thực hiện với nhiều định dạng như HTML, văn bản thường, JSON và thậm chí EBML, nhưng XML là ngôn ngữ thường được sử dụng).
- XML thường là định dạng cho dữ liệu truyền, mặc dầu bất cứ định dạng nào cũng có thể dùng, bao gồm HTML định dạng trước, văn bản thuần (plain text), JSON và ngay cả EBML.

Đây đều là công nghệ sẵn có nhưng Javacript đã lắp ráp, kết nối chúng lại để tạo nên một công nghệ tuyệt vời và hữu ích.

```text
Ajax là kỹ thuật gửi/nhận dữ liệu bất đồng bộ với server mà không cần reload toàn bộ page. Ngày trước thường dùng XMLHttpRequest hoặc $.ajax của jQuery, hiện nay thường dùng fetch hoặc axios.
```

VD: 
```js
$.ajax({
  url: "/api/users",
  method: "GET",
  success: function (data) {
    console.log(data);
  },
  error: function (xhr) {
    console.error(xhr.status);
  },
});
```
