___
When building or deploying a cloud application, two of the biggest considerations are uptime (or availability) and the ability to handle demand (or scale).
	Khi xây dựng hoặc triển khai ứng dụng đám mây, hai yếu tố quan trọng nhất cần xem xét là thời gian hoạt động (hay tính khả dụng) và khả năng đáp ứng nhu cầu (hay khả năng mở rộng).

# High availability
---
When you’re deploying an application, a service, or any IT resources, it’s important the resources are available when needed. High availability focuses on ensuring maximum availability, regardless of disruptions or events that may occur.
	Khi triển khai một ứng dụng, dịch vụ hoặc bất kỳ tài nguyên CNTT nào, điều quan trọng là các tài nguyên đó phải sẵn sàng khi cần thiết. Tính sẵn sàng cao tập trung vào việc đảm bảo tính khả dụng tối đa, bất kể sự gián đoạn hoặc sự kiện nào có thể xảy ra.

When you’re architecting your solution, you’ll need to account for service availability guarantees. Azure is a highly available cloud environment with uptime guarantees depending on the service. These guarantees are part of the service-level agreements (SLAs).
	Khi thiết kế kiến ​​trúc giải pháp, bạn cần phải tính đến các đảm bảo về tính khả dụng của dịch vụ. Azure là một môi trường điện toán đám mây có tính sẵn sàng cao với các đảm bảo về thời gian hoạt động tùy thuộc vào dịch vụ. Những đảm bảo này là một phần của thỏa thuận mức dịch vụ (SLA).
# Scalability
___
Another major benefit of cloud computing is the scalability of cloud resources. Scalability refers to the ability to adjust resources to meet demand. If you suddenly experience peak traffic and your systems are overwhelmed, the ability to scale means you can add more resources to better handle the increased demand.
	Một lợi ích lớn khác của điện toán đám mây là khả năng mở rộng tài nguyên đám mây. Khả năng mở rộng đề cập đến khả năng điều chỉnh tài nguyên để đáp ứng nhu cầu. Nếu đột nhiên lưu lượng truy cập tăng cao và hệ thống bị quá tải, khả năng mở rộng có nghĩa là bạn có thể thêm nhiều tài nguyên hơn để xử lý tốt hơn nhu cầu tăng lên.

The other benefit of scalability is that you aren't overpaying for services. Because the cloud is a consumption-based model, you only pay for what you use. If demand drops off, you can reduce your resources and thereby reduce your costs.
	Lợi ích khác của khả năng mở rộng là bạn không phải trả quá nhiều tiền cho các dịch vụ. Vì điện toán đám mây hoạt động theo mô hình dựa trên mức tiêu thụ, bạn chỉ trả tiền cho những gì bạn sử dụng. Nếu nhu cầu giảm, bạn có thể giảm tài nguyên và do đó giảm chi phí.

Scaling generally comes in two varieties: vertical and horizontal. Vertical scaling is focused on increasing or decreasing the capabilities of resources. Horizontal scaling is adding or subtracting the number of resources.
	Việc mở rộng thường có hai loại: mở rộng theo chiều dọc và mở rộng theo chiều ngang. Mở rộng theo chiều dọc tập trung vào việc tăng hoặc giảm khả năng của tài nguyên. Mở rộng theo chiều ngang là thêm hoặc bớt số lượng tài nguyên.
# Vertical scaling
___
With vertical scaling, if you were developing an app and you needed more processing power, you could vertically scale up to add more CPUs or RAM to the virtual machine. Conversely, if you realized you had over-specified the needs, you could vertically scale down by lowering the CPU or RAM specifications.
	Với mở rộng theo chiều dọc, nếu bạn đang phát triển một ứng dụng và cần nhiều sức mạnh xử lý hơn, bạn có thể mở rộng theo chiều dọc bằng cách thêm CPU hoặc RAM vào máy ảo. Ngược lại, nếu bạn nhận ra mình đã yêu cầu quá cao so với nhu cầu, bạn có thể thu hẹp theo chiều dọc bằng cách giảm thông số kỹ thuật của CPU hoặc RAM.
# Horizontal scaling
With horizontal scaling, if you suddenly experienced a steep jump in demand, your deployed resources could be scaled out (either automatically or manually). For example, you could add additional virtual machines or containers, scaling out. In the same manner, if there was a significant drop in demand, deployed resources could be scaled in (either automatically or manually), scaling in.
	Với mở rộng theo chiều ngang, nếu nhu cầu đột ngột tăng cao, các tài nguyên đã triển khai có thể được mở rộng theo chiều ngang (tự động hoặc thủ công). Ví dụ, bạn có thể thêm máy ảo hoặc container bổ sung, mở rộng theo chiều ngang. Tương tự, nếu nhu cầu giảm đáng kể, các tài nguyên đã triển khai có thể được thu hẹp lại (tự động hoặc thủ công), thu hẹp lại.