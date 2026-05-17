	Azure supports two types of queue mechanisms: **Service Bus queues** and **Storage queues**.
	Azure hỗ trợ hai loại cơ chế hàng đợi: hàng đợi Service Bus và hàng đợi Storage.

Service Bus queues are part of a broader Azure messaging infrastructure that supports queuing, publish/subscribe, and more advanced integration patterns. They're designed to integrate applications or application components that might span multiple communication protocols, data contracts, trust domains, or network environments.
	Hàng đợi Service Bus là một phần của cơ sở hạ tầng nhắn tin Azure rộng lớn hơn, hỗ trợ xếp hàng, xuất bản/đăng ký và các mô hình tích hợp nâng cao hơn. Chúng được thiết kế để tích hợp các ứng dụng hoặc các thành phần ứng dụng có thể trải rộng trên nhiều giao thức truyền thông, hợp đồng dữ liệu, miền tin cậy hoặc môi trường mạng.

Storage queues are part of the Azure Storage infrastructure. They allow you to store large numbers of messages. You access messages from anywhere in the world via authenticated calls using HTTP or HTTPS. A queue might contain millions of messages, up to the total capacity limit of a storage account. Queues are commonly used to create a backlog of work to process asynchronously.
	Hàng đợi Storage là một phần của cơ sở hạ tầng Azure Storage. Chúng cho phép bạn lưu trữ một lượng lớn tin nhắn. Bạn truy cập tin nhắn từ bất cứ đâu trên thế giới thông qua các cuộc gọi được xác thực bằng HTTP hoặc HTTPS. Một hàng đợi có thể chứa hàng triệu tin nhắn, tối đa bằng giới hạn dung lượng của tài khoản lưu trữ. Hàng đợi thường được sử dụng để tạo ra một danh sách công việc cần xử lý bất đồng bộ.

After completing this module, you'll be able to:
	Sau khi hoàn thành mô-đun này, bạn sẽ có thể:

- Choose the appropriate queue mechanism for your solution.
	Chọn cơ chế hàng đợi phù hợp cho giải pháp của bạn.
- Explain how the messaging entities that form the core capabilities of Service Bus operate.
	Giải thích cách thức hoạt động của các thực thể nhắn tin tạo nên các khả năng cốt lõi của Service Bus.
- Send and receive message from a Service Bus queue by using .NET.
	Gửi và nhận tin nhắn từ hàng đợi Service Bus bằng cách sử dụng .NET.
- Identify the key components of Azure Queue Storage
	Xác định các thành phần chính của Azure Queue Storage.
- Create queues and manage messages in Azure Queue Storage by using .NET.
	Tạo hàng đợi và quản lý tin nhắn trong Azure Queue Storage bằng cách sử dụng .NET.

# Choose a message queue solution
___

Storage queues and Service Bus queues have a slightly different feature set. You can choose either one or both, depending on the needs of your particular solution.
	Hàng đợi lưu trữ và hàng đợi Service Bus có bộ tính năng hơi khác nhau. Bạn có thể chọn một trong hai hoặc cả hai, tùy thuộc vào nhu cầu của giải pháp cụ thể của mình.

When determining which queuing technology fits the purpose of a given solution, solution architects and developers should consider these recommendations.
	Khi xác định công nghệ xếp hàng nào phù hợp với mục đích của một giải pháp nhất định, các kiến ​​trúc sư giải pháp và nhà phát triển nên xem xét các khuyến nghị này.

## Consider using Service Bus queues

As a solution architect/developer, **you should consider using Service Bus queues** when:
	Với tư cách là kiến ​​trúc sư/nhà phát triển giải pháp, **bạn nên cân nhắc sử dụng hàng đợi Service Bus** khi:

- Your solution needs to receive messages without having to poll the queue. With Service Bus, you can achieve it by using a long-polling receive operation using the TCP-based protocols that Service Bus supports.
	Giải pháp của bạn cần nhận tin nhắn mà không cần phải thăm dò hàng đợi. Với Service Bus, bạn có thể đạt được điều này bằng cách sử dụng thao tác nhận thăm dò dài hạn bằng các giao thức dựa trên TCP mà Service Bus hỗ trợ.
- Your solution requires the queue to provide a guaranteed first-in-first-out (FIFO) ordered delivery.
	Giải pháp của bạn yêu cầu hàng đợi cung cấp khả năng phân phối theo thứ tự vào trước ra trước (FIFO) được đảm bảo.
- Your solution needs to support automatic duplicate detection.
	Giải pháp của bạn cần hỗ trợ phát hiện trùng lặp tự động.
- You want your application to process messages as parallel long-running streams (messages are associated with a stream using the **session ID** property on the message). In this model, each node in the consuming application competes for streams, as opposed to messages. When a stream is given to a consuming node, the node can examine the state of the application stream state using transactions.
	Bạn muốn ứng dụng của mình xử lý tin nhắn dưới dạng các luồng song song chạy dài (tin nhắn được liên kết với một luồng bằng cách sử dụng thuộc tính **ID phiên** trên tin nhắn). Trong mô hình này, mỗi nút trong ứng dụng tiêu thụ cạnh tranh để có được các luồng, thay vì tin nhắn. Khi một luồng được cung cấp cho một nút tiêu thụ, nút đó có thể kiểm tra trạng thái của luồng ứng dụng bằng cách sử dụng các giao dịch.
- Your solution requires transactional behavior and atomicity when sending or receiving multiple messages from a queue.
	Giải pháp của bạn yêu cầu hành vi giao dịch và tính nguyên tử khi gửi hoặc nhận nhiều tin nhắn từ một hàng đợi.
- Your application handles messages that can exceed 64 KB but won't likely approach the 256 KB or 1-MB limit, depending on the chosen service tier (although Service Bus queues can handle messages up to 100 MB).
	Ứng dụng của bạn xử lý các tin nhắn có thể vượt quá 64 KB nhưng không có khả năng đạt đến giới hạn 256 KB hoặc 1 MB, tùy thuộc vào cấp dịch vụ đã chọn (mặc dù hàng đợi Service Bus có thể xử lý tin nhắn lên đến 100 MB).
- You deal with a requirement to provide a role-based access model to the queues, and different rights/permissions for senders and receivers.
	Bạn phải đối mặt với yêu cầu cung cấp mô hình truy cập dựa trên vai trò cho các hàng đợi, và các quyền/quyền hạn khác nhau cho người gửi và người nhận.

## Consider using Storage queues

As a solution architect/developer, **you should consider using Storage queues** when:
	Với tư cách là kiến ​​trúc sư/nhà phát triển giải pháp, **bạn nên cân nhắc sử dụng hàng đợi lưu trữ** khi:

- Your application must store over 80 gigabytes of messages in a queue.
	Ứng dụng của bạn cần lưu trữ hơn 80 gigabyte tin nhắn trong hàng đợi.
- Your application wants to track progress for processing a message in the queue. It's useful if the worker processing a message crashes. Another worker can then use that information to continue from where the prior worker left off.
	Ứng dụng của bạn muốn theo dõi tiến độ xử lý một tin nhắn trong hàng đợi. Điều này hữu ích nếu tiến trình xử lý tin nhắn bị lỗi. Một tiến trình khác có thể sử dụng thông tin đó để tiếp tục từ nơi tiến trình trước đó đã dừng lại.
- You require server side logs of all of the transactions executed against your queues.
	Bạn cần nhật ký phía máy chủ về tất cả các giao dịch được thực hiện đối với hàng đợi của bạn.
# Explore Azure Service Bus
___

Azure Service Bus is a fully managed enterprise message broker with message queues and publish-subscribe topics. Service Bus is used to decouple applications and services. Data is transferred between different applications and services using **messages**. A message is a container decorated with metadata, and contains data. The data can be any kind of information, including structured data encoded with the common formats such as the following ones: JSON, XML, Apache Avro, and Plain Text.
	Azure Service Bus là một hệ thống môi giới tin nhắn doanh nghiệp được quản lý hoàn toàn với hàng đợi tin nhắn và chủ đề xuất bản-đăng ký. Service Bus được sử dụng để tách rời các ứng dụng và dịch vụ. Dữ liệu được truyền giữa các ứng dụng và dịch vụ khác nhau bằng cách sử dụng **tin nhắn**. Một tin nhắn là một vùng chứa được trang trí bằng siêu dữ liệu và chứa dữ liệu. Dữ liệu có thể là bất kỳ loại thông tin nào, bao gồm dữ liệu có cấu trúc được mã hóa bằng các định dạng phổ biến như: JSON, XML, Apache Avro và Văn bản thuần túy.

Some common messaging scenarios are:
	Một số kịch bản nhắn tin phổ biến là:

- _Messaging_. Transfer business data, such as sales or purchase orders, journals, or inventory movements.
	_Nhắn tin_. Truyền dữ liệu kinh doanh, chẳng hạn như đơn đặt hàng bán hàng hoặc mua hàng, nhật ký hoặc di chuyển hàng tồn kho.
- _Decouple applications_. Improve reliability and scalability of applications and services. Client and service don't have to be online at the same time.
	_Tách rời các ứng dụng_. Cải thiện độ tin cậy và khả năng mở rộng của các ứng dụng và dịch vụ. Máy khách và dịch vụ không cần phải trực tuyến cùng một lúc.
- _Topics and subscriptions_. Enable 1:_n_ relationships between publishers and subscribers.
	_Chủ đề và đăng ký_. Cho phép mối quan hệ 1:n giữa người xuất bản và người đăng ký.
- _Message sessions_. Implement workflows that require message ordering or message deferral.
	_Phiên tin nhắn_. Triển khai các quy trình công việc yêu cầu sắp xếp tin nhắn hoặc trì hoãn tin nhắn.

## Service Bus tiers

Service Bus offers three pricing tiers: **Basic**, **Standard**, and **Premium**. Each tier is designed to serve different use cases and requirements.
	Service Bus cung cấp ba cấp giá: Cơ bản, Tiêu chuẩn và Cao cấp. Mỗi cấp được thiết kế để phục vụ các trường hợp sử dụng và yêu cầu khác nhau.

- **Basic tier** - Suited for simple messaging scenarios with low throughput and minimal feature requirements. The basic tier supports only queues (not topics and subscriptions).
    Cấp Cơ bản - Phù hợp với các kịch bản nhắn tin đơn giản với thông lượng thấp và yêu cầu tính năng tối thiểu. Cấp cơ bản chỉ hỗ trợ hàng đợi (không hỗ trợ chủ đề và đăng ký).
- **Standard tier** - Recommended for developer/test environments or low throughput scenarios where applications aren't sensitive to throttling. Supports both queues and topics with subscriptions.
    Cấp Tiêu chuẩn - Được khuyến nghị cho môi trường phát triển/kiểm thử hoặc các kịch bản thông lượng thấp, nơi các ứng dụng không nhạy cảm với việc điều tiết. Hỗ trợ cả hàng đợi và chủ đề với đăng ký.
- **Premium tier** - Recommended for production scenarios requiring predictable latency and high throughput. Offers resource isolation at the CPU and memory level and advanced features for mission-critical applications.
    Cấp Cao cấp - Được khuyến nghị cho các kịch bản sản xuất yêu cầu độ trễ có thể dự đoán được và thông lượng cao. Cung cấp khả năng cách ly tài nguyên ở cấp độ CPU và bộ nhớ cùng các tính năng nâng cao cho các ứng dụng quan trọng.

For more information on the available tiers, visit [Service Bus pricing](https://azure.microsoft.com/pricing/details/service-bus/).
	Để biết thêm thông tin về các cấp giá hiện có, hãy truy cập trang giá Service Bus.

### Tier comparison

|Feature|Basic|Standard|Premium|
|---|---|---|---|
|Throughput|Low|Variable|High|
|Performance|N/A|Variable latency|Predictable performance|
|Pricing|Pay as you go|Pay as you go variable pricing|Fixed pricing per messaging unit|
|Scaling|N/A|N/A|Ability to scale workload up and down|
|Message size|256 KB|256 KB|Up to 100 MB|
|Topics & Subscriptions|Not supported|Supported|Supported|
|Transactions|Not supported|Supported|Supported|
|Auto-forwarding|Not supported|Supported|Supported|
|Message sessions|Not supported|Supported|Supported|

## Advanced features

Service Bus includes advanced features that enable you to solve more complex messaging problems. The following table describes several of these features.
	Service Bus bao gồm các tính năng nâng cao cho phép bạn giải quyết các vấn đề nhắn tin phức tạp hơn. Bảng sau mô tả một số tính năng này.

| Feature               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Message sessions      | To create a first-in, first-out (FIFO) guarantee in Service Bus, use sessions. Message sessions enable exclusive, ordered handling of unbounded sequences of related messages.<br><br>Để đảm bảo nguyên tắc vào trước ra trước (FIFO) trong Service Bus, hãy sử dụng các phiên (session). Các phiên tin nhắn cho phép xử lý độc quyền, có thứ tự các chuỗi tin nhắn liên quan không giới hạn.                                                                                                                                             |
| Autoforwarding        | The autoforwarding feature chains a queue or subscription to another queue or topic that is in the same namespace.<br><br>Tính năng tự động chuyển tiếp cho phép liên kết một hàng đợi hoặc đăng ký với một hàng đợi hoặc chủ đề khác nằm trong cùng không gian tên.                                                                                                                                                                                                                                                                      |
| Dead-letter queue     | Service Bus supports a dead-letter queue (DLQ). A DLQ holds messages that can't be delivered to any receiver. Service Bus lets you remove messages from the DLQ and inspect them.<br><br>Service Bus hỗ trợ hàng đợi thư chết (DLQ). DLQ chứa các tin nhắn không thể được gửi đến bất kỳ người nhận nào. Service Bus cho phép bạn xóa tin nhắn khỏi DLQ và kiểm tra chúng.                                                                                                                                                                |
| Scheduled delivery    | You can submit messages to a queue or topic for delayed processing. You can schedule a job to become available for processing by a system at a certain time.<br><br>Bạn có thể gửi tin nhắn vào hàng đợi hoặc chủ đề để xử lý sau một khoảng thời gian nhất định. Bạn có thể lên lịch cho một tác vụ để hệ thống xử lý vào một thời điểm cụ thể.                                                                                                                                                                                          |
| Message deferral      | A queue or subscription client can defer retrieval of a message until a later time. The message remains in the queue or subscription, but is set aside.<br><br>Một hàng đợi hoặc máy khách đăng ký có thể trì hoãn việc truy xuất tin nhắn cho đến thời điểm sau đó. Tin nhắn vẫn nằm trong hàng đợi hoặc đăng ký, nhưng được để riêng ra.                                                                                                                                                                                                |
| Transactions          | A transaction groups two or more operations together into an _execution scope_. Service Bus supports grouping operations against a single messaging entity within the scope of a single transaction. A message entity can be a queue, topic, or subscription.<br><br>Một giao dịch nhóm hai hoặc nhiều thao tác lại với nhau thành một phạm vi thực thi. Service Bus hỗ trợ nhóm các thao tác đối với một thực thể nhắn tin duy nhất trong phạm vi của một giao dịch duy nhất. Thực thể nhắn tin có thể là hàng đợi, chủ đề hoặc đăng ký. |
| Filtering and actions | Subscribers can define which messages they want to receive from a topic. These messages are specified in the form of one or more named subscription rules.<br><br>Người đăng ký có thể xác định những tin nhắn họ muốn nhận từ một chủ đề. Những tin nhắn này được chỉ định dưới dạng một hoặc nhiều quy tắc đăng ký được đặt tên.                                                                                                                                                                                                        |
| Autodelete on idle    | Autodelete on idle enables you to specify an idle interval after which a queue is automatically deleted. The minimum duration is 5 minutes.<br><br>Chức năng tự động xóa khi không hoạt động cho phép bạn chỉ định khoảng thời gian không hoạt động, sau đó hàng đợi sẽ tự động bị xóa. Thời gian tối thiểu là 5 phút.                                                                                                                                                                                                                    |
| Duplicate detection   | An error could cause the client to have a doubt about the outcome of a send operation. Duplicate detection enables the sender to resend the same message, or for the queue or topic to discard any duplicate copies.<br><br>Lỗi có thể khiến khách hàng nghi ngờ về kết quả của thao tác gửi. Phát hiện trùng lặp cho phép người gửi gửi lại cùng một tin nhắn, hoặc cho phép hàng đợi hoặc chủ đề loại bỏ bất kỳ bản sao trùng lặp nào.                                                                                                  |
| Security protocols    | Service Bus supports security protocols such as Shared Access Signatures (SAS), Role Based Access Control (RBAC), and Managed identities for Azure resources.<br><br>Service Bus hỗ trợ các giao thức bảo mật như Chữ ký truy cập dùng chung (SAS), Kiểm soát truy cập dựa trên vai trò (RBAC) và Danh tính được quản lý cho các tài nguyên Azure.                                                                                                                                                                                        |
| Geo-disaster recovery | When Azure regions or datacenters experience downtime, Geo-disaster recovery enables data processing to continue operating in a different region or datacenter.<br><br>Khi các khu vực hoặc trung tâm dữ liệu Azure gặp sự cố ngừng hoạt động, tính năng phục hồi thảm họa địa lý cho phép quá trình xử lý dữ liệu tiếp tục hoạt động ở một khu vực hoặc trung tâm dữ liệu khác.                                                                                                                                                          |
| Security              | Service Bus supports standard AMQP 1.0 and HTTP/REST protocols.<br><br>Service Bus hỗ trợ các giao thức chuẩn AMQP 1.0 và HTTP/REST.                                                                                                                                                                                                                                                                                                                                                                                                      |

## Compliance with standards and protocols

The primary wire protocol for Service Bus is [Advanced Messaging Queueing Protocol (AMQP) 1.0](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-amqp-overview), an open ISO/IEC standard. It allows customers to write applications that work against Service Bus and on-premises brokers such as ActiveMQ or RabbitMQ. The [AMQP protocol guide](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-amqp-protocol-guide) provides detailed information in case you want to build such an abstraction.
	Giao thức truyền tải chính cho Service Bus là Giao thức xếp hàng tin nhắn nâng cao (AMQP) 1.0, một tiêu chuẩn mở của ISO/IEC. Nó cho phép khách hàng viết các ứng dụng hoạt động với Service Bus và các máy chủ trung gian tại chỗ như ActiveMQ hoặc RabbitMQ. Hướng dẫn giao thức AMQP cung cấp thông tin chi tiết trong trường hợp bạn muốn xây dựng một lớp trừu tượng như vậy.

Service Bus Premium is fully compliant with the Java/Jakarta EE [Java Message Service (JMS) 2.0](https://learn.microsoft.com/en-us/azure/service-bus-messaging/how-to-use-java-message-service-20) API.
	Service Bus Premium hoàn toàn tuân thủ API Java Message Service (JMS) 2.0 của Java/Jakarta EE.

## Client libraries

Fully supported Service Bus client libraries are available via the Azure SDK.

- [Azure Service Bus for .NET](https://learn.microsoft.com/en-us/dotnet/api/overview/azure/service-bus)
- [Azure Service Bus libraries for Java](https://learn.microsoft.com/en-us/java/api/overview/azure/servicebus)
- [Azure Service Bus provider for Java JMS 2.0](https://learn.microsoft.com/en-us/azure/service-bus-messaging/how-to-use-java-message-service-20)
- [Azure Service Bus Modules for JavaScript and TypeScript](https://learn.microsoft.com/en-us/javascript/api/overview/azure/service-bus)
- [Azure Service Bus libraries for Python](https://learn.microsoft.com/en-us/python/api/overview/azure/servicebus)


# Discover Service Bus queues, topics, and subscriptions
___

The messaging entities that form the core of the messaging capabilities in Service Bus are **queues**, **topics and subscriptions**, and rules/actions.
	Các thực thể nhắn tin tạo nên cốt lõi của khả năng nhắn tin trong Service Bus bao gồm **hàng đợi**, **chủ đề và đăng ký**, và các quy tắc/hành động.

## Queues

Queues offer **First In, First Out** (FIFO) message delivery to one or more competing consumers. That is, receivers typically receive and process messages in the order in which they were added to the queue. And, only one message consumer receives and processes each message. Because messages are stored durably in the queue, producers (senders) and consumers (receivers) don't have to process messages concurrently.
	Hàng đợi cung cấp phương thức truyền tin nhắn **Vào trước, ra trước** (FIFO) cho một hoặc nhiều người tiêu dùng cạnh tranh. Nghĩa là, người nhận thường nhận và xử lý tin nhắn theo thứ tự chúng được thêm vào hàng đợi. Và chỉ có một người tiêu dùng nhận và xử lý mỗi tin nhắn. Vì tin nhắn được lưu trữ bền vững trong hàng đợi, nên người gửi (nhà sản xuất) và người nhận (người tiêu dùng) không cần phải xử lý tin nhắn đồng thời.


A related benefit is **load-leveling**, which enables producers and consumers to send and receive messages at different rates. In many applications, the system load varies over time. However, the processing time required for each unit of work is typically constant. Intermediating message producers and consumers with a queue means that the consuming application only has to be able to handle average load instead of peak load.
	Một lợi ích liên quan là **cân bằng tải**, cho phép người gửi và người tiêu dùng gửi và nhận tin nhắn với tốc độ khác nhau. Trong nhiều ứng dụng, tải hệ thống thay đổi theo thời gian. Tuy nhiên, thời gian xử lý cần thiết cho mỗi đơn vị công việc thường là không đổi. Việc sử dụng hàng đợi làm trung gian giữa người gửi và người tiêu dùng tin nhắn có nghĩa là ứng dụng tiêu thụ chỉ cần xử lý tải trung bình thay vì tải cao điểm.

Using queues to intermediate between message producers and consumers provides an inherent loose coupling between the components. Because producers and consumers aren't aware of each other, a consumer can be upgraded without having any effect on the producer.
	Sử dụng hàng đợi để làm trung gian giữa người gửi và người tiêu dùng tin nhắn tạo ra sự liên kết lỏng lẻo vốn có giữa các thành phần. Vì người gửi và người tiêu dùng không biết về nhau, nên người tiêu dùng có thể được nâng cấp mà không ảnh hưởng đến người gửi.

You can create queues using the Azure portal, PowerShell, CLI, or Resource Manager templates. Then, send and receive messages using clients written in C#, Java, Python, and JavaScript.
	Bạn có thể tạo hàng đợi bằng cổng Azure, PowerShell, CLI hoặc các mẫu của Resource Manager. Sau đó, gửi và nhận tin nhắn bằng các ứng dụng khách được viết bằng C#, Java, Python và JavaScript.

## Receive modes

You can specify two different modes in which Service Bus receives messages: **Receive and delete** or **Peek lock**.
	Bạn có thể chỉ định hai chế độ khác nhau mà Service Bus nhận tin nhắn: **Nhận và xóa** hoặc **Khóa xem trước**.

### Receive and delete

In this mode, when Service Bus receives the request from the consumer, it marks the message as consumed and returns it to the consumer application. This mode is the simplest model. It works best for scenarios in which the application can tolerate not processing a message if a failure occurs. For example, consider a scenario in which the consumer issues the receive request and then crashes before processing it. As Service Bus marks the message as consumed, the application begins consuming messages upon restart. It misses the message that it consumed before the crash.
	Ở chế độ này, khi Service Bus nhận được yêu cầu từ ứng dụng tiêu thụ, nó sẽ đánh dấu thông báo là đã được tiêu thụ và trả lại cho ứng dụng tiêu thụ. Chế độ này là mô hình đơn giản nhất. Nó hoạt động tốt nhất trong các trường hợp mà ứng dụng có thể chấp nhận việc không xử lý thông báo nếu xảy ra lỗi. Ví dụ, hãy xem xét trường hợp ứng dụng tiêu thụ gửi yêu cầu nhận và sau đó bị lỗi trước khi xử lý. Vì Service Bus đánh dấu thông báo là đã được tiêu thụ, ứng dụng bắt đầu tiêu thụ các thông báo khi khởi động lại. Nó sẽ bỏ sót thông báo mà nó đã tiêu thụ trước khi xảy ra lỗi.

### Peek lock

In this mode, the receive operation becomes two-stage, which makes it possible to support applications that can't tolerate missing messages.
	Ở chế độ này, quá trình nhận dữ liệu diễn ra theo hai giai đoạn, cho phép hỗ trợ các ứng dụng không thể chấp nhận việc mất dữ liệu.

1. Finds the next message to be consumed, **locks** it to prevent other consumers from receiving it, and then, return the message to the application.
    Tìm kiếm thông điệp tiếp theo cần được xử lý, **khóa** thông điệp đó để ngăn các trình tiêu thụ khác nhận được, và sau đó, trả lại thông điệp cho ứng dụng.
2. After the application finishes processing the message, it requests the Service Bus service to complete the second stage of the receive process. Then, the service **marks the message as consumed**.
	Sau khi ứng dụng xử lý xong thông báo, nó yêu cầu dịch vụ Service Bus hoàn tất giai đoạn thứ hai của quá trình nhận. Sau đó, dịch vụ đánh dấu thông báo là đã được tiêu thụ.

If the application is unable to process the message for some reason, it can request the Service Bus service to **abandon** the message. Service Bus **unlocks** the message and makes it available to be received again, either by the same consumer or by another competing consumer. Secondly, there's a **timeout** associated with the lock. If the application fails to process the message before the lock timeout expires, Service Bus unlocks the message and makes it available to be received again.
	Nếu ứng dụng không thể xử lý thông báo vì lý do nào đó, nó có thể yêu cầu dịch vụ Service Bus **hủy bỏ** thông báo. Service Bus **mở khóa** thông báo và cho phép thông báo được nhận lại, bởi cùng một người dùng hoặc bởi một người dùng cạnh tranh khác. Thứ hai, có một **thời gian chờ** liên quan đến khóa. Nếu ứng dụng không xử lý được thông báo trước khi thời gian chờ khóa hết hạn, Service Bus sẽ mở khóa thông báo và cho phép thông báo được nhận lại.

## Topics and subscriptions

A queue allows processing of a message by a single consumer. In contrast to queues, topics and subscriptions provide a one-to-many form of communication in a **publish and subscribe** pattern. It's useful for scaling to large numbers of recipients. Each published message is made available to each subscription registered with the topic. Publisher sends a message to a topic and one or more subscribers receive a copy of the message.
	Hàng đợi cho phép xử lý một tin nhắn bởi một người tiêu dùng duy nhất. Ngược lại với hàng đợi, chủ đề và đăng ký cung cấp hình thức giao tiếp một-nhiều theo mô hình **xuất bản và đăng ký**. Điều này hữu ích khi cần mở rộng quy mô cho số lượng lớn người nhận. Mỗi tin nhắn được xuất bản sẽ được cung cấp cho mỗi đăng ký đã đăng ký với chủ đề đó. Người xuất bản gửi tin nhắn đến một chủ đề và một hoặc nhiều người đăng ký sẽ nhận được bản sao của tin nhắn.

The subscriptions can use more filters to restrict the messages that they want to receive. Publishers send messages to a topic in the same way that they send messages to a queue. But, consumers don't receive messages directly from the topic. Instead, consumers receive messages from subscriptions of the topic. A topic subscription resembles a virtual queue that receives copies of the messages that are sent to the topic. Consumers receive messages from a subscription identically to the way they receive messages from a queue.
	Những người đăng ký có thể sử dụng thêm bộ lọc để hạn chế các tin nhắn mà họ muốn nhận. Người xuất bản gửi tin nhắn đến một chủ đề theo cùng một cách mà họ gửi tin nhắn đến một hàng đợi. Nhưng người tiêu dùng không nhận tin nhắn trực tiếp từ chủ đề. Thay vào đó, người tiêu dùng nhận tin nhắn từ các đăng ký của chủ đề. Một đăng ký chủ đề giống như một hàng đợi ảo nhận các bản sao của các tin nhắn được gửi đến chủ đề. Người tiêu dùng nhận tin nhắn từ một đăng ký giống hệt như cách họ nhận tin nhắn từ một hàng đợi.

The message-sending functionality of a queue maps directly to a topic and its message-receiving functionality maps to a subscription. Among other things, this feature means that subscriptions support the same patterns described earlier in this section regarding queues: competing consumer, temporal decoupling, load leveling, and load balancing.
	Chức năng gửi tin nhắn của hàng đợi được ánh xạ trực tiếp đến một chủ đề và chức năng nhận tin nhắn của nó được ánh xạ đến một đăng ký. Trong số những điều khác, tính năng này có nghĩa là các gói đăng ký hỗ trợ các mô hình tương tự như đã mô tả trước đó trong phần này liên quan đến hàng đợi: người tiêu dùng cạnh tranh, tách biệt theo thời gian, san bằng tải và cân bằng tải.

### Rules and actions

In many scenarios, messages that have specific characteristics must be processed in different ways. To enable this processing, you can configure subscriptions to find messages that have desired properties and then perform certain modifications to those properties. While Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue. This filtering is accomplished using subscription filters. Such modifications are called **filter actions**. When a subscription is created, you can supply a filter expression that operates on the properties of the message. The properties can be both the system properties (for example, **Label**) and custom application properties (for example, **StoreName**.) The SQL filter expression is optional in this case. Without a SQL filter expression, any filter action defined on a subscription is performed on all the messages for that subscription.
	Trong nhiều trường hợp, các thông báo có đặc điểm cụ thể cần được xử lý theo những cách khác nhau. Để cho phép xử lý này, bạn có thể cấu hình các đăng ký để tìm các thông báo có thuộc tính mong muốn và sau đó thực hiện một số sửa đổi nhất định đối với các thuộc tính đó. Mặc dù các đăng ký Service Bus xem tất cả các thông báo được gửi đến chủ đề, bạn chỉ có thể sao chép một tập hợp con các thông báo đó vào hàng đợi đăng ký ảo. Việc lọc này được thực hiện bằng cách sử dụng các bộ lọc đăng ký. Những sửa đổi như vậy được gọi là **hành động lọc**. Khi tạo một đăng ký, bạn có thể cung cấp một biểu thức lọc hoạt động trên các thuộc tính của thông báo. Các thuộc tính có thể là cả thuộc tính hệ thống (ví dụ: **Nhãn**) và thuộc tính ứng dụng tùy chỉnh (ví dụ: **Tên cửa hàng**). Biểu thức lọc SQL là tùy chọn trong trường hợp này. Nếu không có biểu thức lọc SQL, bất kỳ hành động lọc nào được định nghĩa trên một đăng ký sẽ được thực hiện trên tất cả các thông báo cho đăng ký đó.

# Explore Service Bus message payloads and serialization
___

Messages carry a payload and metadata. The metadata is in the form of key-value pair properties, and describes the payload, and gives handling instructions to Service Bus and applications. Occasionzzally, that metadata alone is sufficient to carry the information that the sender wants to communicate to receivers, and the payload remains empty.
	Các thông điệp mang theo dữ liệu chính (payload) và siêu dữ liệu (metadata). Siêu dữ liệu có dạng cặp thuộc tính khóa-giá trị, mô tả dữ liệu chính và cung cấp hướng dẫn xử lý cho Service Bus và các ứng dụng. Đôi khi, chỉ riêng siêu dữ liệu đó là đủ để truyền tải thông tin mà người gửi muốn gửi đến người nhận, và dữ liệu chính có thể để trống.

The object model of the official Service Bus clients for .NET and Java maps to and from the wire protocols Service Bus supports.
	Mô hình đối tượng của các máy khách Service Bus chính thức dành cho .NET và Java ánh xạ tới và từ các giao thức truyền tải mà Service Bus hỗ trợ.

A Service Bus message consists of a binary payload section that Service Bus never handles in any form on the service-side, and two sets of properties. The _broker properties_ are system defined. These predefined properties either control message-level functionality inside the broker, or they map to common and standardized metadata items. The _user properties_ are a collection of key-value pairs defined and set by the application.
	Một thông điệp Service Bus bao gồm một phần dữ liệu nhị phân mà Service Bus không bao giờ xử lý dưới bất kỳ hình thức nào ở phía máy chủ, và hai tập hợp thuộc tính. Các _thuộc tính broker_ được hệ thống định nghĩa. Các thuộc tính được định nghĩa trước này hoặc kiểm soát chức năng cấp thông điệp bên trong broker, hoặc chúng ánh xạ tới các mục siêu dữ liệu chung và được tiêu chuẩn hóa. Các _thuộc tính người dùng_ là một tập hợp các cặp khóa-giá trị được định nghĩa và thiết lập bởi ứng dụng.

## Message routing and correlation

A subset of the broker properties, specifically `To`, `ReplyTo`, `ReplyToSessionId`, `MessageId`, `CorrelationId`, and `SessionId`, help applications route messages to particular destinations. The following patterns describe the routing:
	Một tập hợp con các thuộc tính của broker, cụ thể là `To`, `ReplyTo`, `ReplyToSessionId`, `MessageId`, `CorrelationId` và `SessionId`, giúp các ứng dụng định tuyến tin nhắn đến các đích cụ thể. Các mẫu sau mô tả quá trình định tuyến:

- **Simple request/reply:** A publisher sends a message into a queue and expects a reply from the message consumer. The publisher owns a queue to receive the replies. The address of that queue is contained in the `ReplyTo` property of the outbound message. When the consumer responds, it copies the `MessageId` of the handled message into the `CorrelationId` property of the reply message and delivers the message to the destination indicated by the `ReplyTo` property. One message can yield multiple replies, depending on the application context.
    **Yêu cầu/phản hồi đơn giản:** Nhà xuất bản gửi một tin nhắn vào hàng đợi và mong đợi phản hồi từ người tiêu dùng tin nhắn. Nhà xuất bản sở hữu một hàng đợi để nhận các phản hồi. Địa chỉ của hàng đợi đó được chứa trong thuộc tính `ReplyTo` của tin nhắn gửi đi. Khi người tiêu dùng phản hồi, nó sao chép `MessageId` của tin nhắn đã xử lý vào thuộc tính `CorrelationId` của tin nhắn phản hồi và chuyển tiếp tin nhắn đến đích được chỉ định bởi thuộc tính `ReplyTo`. Một tin nhắn có thể tạo ra nhiều phản hồi, tùy thuộc vào ngữ cảnh của ứng dụng.
- **Multicast request/reply:** As a variation of the prior pattern, a publisher sends the message into a topic and multiple subscribers become eligible to consume the message. Each of the subscribers might respond in the fashion described previously. If `ReplyTo` points to a topic, such a set of discovery responses can be distributed to an audience.
    **Yêu cầu/phản hồi đa hướng:** Là một biến thể của mô hình trước đó, người gửi sẽ gửi tin nhắn vào một chủ đề và nhiều người nhận sẽ đủ điều kiện để nhận tin nhắn. Mỗi người nhận có thể phản hồi theo cách đã mô tả trước đó. Nếu `ReplyTo` trỏ đến một chủ đề, một tập hợp các phản hồi khám phá như vậy có thể được phân phối đến một đối tượng.
- **Multiplexing:** This session feature enables multiplexing of streams of related messages through a single queue or subscription such that each session (or group) of related messages, identified by matching `SessionId` values, are routed to a specific receiver while the receiver holds the session under lock. Learn more about the details of sessions [here](https://learn.microsoft.com/en-us/azure/service-bus-messaging/message-sessions).
    **Ghép kênh:** Tính năng phiên này cho phép ghép kênh các luồng tin nhắn liên quan thông qua một hàng đợi hoặc đăng ký duy nhất sao cho mỗi phiên (hoặc nhóm) tin nhắn liên quan, được xác định bằng cách khớp các giá trị `SessionId`, được định tuyến đến một người nhận cụ thể trong khi người nhận giữ phiên đó trong trạng thái khóa. Tìm hiểu thêm về chi tiết của các phiên [tại đây](https://learn.microsoft.com/en-us/azure/service-bus-messaging/message-sessions).
- **Multiplexed request/reply:** This session feature enables multiplexed replies, allowing several publishers to share a reply queue. By setting `ReplyToSessionId`, the publisher can instruct one or more consumers to copy that value into the `SessionId` property of the reply message. The publishing queue or topic doesn't need to be session-aware. When the message is sent the publisher can wait for a session with the given `SessionId` to materialize on the queue by conditionally accepting a session receiver.
	**Yêu cầu/phản hồi đa hướng:** Tính năng phiên này cho phép phản hồi đa hướng, cho phép nhiều người gửi chia sẻ một hàng đợi phản hồi. Bằng cách thiết lập `ReplyToSessionId`, người gửi có thể hướng dẫn một hoặc nhiều người nhận sao chép giá trị đó vào thuộc tính `SessionId` của thông báo phản hồi. Hàng đợi hoặc chủ đề gửi không cần phải nhận biết phiên. Khi thông báo được gửi đi, người gửi có thể chờ một phiên với `SessionId` đã cho xuất hiện trên hàng đợi bằng cách chấp nhận có điều kiện một bộ nhận phiên.

## Payload serialization

When in transit or stored inside of Service Bus, the payload is always an opaque, binary block. The `ContentType` property enables applications to describe the payload, with the suggested format for the property values being a MIME content-type description according to IETF RFC2045; for example, `application/json;charset=utf-8`.
	Khi đang truyền tải hoặc được lưu trữ bên trong Service Bus, dữ liệu tải trọng luôn là một khối nhị phân không rõ ràng. Thuộc tính `ContentType` cho phép các ứng dụng mô tả dữ liệu tải trọng, với định dạng được đề xuất cho các giá trị thuộc tính là mô tả kiểu nội dung MIME theo IETF RFC2045; ví dụ: `application/json;charset=utf-8`.

Unlike the Java or .NET Standard variants, the .NET Framework version of the Service Bus API supports creating `BrokeredMessage` instances by passing arbitrary .NET objects into the constructor.
	Không giống như các phiên bản Java hoặc .NET Standard, phiên bản .NET Framework của API Service Bus hỗ trợ tạo các thể hiện `BrokeredMessage` bằng cách truyền các đối tượng .NET tùy ý vào hàm tạo.

The legacy SBMP protocol serializes objects with the default binary serializer, or with a serializer that is externally supplied. The AMQP protocol serializes objects into an AMQP object. The receiver can retrieve those objects with the `GetBody<T>()` method, supplying the expected type. With AMQP, the objects are serialized into an AMQP graph of `ArrayList` and `IDictionary<string,object>` objects, and any AMQP client can decode them.
	Giao thức SBMP cũ tuần tự hóa các đối tượng bằng bộ tuần tự hóa nhị phân mặc định hoặc bằng bộ tuần tự hóa được cung cấp từ bên ngoài. Giao thức AMQP tuần tự hóa các đối tượng thành một đối tượng AMQP. Bên nhận có thể truy xuất các đối tượng đó bằng phương thức `GetBody<T>()`, cung cấp kiểu dữ liệu mong muốn. Với AMQP, các đối tượng được tuần tự hóa thành một đồ thị AMQP gồm các đối tượng `ArrayList` và `IDictionary<string,object>`, và bất kỳ máy khách AMQP nào cũng có thể giải mã chúng.

While this hidden serialization magic is convenient, if applications should take explicit control of object serialization and turn their object graphs into streams before including them into a message, they should do the reverse operation on the receiver side. While AMQP has a powerful binary encoding model, it's tied to the AMQP messaging ecosystem and HTTP clients have trouble decoding such payloads.
	Mặc dù cơ chế tuần tự hóa ẩn này rất tiện lợi, nhưng nếu các ứng dụng cần kiểm soát rõ ràng việc tuần tự hóa đối tượng và chuyển đổi đồ thị đối tượng của chúng thành các luồng trước khi đưa vào thông điệp, thì chúng nên thực hiện thao tác ngược lại ở phía người nhận. Mặc dù AMQP có mô hình mã hóa nhị phân mạnh mẽ, nhưng nó lại gắn liền với hệ sinh thái nhắn tin AMQP và các máy khách HTTP gặp khó khăn trong việc giải mã các tải trọng như vậy.

# Explore Azure Queue Storage
___

Azure Queue Storage is a service for storing large numbers of messages. You access messages from anywhere in the world via authenticated calls using HTTP or HTTPS. A queue message can be up to 64 KB in size. A queue might contain millions of messages, up to the total capacity limit of a storage account. Queues are commonly used to create a backlog of work to process asynchronously.
	Azure Queue Storage là một dịch vụ dùng để lưu trữ số lượng lớn tin nhắn. Bạn có thể truy cập tin nhắn từ bất cứ đâu trên thế giới thông qua các cuộc gọi được xác thực bằng HTTP hoặc HTTPS. Một tin nhắn trong hàng đợi có thể có kích thước tối đa 64 KB. Một hàng đợi có thể chứa hàng triệu tin nhắn, tối đa bằng giới hạn dung lượng của tài khoản lưu trữ. Hàng đợi thường được sử dụng để tạo ra một danh sách công việc cần xử lý bất đồng bộ.

The Queue service contains the following components:
	Dịch vụ Hàng đợi bao gồm các thành phần sau:

![Image showing components of the queue service](https://learn.microsoft.com/en-us/training/wwl-azure/discover-azure-message-queue/media/queue-storage-service-components.png)

- **URL format:** Queues are addressable using the URL format `https://<storage account>.queue.core.windows.net/<queue>`. For example, the following URL addresses a queue in the diagram above `https://myaccount.queue.core.windows.net/images-to-download`
	**Định dạng URL:** Các hàng đợi có thể được truy cập bằng định dạng URL `https://<tài khoản lưu trữ>.queue.core.windows.net/<hàng đợi>`. Ví dụ, URL sau đây truy cập một hàng đợi trong sơ đồ ở trên: `https://myaccount.queue.core.windows.net/images-to-download`

- **Storage account:** All access to Azure Storage is done through a storage account.
    **Tài khoản lưu trữ:** Tất cả quyền truy cập vào Azure Storage đều được thực hiện thông qua một tài khoản lưu trữ.

- **Queue:** A queue contains a set of messages. All messages must be in a queue. The queue name must be all lowercase.
    **Hàng đợi:** Một hàng đợi chứa một tập hợp các tin nhắn. Tất cả các tin nhắn phải nằm trong một hàng đợi. Tên hàng đợi phải viết thường.

- **Message:** A message, in any format, of up to 64 KB. Before version 2017-07-29, the maximum time-to-live allowed is seven days. For version 2017-07-29 or later, the maximum time-to-live can be any positive number, or -1 indicating that the message doesn't expire. If this parameter is omitted, the default time-to-live is seven days.
	**Tin nhắn:** Một tin nhắn, ở bất kỳ định dạng nào, có dung lượng tối đa 64 KB. Trước phiên bản 2017-07-29, thời gian tồn tại tối đa cho phép là bảy ngày. Đối với phiên bản 2017-07-29 trở lên, thời gian tồn tại tối đa có thể là bất kỳ số dương nào, hoặc -1 cho biết tin nhắn không hết hạn. Nếu bỏ qua tham số này, thời gian tồn tại mặc định là bảy ngày.

# Create and manage Azure Queue Storage and messages by using .NET
___

In this unit we're covering how to create queues and manage messages in Azure Queue Storage by showing code snippets from a .NET project.

The code examples rely on the following NuGet packages:

- [Azure.Core library for .NET](https://www.nuget.org/packages/azure.core/): This package provides shared primitives, abstractions, and helpers for modern .NET Azure SDK client libraries.
- [Azure.Storage.Common client library for .NET](https://www.nuget.org/packages/azure.storage.common/): This package provides infrastructure shared by the other Azure Storage client libraries.
- [Azure.Storage.Queues client library for .NET](https://www.nuget.org/packages/azure.storage.queues/): This package enables working with Azure Queue Storage for storing messages that accessed by a client.
- [System.Configuration.ConfigurationManager library for .NET](https://www.nuget.org/packages/system.configuration.configurationmanager/): This package provides access to configuration files for client applications.

## Create the Queue service client

The `QueueClient` class enables you to retrieve queues stored in Queue storage. Here's one way to create the service client:

C#
```
QueueClient queueClient = new QueueClient(connectionString, queueName);
```

## Create a queue

This example shows how to create a queue if it doesn't already exist:

C#

```
// Get the connection string from app settings
string connectionString = ConfigurationManager.AppSettings["StorageConnectionString"];

// Instantiate a QueueClient which will be used to create and manipulate the queue
QueueClient queueClient = new QueueClient(connectionString, queueName);

// Create the queue
queueClient.CreateIfNotExists();
```

## Insert a message into a queue

To insert a message into an existing queue, call the `SendMessage` method. A message can be either a string (in UTF-8 format) or a byte array. The following code creates a queue (if it doesn't exist) and inserts a message:

C#
```
// Get the connection string from app settings
string connectionString = ConfigurationManager.AppSettings["StorageConnectionString"];

// Instantiate a QueueClient which will be used to create and manipulate the queue
QueueClient queueClient = new QueueClient(connectionString, queueName);

// Create the queue if it doesn't already exist
queueClient.CreateIfNotExists();

if (queueClient.Exists())
{
    // Send a message to the queue
    queueClient.SendMessage(message);
}
```

## Peek at the next message

You can peek at the messages in the queue without removing them from the queue by calling the `PeekMessages` method. If you don't pass a value for the `maxMessages` parameter, the default is to peek at one message.

C#

```
// Get the connection string from app settings
string connectionString = ConfigurationManager.AppSettings["StorageConnectionString"];

// Instantiate a QueueClient which will be used to manipulate the queue
QueueClient queueClient = new QueueClient(connectionString, queueName);

if (queueClient.Exists())
{ 
    // Peek at the next message
    PeekedMessage[] peekedMessage = queueClient.PeekMessages();
}
```

## Change the contents of a queued message

You can change the contents of a message in-place in the queue. If the message represents a work task, you could use this feature to update the status of the work task. The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds. This saves the state of work associated with the message, and gives the client another minute to continue working on the message.

C#
```
// Get the connection string from app settings
string connectionString = ConfigurationManager.AppSettings["StorageConnectionString"];

// Instantiate a QueueClient which will be used to manipulate the queue
QueueClient queueClient = new QueueClient(connectionString, queueName);

if (queueClient.Exists())
{
    // Get the message from the queue
    QueueMessage[] message = queueClient.ReceiveMessages();

    // Update the message contents
    queueClient.UpdateMessage(message[0].MessageId, 
            message[0].PopReceipt, 
            "Updated contents",
            TimeSpan.FromSeconds(60.0)  // Make it invisible for another 60 seconds
        );
}
```

## Dequeue the next message

Dequeue a message from a queue in two steps. When you call `ReceiveMessages`, you get the next message in a queue. A message returned from `ReceiveMessages` becomes invisible to any other code reading messages from this queue. By default, this message stays invisible for 30 seconds. To finish removing the message from the queue, you must also call `DeleteMessage`. This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again. Your code calls `DeleteMessage` right after the message has been processed.

C#
```
// Get the connection string from app settings
string connectionString = ConfigurationManager.AppSettings["StorageConnectionString"];

// Instantiate a QueueClient which will be used to manipulate the queue
QueueClient queueClient = new QueueClient(connectionString, queueName);

if (queueClient.Exists())
{
    // Get the next message
    QueueMessage[] retrievedMessage = queueClient.ReceiveMessages();

    // Process (i.e. print) the message in less than 30 seconds
    Console.WriteLine($"Dequeued message: '{retrievedMessage[0].Body}'");

    // Delete the message
    queueClient.DeleteMessage(retrievedMessage[0].MessageId, retrievedMessage[0].PopReceipt);
}
```

## Get the queue length

You can get an estimate of the number of messages in a queue. The `GetProperties` method returns queue properties including the message count. The `ApproximateMessagesCount` property contains the approximate number of messages in the queue. This number isn't lower than the actual number of messages in the queue, but could be higher.

C#
```
/// Instantiate a QueueClient which will be used to manipulate the queue
QueueClient queueClient = new QueueClient(connectionString, queueName);

if (queueClient.Exists())
{
    QueueProperties properties = queueClient.GetProperties();

    // Retrieve the cached approximate message count.
    int cachedMessagesCount = properties.ApproximateMessagesCount;

    // Display number of messages.
    Console.WriteLine($"Number of messages in queue: {cachedMessagesCount}");
}
```

## Delete a queue

To delete a queue and all the messages contained in it, call the `Delete` method on the queue object.

C#
```
/// Get the connection string from app settings
string connectionString = ConfigurationManager.AppSettings["StorageConnectionString"];

// Instantiate a QueueClient which will be used to manipulate the queue
QueueClient queueClient = new QueueClient(connectionString, queueName);

if (queueClient.Exists())
{
    // Delete the queue
    queueClient.Delete();
}
```