- You may have heard of the shared responsibility model, but you may not understand what it means or how it impacts cloud computing.
	Có thể bạn đã nghe nói về mô hình trách nhiệm chung, nhưng có thể bạn chưa hiểu ý nghĩa của nó hoặc tác động của nó đến điện toán đám mây.

- Start with a traditional corporate datacenter. The company is responsible for maintaining the physical space, ensuring security, and maintaining or replacing the servers if anything happens. The IT department is responsible for maintaining all the infrastructure and software needed to keep the datacenter up and running. They’re also likely to be responsible for keeping all systems patched and on the correct version.
	Hãy bắt đầu với một trung tâm dữ liệu doanh nghiệp truyền thống. Công ty chịu trách nhiệm duy trì không gian vật lý, đảm bảo an ninh và bảo trì hoặc thay thế máy chủ nếu có sự cố xảy ra. Bộ phận CNTT chịu trách nhiệm duy trì toàn bộ cơ sở hạ tầng và phần mềm cần thiết để giữ cho trung tâm dữ liệu hoạt động. Họ cũng có thể chịu trách nhiệm cập nhật các hệ thống và đảm bảo chúng ở phiên bản chính xác.

- With the shared responsibility model, these responsibilities get shared between the cloud provider and the consumer. Physical security, power, cooling, and network connectivity are the responsibility of the cloud provider. The consumer isn’t collocated with the datacenter, so it wouldn’t make sense for the consumer to have any of those responsibilities.
	Với mô hình trách nhiệm chung, những trách nhiệm này được chia sẻ giữa nhà cung cấp dịch vụ đám mây và người tiêu dùng. An ninh vật lý, điện năng, làm mát và kết nối mạng là trách nhiệm của nhà cung cấp dịch vụ đám mây. Người tiêu dùng không đặt máy chủ cùng vị trí với trung tâm dữ liệu, vì vậy sẽ không hợp lý nếu người tiêu dùng phải chịu bất kỳ trách nhiệm nào trong số đó.

- At the same time, the consumer is responsible for the data and information stored in the cloud. (You wouldn’t want the cloud provider to be able to read your information.) The consumer is also responsible for access security, meaning you only give access to those who need it.
	Đồng thời, người tiêu dùng chịu trách nhiệm về dữ liệu và thông tin được lưu trữ trên đám mây. (Bạn sẽ không muốn nhà cung cấp dịch vụ đám mây có thể đọc thông tin của bạn.) Người tiêu dùng cũng chịu trách nhiệm về bảo mật truy cập, nghĩa là bạn chỉ cấp quyền truy cập cho những người cần thiết.

- Then, for some things, the responsibility depends on the situation. If you’re using a cloud SQL database, the cloud provider would be responsible for maintaining the actual database. However, you’re still responsible for the data that gets ingested into the database. If you deployed a virtual machine and installed an SQL database on it, you’d be responsible for database patches and updates, as well as maintaining the data and information stored in the database.
	Đối với một số vấn đề, trách nhiệm phụ thuộc vào tình huống. Nếu bạn sử dụng cơ sở dữ liệu SQL trên đám mây, nhà cung cấp dịch vụ đám mây sẽ chịu trách nhiệm bảo trì cơ sở dữ liệu thực tế. Tuy nhiên, bạn vẫn chịu trách nhiệm về dữ liệu được đưa vào cơ sở dữ liệu. Nếu bạn triển khai một máy ảo và cài đặt cơ sở dữ liệu SQL trên đó, bạn sẽ chịu trách nhiệm về các bản vá và cập nhật cơ sở dữ liệu, cũng như bảo trì dữ liệu và thông tin được lưu trữ trong cơ sở dữ liệu.

- With an on-premises datacenter, you’re responsible for everything. With cloud computing, those responsibilities shift. The shared responsibility model is heavily tied into the cloud service types (covered later in this learning path): [[Infrastructure as a service (IaaS)]], [[Platform as a service (PaaS)]], and [[Software as a service (SaaS)]]. IaaS places the most responsibility on the consumer, with the cloud provider being responsible for the basics of physical security, power, and connectivity. On the other end of the spectrum, SaaS places most of the responsibility with the cloud provider. PaaS, being a middle ground between IaaS and SaaS, rests somewhere in the middle and evenly distributes responsibility between the cloud provider and the consumer.
	Với trung tâm dữ liệu tại chỗ, bạn chịu trách nhiệm cho mọi thứ. Với điện toán đám mây, những trách nhiệm đó sẽ thay đổi. Mô hình trách nhiệm chung gắn liền chặt chẽ với các loại dịch vụ đám mây (sẽ được đề cập sau trong lộ trình học này): cơ sở hạ tầng như một dịch vụ (IaaS), nền tảng như một dịch vụ (PaaS) và phần mềm như một dịch vụ (SaaS). IaaS đặt phần lớn trách nhiệm lên người dùng, trong khi nhà cung cấp dịch vụ đám mây chịu trách nhiệm về các vấn đề cơ bản như bảo mật vật lý, nguồn điện và kết nối. Ngược lại, SaaS đặt phần lớn trách nhiệm lên nhà cung cấp dịch vụ đám mây. PaaS, nằm giữa IaaS và SaaS, đảm nhiệm vị trí trung gian và phân bổ trách nhiệm đồng đều giữa nhà cung cấp dịch vụ đám mây và người tiêu dùng. ^74d89d

The following diagram highlights how the Shared Responsibility Model informs who is responsible for what, depending on the cloud service type.
	Sơ đồ sau đây minh họa cách Mô hình Trách nhiệm Chung xác định ai chịu trách nhiệm về điều gì, tùy thuộc vào loại dịch vụ đám mây.

![Diagram showing the responsibilities of the shared responsibility model.](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-compute/media/shared-responsibility-b3829bfe.svg)


When using a cloud provider, you’ll always be responsible for:
- The information and data stored in the cloud
- Devices that are allowed to connect to your cloud (cell phones, computers, and so on)
- The accounts and identities of the people, services, and devices within your organization
The cloud provider is always responsible for:
- The physical datacenter
- The physical network
- The physical hosts
Your service model will determine responsibility for things like:
- Operating systems
- Network controls
- Applications
- Identity and infrastructure

	Khi sử dụng nhà cung cấp dịch vụ đám mây, bạn sẽ luôn chịu trách nhiệm về:
	- Thông tin và dữ liệu được lưu trữ trên đám mây
	- Các thiết bị được phép kết nối với đám mây của bạn (điện thoại di động, máy tính, v.v.)
	- Các tài khoản và danh tính của người dùng, dịch vụ và thiết bị trong tổ chức của bạn
	Nhà cung cấp dịch vụ đám mây luôn chịu trách nhiệm về:
	- Trung tâm dữ liệu vật lý
	- Mạng vật lý
	- Các máy chủ vật lý
	Mô hình dịch vụ của bạn sẽ xác định trách nhiệm đối với các vấn đề như:
	- Hệ điều hành
	- Kiểm soát mạng
	- Ứng dụng
	- Danh tính và cơ sở hạ tầng