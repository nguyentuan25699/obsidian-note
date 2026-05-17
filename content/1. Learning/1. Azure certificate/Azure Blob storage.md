Azure Blob storage is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.
	Azure Blob Storage là giải pháp lưu trữ đối tượng của Microsoft dành cho điện toán đám mây. Blob Storage được tối ưu hóa để lưu trữ lượng lớn dữ liệu phi cấu trúc. Dữ liệu phi cấu trúc là dữ liệu không tuân theo một mô hình hoặc định nghĩa dữ liệu cụ thể nào, chẳng hạn như dữ liệu văn bản hoặc dữ liệu nhị phân.

Blob storage is designed for:
	Blob Storage được thiết kế cho:

- Serving images or documents directly to a browser.
	Cung cấp hình ảnh hoặc tài liệu trực tiếp cho trình duyệt.
- Storing files for distributed access.
	Lưu trữ tệp để truy cập phân tán.
- Streaming video and audio.
	Truy cập video và âm thanh trực tuyến.
- Writing to log files.
	Ghi vào tệp nhật ký.
- Storing data for backup and restore, disaster recovery, and archiving.
	Lưu trữ dữ liệu để sao lưu và khôi phục, phục hồi thảm họa và lưu trữ.
- Storing data for analysis by an on-premises or Azure-hosted service.
	Lưu trữ dữ liệu để phân tích bởi dịch vụ tại chỗ hoặc dịch vụ được lưu trữ trên Azure.

Users or client applications can access objects in Blob storage via HTTP/HTTPS, from anywhere in the world. Objects in Blob storage are accessible via the Azure Storage REST API, Azure PowerShell, Azure CLI, or an Azure Storage client library.
	Người dùng hoặc ứng dụng khách có thể truy cập các đối tượng trong Blob Storage thông qua HTTP/HTTPS, từ bất cứ đâu trên thế giới. Các đối tượng trong Blob Storage có thể truy cập được thông qua API REST của Azure Storage, Azure PowerShell, Azure CLI hoặc thư viện máy khách Azure Storage.

An Azure Storage account is the top-level container for all of your Azure Blob storage. The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the world over HTTP or HTTPS.
	Tài khoản Azure Storage là vùng chứa cấp cao nhất cho tất cả Azure Blob Storage của bạn. Tài khoản lưu trữ cung cấp một không gian tên duy nhất cho dữ liệu Azure Storage của bạn, có thể truy cập được từ bất cứ đâu trên thế giới qua HTTP hoặc HTTPS.

# Types of storage accounts
___
Azure Storage offers two performance levels of storage accounts, standard and premium. Each performance level supports different features and has its own pricing model.
	Azure Storage cung cấp hai cấp độ hiệu năng tài khoản lưu trữ: tiêu chuẩn và cao cấp. Mỗi cấp độ hiệu năng hỗ trợ các tính năng khác nhau và có mô hình giá riêng.

- **Standard:** This is the standard general-purpose v2 account and is recommended for most scenarios using Azure Storage.
	Tiêu chuẩn: Đây là tài khoản v2 đa năng tiêu chuẩn và được khuyến nghị cho hầu hết các trường hợp sử dụng Azure Storage.

- **Premium:** Premium accounts offer higher performance by using solid-state drives. If you create a premium account you can choose between three account types, block blobs, page blobs, or file shares.
	Cao cấp: Tài khoản cao cấp cung cấp hiệu năng cao hơn bằng cách sử dụng ổ đĩa trạng thái rắn (SSD). Nếu bạn tạo tài khoản cao cấp, bạn có thể chọn giữa ba loại tài khoản: khối blob, trang blob hoặc chia sẻ tệp.

The following table describes the types of storage accounts recommended by Microsoft for most scenarios using Blob storage.
	Bảng sau mô tả các loại tài khoản lưu trữ được Microsoft khuyến nghị cho hầu hết các trường hợp sử dụng lưu trữ Blob.

| Type of storage account     | Supported storage services                                                                                                                                                             | Redundancy options                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Usage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Standard general-purpose v2 | Blob Storage (including Data Lake Storage), Queue Storage, Table Storage, and Azure Files<br><br>Blob Storage (bao gồm Data Lake Storage), Queue Storage, Table Storage và Azure Files | Locally redundant storage (LRS) / geo-redundant storage (GRS) / read-access geo-redundant storage (RA-GRS)  <br>  <br>Zone-redundant storage (ZRS) / geo-zone-redundant storage (GZRS) / read-access geo-zone-redundant storage (RA-GZRS)<br><br>Lưu trữ dự phòng cục bộ (LRS) / lưu trữ dự phòng địa lý (GRS) / lưu trữ dự phòng địa lý truy cập đọc (RA-GRS) <br> <br>Lưu trữ dự phòng theo vùng (ZRS) / lưu trữ dự phòng theo vùng địa lý (GZRS) / lưu trữ dự phòng theo vùng địa lý truy cập đọc (RA-GZRS) | Standard storage account type for blobs, file shares, queues, and tables. Recommended for most scenarios using Azure Storage. If you want support for network file system (NFS) in Azure Files, use the premium file shares account type.<br><br>Loại tài khoản lưu trữ tiêu chuẩn dành cho blob, chia sẻ tệp, hàng đợi và bảng. Được khuyến nghị cho hầu hết các trường hợp sử dụng Azure Storage. Nếu bạn muốn hỗ trợ hệ thống tệp mạng (NFS) trong Azure Files, hãy sử dụng loại tài khoản chia sẻ tệp cao cấp. |
| Premium block blobs         | Blob Storage (including Data Lake Storage)<br><br>Lưu trữ Blob (bao gồm cả Lưu trữ Hồ Dữ liệu)                                                                                         | LRS and ZRS                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Premium storage account type for block blobs and append blobs. Recommended for scenarios with high transaction rates or that use smaller objects or require consistently low storage latency.<br><br>Loại tài khoản lưu trữ cao cấp dành cho các khối dữ liệu lớn (block blobs) và các khối dữ liệu được thêm vào (append blobs). Được khuyến nghị cho các trường hợp có tốc độ giao dịch cao, sử dụng các đối tượng nhỏ hơn hoặc yêu cầu độ trễ lưu trữ thấp ổn định.                                             |
| Premium file shares         | Azure Files                                                                                                                                                                            | LRS and ZRS                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Premium storage account type for file shares only. Recommended for enterprise or high-performance scale applications.<br><br>Loại tài khoản lưu trữ cao cấp chỉ dành cho chia sẻ tập tin. Khuyến nghị sử dụng cho các ứng dụng doanh nghiệp hoặc ứng dụng quy mô lớn đòi hỏi hiệu năng cao.                                                                                                                                                                                                                        |
| Premium page blobs          | Page blobs only                                                                                                                                                                        | LRS and ZRS                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Premium storage account type for page blobs only.<br><br>Loại tài khoản lưu trữ cao cấp chỉ dành cho các khối dữ liệu trang (page blobs).                                                                                                                                                                                                                                                                                                                                                                          |

# Access tiers for block blob data
___
Azure Storage provides different options for accessing block blob data based on usage patterns. Each access tier in Azure Storage is optimized for a particular pattern of data usage. By selecting the right access tier for your needs, you can store your block blob data in the most cost-effective manner.
	Azure Storage cung cấp nhiều tùy chọn khác nhau để truy cập dữ liệu khối blob dựa trên mô hình sử dụng. Mỗi cấp độ truy cập trong Azure Storage được tối ưu hóa cho một mô hình sử dụng dữ liệu cụ thể. Bằng cách chọn cấp độ truy cập phù hợp với nhu cầu của mình, bạn có thể lưu trữ dữ liệu khối blob một cách tiết kiệm chi phí nhất.

The available access tiers are:
	Các cấp độ truy cập hiện có là:

- The **Hot** access tier, which is optimized for frequent access of objects in the storage account. The Hot tier has the highest storage costs, but the lowest access costs. New storage accounts are created in the hot tier by default.
    Cấp độ truy cập **Nóng**, được tối ưu hóa cho việc truy cập thường xuyên các đối tượng trong tài khoản lưu trữ. Cấp độ Nóng có chi phí lưu trữ cao nhất, nhưng chi phí truy cập thấp nhất. Các tài khoản lưu trữ mới được tạo ở cấp độ nóng theo mặc định.

- The **Cool** access tier, which is optimized for storing large amounts of data that is infrequently accessed and stored for a minimum of 30 days. The Cool tier has lower storage costs and higher access costs compared to the Hot tier.
    Cấp độ truy cập **Mát**, được tối ưu hóa để lưu trữ lượng lớn dữ liệu ít được truy cập và được lưu trữ tối thiểu 30 ngày. Cấp độ Mát có chi phí lưu trữ thấp hơn và chi phí truy cập cao hơn so với cấp độ Nóng.

- The **Cold** access tier, which is optimized for storing data that is infrequently accessed and stored for a minimum of 90 days. The cold tier has lower storage costs and higher access costs compared to the cool tier.
    Cấp độ truy cập **Lạnh**, được tối ưu hóa để lưu trữ dữ liệu ít được truy cập và được lưu trữ tối thiểu 90 ngày. Cấp độ Lạnh có chi phí lưu trữ thấp hơn và chi phí truy cập cao hơn so với cấp độ Mát.

- The **Archive** tier, which is available only for individual block blobs. The archive tier is optimized for data that can tolerate several hours of retrieval latency and remains in the Archive tier for a minimum 180 days. The archive tier is the most cost-effective option for storing data, but accessing that data is more expensive than accessing data in the hot or cool tiers.
    Tầng **Lưu trữ**, chỉ dành cho các khối dữ liệu riêng lẻ. Tầng lưu trữ được tối ưu hóa cho dữ liệu có thể chịu được độ trễ truy xuất vài giờ và được lưu giữ trong tầng Lưu trữ tối thiểu 180 ngày. Tầng lưu trữ là lựa chọn tiết kiệm chi phí nhất để lưu trữ dữ liệu, nhưng việc truy cập dữ liệu đó sẽ tốn kém hơn so với việc truy cập dữ liệu trong các tầng "nóng" hoặc "lạnh".

If there's a change in the usage pattern of your data, you can switch between these access tiers at any time
	Nếu có sự thay đổi trong mô hình sử dụng dữ liệu của bạn, bạn có thể chuyển đổi giữa các tầng truy cập này bất cứ lúc nào.

# Discover Azure Blob storage resource types
___
Blob storage offers three types of resources:
- The **storage account**.
	Tài khoản lưu trữ.
- A **container** in the storage account
	Một vùng chứa trong tài khoản lưu trữ
- A **blob** in a container
	Một blob trong vùng chứa

# Storage accounts
___
A storage account provides a unique namespace in Azure for your data. Every object that you store in Azure Storage has an address that includes your unique account name. The combination of the account name and the Azure Storage blob endpoint forms the base address for the objects in your storage account.
	Tài khoản lưu trữ cung cấp một không gian tên duy nhất trong Azure cho dữ liệu của bạn. Mỗi đối tượng bạn lưu trữ trong Azure Storage đều có một địa chỉ bao gồm tên tài khoản duy nhất của bạn. Sự kết hợp giữa tên tài khoản và điểm cuối blob của Azure Storage tạo thành địa chỉ cơ sở cho các đối tượng trong tài khoản lưu trữ của bạn.

For example, if your storage account is named _mystorageaccount_, then the default endpoint for Blob storage is:
	Ví dụ: nếu tài khoản lưu trữ của bạn có tên là _mystorageaccount_, thì điểm cuối mặc định cho Blob storage là:

```
http://mystorageaccount.blob.core.windows.net
```

# Containers
___
A container organizes a set of blobs, similar to a directory in a file system. A storage account can include an unlimited number of containers, and a container can store an unlimited number of blobs.
	Một container tổ chức một tập hợp các blob, tương tự như một thư mục trong hệ thống tệp. Một tài khoản lưu trữ có thể bao gồm số lượng container không giới hạn, và một container có thể lưu trữ số lượng blob không giới hạn.

A container name must be a valid DNS name, as it forms part of the unique URI (Uniform resource identifier) used to address the container or its blobs. Follow these rules when naming a container:
	Tên container phải là một tên DNS hợp lệ, vì nó tạo thành một phần của URI (Uniform Resource Identifier) ​​duy nhất được sử dụng để truy cập container hoặc các blob của nó. Hãy tuân theo các quy tắc sau khi đặt tên cho container:

- Container names can be between 3 and 63 characters long.
	Tên container có thể dài từ 3 đến 63 ký tự.
- Container names must start with a letter or number, and can contain only lowercase letters, numbers, and the dash (-) character.
	Tên container phải bắt đầu bằng một chữ cái hoặc số, và chỉ có thể chứa các chữ cái viết thường, số và ký tự gạch ngang (-).
- Two or more consecutive dash characters aren't permitted in container names.
	Không được phép có hai hoặc nhiều ký tự gạch ngang liên tiếp trong tên container.

The URI for a container is similar to:
```
https://myaccount.blob.core.windows.net/mycontainer
```

# Blobs
___
Azure Storage supports three types of blobs:
	Azure Storage hỗ trợ ba loại blob:

- **Block blobs** store text and binary data. Block blobs are made up of blocks of data that can be managed individually. Block blobs can store up to about 190.7 TiB.
	**Blob khối** lưu trữ dữ liệu văn bản và nhị phân. Blob khối được tạo thành từ các khối dữ liệu có thể được quản lý riêng lẻ. Blob khối có thể lưu trữ tối đa khoảng 190,7 TiB.
- **Append blobs** are made up of blocks like block blobs, but are optimized for append operations. Append blobs are ideal for scenarios such as logging data from virtual machines.
	**Blob nối** được tạo thành từ các khối tương tự như blob khối, nhưng được tối ưu hóa cho các thao tác nối thêm. Blob nối lý tưởng cho các trường hợp như ghi nhật ký dữ liệu từ máy ảo.
- **Page blobs** store random access files up to 8 TB in size. Page blobs store virtual hard drive (VHD) files and serve as disks for Azure virtual machines.
	**Blob trang** lưu trữ các tệp truy cập ngẫu nhiên có kích thước lên đến 8 TB. Blob trang lưu trữ các tệp ổ cứng ảo (VHD) và đóng vai trò là đĩa cho các máy ảo Azure.

The URI for a blob is similar to:

```
https://myaccount.blob.core.windows.net/mycontainer/myblob
```

or

```
https://myaccount.blob.core.windows.net/mycontainer/myvirtualdirectory/myblob
```

# Explore Azure Storage security features
___
Azure Storage uses service-side encryption (SSE) to automatically encrypt your data when it's persisted to the cloud. Azure Storage encryption protects your data and to help you to meet your organizational security and compliance commitments.
	Azure Storage sử dụng mã hóa phía máy chủ (SSE) để tự động mã hóa dữ liệu của bạn khi dữ liệu được lưu trữ trên đám mây. Mã hóa của Azure Storage bảo vệ dữ liệu của bạn và giúp bạn đáp ứng các cam kết về bảo mật và tuân thủ của tổ chức.

Microsoft recommends using service-side encryption to protect your data for most scenarios. However, the Azure Storage client libraries for Blob Storage and Queue Storage also provide client-side encryption for customers who need to encrypt data on the client.
	Microsoft khuyến nghị sử dụng mã hóa phía máy chủ để bảo vệ dữ liệu của bạn trong hầu hết các trường hợp. Tuy nhiên, thư viện máy khách Azure Storage dành cho Blob Storage và Queue Storage cũng cung cấp mã hóa phía máy khách cho những khách hàng cần mã hóa dữ liệu ở phía máy khách.

# Azure Storage encryption for data at rest
___
Azure Storage automatically encrypts your data when persisting it to the cloud. Encryption protects your data and helps you meet your organizational security and compliance commitments. Data in Azure Storage is encrypted and decrypted transparently using 256-bit Advanced Encryption Standard (AES) encryption, one of the strongest block ciphers available, and is Federal Information Processing Standards (FIPS) 140-2 compliant. Azure Storage encryption is similar to BitLocker encryption on Windows.
	Azure Storage tự động mã hóa dữ liệu của bạn khi lưu trữ lên đám mây. Mã hóa bảo vệ dữ liệu của bạn và giúp bạn đáp ứng các cam kết về bảo mật và tuân thủ của tổ chức. Dữ liệu trong Azure Storage được mã hóa và giải mã một cách minh bạch bằng cách sử dụng mã hóa Chuẩn Mã hóa Nâng cao (AES) 256 bit, một trong những thuật toán mã hóa khối mạnh nhất hiện có và tuân thủ Tiêu chuẩn Xử lý Thông tin Liên bang (FIPS) 140-2. Mã hóa Azure Storage tương tự như mã hóa BitLocker trên Windows.

Azure Storage encryption is enabled for all storage accounts and can't be disabled. Because your data is secured by default, you don't need to modify your code or applications to take advantage of Azure Storage encryption.
	Mã hóa Azure Storage được bật cho tất cả các tài khoản lưu trữ và không thể tắt. Vì dữ liệu của bạn được bảo mật theo mặc định, bạn không cần sửa đổi mã hoặc ứng dụng của mình để tận dụng tính năng mã hóa Azure Storage.

Data in a storage account is encrypted regardless of performance tier, access tier, or deployment model. All new and existing block blobs, append blobs, and page blobs are encrypted, including blobs in the archive tier. All Azure Storage redundancy options support encryption, and all data in both the primary and secondary regions is encrypted when geo-replication is enabled. All Azure Storage resources are encrypted, including blobs, disks, files, queues, and tables. All object metadata is also encrypted.
	Dữ liệu trong tài khoản lưu trữ được mã hóa bất kể cấp hiệu năng, cấp truy cập hay mô hình triển khai. Tất cả các blob khối, blob nối thêm và blob trang mới và hiện có đều được mã hóa, bao gồm cả các blob trong cấp lưu trữ. Tất cả các tùy chọn dự phòng Azure Storage đều hỗ trợ mã hóa và tất cả dữ liệu trong cả vùng chính và vùng phụ đều được mã hóa khi bật sao chép địa lý. Tất cả tài nguyên Azure Storage đều được mã hóa, bao gồm blob, đĩa, tập tin, hàng đợi và bảng. Tất cả siêu dữ liệu đối tượng cũng được mã hóa.

There's no extra cost for Azure Storage encryption.
	Không có chi phí bổ sung nào cho việc mã hóa Azure Storage.


# Encryption key management
___
Data in a new storage account is encrypted with Microsoft-managed keys by default. You can continue to rely on Microsoft-managed keys for the encryption of your data, or you can manage encryption with your own keys. If you choose to manage encryption with your own keys, you have two options. You can use either type of key management, or both:
	Dữ liệu trong tài khoản lưu trữ mới được mã hóa bằng khóa do Microsoft quản lý theo mặc định. Bạn có thể tiếp tục dựa vào khóa do Microsoft quản lý để mã hóa dữ liệu của mình hoặc bạn có thể tự quản lý mã hóa bằng khóa riêng. Nếu bạn chọn tự quản lý mã hóa bằng khóa riêng, bạn có hai tùy chọn. Bạn có thể sử dụng một trong hai loại quản lý khóa hoặc cả hai:

- You can specify a _customer-managed key_ to use for encrypting and decrypting data in Blob Storage and in Azure Files.Customer-managed keys must be stored in Azure Key Vault or Azure Key Vault Managed Hardware Security Model (HSM).
	Bạn có thể chỉ định một _khóa do khách hàng quản lý_ để sử dụng cho việc mã hóa và giải mã dữ liệu trong Blob Storage và Azure Files. Khóa do khách hàng quản lý phải được lưu trữ trong Azure Key Vault hoặc Azure Key Vault Managed Hardware Security Model (HSM).

- You can specify a _customer-provided key_ on Blob Storage operations. A client can include an encryption key on a read/write request for granular control over how blob data is encrypted and decrypted.
    Bạn có thể chỉ định một _khóa do khách hàng cung cấp_ trong các thao tác Blob Storage. Khách hàng có thể bao gồm khóa mã hóa trong yêu cầu đọc/ghi để kiểm soát chi tiết hơn về cách dữ liệu blob được mã hóa và giải mã.

The following table compares key management options for Azure Storage encryption.
	Bảng sau so sánh các tùy chọn quản lý khóa cho mã hóa Azure Storage.

| Key management parameter         | Microsoft-managed keys                | Customer-managed keys                 | Customer-provided keys   |
| -------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------ |
| Encryption/decryption operations | Azure                                 | Azure                                 | Azure                    |
| Azure Storage services supported | All                                   | Blob Storage, Azure Files             | Blob Storage             |
| Key storage                      | Microsoft key store                   | Azure Key Vault or Key Vault HSM      | Customer's own key store |
| Key rotation responsibility      | Microsoft                             | Customer                              | Customer                 |
| Key control                      | Microsoft                             | Customer                              | Customer                 |
| Key scope                        | Account (default), container, or blob | Account (default), container, or blob | N/A                      |

# Client-side encryption
___
The Azure Blob Storage client libraries for .NET, Java, and Python support encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client. The Queue Storage client libraries for .NET and Python also support client-side encryption.
	Các thư viện máy khách Azure Blob Storage dành cho .NET, Java và Python hỗ trợ mã hóa dữ liệu trong các ứng dụng máy khách trước khi tải lên Azure Storage và giải mã dữ liệu trong khi tải xuống máy khách. Các thư viện máy khách Queue Storage dành cho .NET và Python cũng hỗ trợ mã hóa phía máy khách.

The Blob Storage and Queue Storage client libraries uses AES in order to encrypt user data. There are two versions of client-side encryption available in the client libraries:
	Các thư viện máy khách Blob Storage và Queue Storage sử dụng AES để mã hóa dữ liệu người dùng. Có hai phiên bản mã hóa phía máy khách có sẵn trong các thư viện máy khách:

- Version 2 uses Galois/Counter Mode (GCM) mode with AES. The Blob Storage and Queue Storage SDKs support client-side encryption with v2.
	Phiên bản 2 sử dụng chế độ Galois/Counter Mode (GCM) với AES. SDK Blob Storage và Queue Storage hỗ trợ mã hóa phía máy khách với phiên bản 2.
- Version 1 uses Cipher Block Chaining (CBC) mode with AES. The Blob Storage, Queue Storage, and Table Storage SDKs support client-side encryption with v1.
	- Phiên bản 1 sử dụng chế độ Cipher Block Chaining (CBC) với AES. SDK Blob Storage, Queue Storage và Table Storage hỗ trợ mã hóa phía máy khách với phiên bản 1.


# **Recap nhanh Blob Storage (để nhớ lâu)**
---
## **Blob types**

| **Type**    | **Use**                 |
| ----------- | ----------------------- |
| Block Blob  | images / videos / files |
| Append Blob | logs                    |
| Page Blob   | VM disks                |
## **Access tiers**

| **Tier** | **Scenario**                     |
| -------- | -------------------------------- |
| Hot      | frequently accessed              |
| Cool     | infrequently accessed but online |
| Archive  | long-term storage                |
## **SAS token**
Use when:
```
temporary access to blob
external access
limited permission
```

## **Lifecycle policy**
Use when:
```
move data to cheaper tier
delete old data
automate storage management
```