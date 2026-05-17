Platform as a service (PaaS) is a middle ground between renting space in a datacenter (infrastructure as a service) and paying for a complete and deployed solution (software as a service). In a PaaS environment, the cloud provider maintains the physical infrastructure, physical security, and connection to the internet. They also maintain the operating systems, middleware, development tools, and business intelligence services that make up a cloud solution. In a PaaS scenario, you don't have to worry about the licensing or patching for operating systems and databases.
	Nền tảng dưới dạng dịch vụ (PaaS) là giải pháp trung gian giữa việc thuê không gian trong trung tâm dữ liệu (cơ sở hạ tầng dưới dạng dịch vụ) và trả tiền cho một giải pháp hoàn chỉnh đã được triển khai (phần mềm dưới dạng dịch vụ). Trong môi trường PaaS, nhà cung cấp dịch vụ đám mây duy trì cơ sở hạ tầng vật lý, bảo mật vật lý và kết nối internet. Họ cũng duy trì hệ điều hành, phần mềm trung gian, công cụ phát triển và dịch vụ phân tích kinh doanh tạo nên một giải pháp đám mây. Trong kịch bản PaaS, bạn không cần phải lo lắng về việc cấp phép hoặc vá lỗi cho hệ điều hành và cơ sở dữ liệu.

PaaS is well suited to provide a complete development environment without the headache of maintaining all the development infrastructure.
	PaaS rất phù hợp để cung cấp một môi trường phát triển hoàn chỉnh mà không cần phải đau đầu duy trì toàn bộ cơ sở hạ tầng phát triển.

# Shared responsibility model

The shared responsibility model applies to all the cloud service types. PaaS splits the responsibility between you and the cloud provider. The cloud provider is responsible for maintaining the physical infrastructure and its access to the internet, just like in IaaS. In the PaaS model, the cloud provider will also maintain the operating systems, databases, and development tools. Think of PaaS like using a domain joined machine: IT maintains the device with regular updates, patches, and refreshes.
	Mô hình chia sẻ trách nhiệm áp dụng cho tất cả các loại dịch vụ đám mây. PaaS phân chia trách nhiệm giữa bạn và nhà cung cấp dịch vụ đám mây. Nhà cung cấp dịch vụ đám mây chịu trách nhiệm duy trì cơ sở hạ tầng vật lý và quyền truy cập internet, giống như trong IaaS. Trong mô hình PaaS, nhà cung cấp dịch vụ đám mây cũng sẽ duy trì hệ điều hành, cơ sở dữ liệu và các công cụ phát triển. Hãy hình dung PaaS giống như việc sử dụng một máy tính được kết nối vào miền: bộ phận CNTT duy trì thiết bị bằng các bản cập nhật, bản vá lỗi và làm mới thường xuyên.

Depending on the configuration, you or the cloud provider may be responsible for networking settings and connectivity within your cloud environment, network and application security, and the directory infrastructure.
	Tùy thuộc vào cấu hình, bạn hoặc nhà cung cấp dịch vụ đám mây có thể chịu trách nhiệm về cài đặt mạng và kết nối trong môi trường đám mây của bạn, bảo mật mạng và ứng dụng, và cơ sở hạ tầng thư mục.

![Diagram showing the responsibilities of the shared responsibility model.](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-service-types/media/shared-responsibility-b3829bfe.svg)


# Scenarios
Some common scenarios where PaaS might make sense include:
	Một số trường hợp phổ biến mà PaaS có thể mang lại hiệu quả bao gồm:
- Development framework: PaaS provides a framework that developers can build upon to develop or customize cloud-based applications. Similar to the way you create an Excel macro, PaaS lets developers create applications using built-in software components. Cloud features such as scalability, high-availability, and multi-tenant capability are included, reducing the amount of coding that developers must do.
	Khung phát triển: PaaS cung cấp một khung mà các nhà phát triển có thể xây dựng hoặc tùy chỉnh các ứng dụng dựa trên đám mây. Tương tự như cách bạn tạo macro trong Excel, PaaS cho phép các nhà phát triển tạo ứng dụng bằng cách sử dụng các thành phần phần mềm tích hợp sẵn. Các tính năng của đám mây như khả năng mở rộng, tính khả dụng cao và khả năng đa người dùng được bao gồm, giúp giảm lượng mã mà các nhà phát triển phải thực hiện.
- Analytics or business intelligence: Tools provided as a service with PaaS allow organizations to analyze and mine their data, finding insights and patterns and predicting outcomes to improve forecasting, product design decisions, investment returns, and other business decisions.
	Phân tích hoặc trí tuệ kinh doanh: Các công cụ được cung cấp dưới dạng dịch vụ với PaaS cho phép các tổ chức phân tích và khai thác dữ liệu của họ, tìm ra những hiểu biết và mô hình, đồng thời dự đoán kết quả để cải thiện dự báo, quyết định thiết kế sản phẩm, lợi tức đầu tư và các quyết định kinh doanh khác.
