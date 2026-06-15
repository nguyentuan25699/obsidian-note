---
date: 2026-06-15
tags:
  - code
  - learning
draft: false
---
## CORS là gì
CORS là viết tắt của `Cross-Origin Resource Sharing`, nó có nghĩa là chia sẻ tài nguyên có nhiều nguồn khác nhau. `same origin policy` là cơ chế bảo mật rất quan trọng, được hiện thực trên trình duyệt để chặn code JS có thể tạo ra những request đến những nguồn khác với nguồn mà nó được trả về. Client từ các nguồn khác nhau không thể truy cập tài nguyên của nhau nếu không được phép.

Ví dụ bạn vừa truy cập một trang web có chứa mã độc A, trang A lấy dữ liệu từ mạng xã hội B, và nếu như bạn đang sử dụng mạng xã hội B này và không có `same-origin policy` thì trang A kia có thể dễ dàng lấy dữ liệu của bạn, `same-origin policy` dùng để ngăn trường hợp như vậy xảy ra.

Những trường hợp sau được coi là cross origin:
- khác domain
- khác protocol
- khác subdomain
- khác port

![[Pasted image 20260615222426.png]]

## Cơ chế hoạt động

Trong thực tế chúng ta vẫn có thể sẽ cần truy vấn tới một trang khác, lúc đó cần đến CORS. Dựa vào HTTP header để khai báo cho trình duyệt biết web A có thể truy cập vào tài nguyên ở web B.

Các trình duyệt đều cài đặt `same-origin policy`, do đó truy vấn ở trên sẽ không nhận được data, trừ khi server trả về response có header CORS phù hợp.

Phía client gửi request lên server, những request khi gửi sẽ kèm theo header tên là `origin` để chỉ định origin của client code. Server sẽ kiếm tra origin có hợp lệ hay không, nếu hợp lệ sẽ trả về response kèm header `Access-Control-Allow-Origin`. Header này cho client biết có phải nguồn hợp lệ để trình duyệt tiếp tục request hay không.

Thường thì `Access-Control-Allow-Origin` có giá trị giống như `origin`, hoặc là regex, hoặc là `*`, khi giá trị của nó là `*` thì được coi là không an toàn, chỉ phù hợp khi API được public.

Các request có thay đổi dữ liệu như `POST`, `PUT`, `PATCH`, `DELETE`, ... thì trình duyệt sẽ tự động thực hiện request gọi là `preflight request` trước khi thực sự thực hiện request để kiểm tra phía server đã thực hiện CORS chưa, và cũng để biết được request có hợp lệ hay không. Hơn nữa nếu chúng ta có custom header vào request thì việc gửi `preflight request` là cần thiết.

![[Pasted image 20260615223000.png]]

![[Pasted image 20260615223008.png]]