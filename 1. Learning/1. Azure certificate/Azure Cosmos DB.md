Azure Cosmos DB is a globally distributed database system that allows you to read and write data from the local replicas of your database and it transparently replicates the data to all the regions associated with your Cosmos account.
	Azure Cosmos DB là một hệ thống cơ sở dữ liệu phân tán toàn cầu cho phép bạn đọc và ghi dữ liệu từ các bản sao cục bộ của cơ sở dữ liệu và tự động sao chép dữ liệu đến tất cả các khu vực được liên kết với tài khoản Cosmos của bạn.

After completing this module, you'll be able to:
	Sau khi hoàn thành mô-đun này, bạn sẽ có thể:

- Identify the key benefits provided by Azure Cosmos DB
	Xác định các lợi ích chính mà Azure Cosmos DB cung cấp
- Describe the elements in an Azure Cosmos DB account and how they're organized
	Mô tả các thành phần trong tài khoản Azure Cosmos DB và cách chúng được tổ chức
- Explain the different consistency levels and choose the correct one for your project
	Giải thích các cấp độ nhất quán khác nhau và chọn cấp độ phù hợp cho dự án của bạn
- Explore the APIs supported in Azure Cosmos DB and choose the appropriate API for your solution
	Khám phá các API được hỗ trợ trong Azure Cosmos DB và chọn API phù hợp cho giải pháp của bạn
- Describe how request units impact costs
	Mô tả cách đơn vị yêu cầu ảnh hưởng đến chi phí
- Create Azure Cosmos DB resources by using the Azure portal.
	Tạo tài nguyên Azure Cosmos DB bằng cách sử dụng cổng thông tin Azure.

# Identify key benefits of Azure Cosmos DB
___
Azure **Cosmos** DB is a fully managed NoSQL database designed to provide low latency, elastic scalability of throughput, well-defined semantics for data consistency, and high availability.
	Azure Cosmos DB là cơ sở dữ liệu NoSQL được quản lý hoàn toàn, được thiết kế để cung cấp độ trễ thấp, khả năng mở rộng linh hoạt về thông lượng, ngữ nghĩa được xác định rõ ràng cho tính nhất quán dữ liệu và tính khả dụng cao.

You can configure your databases to be globally distributed and available in any of the Azure regions. To lower the latency, place the data close to where your users are. Choosing the required regions depends on the global reach of your application and where your users are located.
	Bạn có thể cấu hình cơ sở dữ liệu của mình để phân tán toàn cầu và khả dụng ở bất kỳ vùng nào của Azure. Để giảm độ trễ, hãy đặt dữ liệu gần nơi người dùng của bạn đang ở. Việc lựa chọn các vùng cần thiết phụ thuộc vào phạm vi toàn cầu của ứng dụng và vị trí của người dùng.

With Azure Cosmos DB, you can add or remove the regions associated with your account at any time. Your application doesn't need to be paused or redeployed to add or remove a region.
	Với Azure Cosmos DB, bạn có thể thêm hoặc xóa các vùng được liên kết với tài khoản của mình bất cứ lúc nào. Ứng dụng của bạn không cần phải tạm dừng hoặc triển khai lại để thêm hoặc xóa một vùng.
## Key benefits of global distribution
___
With its novel multi-master replication protocol, every region supports both writes and reads. The multi-master capability also enables:
	Với giao thức sao chép đa chủ (multi-master replication protocol) tiên tiến, mọi khu vực đều hỗ trợ cả ghi và đọc. Khả năng đa chủ cũng cho phép:

- Unlimited elastic write and read scalability.
	Khả năng mở rộng ghi và đọc linh hoạt không giới hạn.
- 99.999% read and write availability all around the world.
	Độ khả dụng đọc và ghi 99,999% trên toàn thế giới.
- Guaranteed reads and writes served in less than 10 milliseconds at the 99th percentile.
	Đảm bảo các thao tác đọc và ghi được thực hiện trong vòng chưa đến 10 mili giây ở phân vị thứ 99.

Your application can perform near real-time reads and writes against all the regions you chose for your database. Azure Cosmos DB internally handles the data replication between regions with consistency level guarantees of the level you selected.
	Ứng dụng của bạn có thể thực hiện các thao tác đọc và ghi gần như thời gian thực đối với tất cả các khu vực bạn đã chọn cho cơ sở dữ liệu của mình. Azure Cosmos DB tự động xử lý việc sao chép dữ liệu giữa các khu vực với mức độ nhất quán được đảm bảo theo mức bạn đã chọn.

Running a database in multiple regions worldwide increases the availability of a database. If one region is unavailable, other regions automatically handle application requests. Azure Cosmos DB offers 99.999% read and write availability for multi-region databases.
	Việc chạy cơ sở dữ liệu ở nhiều khu vực trên toàn thế giới làm tăng tính khả dụng của cơ sở dữ liệu. Nếu một khu vực không khả dụng, các khu vực khác sẽ tự động xử lý các yêu cầu của ứng dụng. Azure Cosmos DB cung cấp độ khả dụng đọc và ghi 99,999% cho các cơ sở dữ liệu đa khu vực.

# Explore the resource hierarchy
___
The Azure Cosmos DB account is the fundamental unit of global distribution and high availability. Your Azure Cosmos DB account contains a unique Domain Name System (DNS) name and you can manage an account by using the Azure portal or the Azure CLI, or by using different language-specific SDKs. For globally distributing your data and throughput across multiple Azure regions, you can add and remove Azure regions to your account at any time.
	Tài khoản Azure Cosmos DB là đơn vị cơ bản của phân phối toàn cầu và tính khả dụng cao. Tài khoản Azure Cosmos DB của bạn chứa một tên Hệ thống Tên miền (DNS) duy nhất và bạn có thể quản lý tài khoản bằng cách sử dụng cổng thông tin Azure hoặc Azure CLI, hoặc bằng cách sử dụng các SDK dành riêng cho từng ngôn ngữ. Để phân phối dữ liệu và thông lượng của bạn trên toàn cầu trên nhiều vùng Azure, bạn có thể thêm và xóa các vùng Azure khỏi tài khoản của mình bất cứ lúc nào.
## Elements in an Azure Cosmos DB account

An Azure Cosmos DB container is the fundamental unit of scalability. You can virtually have an unlimited provisioned throughput (RU/s) and storage on a container. Azure Cosmos DB transparently partitions your container using the logical partition key that you specify in order to elastically scale your provisioned throughput and storage.
	Một container Azure Cosmos DB là đơn vị cơ bản của khả năng mở rộng. Bạn có thể có thông lượng (RU/s) và dung lượng lưu trữ được cấp phát gần như không giới hạn trên một container. Azure Cosmos DB tự động phân vùng container của bạn bằng cách sử dụng khóa phân vùng logic mà bạn chỉ định để mở rộng thông lượng và dung lượng lưu trữ được cấp phát một cách linh hoạt.

Currently, you can create a maximum of 50 Azure Cosmos DB accounts under an Azure subscription (can be increased via support request). After you create an account under your Azure subscription, you can manage the data in your account by creating databases, containers, and items.
	Hiện tại, bạn có thể tạo tối đa 50 tài khoản Azure Cosmos DB trong một gói đăng ký Azure (có thể tăng lên thông qua yêu cầu hỗ trợ). Sau khi tạo tài khoản trong gói đăng ký Azure của mình, bạn có thể quản lý dữ liệu trong tài khoản bằng cách tạo cơ sở dữ liệu, container và các mục.

The following image shows the hierarchy of different entities in an Azure Cosmos DB account:
	Hình ảnh sau đây hiển thị thứ bậc của các thực thể khác nhau trong tài khoản Azure Cosmos DB:

![Image showing the hierarchy of Azure Cosmos DB entities: Database accounts are at the top, databases are grouped under accounts, and containers are grouped under databases.](https://learn.microsoft.com/en-us/training/wwl-azure/explore-azure-cosmos-db/media/cosmos-entities.png)

## Azure Cosmos DB databases

You can create one or multiple Azure Cosmos DB databases under your account. A database is analogous to a namespace. A database is the unit of management for a set of Azure Cosmos DB containers.
	Bạn có thể tạo một hoặc nhiều cơ sở dữ liệu Azure Cosmos DB trong tài khoản của mình. Cơ sở dữ liệu tương tự như một không gian tên. Cơ sở dữ liệu là đơn vị quản lý cho một tập hợp các container Azure Cosmos DB.

## Azure Cosmos DB containers

An Azure Cosmos DB container is where data is stored. Unlike most relational databases, which scale up with larger sizes of virtual machines, Azure Cosmos DB scales out.
	Một container Azure Cosmos DB là nơi dữ liệu được lưu trữ. Không giống như hầu hết các cơ sở dữ liệu quan hệ, mở rộng quy mô theo kích thước máy ảo lớn hơn, Azure Cosmos DB mở rộng theo chiều ngang.

Data is stored on one or more servers called _partitions_. To increase partitions, you increase throughput, or they grow automatically as storage increases. This relationship provides a virtually unlimited amount of throughput and storage for a container.
	Dữ liệu được lưu trữ trên một hoặc nhiều máy chủ được gọi là phân vùng. Để tăng số lượng phân vùng, bạn tăng thông lượng, hoặc chúng sẽ tự động tăng khi dung lượng lưu trữ tăng. Mối quan hệ này cung cấp thông lượng và dung lượng lưu trữ gần như không giới hạn cho một container.

When you create a container, you need to supply a partition key. The partition key is a property that you select from your items to help Azure Cosmos DB distribute the data efficiently across partitions. Azure Cosmos DB uses the value of this property to route data to the appropriate partition to be written, updated, or deleted. You can also use the partition key in the `WHERE` clause in queries for efficient data retrieval.
	Khi tạo một container, bạn cần cung cấp một khóa phân vùng. Khóa phân vùng là một thuộc tính mà bạn chọn từ các mục của mình để giúp Azure Cosmos DB phân phối dữ liệu hiệu quả trên các phân vùng. Azure Cosmos DB sử dụng giá trị của thuộc tính này để định tuyến dữ liệu đến phân vùng thích hợp để ghi, cập nhật hoặc xóa. Bạn cũng có thể sử dụng khóa phân vùng trong mệnh đề WHERE trong các truy vấn để truy xuất dữ liệu hiệu quả.

The underlying storage mechanism for data in Azure Cosmos DB is called a _physical partition_. Physical partitions can have a throughput amount up to 10,000 Request Units per second, and they can store up to 50 GB of data. Azure Cosmos DB abstracts this partitioning concept with a logical partition, which can store up to 20 GB of data.
	Cơ chế lưu trữ dữ liệu cơ bản trong Azure Cosmos DB được gọi là phân vùng vật lý. Các phân vùng vật lý có thể có thông lượng lên đến 10.000 đơn vị yêu cầu mỗi giây và chúng có thể lưu trữ tối đa 50 GB dữ liệu. Azure Cosmos DB trừu tượng hóa khái niệm phân vùng này bằng một phân vùng logic, có thể lưu trữ tối đa 20 GB dữ liệu.

When you create a container, you configure throughput in one of the following modes:
	Khi bạn tạo một vùng chứa, bạn cấu hình thông lượng theo một trong các chế độ sau:

- **Dedicated throughput**: The throughput on a container is exclusively reserved for that container. There are two types of dedicated throughput: standard and autoscale.
    Thông lượng chuyên dụng: Thông lượng trên một vùng chứa được dành riêng cho vùng chứa đó. Có hai loại thông lượng chuyên dụng: tiêu chuẩn và tự động mở rộng.
- **Shared throughput**: Throughput is specified at the database level and then shared with up to 25 containers within the database. Sharing of throughput excludes containers that are configured with their own dedicated throughput.
    Thông lượng chia sẻ: Thông lượng được chỉ định ở cấp độ cơ sở dữ liệu và sau đó được chia sẻ với tối đa 25 vùng chứa trong cơ sở dữ liệu. Việc chia sẻ thông lượng không bao gồm các vùng chứa được cấu hình với thông lượng chuyên dụng riêng.

## Azure Cosmos DB items

Depending on which API you use, individual data entities can be represented in various ways:
	Tùy thuộc vào API bạn sử dụng, các thực thể dữ liệu riêng lẻ có thể được biểu diễn theo nhiều cách khác nhau:

| Azure Cosmos DB entity | API for NoSQL | API for Cassandra | API for MongoDB | API for Gremlin | API for Table |
| ---------------------- | ------------- | ----------------- | --------------- | --------------- | ------------- |
| Azure Cosmos DB item   | Item          | Row               | Document        | Node or edge    | Item          |
# Explore consistency levels
___
Azure Cosmos DB approaches data consistency as a spectrum of choices instead of two extremes. Strong consistency and eventual consistency are at the ends of the spectrum, but there are many consistency choices along the spectrum. Developers can use these options to make precise choices and granular tradeoffs with respect to high availability and performance.
	Azure Cosmos DB tiếp cận tính nhất quán dữ liệu như một chuỗi các lựa chọn thay vì hai thái cực. Tính nhất quán mạnh và tính nhất quán cuối cùng nằm ở hai đầu của chuỗi, nhưng có rất nhiều lựa chọn nhất quán khác nhau dọc theo chuỗi. Các nhà phát triển có thể sử dụng các tùy chọn này để đưa ra các lựa chọn chính xác và sự đánh đổi chi tiết liên quan đến tính khả dụng cao và hiệu suất.

Azure Cosmos DB offers five well-defined levels. From strongest to weakest, the levels are:
	Azure Cosmos DB cung cấp năm cấp độ được xác định rõ ràng. Từ mạnh nhất đến yếu nhất, các cấp độ là:

- Strong
	Mạnh
- Bounded staleness
	Độ trễ có giới hạn
- Session
	Phiên
- Consistent prefix
	Tiền tố nhất quán
- Eventual
	Cuối cùng

Each level provides availability and performance tradeoffs. The following image shows the different consistency levels as a spectrum.
	Mỗi cấp độ đều cung cấp sự đánh đổi về tính khả dụng và hiệu suất. Hình ảnh sau đây cho thấy các cấp độ nhất quán khác nhau như một chuỗi.

![Image showing data consistency as a spectrum.](https://learn.microsoft.com/en-us/training/wwl-azure/explore-azure-cosmos-db/media/five-consistency-levels.png)

The consistency levels are region-agnostic and are guaranteed for all operations, regardless of:
	Các mức độ nhất quán không phụ thuộc vào khu vực và được đảm bảo cho tất cả các thao tác, bất kể:

- The region where the reads and writes are served
	Khu vực nơi các thao tác đọc và ghi được thực hiện
- The number of regions associated with your Azure Cosmos DB account
	Số lượng khu vực được liên kết với tài khoản Azure Cosmos DB của bạn
- Whether your account is configured with a single or multiple write regions.
	Tài khoản của bạn được cấu hình với một hay nhiều khu vực ghi.

Read consistency applies to a single read operation scoped within a partition-key range or a logical partition.
	Tính nhất quán khi đọc áp dụng cho một thao tác đọc duy nhất nằm trong phạm vi khóa phân vùng hoặc phân vùng logic.

# Choose the right consistency level

___
Each of the consistency models can be used for specific real-world scenarios. Each provides precise availability and performance tradeoffs backed by comprehensive SLAs. The following simple considerations help you make the right choice in many common scenarios.
	Mỗi mô hình nhất quán có thể được sử dụng cho các tình huống thực tế cụ thể. Mỗi mô hình cung cấp sự đánh đổi chính xác giữa tính khả dụng và hiệu suất, được hỗ trợ bởi các SLA toàn diện. Những cân nhắc đơn giản sau đây sẽ giúp bạn đưa ra lựa chọn đúng đắn trong nhiều tình huống phổ biến.

## Configure the default consistency level

You can configure the default consistency level on your Azure Cosmos DB account at any time. The default consistency level configured on your account applies to all Azure Cosmos DB databases and containers under that account. All reads and queries issued against a container or a database use the specified consistency level by default.
	Bạn có thể cấu hình mức độ nhất quán mặc định trên tài khoản Azure Cosmos DB của mình bất cứ lúc nào. Mức độ nhất quán mặc định được cấu hình trên tài khoản của bạn sẽ áp dụng cho tất cả các cơ sở dữ liệu và vùng chứa Azure Cosmos DB thuộc tài khoản đó. Theo mặc định, tất cả các thao tác đọc và truy vấn được thực hiện đối với một vùng chứa hoặc cơ sở dữ liệu đều sử dụng mức độ nhất quán được chỉ định.

Read consistency applies to a single read operation scoped within a logical partition. The read operation can be issued by a remote client or a stored procedure.
	Tính nhất quán đọc áp dụng cho một thao tác đọc duy nhất nằm trong phạm vi một phân vùng logic. Thao tác đọc có thể được thực hiện bởi một máy khách từ xa hoặc một thủ tục lưu trữ.

## Guarantees associated with consistency levels

Azure Cosmos DB guarantees that 100 percent of read requests meet the consistency guarantee for the consistency level chosen. The precise definitions of the five consistency levels in Azure Cosmos DB using the TLA+ specification language are provided in the [azure-cosmos-tla](https://github.com/Azure/azure-cosmos-tla) GitHub repo.
	Azure Cosmos DB đảm bảo 100% yêu cầu đọc đáp ứng được đảm bảo tính nhất quán cho cấp độ nhất quán đã chọn. Định nghĩa chính xác của năm cấp độ nhất quán trong Azure Cosmos DB sử dụng ngôn ngữ đặc tả TLA+ được cung cấp trong kho lưu trữ GitHub [azure-cosmos-tla](https://github.com/Azure/azure-cosmos-tla).

### Strong consistency

Strong consistency offers a linearizability guarantee. Linearizability refers to serving requests concurrently. The reads are guaranteed to return the most recent committed version of an item. A client never sees an uncommitted or partial write. Users are always guaranteed to read the latest committed write.
	Tính nhất quán mạnh cung cấp đảm bảo tính tuyến tính. Tính tuyến tính đề cập đến việc phục vụ các yêu cầu đồng thời. Các thao tác đọc được đảm bảo trả về phiên bản đã được cam kết gần đây nhất của một mục. Máy khách không bao giờ thấy một thao tác ghi chưa được cam kết hoặc ghi một phần. Người dùng luôn được đảm bảo đọc bản ghi đã được cam kết mới nhất.


### Bounded staleness consistency

In bounded staleness consistency, the lag of data between any two regions is always less than a specified amount. The amount can be _K_ versions (that is, _updates_) of an item or by _T_ time intervals, whichever is reached first. In other words, when you choose bounded staleness, the maximum "staleness" of the data in any region can be configured in two ways:
	Trong tính nhất quán độ trễ có giới hạn, độ trễ dữ liệu giữa bất kỳ hai vùng nào luôn nhỏ hơn một lượng được chỉ định. Lượng này có thể là _K_ phiên bản (tức là _bản cập nhật_) của một mục hoặc _T_ khoảng thời gian, tùy thuộc vào điều kiện nào đạt được trước. Nói cách khác, khi bạn chọn độ trễ có giới hạn, độ trễ tối đa của dữ liệu trong bất kỳ vùng nào có thể được cấu hình theo hai cách:

- The number of versions (_K_) of the item
	Số lượng phiên bản (_K_) của mục
- The time interval (_T_) reads might lag behind the writes
	Khoảng thời gian (_T_) mà các thao tác đọc có thể chậm hơn so với các thao tác ghi

Bounded Staleness is beneficial primarily to single-region write accounts with two or more regions. If the data lag in a region (determined per physical partition) exceeds the configured staleness value, writes for that partition are throttled until staleness is back within the configured upper bound.
	Độ trễ có giới hạn chủ yếu có lợi cho các tài khoản ghi đơn vùng có từ hai vùng trở lên. Nếu độ trễ dữ liệu trong một vùng (được xác định trên mỗi phân vùng vật lý) vượt quá giá trị độ trễ đã cấu hình, các thao tác ghi cho phân vùng đó sẽ bị hạn chế cho đến khi độ trễ trở lại trong giới hạn trên đã cấu hình.

For a single-region account, Bounded Staleness provides the same write consistency guarantees as Session and Eventual Consistency. With Bounded Staleness, data is replicated to a local majority (three replicas in a four replica set) in the single region.
	Đối với tài khoản đơn vùng, độ trễ có giới hạn cung cấp các đảm bảo tính nhất quán ghi tương tự như tính nhất quán phiên và tính nhất quán cuối cùng. Với độ trễ có giới hạn, dữ liệu được sao chép đến đa số cục bộ (ba bản sao trong một bộ bốn bản sao) trong vùng duy nhất.

### Session consistency

In session consistency, within a single client session, reads are guaranteed to honor the read-your-writes, and write-follows-reads guarantees. This guarantee assumes a single “writer" session or sharing the session token for multiple writers.
	Trong tính nhất quán phiên, trong một phiên máy khách duy nhất, các thao tác đọc được đảm bảo tuân thủ các đảm bảo "đọc theo ghi" và "ghi theo sau đọc". Sự đảm bảo này giả định một phiên "người ghi" duy nhất hoặc chia sẻ mã thông báo phiên cho nhiều người ghi.

Like all consistency levels weaker than Strong, writes are replicated to a minimum of three replicas (in a four replica set) in the local region, with asynchronous replication to all other regions.
	Giống như tất cả các cấp độ nhất quán yếu hơn Strong, các thao tác ghi được sao chép đến tối thiểu ba bản sao (trong một bộ bốn bản sao) trong vùng cục bộ, với sao chép không đồng bộ đến tất cả các vùng khác.

### Consistent prefix consistency

In consistent prefix, updates made as single document writes see eventual consistency. Updates made as a batch within a transaction, are returned consistent to the transaction in which they were committed. Write operations within a transaction of multiple documents are always visible together.
	Trong tính nhất quán tiền tố Consistent, các bản cập nhật được thực hiện dưới dạng ghi tài liệu đơn lẻ sẽ thấy tính nhất quán cuối cùng. Các bản cập nhật được thực hiện theo lô trong một giao dịch sẽ được trả về nhất quán với giao dịch mà chúng được cam kết. Các thao tác ghi trong một giao dịch gồm nhiều tài liệu luôn hiển thị cùng nhau.

Assume two write operations are performed on documents _Doc 1_ and _Doc 2_, within transactions T1 and T2. When client does a read in any replica, the user sees either "_Doc 1_ v1 and _Doc 2_ v1" or "_Doc 1_ v2 and _Doc 2_ v2," but never "_Doc 1_ v1 and _Doc 2_ v2" or "_Doc 1_ v2 and _Doc 2_ v1" for the same read or query operation.
	Giả sử hai thao tác ghi được thực hiện trên các tài liệu _Doc 1_ và _Doc 2_, trong các giao dịch T1 và T2. Khi máy khách thực hiện thao tác đọc trên bất kỳ bản sao nào, người dùng sẽ thấy "_Doc 1_ v1 và _Doc 2_ v1" hoặc "_Doc 1_ v2 và _Doc 2_ v2," nhưng không bao giờ thấy "_Doc 1_ v1 và _Doc 2_ v2" hoặc "_Doc 1_ v2 và _Doc 2_ v1" cho cùng một thao tác đọc hoặc truy vấn.

### Eventual consistency

In eventual consistency, there's no ordering guarantee for reads. In the absence of any further writes, the replicas eventually converge.
	Trong tính nhất quán cuối cùng, không có sự đảm bảo về thứ tự cho các thao tác đọc. Nếu không có thêm thao tác ghi nào, các bản sao cuối cùng sẽ hội tụ.

Eventual consistency is the weakest form of consistency because a client might read the values that are older than the ones it read before. Eventual consistency is ideal where the application doesn't require any ordering guarantees. Examples include count of Retweets, Likes, or nonthreaded comments
	Tính nhất quán cuối cùng là hình thức nhất quán yếu nhất vì máy khách có thể đọc các giá trị cũ hơn các giá trị mà nó đã đọc trước đó. Tính nhất quán cuối cùng lý tưởng khi ứng dụng không yêu cầu bất kỳ sự đảm bảo nào về thứ tự. Ví dụ bao gồm số lượt Retweet, Like hoặc bình luận không theo luồng.

# Explore supported APIs
___

Azure Cosmos DB offers multiple database APIs, which include NoSQL, MongoDB, PostgreSQL, Cassandra, Gremlin, and Table. By using these APIs, you can model real world data using documents, key-value, graph, and column-family data models. These APIs allow your applications to treat Azure Cosmos DB as if it were various other databases technologies, without the overhead of management, and scaling approaches. Azure Cosmos DB helps you to use the ecosystems, tools, and skills you already have for data modeling and querying with its various APIs.
	Azure Cosmos DB cung cấp nhiều API cơ sở dữ liệu, bao gồm NoSQL, MongoDB, PostgreSQL, Cassandra, Gremlin và Table. Bằng cách sử dụng các API này, bạn có thể mô hình hóa dữ liệu thực tế bằng các mô hình dữ liệu dạng tài liệu, cặp khóa-giá trị, đồ thị và cột. Các API này cho phép ứng dụng của bạn coi Azure Cosmos DB như thể đó là nhiều công nghệ cơ sở dữ liệu khác nhau, mà không cần phải quản lý và mở rộng quy mô phức tạp. Azure Cosmos DB giúp bạn tận dụng hệ sinh thái, công cụ và kỹ năng bạn đã có để mô hình hóa và truy vấn dữ liệu với nhiều API khác nhau.

All the APIs offer automatic scaling of storage and throughput, flexibility, and performance guarantees. There's no one best API, and you can choose any one of the APIs to build your application
	Tất cả các API đều cung cấp khả năng tự động mở rộng dung lượng lưu trữ và thông lượng, tính linh hoạt và đảm bảo hiệu suất. Không có API nào là tốt nhất, và bạn có thể chọn bất kỳ API nào để xây dựng ứng dụng của mình.

## Considerations when choosing an API
	Những điều cần cân nhắc khi chọn API

API for NoSQL is native to Azure Cosmos DB.
	API cho NoSQL là API gốc của Azure Cosmos DB.

API for MongoDB, PostgreSQL, Cassandra, Gremlin, and Table implement the wire protocol of open-source database engines. These APIs are best suited if the following conditions are true:
	API cho MongoDB, PostgreSQL, Cassandra, Gremlin và Table triển khai giao thức truyền tải của các công cụ cơ sở dữ liệu mã nguồn mở. Các API này phù hợp nhất nếu đáp ứng các điều kiện sau:

- If you have existing MongoDB, PostgreSQL, Cassandra, or Gremlin applications
	Nếu bạn đã có sẵn các ứng dụng MongoDB, PostgreSQL, Cassandra hoặc Gremlin
- If you don't want to rewrite your entire data access layer
	Nếu bạn không muốn viết lại toàn bộ lớp truy cập dữ liệu
- If you want to use the open-source developer ecosystem, client-drivers, expertise, and resources for your database
	Nếu bạn muốn sử dụng hệ sinh thái nhà phát triển mã nguồn mở, trình điều khiển phía máy khách, chuyên môn và tài nguyên cho cơ sở dữ liệu của mình

## API for NoSQL

The Azure Cosmos DB API for NoSQL stores data as JSON documents (called items). It offers the best end-to-end experience as we have full control over the interface, service, and the SDK client libraries. Any new feature that is rolled out to Azure Cosmos DB is first available on API for NoSQL accounts. NoSQL accounts provide support for querying items using the Structured Query Language (SQL) syntax.
	API Azure Cosmos DB dành cho NoSQL lưu trữ dữ liệu dưới dạng tài liệu JSON (gọi là các mục). Nó cung cấp trải nghiệm toàn diện tốt nhất vì chúng ta có toàn quyền kiểm soát giao diện, dịch vụ và thư viện máy khách SDK. Bất kỳ tính năng mới nào được triển khai cho Azure Cosmos DB đều được cung cấp đầu tiên trên các tài khoản API dành cho NoSQL. Các tài khoản NoSQL hỗ trợ truy vấn các mục bằng cú pháp Ngôn ngữ truy vấn có cấu trúc (SQL).

## API for MongoDB

The Azure Cosmos DB API for MongoDB stores data in a document structure, via BSON format. It's compatible with MongoDB wire protocol; however, it doesn't use any native MongoDB related code. The API for MongoDB is a great choice if you want to use the broader MongoDB ecosystem and skills, without compromising on using Azure Cosmos DB features.
	API Azure Cosmos DB dành cho MongoDB lưu trữ dữ liệu theo cấu trúc tài liệu, thông qua định dạng BSON. Nó tương thích với giao thức truyền tải của MongoDB; tuy nhiên, nó không sử dụng bất kỳ mã nào liên quan đến MongoDB gốc. API dành cho MongoDB là một lựa chọn tuyệt vời nếu bạn muốn sử dụng hệ sinh thái và kỹ năng rộng lớn hơn của MongoDB, mà không cần phải hy sinh các tính năng của Azure Cosmos DB.
## API for PostgreSQL

Azure Cosmos DB for PostgreSQL is a managed service for running PostgreSQL at any scale, with the [Citus open source](https://github.com/citusdata/citus) superpower of distributed tables. It stores data either on a single node, or distributed in a multi-node configuration.
	Azure Cosmos DB for PostgreSQL là một dịch vụ được quản lý để chạy PostgreSQL ở mọi quy mô, với sức mạnh của các bảng phân tán từ [mã nguồn mở Citus](https://github.com/citusdata/citus). Nó lưu trữ dữ liệu trên một nút duy nhất hoặc phân tán trong cấu hình đa nút.
## API for Apache Cassandra

The Azure Cosmos DB API for Cassandra stores data in column-oriented schema. Apache Cassandra offers a highly distributed, horizontally scaling approach to storing large volumes of data while offering a flexible approach to a column-oriented schema. API for Cassandra in Azure Cosmos DB aligns with this philosophy to approaching distributed NoSQL databases. This API for Cassandra is wire protocol compatible with native Apache Cassandra.
	API Azure Cosmos DB dành cho Cassandra lưu trữ dữ liệu theo lược đồ hướng cột. Apache Cassandra cung cấp phương pháp phân tán cao, có khả năng mở rộng theo chiều ngang để lưu trữ khối lượng dữ liệu lớn, đồng thời cung cấp cách tiếp cận linh hoạt đối với lược đồ hướng cột. API dành cho Cassandra trong Azure Cosmos DB phù hợp với triết lý này trong việc tiếp cận các cơ sở dữ liệu NoSQL phân tán. API dành cho Cassandra này tương thích với giao thức truyền tải gốc của Apache Cassandra.

## API for Apache Gremlin

The Azure Cosmos DB API for Gremlin allows users to make graph queries and stores data as edges and vertices.
	API Azure Cosmos DB dành cho Gremlin cho phép người dùng thực hiện truy vấn đồ thị và lưu trữ dữ liệu dưới dạng cạnh và đỉnh.

Use the API for Gremlin for scenarios:
	Sử dụng API dành cho Gremlin trong các trường hợp:

- Involving dynamic data
	Liên quan đến dữ liệu động
- Involving data with complex relations
	Liên quan đến dữ liệu có mối quan hệ phức tạp
- Involving data that is too complex to be modeled with relational databases
	Liên quan đến dữ liệu quá phức tạp để mô hình hóa bằng cơ sở dữ liệu quan hệ
- If you want to use the existing Gremlin ecosystem and skills
	Nếu bạn muốn sử dụng hệ sinh thái và kỹ năng Gremlin hiện có

## API for Table

The Azure Cosmos DB API for Table stores data in key/value format. If you're currently using Azure Table storage, you might see some limitations in latency, scaling, throughput, global distribution, index management, low query performance. API for Table overcomes these limitations and the recommendation is to migrate your app if you want to use the benefits of Azure Cosmos DB. API for Table only supports OLTP scenarios.
	API for Table của Azure Cosmos DB lưu trữ dữ liệu ở định dạng cặp khóa/giá trị. Nếu hiện tại bạn đang sử dụng Azure Table Storage, bạn có thể gặp một số hạn chế về độ trễ, khả năng mở rộng, thông lượng, phân phối toàn cầu, quản lý chỉ mục và hiệu suất truy vấn thấp. API for Table khắc phục những hạn chế này và chúng tôi khuyến nghị bạn nên chuyển ứng dụng của mình sang API for Table nếu muốn tận dụng những lợi ích của Azure Cosmos DB. API for Table chỉ hỗ trợ các kịch bản OLTP (Giao dịch trực tuyến và ngoại tuyến).

# Discover request units
___

With Azure Cosmos DB, you pay for the throughput you provision and the storage you consume on an hourly basis. Throughput must be provisioned to ensure that sufficient system resources are available for your Azure Cosmos database always.
	Với Azure Cosmos DB, bạn trả tiền dựa trên thông lượng bạn cấp phát và dung lượng lưu trữ bạn sử dụng theo giờ. Thông lượng phải được cấp phát để đảm bảo luôn có đủ tài nguyên hệ thống cho cơ sở dữ liệu Azure Cosmos của bạn.

The cost of all database operations is normalized in Azure Cosmos DB and expressed by _request units_ (or RUs, for short). A request unit represents the system resources such as CPU, IOPS, and memory that are required to perform the database operations supported by Azure Cosmos DB.
	Chi phí của tất cả các thao tác cơ sở dữ liệu được chuẩn hóa trong Azure Cosmos DB và được biểu thị bằng _đơn vị yêu cầu_ (hoặc RU, viết tắt). Một đơn vị yêu cầu đại diện cho các tài nguyên hệ thống như CPU, IOPS và bộ nhớ cần thiết để thực hiện các thao tác cơ sở dữ liệu được Azure Cosmos DB hỗ trợ.

The cost to do a point read, which is fetching a single item by its ID and partition key value, for a 1-KB item is 1RU. All other database operations are similarly assigned a cost using RUs. No matter which API you use to interact with your Azure Cosmos container, costs are measured by RUs. Whether the database operation is a write, point read, or query, costs are measured in RUs.
	Chi phí để thực hiện thao tác đọc điểm, tức là truy xuất một mục duy nhất theo ID và giá trị khóa phân vùng, đối với mục có kích thước 1 KB là 1 RU. Tất cả các thao tác cơ sở dữ liệu khác cũng được gán chi phí tương tự bằng RU. Bất kể bạn sử dụng API nào để tương tác với vùng chứa Azure Cosmos của mình, chi phí đều được đo bằng RU. Cho dù thao tác cơ sở dữ liệu là ghi, đọc điểm hay truy vấn, chi phí đều được đo bằng RU.

The following image shows the high-level idea of RUs:
	Hình ảnh sau đây cho thấy ý tưởng tổng quan về RU.:

![Image showing how database operations consume request units.](https://learn.microsoft.com/en-us/training/wwl-azure/explore-azure-cosmos-db/media/request-units.png)

The type of Azure Cosmos DB account you're using determines the way consumed RUs get charged. There are two modes for account creation:
	Loại tài khoản Azure Cosmos DB bạn đang sử dụng sẽ quyết định cách tính phí cho các đơn vị yêu cầu (RU) đã sử dụng. Có hai chế độ tạo tài khoản:

- **Provisioned throughput mode**: In this mode, you provision the number of RUs for your application on a per-second basis in increments of 100 RUs per second. To scale the provisioned throughput for your application, you can increase or decrease the number of RUs at any time in increments or decrements of 100 RUs. You can make your changes either programmatically or by using the Azure portal. You can provision throughput at container and database granularity level.
    **Chế độ thông lượng được cấp phát**: Ở chế độ này, bạn cấp phát số lượng RU cho ứng dụng của mình theo từng giây, với mức tăng là 100 RU mỗi giây. Để mở rộng thông lượng được cấp phát cho ứng dụng của bạn, bạn có thể tăng hoặc giảm số lượng RU bất cứ lúc nào, với mức tăng hoặc giảm là 100 RU. Bạn có thể thực hiện các thay đổi bằng lập trình hoặc thông qua cổng thông tin Azure. Bạn có thể cấp phát thông lượng ở cấp độ vùng chứa và cơ sở dữ liệu.

- **Serverless mode**: In this mode, you don't have to provision any throughput when creating resources in your Azure Cosmos DB account. At the end of your billing period, you get billed for the number of request units consumed by your database operations.
	**Chế độ không máy chủ**: Ở chế độ này, bạn không cần phải cấp phát bất kỳ thông lượng nào khi tạo tài nguyên trong tài khoản Azure Cosmos DB của mình. Vào cuối kỳ thanh toán, bạn sẽ bị tính phí dựa trên số lượng đơn vị yêu cầu được sử dụng bởi các thao tác cơ sở dữ liệu của bạn.
