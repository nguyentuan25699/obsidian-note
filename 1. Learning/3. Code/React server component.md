## React Server Components là gì?
Thông thường, React render component trên trình duyệt bằng JavaScript. Nhưng với RSC, một số component được render trên server và gửi HTML về client, giúp giảm đáng kể kích thước bundle JavaScript.

### Cách RSC hoạt động
RSC chạy trên server, thực hiện logic và gửi kết quả đã được serialize về client. Khác với Server-Side Rendering (SSR) gửi nguyên trang HTML đã render, RSC cho phép render từng phần và truyền dần xuống client.
Điều này giúp RSC có thể truy vấn dữ liệu trực tiếp từ database hoặc API mà không cần thêm request từ client, giảm độ trễ và tối ưu hiệu suất.

### Lợi ích của RSC

- **Giảm JavaScript tải xuống client**: Không gửi JavaScript thừa về trình duyệt, giúp trang tải nhanh hơn.
- **Cải thiện SEO**: Nội dung render sẵn trên server giúp công cụ tìm kiếm dễ dàng thu thập dữ liệu.
- **Tối ưu hóa việc lấy dữ liệu**: Fetch dữ liệu trực tiếp trên server, không cần gọi API từ client.
- **Tích hợp dễ dàng**: Có thể sử dụng cùng với Client Components khi cần.
- **Tăng tốc độ tải trang**: Gửi HTML đã render sẵn giúp người dùng thấy nội dung ngay lập tức.
- **Giảm tải bộ nhớ trình duyệt**: Trạng thái được xử lý trên server, giúp trình duyệt hoạt động mượt mà hơn.