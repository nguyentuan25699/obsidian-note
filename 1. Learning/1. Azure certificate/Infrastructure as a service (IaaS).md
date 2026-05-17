Infrastructure as a service (IaaS) is the most flexible category of cloud services, as it provides you the maximum amount of control for your cloud resources. In an IaaS model, the cloud provider is responsible for maintaining the hardware, network connectivity (to the internet), and physical security. You’re responsible for everything else: operating system installation, configuration, and maintenance; network configuration; database and storage configuration; and so on. With IaaS, you’re essentially renting the hardware in a cloud datacenter, but what you do with that hardware is up to you.
	Cơ sở hạ tầng như một dịch vụ (IaaS) là loại dịch vụ đám mây linh hoạt nhất, vì nó cung cấp cho bạn quyền kiểm soát tối đa đối với các tài nguyên đám mây của mình. Trong mô hình IaaS, nhà cung cấp dịch vụ đám mây chịu trách nhiệm bảo trì phần cứng, kết nối mạng (với internet) và bảo mật vật lý. Bạn chịu trách nhiệm cho mọi thứ khác: cài đặt, cấu hình và bảo trì hệ điều hành; cấu hình mạng; cấu hình cơ sở dữ liệu và lưu trữ; và vân vân. Với IaaS, về cơ bản bạn đang thuê phần cứng trong trung tâm dữ liệu đám mây, nhưng bạn làm gì với phần cứng đó là tùy thuộc vào bạn.
# Shared responsibility model
___
The shared responsibility model applies to all the cloud service types. IaaS places the largest share of responsibility with you. The cloud provider is responsible for maintaining the physical infrastructure and its access to the internet. You’re responsible for installation and configuration, patching and updates, and security.
	Mô hình trách nhiệm chung áp dụng cho tất cả các loại dịch vụ đám mây. IaaS (Cơ sở hạ tầng dưới dạng dịch vụ) đặt phần lớn trách nhiệm lên vai bạn. Nhà cung cấp dịch vụ đám mây chịu trách nhiệm duy trì cơ sở hạ tầng vật lý và quyền truy cập internet. Bạn chịu trách nhiệm cài đặt và cấu hình, vá lỗi và cập nhật, cũng như bảo mật.

![Diagram showing the responsibilities of the shared responsibility model.](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-service-types/media/shared-responsibility-b3829bfe.svg)

# Scenarios
___
Some common scenarios where IaaS might make sense include:
	Một số trường hợp phổ biến mà IaaS có thể phù hợp bao gồm:
- Lift-and-shift migration: You’re setting up cloud resources similar to your on-prem datacenter, and then simply moving the things running on-prem to running on the IaaS infrastructure.
	Di chuyển nguyên trạng: Bạn đang thiết lập các tài nguyên đám mây tương tự như trung tâm dữ liệu tại chỗ của mình, và sau đó chỉ cần di chuyển những thứ đang chạy tại chỗ sang chạy trên cơ sở hạ tầng IaaS.
- Testing and development: You have established configurations for development and test environments that you need to rapidly replicate. You can start up or shut down the different environments rapidly with an IaaS structure, while maintaining complete control.
	Kiểm thử và phát triển: Bạn đã thiết lập cấu hình cho môi trường phát triển và kiểm thử mà bạn cần sao chép nhanh chóng. Bạn có thể khởi động hoặc tắt các môi trường khác nhau một cách nhanh chóng với cấu trúc IaaS, đồng thời duy trì quyền kiểm soát hoàn toàn.