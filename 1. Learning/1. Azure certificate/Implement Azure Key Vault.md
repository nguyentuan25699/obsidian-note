Azure Key Vault is a cloud service for securely storing and accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, certificates, or cryptographic keys.
	Azure Key Vault là một dịch vụ đám mây để lưu trữ và truy cập các bí mật một cách an toàn. Bí mật là bất cứ thứ gì bạn muốn kiểm soát chặt chẽ quyền truy cập, chẳng hạn như khóa API, mật khẩu, chứng chỉ hoặc khóa mã hóa.

# Explore Azure Key Vault
___
The Azure Key Vault service supports two types of containers: vaults and managed hardware security module(HSM) pools. Vaults support storing software and HSM-backed keys, secrets, and certificates. Managed HSM pools only support HSM-backed keys.
	Dịch vụ Azure Key Vault hỗ trợ hai loại vùng chứa: kho lưu trữ (vault) và nhóm mô-đun bảo mật phần cứng (HSM) được quản lý. Kho lưu trữ hỗ trợ lưu trữ các khóa, bí mật và chứng chỉ được hỗ trợ bởi phần mềm và HSM. Nhóm HSM được quản lý chỉ hỗ trợ các khóa được hỗ trợ bởi HSM.

Azure Key Vault helps solve the following problems:
	Azure Key Vault giúp giải quyết các vấn đề sau:

- **Secrets Management:** Azure Key Vault can be used to Securely store and tightly control access to tokens, passwords, certificates, API keys, and other secrets
    **Quản lý bí mật:** Azure Key Vault có thể được sử dụng để lưu trữ an toàn và kiểm soát chặt chẽ quyền truy cập vào mã thông báo, mật khẩu, chứng chỉ, khóa API và các bí mật khác.
- **Key Management:** Azure Key Vault can also be used as a Key Management solution. Azure Key Vault makes it easy to create and control the encryption keys used to encrypt your data.
    **Quản lý khóa:** Azure Key Vault cũng có thể được sử dụng như một giải pháp quản lý khóa. Azure Key Vault giúp dễ dàng tạo và kiểm soát các khóa mã hóa được sử dụng để mã hóa dữ liệu của bạn.
- **Certificate Management:** Azure Key Vault is also a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with Azure and your internal connected resources.
    **Quản lý chứng chỉ:** Azure Key Vault cũng là một dịch vụ cho phép bạn dễ dàng cung cấp, quản lý và triển khai các chứng chỉ SSL/TLS công khai và riêng tư để sử dụng với Azure và các tài nguyên được kết nối nội bộ của bạn.

Azure Key Vault has two service tiers: Standard, which encrypts with a software key, and a Premium tier, which includes hardware security module(HSM)-protected keys. To see a comparison between the Standard and Premium tiers, see the [Azure Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).
	Azure Key Vault có hai cấp dịch vụ: Standard, mã hóa bằng khóa phần mềm, và cấp Premium, bao gồm các khóa được bảo vệ bằng mô-đun bảo mật phần cứng (HSM). Để xem so sánh giữa cấp Standard và Premium, hãy xem trang giá Azure Key Vault tại [https://azure.microsoft.com/pricing/details/key-vault/].

## Key benefits of using Azure Key Vault

- **Centralized application secrets:** Centralizing storage of application secrets in Azure Key Vault allows you to control their distribution. For example, instead of storing the connection string in the app's code you can store it securely in Key Vault. Your applications can securely access the information they need by using URIs. These URIs allow the applications to retrieve specific versions of a secret.
    **Lưu trữ bí mật ứng dụng tập trung:** Việc lưu trữ tập trung các bí mật ứng dụng trong Azure Key Vault cho phép bạn kiểm soát việc phân phối chúng. Ví dụ, thay vì lưu trữ chuỗi kết nối trong mã ứng dụng, bạn có thể lưu trữ nó một cách an toàn trong Key Vault. Các ứng dụng của bạn có thể truy cập thông tin cần thiết một cách an toàn bằng cách sử dụng URI. Các URI này cho phép các ứng dụng truy xuất các phiên bản cụ thể của một bí mật.

- **Securely store secrets and keys:** Access to a key vault requires proper authentication and authorization before a caller (user or application) can get access. Authentication is done via Microsoft Entra ID. Authorization might be done via Azure role-based access control (Azure RBAC) or Key Vault access policy. Azure RBAC can be used for both management of the vaults, and to access data stored in a vault. A key vault access policy can only be used when attempting to access data stored in a vault. Azure Key Vaults might be either software-protected or, with the Azure Key Vault Premium tier, hardware-protected by hardware security modules (HSMs).
    **Lưu trữ bí mật và khóa một cách an toàn:** Việc truy cập vào kho khóa yêu cầu xác thực và ủy quyền thích hợp trước khi người gọi (người dùng hoặc ứng dụng) có thể truy cập. Việc xác thực được thực hiện thông qua Microsoft Entra ID. Việc ủy ​​quyền có thể được thực hiện thông qua kiểm soát truy cập dựa trên vai trò của Azure (Azure RBAC) hoặc chính sách truy cập Key Vault. Azure RBAC có thể được sử dụng cho cả việc quản lý các kho lưu trữ và truy cập dữ liệu được lưu trữ trong kho lưu trữ. Chính sách truy cập Key Vault chỉ có thể được sử dụng khi cố gắng truy cập dữ liệu được lưu trữ trong kho lưu trữ. Azure Key Vault có thể được bảo vệ bằng phần mềm hoặc, với gói Azure Key Vault Premium, được bảo vệ bằng phần cứng bởi các mô-đun bảo mật phần cứng (HSM).

- **Monitor access and use:** You can monitor activity by enabling logging for your vaults. You have control over your logs and you might secure them by restricting access and you might also delete logs that you no longer need. Azure Key Vault diagnostic logs and metrics can be configured to:
    **Giám sát quyền truy cập và sử dụng:** Bạn có thể giám sát hoạt động bằng cách bật tính năng ghi nhật ký cho các kho lưu trữ của mình. Bạn có quyền kiểm soát nhật ký của mình và bạn có thể bảo mật chúng bằng cách hạn chế quyền truy cập và bạn cũng có thể xóa các nhật ký mà bạn không còn cần nữa. Nhật ký chẩn đoán và số liệu của Azure Key Vault có thể được cấu hình để:

    - Archive to a storage account.
	    Lưu trữ vào tài khoản lưu trữ.
    - Stream to an event hub.
	    Truyền phát đến trung tâm sự kiện.
    - Send the logs to Azure Monitor logs.
	    Gửi nhật ký đến nhật ký Azure Monitor.
- **Simplified administration of application secrets:** Security information must be secured, it must follow a life cycle, and it must be highly available. Azure Key Vault simplifies the process of meeting these requirements by:
	**Đơn giản hóa việc quản trị bí mật ứng dụng:** Thông tin bảo mật phải được bảo mật, phải tuân theo vòng đời và phải có tính khả dụng cao. Azure Key Vault đơn giản hóa quá trình đáp ứng các yêu cầu này bằng cách:

    - Removing the need for in-house knowledge of Hardware Security Modules
	    Loại bỏ nhu cầu về kiến ​​thức nội bộ về Mô-đun Bảo mật Phần cứng
    - Scaling up on short notice to meet your organization’s usage spikes.
		Mở rộng quy mô nhanh chóng để đáp ứng nhu cầu sử dụng tăng đột biến của tổ chức.
    - Replicating the contents of your Key Vault within a region and to a secondary region. Data replication ensures high availability and takes away the need of any action from the administrator to trigger the failover.
	    Sao chép nội dung Key Vault của bạn trong cùng một khu vực và sang khu vực thứ cấp. Sao chép dữ liệu đảm bảo tính khả dụng cao và loại bỏ nhu cầu thực hiện bất kỳ thao tác nào từ quản trị viên để kích hoạt chuyển đổi dự phòng.
    - Providing standard Azure administration options via the portal, Azure CLI and PowerShell.
	    Cung cấp các tùy chọn quản trị Azure tiêu chuẩn thông qua cổng thông tin, Azure CLI và PowerShell.
    - Automating certain tasks on certificates that you purchase from Public CAs, such as enrollment and renewal.
	    Tự động hóa một số tác vụ trên chứng chỉ mà bạn mua từ các CA công cộng, chẳng hạn như đăng ký và gia hạn.

# Discover Azure Key Vault best practices
___

Azure Key Vault is a tool for securely storing and accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, or certificates. A vault is logical group of secrets.
	Azure Key Vault là một công cụ để lưu trữ và truy cập các bí mật một cách an toàn. Bí mật là bất cứ thứ gì bạn muốn kiểm soát chặt chẽ quyền truy cập, chẳng hạn như khóa API, mật khẩu hoặc chứng chỉ. Một vault là một nhóm bí mật logic.

## Authentication

To do any operations with Key Vault, you first need to authenticate to it. There are three ways to authenticate to Key Vault:
	Để thực hiện bất kỳ thao tác nào với Key Vault, trước tiên bạn cần phải xác thực với nó. Có ba cách để xác thực với Key Vault:

- **Managed identities for Azure resources**: When you deploy an app on a virtual machine in Azure, you can assign an identity to your virtual machine that has access to Key Vault. You can also assign identities to other Azure resources. The benefit of this approach is that the app or service isn't managing the rotation of the first secret. Azure automatically rotates the service principal client secret associated with the identity. We recommend this approach as a best practice.
    **Danh tính được quản lý cho tài nguyên Azure**: Khi bạn triển khai một ứng dụng trên máy ảo trong Azure, bạn có thể gán một danh tính cho máy ảo của mình để có quyền truy cập vào Key Vault. Bạn cũng có thể gán danh tính cho các tài nguyên Azure khác. Lợi ích của phương pháp này là ứng dụng hoặc dịch vụ không phải quản lý việc xoay vòng bí mật đầu tiên. Azure tự động xoay vòng bí mật máy khách của principal dịch vụ được liên kết với danh tính. Chúng tôi khuyến nghị phương pháp này như một thực tiễn tốt nhất.

- **Service principal and certificate**: You can use a service principal and an associated certificate that has access to Key Vault. We don't recommend this approach because the application owner or developer must rotate the certificate.
    **Principal dịch vụ và chứng chỉ**: Bạn có thể sử dụng một principal dịch vụ và một chứng chỉ được liên kết để có quyền truy cập vào Key Vault. Chúng tôi không khuyến nghị phương pháp này vì chủ sở hữu hoặc nhà phát triển ứng dụng phải xoay vòng chứng chỉ.
- **Service principal and secret**: Although you can use a service principal and a secret to authenticate to Key Vault, we don't recommend it. It's hard to automatically rotate the bootstrap secret that's used to authenticate to Key Vault.
    **Tên người dùng dịch vụ và mã bí mật**: Mặc dù bạn có thể sử dụng tên người dùng dịch vụ và mã bí mật để xác thực với Key Vault, nhưng chúng tôi không khuyến nghị điều này. Việc tự động xoay vòng mã bí mật khởi tạo được sử dụng để xác thực với Key Vault rất khó khăn.

## Encryption of data in transit
	Mã hóa dữ liệu khi truyền tải

Azure Key Vault enforces Transport Layer Security (TLS) protocol to protect data when it’s traveling between Azure Key Vault and clients. Clients negotiate a TLS connection with Azure Key Vault. TLS provides strong authentication, message privacy, and integrity (enabling detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, and ease of deployment and use.
	Azure Key Vault thực thi giao thức Bảo mật Lớp Vận chuyển (TLS) để bảo vệ dữ liệu khi dữ liệu được truyền giữa Azure Key Vault và máy khách. Máy khách thiết lập kết nối TLS với Azure Key Vault. TLS cung cấp xác thực mạnh mẽ, bảo mật thông điệp và tính toàn vẹn (cho phép phát hiện việc giả mạo, chặn và làm sai lệch thông điệp), khả năng tương tác, tính linh hoạt của thuật toán và dễ dàng triển khai và sử dụng.

Perfect Forward Secrecy (PFS) protects connections between customers’ client systems and Microsoft cloud services by unique keys. Connections also use RSA-based 2,048-bit encryption key lengths. This combination makes it difficult for someone to intercept and access data that is in transit.
	Bảo mật Chuyển tiếp Hoàn hảo (PFS) bảo vệ các kết nối giữa hệ thống máy khách của khách hàng và các dịch vụ đám mây của Microsoft bằng các khóa duy nhất. Các kết nối cũng sử dụng độ dài khóa mã hóa 2048 bit dựa trên RSA. Sự kết hợp này khiến việc chặn và truy cập dữ liệu đang được truyền tải trở nên khó khăn.

## Azure Key Vault best practices

- **Use separate key vaults:** Recommended using a vault per application per environment (Development, Pre-Production and Production). This pattern helps you not share secrets across environments and also reduces the threat if there is a breach.
    **Sử dụng các kho khóa riêng biệt:** Nên sử dụng một kho khóa cho mỗi ứng dụng trong mỗi môi trường (Phát triển, Tiền sản xuất và Sản xuất). Mô hình này giúp bạn không chia sẻ bí mật giữa các môi trường và cũng giảm thiểu nguy cơ bị xâm phạm.

- **Control access to your vault:** Key Vault data is sensitive and business critical, you need to secure access to your key vaults by allowing only authorized applications and users.
    **Kiểm soát quyền truy cập vào kho khóa của bạn:** Dữ liệu trong Key Vault rất nhạy cảm và quan trọng đối với hoạt động kinh doanh, bạn cần bảo mật quyền truy cập vào kho khóa của mình bằng cách chỉ cho phép các ứng dụng và người dùng được ủy quyền.

- **Backup:** Create regular back ups of your vault on update/delete/create of objects within a Vault.
    **Sao lưu:** Tạo bản sao lưu thường xuyên cho kho khóa của bạn khi cập nhật/xóa/tạo mới các đối tượng trong kho khóa.
- **Logging:** Be sure to turn on logging and alerts.
    **Ghi nhật ký:** Đảm bảo bật tính năng ghi nhật ký và cảnh báo.
- **Recovery options:** Turn on [soft-delete](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) and purge protection if you want to guard against force deletion of the secret.
	**Các tùy chọn khôi phục:** Bật [xóa mềm](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) và bảo vệ xóa vĩnh viễn nếu bạn muốn bảo vệ chống lại việc xóa bắt buộc bí mật.

# Authenticate to Azure Key Vault
___
Authentication with Key Vault works with Microsoft Entra ID, which is responsible for authenticating the identity of any given security principal. A security principal is anything that can request access to Azure resources. This includes:
	Xác thực bằng Key Vault hoạt động với Microsoft Entra ID, chịu trách nhiệm xác thực danh tính của bất kỳ đối tượng bảo mật nào. Đối tượng bảo mật là bất kỳ thứ gì có thể yêu cầu quyền truy cập vào tài nguyên Azure. Điều này bao gồm:

- Users – Real people with accounts in Microsoft Entra ID.
	Người dùng – Những người thật có tài khoản trong Microsoft Entra ID.
- Groups – Collections of users. Permissions given to the group apply to all its members.
	Nhóm – Tập hợp người dùng. Quyền được cấp cho nhóm áp dụng cho tất cả các thành viên của nhóm.
- Service Principals – Represent apps or services (not people). Think of it like a user account for an app.
	Đối tượng dịch vụ – Đại diện cho các ứng dụng hoặc dịch vụ (không phải người). Hãy nghĩ về nó như một tài khoản người dùng cho một ứng dụng.

For applications, there are two main ways to obtain a service principal:
	Đối với các ứng dụng, có hai cách chính để có được đối tượng dịch vụ:

- Use a managed identity (recommended): Azure creates and manages the service principal for you. The app can securely access other Azure services without storing credentials. Works with services like App Service, Azure Functions, and Virtual Machines.
    Sử dụng danh tính được quản lý (được khuyến nghị): Azure tạo và quản lý đối tượng dịch vụ cho bạn. Ứng dụng có thể truy cập an toàn vào các dịch vụ Azure khác mà không cần lưu trữ thông tin xác thực. Hoạt động với các dịch vụ như App Service, Azure Functions và Máy ảo.

- Register the app manually: You register the app in Microsoft Entra ID. This creates a service principal and an app object that identifies the app across all tenants.
	Đăng ký ứng dụng theo cách thủ công: Bạn đăng ký ứng dụng trong Microsoft Entra ID. Điều này tạo ra một đối tượng dịch vụ và một đối tượng ứng dụng xác định ứng dụng trên tất cả các tenant.
## Authentication to Key Vault in application code

Key Vault SDK is using Azure Identity client library, which allows seamless authentication to Key Vault across environments with same code. The following table provides information on the Azure Identity client libraries:
	Key Vault SDK sử dụng thư viện máy khách Azure Identity, cho phép xác thực liền mạch với Key Vault trên các môi trường khác nhau bằng cùng một mã. Bảng sau cung cấp thông tin về các thư viện máy khách Azure Identity:

|.NET|Python|Java|JavaScript|
|---|---|---|---|
|[Azure Identity SDK .NET](https://learn.microsoft.com/en-us/dotnet/api/overview/azure/identity-readme)|[Azure Identity SDK Python](https://learn.microsoft.com/en-us/python/api/overview/azure/identity-readme)|[Azure Identity SDK Java](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)|[Azure Identity SDK JavaScript](https://learn.microsoft.com/en-us/javascript/api/overview/azure/identity-readme)|

## Authentication to Key Vault with REST

Access tokens must be sent to the service using the HTTP Authorization header:
	Mã thông báo truy cập phải được gửi đến dịch vụ bằng cách sử dụng tiêu đề HTTP Authorization:

HTTP
```
PUT /keys/MYKEY?api-version=<api_version>  HTTP/1.1  
Authorization: Bearer <access_token>
```

When an access token isn't supplied, or when the service rejects a token, an `HTTP 401` error is returned to the client and includes the `WWW-Authenticate` header, for example:
	Khi không cung cấp mã thông báo truy cập, hoặc khi dịch vụ từ chối mã thông báo, lỗi `HTTP 401` sẽ được trả về cho máy khách và bao gồm tiêu đề `WWW-Authenticate`, ví dụ:

HTTP
```
401 Not Authorized  
WWW-Authenticate: Bearer authorization="…", resource="…"
```

The parameters on the `WWW-Authenticate` header are:
	Các tham số trên tiêu đề `WWW-Authenticate` là:

- authorization: The address of the OAuth2 authorization service that might be used to obtain an access token for the request.
	authorization: Địa chỉ của dịch vụ ủy quyền OAuth2 có thể được sử dụng để lấy mã thông báo truy cập cho yêu cầu.

- resource: The name of the resource (`https://vault.azure.net`) to use in the authorization request.
    resource: Tên của tài nguyên (`https://vault.azure.net`) sẽ được sử dụng trong yêu cầu ủy quyền.

## Other resources

- [Azure Key Vault developer's guide](https://learn.microsoft.com/en-us/azure/key-vault/general/developers-guide)
- [Azure Key Vault availability and redundancy](https://learn.microsoft.com/en-us/azure/key-vault/general/disaster-recovery-guidance)