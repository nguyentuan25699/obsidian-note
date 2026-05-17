AI applications require secure, centralized credential management to protect API keys, connection strings, and encryption keys across development, staging, and production environments. This module guides you through using Azure Key Vault to store, retrieve, and manage secrets in AI solutions on Azure.
	Các ứng dụng AI yêu cầu quản lý thông tin xác thực tập trung, an toàn để bảo vệ khóa API, chuỗi kết nối và khóa mã hóa trên các môi trường phát triển, thử nghiệm và sản xuất. Mô-đun này hướng dẫn bạn cách sử dụng Azure Key Vault để lưu trữ, truy xuất và quản lý các bí mật trong các giải pháp AI trên Azure.

Imagine you're a developer building a RAG pipeline that connects to multiple backend services. The pipeline calls an Azure OpenAI endpoint for embeddings generation, reads from an Azure Cosmos DB vector store, and writes processed results to Azure Blob Storage. Each service requires its own credentials, and those credentials differ across development, staging, and production environments. Today, the team stores connection strings in environment variables and configuration files checked into source control. A recent security audit flagged this practice as a risk because credentials are visible to anyone with repository access, and rotating a compromised key requires redeploying every service that uses it. The client expects credential rotation within four hours of a suspected compromise, with zero downtime during the rotation window. Your team needs a centralized secrets store that controls access through identity-based permissions, tracks every secret access in audit logs, and supports versioned secrets so applications can transition to new credentials without interruption. Caching secrets locally also matters because the pipeline processes thousands of documents per hour, and calling a remote vault for every operation adds unacceptable latency. Azure Key Vault provides the secure storage, versioning, rotation support, and SDK integration that this architecture requires.
	Hãy tưởng tượng bạn là một nhà phát triển đang xây dựng một pipeline RAG kết nối với nhiều dịch vụ phụ trợ. Pipeline gọi một điểm cuối Azure OpenAI để tạo embedding, đọc từ kho lưu trữ vector Azure Cosmos DB và ghi kết quả đã xử lý vào Azure Blob Storage. Mỗi dịch vụ yêu cầu thông tin xác thực riêng và các thông tin xác thực này khác nhau giữa các môi trường phát triển, thử nghiệm và sản xuất. Hiện tại, nhóm đang lưu trữ chuỗi kết nối trong các biến môi trường và tệp cấu hình được kiểm tra trong hệ thống kiểm soát nguồn. Một cuộc kiểm toán bảo mật gần đây đã chỉ ra thực tiễn này là một rủi ro vì thông tin xác thực có thể bị lộ cho bất kỳ ai có quyền truy cập kho lưu trữ và việc xoay vòng khóa bị xâm phạm yêu cầu phải triển khai lại mọi dịch vụ sử dụng nó. Khách hàng mong muốn việc xoay vòng thông tin xác thực trong vòng bốn giờ kể từ khi nghi ngờ bị xâm phạm, với thời gian ngừng hoạt động bằng không trong suốt quá trình xoay vòng. Nhóm của bạn cần một kho lưu trữ bí mật tập trung, kiểm soát quyền truy cập thông qua quyền dựa trên danh tính, theo dõi mọi truy cập bí mật trong nhật ký kiểm toán và hỗ trợ bí mật có phiên bản để các ứng dụng có thể chuyển sang thông tin xác thực mới mà không bị gián đoạn. Việc lưu trữ bí mật cục bộ cũng rất quan trọng vì quy trình xử lý hàng nghìn tài liệu mỗi giờ, và việc gọi đến kho lưu trữ từ xa cho mỗi thao tác sẽ làm tăng độ trễ không thể chấp nhận được. Azure Key Vault cung cấp khả năng lưu trữ an toàn, quản lý phiên bản, hỗ trợ xoay vòng và tích hợp SDK mà kiến ​​trúc này yêu cầu.

After completing this module, you'll be able to:
	Sau khi hoàn thành mô-đun này, bạn sẽ có thể:

- Explain how Azure Key Vault stores and organizes secrets, keys, and certificates, and identify when to use each object type in an AI solution.
	Giải thích cách Azure Key Vault lưu trữ và sắp xếp các bí mật, khóa và chứng chỉ, và xác định khi nào nên sử dụng từng loại đối tượng trong giải pháp AI.
- Retrieve secrets programmatically using Azure SDK client libraries with managed identity authentication.
	Truy xuất bí mật theo chương trình bằng cách sử dụng thư viện máy khách Azure SDK với xác thực danh tính được quản lý.
- Handle secret versioning and rotation in application code to support zero-downtime credential updates.
	Xử lý việc quản lý phiên bản và xoay vòng bí mật trong mã ứng dụng để hỗ trợ cập nhật thông tin xác thực không gây gián đoạn.
- Implement caching strategies that reduce Key Vault API calls while maintaining security and freshness guarantees.
	Triển khai các chiến lược lưu trữ giúp giảm số lượng cuộc gọi API Key Vault trong khi vẫn duy trì bảo mật và đảm bảo tính mới.

# Store and organize secrets, keys, and certificates
___
Azure Key Vault is a cloud-hosted service that provides centralized storage and management for sensitive data such as API keys, connection strings, encryption keys, and TLS certificates. AI solutions on Azure handle credentials across every layer of their architecture. A RAG pipeline, for example, might store an Azure OpenAI API key, a Cosmos DB connection string, a storage account key, and a TLS certificate for its public endpoint. Azure Key Vault gives developers a single, secure location to store all of these credentials and retrieve them at runtime through SDK calls, without embedding secrets in application code or configuration files.
	Azure Key Vault là một dịch vụ được lưu trữ trên đám mây, cung cấp khả năng lưu trữ và quản lý tập trung cho các dữ liệu nhạy cảm như khóa API, chuỗi kết nối, khóa mã hóa và chứng chỉ TLS. Các giải pháp AI trên Azure xử lý thông tin xác thực trên mọi lớp kiến ​​trúc của chúng. Ví dụ, một pipeline RAG có thể lưu trữ khóa API Azure OpenAI, chuỗi kết nối Cosmos DB, khóa tài khoản lưu trữ và chứng chỉ TLS cho điểm cuối công khai của nó. Azure Key Vault cung cấp cho các nhà phát triển một vị trí an toàn duy nhất để lưu trữ tất cả các thông tin xác thực này và truy xuất chúng trong thời gian chạy thông qua các lệnh gọi SDK, mà không cần nhúng các bí mật vào mã ứng dụng hoặc tệp cấu hình.

## Understand Key Vault capabilities and service tiers

Azure Key Vault provides three core capabilities: secrets management, key management, and certificate management. Each capability addresses a different type of sensitive data, and understanding the distinctions helps you choose the right object type for each credential in your AI application. Key Vault encrypts all stored objects at rest and controls access through Microsoft Entra ID authentication combined with Azure role-based access control (RBAC) authorization.
	Azure Key Vault cung cấp ba khả năng cốt lõi: quản lý bí mật, quản lý khóa và quản lý chứng chỉ. Mỗi khả năng giải quyết một loại dữ liệu nhạy cảm khác nhau và việc hiểu rõ sự khác biệt giúp bạn chọn đúng loại đối tượng cho từng thông tin xác thực trong ứng dụng AI của mình. Key Vault mã hóa tất cả các đối tượng được lưu trữ khi ở trạng thái nghỉ và kiểm soát quyền truy cập thông qua xác thực Microsoft Entra ID kết hợp với ủy quyền kiểm soát truy cập dựa trên vai trò (RBAC) của Azure.

Key Vault operates in two service tiers that determine how cryptographic keys are protected:
	Key Vault hoạt động theo hai cấp độ dịch vụ, quyết định cách thức bảo vệ các khóa mã hóa:

- **Standard tier:** Encrypts keys using software libraries validated to FIPS 140 Level 1. This tier is suitable for most application scenarios where software-protected keys provide sufficient security.
	**Cấp độ tiêu chuẩn:** Mã hóa khóa bằng thư viện phần mềm được chứng nhận theo tiêu chuẩn FIPS 140 Cấp độ 1. Cấp độ này phù hợp với hầu hết các trường hợp ứng dụng mà khóa được bảo vệ bằng phần mềm cung cấp đủ độ bảo mật.
- **Premium tier:** Protects keys using FIPS 140-3 Level 3 validated hardware security modules (HSMs). Key material never leaves the HSM boundary. You can choose this tier when regulatory or compliance requirements mandate HSM-protected keys.
	**Cấp độ cao cấp:** Bảo vệ khóa bằng các mô-đun bảo mật phần cứng (HSM) được chứng nhận theo tiêu chuẩn FIPS 140-3 Cấp độ 3. Vật liệu khóa không bao giờ rời khỏi phạm vi của HSM. Bạn có thể chọn cấp độ này khi các yêu cầu về quy định hoặc tuân thủ bắt buộc phải sử dụng khóa được bảo vệ bằng HSM.
Developers interact with Key Vault through REST APIs, Azure SDKs (available for Python, .NET, Java, JavaScript, and Go), the Azure CLI, and the Azure portal. The Python SDK is the primary client library used throughout this module.
## Choose the right object type for your credentials

Key Vault stores three object types: secrets, keys, and certificates. Each type serves a distinct purpose, and AI applications often use all three. Selecting the correct object type ensures that your credentials benefit from the appropriate storage, access control, and lifecycle management features.
	Key Vault lưu trữ ba loại đối tượng: bí mật, khóa và chứng chỉ. Mỗi loại phục vụ một mục đích riêng biệt, và các ứng dụng AI thường sử dụng cả ba. Việc chọn đúng loại đối tượng đảm bảo rằng thông tin xác thực của bạn được hưởng lợi từ các tính năng lưu trữ, kiểm soát truy cập và quản lý vòng đời phù hợp.

**Secrets** store arbitrary string values up to 25 KB, such as API keys, connection strings, passwords, and tokens. AI applications use secrets for model endpoint keys, database credentials, and third-party service tokens. Key Vault treats secret values as opaque byte sequences and doesn't enforce any particular structure on the stored data. You can set a `content_type` property (up to 255 characters) to help consumers interpret the value. For example, a `content_type` of `text/plain` signals a simple string, while `application/json` indicates a structured JSON payload.
	**Bí mật** lưu trữ các giá trị chuỗi tùy ý lên đến 25 KB, chẳng hạn như khóa API, chuỗi kết nối, mật khẩu và mã thông báo. Các ứng dụng AI sử dụng bí mật cho khóa điểm cuối mô hình, thông tin xác thực cơ sở dữ liệu và mã thông báo dịch vụ của bên thứ ba. Key Vault coi các giá trị bí mật là các chuỗi byte không rõ ràng và không bắt buộc bất kỳ cấu trúc cụ thể nào đối với dữ liệu được lưu trữ. Bạn có thể đặt thuộc tính `content_type` (tối đa 255 ký tự) để giúp người dùng hiểu giá trị. Ví dụ, `content_type` là `text/plain` báo hiệu một chuỗi đơn giản, trong khi `application/json` cho biết tải trọng JSON có cấu trúc.

Python
```
# Code fragment - focus on setting a secret with content_type
client.set_secret(
    "openai-api-key",
    "sk-abc123def456",
    content_type="text/plain",
    tags={"environment": "production", "team": "ai-platform"}
)
```

**Keys** store cryptographic keys for encryption, signing, and key wrapping operations. Key Vault performs cryptographic operations server-side, so the key material never leaves the vault boundary. AI pipelines that encrypt training data at rest or sign model artifacts use Key Vault keys. Keys support RSA (2048, 3072, and 4096 bit), elliptic curve (P-256, P-256K, P-384, P-521), and symmetric (oct) key types. Because the vault performs the cryptographic operations rather than exposing raw key material, you get stronger security guarantees than managing key files locally.
	**Khóa** lưu trữ các khóa mật mã cho các thao tác mã hóa, ký và đóng gói khóa. Key Vault thực hiện các thao tác mật mã ở phía máy chủ, do đó vật liệu khóa không bao giờ rời khỏi phạm vi của kho lưu trữ. Các quy trình AI mã hóa dữ liệu huấn luyện khi lưu trữ hoặc ký các tạo phẩm mô hình sử dụng khóa Key Vault. Khóa hỗ trợ các loại khóa RSA (2048, 3072 và 4096 bit), đường cong elip (P-256, P-256K, P-384, P-521) và đối xứng (oct). Vì kho lưu trữ thực hiện các thao tác mật mã thay vì để lộ vật liệu khóa thô, bạn sẽ nhận được các đảm bảo bảo mật mạnh mẽ hơn so với việc quản lý các tệp khóa cục bộ.

**Certificates** store and manage X.509 certificates along with their private keys. Key Vault handles certificate lifecycle operations including issuance, renewal, and revocation through integration with certificate authorities. AI services that expose HTTPS endpoints or use mutual TLS for service-to-service authentication benefit from certificate management in Key Vault. When Key Vault stores a certificate, it creates a corresponding key and secret object that you can access through the key and secret APIs respectively.
	**Chứng chỉ** lưu trữ và quản lý các chứng chỉ X.509 cùng với các khóa riêng của chúng. Key Vault xử lý các hoạt động vòng đời chứng chỉ bao gồm cấp phát, gia hạn và thu hồi thông qua tích hợp với các cơ quan cấp chứng chỉ. Các dịch vụ AI hiển thị các điểm cuối HTTPS hoặc sử dụng TLS hai chiều để xác thực dịch vụ với dịch vụ sẽ được hưởng lợi từ việc quản lý chứng chỉ trong Key Vault. Khi Key Vault lưu trữ chứng chỉ, nó sẽ tạo ra một đối tượng khóa và bí mật tương ứng mà bạn có thể truy cập thông qua các API khóa và bí mật tương ứng.

## Organize vaults and objects for AI solutions

A well-organized vault structure simplifies secret management as your AI application scales across environments and teams. Key Vault doesn't restrict the number of secrets, keys, or certificates you can store in a single vault, but organizing objects with clear boundaries reduces security risk and operational complexity.
	Cấu trúc kho lưu trữ được tổ chức tốt giúp đơn giản hóa việc quản lý bí mật khi ứng dụng AI của bạn mở rộng quy mô trên nhiều môi trường và nhóm. Key Vault không giới hạn số lượng bí mật, khóa hoặc chứng chỉ bạn có thể lưu trữ trong một kho duy nhất, nhưng việc tổ chức các đối tượng với ranh giới rõ ràng giúp giảm rủi ro bảo mật và độ phức tạp trong vận hành.

**Vault-per-application boundary:** You can create separate vaults for each application and environment combination. For example, a RAG pipeline might use `kv-ragpipeline-dev`, `kv-ragpipeline-staging`, and `kv-ragpipeline-prod`. This separation limits the blast radius of a security incident. A compromised vault exposes only the secrets for one application in one environment. Vault-per-application boundaries also simplify RBAC assignments because you can grant a development team access to the development vault without exposing production credentials.
	**Ranh giới kho lưu trữ cho mỗi ứng dụng:** Bạn có thể tạo các kho lưu trữ riêng biệt cho mỗi sự kết hợp giữa ứng dụng và môi trường. Ví dụ, một pipeline RAG có thể sử dụng `kv-ragpipeline-dev`, `kv-ragpipeline-staging` và `kv-ragpipeline-prod`. Sự phân tách này giới hạn phạm vi ảnh hưởng của một sự cố bảo mật. Một kho lưu trữ bị xâm phạm chỉ làm lộ các bí mật của một ứng dụng trong một môi trường. Ranh giới kho lưu trữ cho mỗi ứng dụng cũng đơn giản hóa việc phân quyền RBAC vì bạn có thể cấp cho nhóm phát triển quyền truy cập vào kho lưu trữ phát triển mà không làm lộ thông tin xác thực sản xuất.

**Naming conventions:** You can use descriptive, hyphenated names that encode the resource type and purpose. Examples include `cosmosdb-connection-string`, `openai-api-key`, and `blob-storage-account-key`. Consistent naming simplifies programmatic lookups and reduces errors when referencing secrets in code. Vault names themselves must be globally unique within Azure, three to 24 characters long, and contain only alphanumeric characters and hyphens. Vault names must begin with a letter, end with a letter or digit, and can't contain consecutive hyphens.
	**Quy ước đặt tên:** Bạn có thể sử dụng các tên mô tả, có dấu gạch ngang để mã hóa loại tài nguyên và mục đích. Ví dụ bao gồm `cosmosdb-connection-string`, `openai-api-key` và `blob-storage-account-key`. Việc đặt tên nhất quán giúp đơn giản hóa việc tra cứu lập trình và giảm lỗi khi tham chiếu các bí mật trong mã. Tên Vault phải là duy nhất trên toàn cầu trong Azure, dài từ 3 đến 24 ký tự và chỉ chứa các ký tự chữ số và dấu gạch ngang. Tên Vault phải bắt đầu bằng một chữ cái, kết thúc bằng một chữ cái hoặc chữ số và không được chứa các dấu gạch ngang liên tiếp.

**Tags for metadata:** You can attach tags to secrets for filtering and management. Each secret supports up to 15 tags, with tag names limited to 512 characters and values limited to 256 characters. Tags like `environment=production`, `team=ai-platform`, and `rotation-policy=90-days` enable bulk operations and reporting across large numbers of vault objects. Anyone with `list` or `get` permission on secrets can read tags, so don't store sensitive data in tag values.
	**Thẻ cho siêu dữ liệu:** Bạn có thể gắn thẻ vào các bí mật để lọc và quản lý. Mỗi bí mật hỗ trợ tối đa 15 thẻ, với tên thẻ giới hạn ở 512 ký tự và giá trị giới hạn ở 256 ký tự. Các thẻ như `environment=production`, `team=ai-platform` và `rotation-policy=90-days` cho phép thực hiện các thao tác hàng loạt và báo cáo trên số lượng lớn đối tượng Vault. Bất kỳ ai có quyền `list` hoặc `get` đối với các thông tin bí mật đều có thể đọc các thẻ, vì vậy đừng lưu trữ dữ liệu nhạy cảm trong giá trị của thẻ.

## Control access with Azure RBAC

Azure Key Vault supports two authorization models: Azure RBAC and legacy access policies. Azure RBAC is the recommended approach because it provides granular permission control at the Azure resource level, supports Privileged Identity Management (PIM) for just-in-time access, and works consistently across both the control plane (vault management) and the data plane (secret, key, and certificate operations).
	Azure Key Vault hỗ trợ hai mô hình ủy quyền: Azure RBAC và chính sách truy cập truyền thống. Azure RBAC là phương pháp được khuyến nghị vì nó cung cấp khả năng kiểm soát quyền chi tiết ở cấp độ tài nguyên Azure, hỗ trợ Quản lý Danh tính Đặc quyền (PIM) để truy cập tức thời và hoạt động nhất quán trên cả mặt phẳng điều khiển (quản lý kho lưu trữ) và mặt phẳng dữ liệu (các thao tác với bí mật, khóa và chứng chỉ).

Key Vault defines several built-in data plane roles that map to common access patterns. The following roles are the most relevant for secret management in AI applications:
	Key Vault định nghĩa một số vai trò mặt phẳng dữ liệu tích hợp sẵn tương ứng với các mẫu truy cập phổ biến. Các vai trò sau đây là phù hợp nhất cho việc quản lý bí mật trong các ứng dụng AI:

- **Key Vault Secrets User:** Grants read-only access to secret values, including the ability to read certificate private keys stored as secrets. Assign this role to application managed identities that need to retrieve credentials at runtime.
	**Người dùng Bí mật Key Vault:** Cấp quyền truy cập chỉ đọc vào các giá trị bí mật, bao gồm khả năng đọc khóa riêng của chứng chỉ được lưu trữ dưới dạng bí mật. Gán vai trò này cho các danh tính được quản lý bởi ứng dụng cần truy xuất thông tin xác thực trong thời gian chạy.
- **Key Vault Secrets Officer:** Grants full management permissions on secrets, including create, update, delete, and list operations. Assign this role to operators or CI/CD pipelines responsible for secret lifecycle management.
	**Cán bộ Bí mật Key Vault:** Cấp quyền quản lý đầy đủ đối với các bí mật, bao gồm các thao tác tạo, cập nhật, xóa và liệt kê. Gán vai trò này cho các nhà điều hành hoặc các đường ống CI/CD chịu trách nhiệm quản lý vòng đời bí mật.
- **Key Vault Administrator:** Grants all data plane operations on keys, secrets, and certificates. This role doesn't grant control plane permissions to manage the vault resource itself or modify role assignments.
	**Quản trị viên Key Vault:** Cấp quyền thực hiện tất cả các thao tác trên mặt phẳng dữ liệu đối với khóa, bí mật và chứng chỉ. Vai trò này không cấp quyền trên mặt phẳng điều khiển để quản lý tài nguyên kho lưu trữ hoặc sửa đổi việc phân công vai trò.
- **Key Vault Reader:** Grants read access to vault metadata (such as secret names and properties) without revealing secret values or key material. Useful for monitoring and discovery tools that need to verify which secrets exist without accessing their contents.
	**Người đọc Key Vault:** Cấp quyền truy cập đọc vào siêu dữ liệu của kho lưu trữ (chẳng hạn như tên và thuộc tính bí mật) mà không tiết lộ giá trị bí mật hoặc vật liệu khóa. Hữu ích cho các công cụ giám sát và khám phá cần xác minh bí mật nào tồn tại mà không cần truy cập nội dung của chúng.

You can use managed identities for application-to-vault authentication. A managed identity eliminates the need to store any credential in your application code or configuration. The application authenticates to Key Vault through Microsoft Entra ID, and the RBAC role assignment determines what operations the identity can perform. This pattern means your application needs zero stored credentials to access the vault that holds all of its other credentials.
	Bạn có thể sử dụng danh tính được quản lý để xác thực ứng dụng với kho lưu trữ. Danh tính được quản lý loại bỏ nhu cầu lưu trữ bất kỳ thông tin xác thực nào trong mã ứng dụng hoặc cấu hình của bạn. Ứng dụng xác thực với Key Vault thông qua Microsoft Entra ID và việc phân công vai trò RBAC xác định các thao tác mà danh tính có thể thực hiện. Mô hình này có nghĩa là ứng dụng của bạn không cần bất kỳ thông tin xác thực nào được lưu trữ để truy cập vào kho lưu trữ chứa tất cả các thông tin xác thực khác của nó.

## Protect against accidental deletion with soft delete and purge protection

Key Vault enables soft delete by default on all new vaults, and you can't disable it once enabled. When you delete a secret, key, or certificate, Key Vault retains the object in a deleted state for a configurable retention period between seven and 90 days (the default is 90 days). You set the retention period at vault creation, and you can't change it afterward. During the retention window, you can recover deleted objects to their previous state.
	Key Vault mặc định bật tính năng xóa mềm trên tất cả các vault mới và bạn không thể tắt tính năng này sau khi đã bật. Khi bạn xóa một secret, key hoặc certificate, Key Vault sẽ giữ lại đối tượng ở trạng thái đã xóa trong một khoảng thời gian lưu giữ có thể cấu hình từ bảy đến 90 ngày (mặc định là 90 ngày). Bạn thiết lập thời gian lưu giữ khi tạo vault và không thể thay đổi sau đó. Trong thời gian lưu giữ, bạn có thể khôi phục các đối tượng đã xóa về trạng thái trước đó.

Purge protection is an optional feature that prevents permanent deletion of soft-deleted objects during the retention period. When purge protection is enabled, no one can permanently remove a secret until the retention period expires. Purge protection is especially important for AI solutions where losing an encryption key or certificate can render stored data permanently inaccessible. Consider enabling purge protection on production vaults to guard against both accidental and malicious data loss.
	Bảo vệ chống xóa vĩnh viễn là một tính năng tùy chọn ngăn chặn việc xóa vĩnh viễn các đối tượng đã xóa mềm trong thời gian lưu giữ. Khi tính năng bảo vệ chống xóa vĩnh viễn được bật, không ai có thể xóa vĩnh viễn một secret cho đến khi thời gian lưu giữ hết hạn. Tính năng bảo vệ chống xóa vĩnh viễn đặc biệt quan trọng đối với các giải pháp AI, nơi việc mất khóa mã hóa hoặc certificate có thể khiến dữ liệu được lưu trữ không thể truy cập vĩnh viễn. Hãy cân nhắc bật tính năng bảo vệ chống xóa vĩnh viễn trên các vault sản xuất để bảo vệ chống lại cả việc mất dữ liệu do vô tình và do cố ý.

When a Key Vault itself is soft-deleted, its RBAC role assignments and Event Grid subscriptions are also deleted. These resources aren't automatically restored when you recover the vault, so you need to recreate them manually after recovery.
	Khi chính Key Vault bị xóa mềm, các gán vai trò RBAC và đăng ký Event Grid của nó cũng bị xóa. Các tài nguyên này không được tự động khôi phục khi bạn khôi phục kho dữ liệu, vì vậy bạn cần tạo lại chúng theo cách thủ công sau khi khôi phục.

# Retrieve secrets using Azure SDK client libraries
___
The Python `azure-keyvault-secrets` library provides the `SecretClient` class for all secret operations against Azure Key Vault. Combined with the `azure-identity` library for authentication, these two packages give your AI application everything it needs to retrieve credentials at runtime without storing any vault credentials in code. This unit walks through client setup, secret retrieval, listing operations, error handling, and async patterns for high-throughput AI services.
	Thư viện Python azure-keyvault-secrets cung cấp lớp SecretClient cho tất cả các thao tác liên quan đến thông tin bí mật trên Azure Key Vault. Kết hợp với thư viện azure-identity để xác thực, hai gói này cung cấp cho ứng dụng AI của bạn mọi thứ cần thiết để truy xuất thông tin xác thực trong thời gian chạy mà không cần lưu trữ bất kỳ thông tin xác thực nào trong mã. Bài học này sẽ hướng dẫn bạn qua quá trình thiết lập máy khách, truy xuất thông tin bí mật, các thao tác liệt kê, xử lý lỗi và các mẫu bất đồng bộ cho các dịch vụ AI có thông lượng cao.

## Install and configure the SDK

The Key Vault secrets SDK requires two packages: `azure-keyvault-secrets` for vault operations and `azure-identity` for authentication. You install both packages together because every `SecretClient` instance requires a credential object to authenticate with Key Vault. The `SecretClient` class provides all CRUD and listing operations for secrets, and you initialize it with the vault URL and a credential.
	SDK bí mật Key Vault yêu cầu hai gói: azure-keyvault-secrets cho các thao tác với vault và azure-identity cho xác thực. Bạn cần cài đặt cả hai gói cùng nhau vì mỗi instance SecretClient đều yêu cầu một đối tượng thông tin xác thực để xác thực với Key Vault. Lớp SecretClient cung cấp tất cả các thao tác CRUD và liệt kê bí mật, và bạn khởi tạo nó với URL vault và thông tin xác thực.

Bash
```
pip install azure-keyvault-secrets azure-identity
```

The vault URL follows the pattern `https://<vault-name>.vault.azure.net/`. You can find this URL in the Azure portal on the vault's overview page, or retrieve it with the Azure CLI using `az keyvault show --name <vault-name> --query properties.vaultUri`.
	URL vault tuân theo mẫu https://< vault-name >.vault.azure.net/. Bạn có thể tìm thấy URL này trong cổng Azure trên trang tổng quan của vault hoặc truy xuất nó bằng Azure CLI bằng lệnh az keyvault show --name < vault-name > --query properties.vaultUri.

## Authenticate with DefaultAzureCredential

`DefaultAzureCredential` from the `azure-identity` library chains multiple authentication methods in a defined order, trying each one until authentication succeeds. This single credential class works across development and production environments without code changes. In production, managed identity authenticates the application without any stored credentials. In local development, the Azure CLI or Azure Developer CLI credential provides access.
	DefaultAzureCredential từ thư viện azure-identity kết hợp nhiều phương thức xác thực theo một thứ tự xác định, thử từng phương thức cho đến khi xác thực thành công. Lớp thông tin xác thực duy nhất này hoạt động trên cả môi trường phát triển và sản xuất mà không cần thay đổi mã. Trong môi trường sản xuất, danh tính được quản lý sẽ xác thực ứng dụng mà không cần bất kỳ thông tin xác thực nào được lưu trữ. Trong môi trường phát triển cục bộ, thông tin xác thực Azure CLI hoặc Azure Developer CLI cung cấp quyền truy cập.

The authentication chain follows this order:

1. **EnvironmentCredential:** Reads `AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, and `AZURE_CLIENT_SECRET` environment variables for service principal authentication.
	EnvironmentCredential: Đọc các biến môi trường AZURE_CLIENT_ID, AZURE_TENANT_ID và AZURE_CLIENT_SECRET để xác thực tài khoản dịch vụ.
2. **WorkloadIdentityCredential:** Authenticates using Kubernetes workload identity tokens.
	WorkloadIdentityCredential: Xác thực bằng cách sử dụng mã thông báo nhận dạng khối lượng công việc Kubernetes.
3. **ManagedIdentityCredential:** Uses the Azure managed identity (system-assigned or user-assigned) attached to the compute resource.
	ManagedIdentityCredential: Sử dụng danh tính được quản lý của Azure (do hệ thống hoặc người dùng chỉ định) được gắn với tài nguyên điện toán.
4. **AzureCliCredential:** Authenticates using the account from `az login`.
	AzureCliCredential: Xác thực bằng tài khoản từ lệnh `az login`.
5. **AzureDeveloperCliCredential:** Authenticates using the account from `azd auth login`.
	AzureDeveloperCliCredential: Xác thực bằng tài khoản từ lệnh `azd auth login`.
6. **AzurePowerShellCredential:** Authenticates using the account from `Connect-AzAccount`.
	AzurePowerShellCredential: Xác thực bằng tài khoản từ lệnh `Connect-AzAccount`.

For deployed AI services running on Azure compute resources (such as Azure Container Apps, Azure Kubernetes Service, or Azure App Service), managed identity is the recommended authentication method. The application authenticates to Key Vault through Microsoft Entra ID without any stored credentials. You assign the `Key Vault Secrets User` role to the managed identity, and the application gains read access to secrets in the vault.
	Đối với các dịch vụ AI đã triển khai chạy trên tài nguyên điện toán Azure (chẳng hạn như Azure Container Apps, Azure Kubernetes Service hoặc Azure App Service), danh tính được quản lý là phương pháp xác thực được khuyến nghị. Ứng dụng xác thực với Key Vault thông qua Microsoft Entra ID mà không cần lưu trữ bất kỳ thông tin xác thực nào. Bạn gán vai trò Người dùng Bí mật Key Vault cho danh tính được quản lý, và ứng dụng sẽ có quyền truy cập đọc vào các bí mật trong kho.

## Retrieve a secret by name

The `get_secret()` method retrieves the current version of a secret from Key Vault. The returned `KeyVaultSecret` object contains the secret value, name, and a `properties` object with metadata such as version, creation date, expiration date, enabled status, content type, and tags. Retrieving a single secret is the most common operation in AI application code because your services call it at startup or on-demand to load credentials for downstream services.
	Phương thức get_secret() truy xuất phiên bản hiện tại của một bí mật từ Key Vault. Đối tượng KeyVaultSecret được trả về chứa giá trị bí mật, tên và một đối tượng thuộc tính với siêu dữ liệu như phiên bản, ngày tạo, ngày hết hạn, trạng thái kích hoạt, loại nội dung và thẻ. Truy xuất một bí mật duy nhất là thao tác phổ biến nhất trong mã ứng dụng AI vì các dịch vụ của bạn gọi nó khi khởi động hoặc theo yêu cầu để tải thông tin xác thực cho các dịch vụ hạ nguồn.

Python
```
# Code fragment - focus on retrieving a secret with DefaultAzureCredential
from azure.identity import DefaultAzureCredential
from azure.keyvault.secrets import SecretClient

credential = DefaultAzureCredential()
client = SecretClient(
    vault_url="https://kv-ragpipeline-prod.vault.azure.net/",
    credential=credential
)

secret = client.get_secret("openai-api-key")

# Access the secret value and metadata
api_key = secret.value
version = secret.properties.version
created = secret.properties.created_on
content_type = secret.properties.content_type
```

The `secret.value` property contains the secret string that your application passes to downstream service clients. The `properties` object provides metadata for logging and debugging. You can log the secret name and version for audit purposes without exposing the actual secret value.
	Thuộc tính secret.value chứa chuỗi bí mật mà ứng dụng của bạn chuyển cho các máy khách dịch vụ hạ nguồn. Đối tượng thuộc tính cung cấp siêu dữ liệu để ghi nhật ký và gỡ lỗi. Bạn có thể ghi nhật ký tên và phiên bản bí mật cho mục đích kiểm toán mà không làm lộ giá trị bí mật thực tế.

## List secret properties

The `list_properties_of_secrets()` method enumerates all secrets in the vault without retrieving their values. This operation returns `SecretProperties` objects that contain metadata such as name, version, content type, tags, and enabled status. You can use this method to discover available secrets, build configuration maps at startup, or verify that expected secrets exist before your application begins processing requests.
	Phương thức list_properties_of_secrets() liệt kê tất cả các bí mật trong kho mà không truy xuất giá trị của chúng. Thao tác này trả về các đối tượng SecretProperties chứa siêu dữ liệu như tên, phiên bản, loại nội dung, thẻ và trạng thái kích hoạt. Bạn có thể sử dụng phương pháp này để tìm các bí mật có sẵn, xây dựng bản đồ cấu hình khi khởi động hoặc xác minh rằng các bí mật mong muốn tồn tại trước khi ứng dụng của bạn bắt đầu xử lý yêu cầu.

Python
```
# Code fragment - focus on listing secret properties for discovery
secret_properties = client.list_properties_of_secrets()

for prop in secret_properties:
    print(f"Secret: {prop.name}, Enabled: {prop.enabled}, "
          f"Content type: {prop.content_type}")
    if prop.tags:
        print(f"  Tags: {prop.tags}")
```

This listing operation is useful during application startup to validate that all required credentials exist in the vault. If your AI service needs five specific secrets (such as an API key, a database connection string, and three service tokens), you can check for their existence before attempting to retrieve values. This approach surfaces configuration errors early rather than failing on the first request that needs a missing credential.
	Thao tác liệt kê này hữu ích trong quá trình khởi động ứng dụng để xác thực rằng tất cả các thông tin xác thực cần thiết đều tồn tại trong kho lưu trữ. Nếu dịch vụ AI của bạn cần năm bí mật cụ thể (chẳng hạn như khóa API, chuỗi kết nối cơ sở dữ liệu và ba mã thông báo dịch vụ), bạn có thể kiểm tra sự tồn tại của chúng trước khi cố gắng truy xuất giá trị. Cách tiếp cận này giúp phát hiện lỗi cấu hình sớm hơn thay vì gặp lỗi ở yêu cầu đầu tiên cần thông tin xác thực bị thiếu.

## Handle errors and exceptions

The SDK raises specific exception types for different failure scenarios, and your application should handle each type differently. A missing secret indicates a configuration error that requires operator intervention, while a transient network error warrants a retry. Distinguishing between these cases in your error handling logic prevents your application from retrying errors that won't resolve on their own and helps operators diagnose issues faster.
	Bộ SDK sẽ đưa ra các loại ngoại lệ cụ thể cho các tình huống lỗi khác nhau, và ứng dụng của bạn nên xử lý từng loại một cách riêng biệt. Việc thiếu mã bí mật cho thấy lỗi cấu hình cần sự can thiệp của người vận hành, trong khi lỗi mạng tạm thời cần phải thử lại. Việc phân biệt giữa các trường hợp này trong logic xử lý lỗi của bạn sẽ ngăn ứng dụng thử lại các lỗi không tự khắc phục được và giúp người vận hành chẩn đoán sự cố nhanh hơn.

Python
```
# Code fragment - focus on structured error handling for secret retrieval
from azure.core.exceptions import (
    ResourceNotFoundError,
    HttpResponseError,
    ServiceRequestError
)

def get_secret_safely(client, secret_name):
    try:
        secret = client.get_secret(secret_name)
        return secret.value
    except ResourceNotFoundError:
        # Secret doesn't exist - configuration error
        print(f"Secret '{secret_name}' not found in vault. "
              "Verify the secret name and vault configuration.")
        raise
    except HttpResponseError as e:
        # Authentication or authorization failure
        print(f"Access denied or server error for '{secret_name}': "
              f"{e.status_code} - {e.message}")
        raise
    except ServiceRequestError:
        # Network connectivity issue - may be transient
        print(f"Network error retrieving '{secret_name}'. "
              "Check connectivity to Key Vault.")
        raise
```

`ResourceNotFoundError` fires when the secret name doesn't exist in the vault. `HttpResponseError` covers authentication failures (the identity lacks the required RBAC role), authorization errors, and server-side issues. `ServiceRequestError` indicates a network-level problem, such as DNS resolution failure or a timeout, which might resolve on retry.
	Lỗi `ResourceNotFoundError` xảy ra khi tên bí mật không tồn tại trong kho lưu trữ. Lỗi `HttpResponseError` bao gồm các lỗi xác thực (danh tính thiếu vai trò RBAC cần thiết), lỗi ủy quyền và các sự cố phía máy chủ. Lỗi `ServiceRequestError` cho biết sự cố ở cấp độ mạng, chẳng hạn như lỗi phân giải DNS hoặc hết thời gian chờ, có thể được khắc phục khi thử lại.

## Use the async client for high-throughput applications

The `azure.keyvault.secrets.aio` module provides an async `SecretClient` for applications that use asyncio. AI services that process concurrent requests benefit from async secret retrieval because it avoids blocking the event loop during vault calls. The async client exposes the same API surface as the synchronous client, so you can switch between them without changing your application logic.
	Mô-đun `azure.keyvault.secrets.aio` cung cấp một `SecretClient` bất đồng bộ cho các ứng dụng sử dụng asyncio. Các dịch vụ AI xử lý các yêu cầu đồng thời sẽ được hưởng lợi từ việc truy xuất bí mật bất đồng bộ vì nó tránh làm tắc nghẽn vòng lặp sự kiện trong quá trình gọi vault. Client bất đồng bộ cung cấp cùng một giao diện API như client đồng bộ, vì vậy bạn có thể chuyển đổi giữa chúng mà không cần thay đổi logic ứng dụng của mình.

Python
```
# Code fragment - focus on async secret retrieval
from azure.identity.aio import DefaultAzureCredential
from azure.keyvault.secrets.aio import SecretClient

async def get_ai_credentials():
    credential = DefaultAzureCredential()
    client = SecretClient(
        vault_url="https://kv-ragpipeline-prod.vault.azure.net/",
        credential=credential
    )

    async with client:
        secret = await client.get_secret("openai-api-key")

    await credential.close()
    return secret.value
```

The async client and credential are both async context managers. You should use `async with` or explicitly call `await client.close()` and `await credential.close()` when you're done with them. In web frameworks like FastAPI or aiohttp, create the client once at application startup and reuse it across requests to avoid the overhead of creating new connections for each operation.
	Cả client bất đồng bộ và credential đều là các trình quản lý ngữ cảnh bất đồng bộ. Bạn nên sử dụng `async with` hoặc gọi rõ ràng `await client.close()` và `await credential.close()` khi bạn đã sử dụng xong chúng. Trong các framework web như FastAPI hoặc aiohttp, hãy tạo client một lần khi ứng dụng khởi động và tái sử dụng nó trong các yêu cầu để tránh chi phí tạo kết nối mới cho mỗi thao tác.