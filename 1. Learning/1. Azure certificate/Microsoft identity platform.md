	The Microsoft identity platform helps you build applications your users and customers can sign in to using their Microsoft identities or social accounts, and provide authorized access to your own APIs or Microsoft APIs like Microsoft Graph.
	Nền tảng định danh của Microsoft giúp bạn xây dựng các ứng dụng mà người dùng và khách hàng có thể đăng nhập bằng danh tính Microsoft hoặc tài khoản mạng xã hội của họ, đồng thời cung cấp quyền truy cập được ủy quyền vào API của riêng bạn hoặc API của Microsoft như Microsoft Graph.

There are several components that make up the Microsoft identity platform:
	Nền tảng định danh của Microsoft bao gồm một số thành phần:

- **OAuth 2.0 and OpenID Connect standard-compliant authentication service** enabling developers to authenticate several identity types, including:
	Dịch vụ xác thực tuân thủ tiêu chuẩn OAuth 2.0 và OpenID Connect cho phép các nhà phát triển xác thực nhiều loại danh tính, bao gồm:
	- Work or school accounts, provisioned through Microsoft Entra ID
		Tài khoản công việc hoặc trường học, được cấp thông qua Microsoft Entra ID
	- Personal Microsoft account, like Xbox, and Outlook.com
		Tài khoản cá nhân của Microsoft, như Xbox và Outlook.com
	- Social or local accounts, by using Azure Active Directory B2C
		Tài khoản mạng xã hội hoặc tài khoản cục bộ, bằng cách sử dụng Azure Active Directory B2C
	- Social or local customer accounts, by using Microsoft Entra External ID
		Tài khoản khách hàng mạng xã hội hoặc tài khoản cục bộ, bằng cách sử dụng Microsoft Entra External ID
	- **Open-source libraries**: Microsoft Authentication Libraries (MSAL) and support for other standards-compliant libraries
		Thư viện mã nguồn mở: Thư viện xác thực Microsoft (MSAL) và hỗ trợ các thư viện tuân thủ tiêu chuẩn khác
    
- **Microsoft identity platform endpoint**: Works with the Microsoft Authentication Libraries (MSAL) or any other standards-compliant library. It implements human readable scopes, in accordance with industry standards.
    Điểm cuối nền tảng định danh của Microsoft: Hoạt động với Thư viện xác thực Microsoft (MSAL) hoặc bất kỳ thư viện tuân thủ tiêu chuẩn nào khác. Nó triển khai các phạm vi dễ đọc, phù hợp với các tiêu chuẩn ngành.

- **Application management portal**: A registration and configuration experience in the Azure portal, along with the other Azure management capabilities.
    Cổng quản lý ứng dụng: Trải nghiệm đăng ký và cấu hình trong cổng Azure, cùng với các khả năng quản lý Azure khác.

- **Application configuration API and PowerShell**: Programmatic configuration of your applications through the Microsoft Graph API and PowerShell so you can automate your DevOps tasks.
    API cấu hình ứng dụng và PowerShell: Cấu hình ứng dụng của bạn theo chương trình thông qua API Microsoft Graph và PowerShell để bạn có thể tự động hóa các tác vụ DevOps.

For developers, the Microsoft identity platform offers integration of modern innovations in the identity and security space like passwordless authentication, step-up authentication, and Conditional Access. You don’t need to implement such functionality yourself: applications integrated with the Microsoft identity platform natively take advantage of such innovations.
	Đối với các nhà phát triển, nền tảng định danh của Microsoft cung cấp khả năng tích hợp các cải tiến hiện đại trong lĩnh vực định danh và bảo mật như xác thực không cần mật khẩu, xác thực tăng cường và truy cập có điều kiện. Bạn không cần phải tự triển khai các chức năng này: các ứng dụng được tích hợp với nền tảng định danh của Microsoft sẽ tự động tận dụng những cải tiến này.

# Explore service principals
___

To delegate Identity and Access Management functions to Microsoft Entra ID, an application must be registered with a Microsoft Entra tenant. When you register your application with Microsoft Entra ID, you're creating an identity configuration for your application that allows it to integrate with Microsoft Entra ID. When you register an app in the Azure portal, you choose whether it is:
	Để ủy quyền các chức năng Quản lý Danh tính và Truy cập cho Microsoft Entra ID, ứng dụng phải được đăng ký với một tenant của Microsoft Entra. Khi bạn đăng ký ứng dụng của mình với Microsoft Entra ID, bạn đang tạo một cấu hình danh tính cho ứng dụng của mình, cho phép ứng dụng tích hợp với Microsoft Entra ID. Khi bạn đăng ký một ứng dụng trong cổng Azure, bạn chọn xem đó là:

- **Single tenant**: only accessible in your tenant
	**Single tenant**: chỉ có thể truy cập trong tenant của bạn
- **Multi-tenant**: accessible in other tenants
	**Multi-tenant**: có thể truy cập trong các tenant khác

If you register an application in the portal, an application object (the globally unique instance of the app) and a service principal object are automatically created in your home tenant. You also have a globally unique ID for your app (the app or client ID). In the portal, you can then add secrets or certificates and scopes to make your app work, customize the branding of your app in the sign-in dialog, and more.
	Nếu bạn đăng ký một ứng dụng trong cổng, một đối tượng ứng dụng (phiên bản duy nhất trên toàn cầu của ứng dụng) và một đối tượng chính dịch vụ sẽ tự động được tạo trong tenant chính của bạn. Bạn cũng có một ID duy nhất trên toàn cầu cho ứng dụng của mình (ID ứng dụng hoặc ID máy khách). Trong cổng, bạn có thể thêm các bí mật hoặc chứng chỉ và phạm vi để ứng dụng của bạn hoạt động, tùy chỉnh thương hiệu của ứng dụng trong hộp thoại đăng nhập, v.v.

## Application object

A Microsoft Entra application is scoped to its one and only application object. The application object resides in the Microsoft Entra tenant where the application was registered (known as the application's "home" tenant). An application object is used as a template or blueprint to create one or more service principal objects. A service principal is created in every tenant where the application is used. Similar to a class in object-oriented programming, the application object has some static properties that are applied to all the created service principals (or application instances).
	Một ứng dụng Microsoft Entra chỉ giới hạn trong một đối tượng ứng dụng duy nhất. Đối tượng ứng dụng này nằm trong tenant Microsoft Entra nơi ứng dụng được đăng ký (được gọi là tenant "chính" của ứng dụng). Đối tượng ứng dụng được sử dụng như một mẫu hoặc bản thiết kế để tạo ra một hoặc nhiều đối tượng principal dịch vụ. Một principal dịch vụ được tạo trong mỗi tenant nơi ứng dụng được sử dụng. Tương tự như một lớp trong lập trình hướng đối tượng, đối tượng ứng dụng có một số thuộc tính tĩnh được áp dụng cho tất cả các principal dịch vụ (hoặc các thể hiện ứng dụng) được tạo ra.

The application object describes three aspects of an application:
	Đối tượng ứng dụng mô tả ba khía cạnh của một ứng dụng:

- How the service can issue tokens in order to access the application.
	Cách thức dịch vụ có thể cấp mã thông báo để truy cập ứng dụng.
- Resources that the application might need to access.
	Các tài nguyên mà ứng dụng có thể cần truy cập.
- The actions that the application can take.
	Các hành động mà ứng dụng có thể thực hiện.

The Microsoft Graph [Application entity](https://learn.microsoft.com/en-us/graph/api/resources/application) defines the schema for an application object's properties.
	Thực thể Ứng dụng của Microsoft Graph định nghĩa lược đồ cho các thuộc tính của đối tượng ứng dụng.

## Service principal object

To access resources secured by a Microsoft Entra tenant, the entity that is requesting access must be represented by a security principal. This is true for both users (user principal) and applications (service principal).
	Để truy cập các tài nguyên được bảo mật bởi một tenant Microsoft Entra, thực thể yêu cầu truy cập phải được đại diện bởi một đối tượng chính bảo mật. Điều này đúng cho cả người dùng (đối tượng chính người dùng) và ứng dụng (đối tượng chính dịch vụ).

The security principal defines the access policy and permissions for the user/application in the Microsoft Entra tenant. This enables core features such as authentication of the user/application during sign-in, and authorization during resource access.
	Đối tượng chính bảo mật xác định chính sách truy cập và quyền hạn cho người dùng/ứng dụng trong tenant Microsoft Entra. Điều này cho phép các tính năng cốt lõi như xác thực người dùng/ứng dụng trong quá trình đăng nhập và ủy quyền trong quá trình truy cập tài nguyên.

There are three types of service principal:
	Có ba loại đối tượng chính dịch vụ:

- **Application** - This type of service principal is the local representation, or application instance, of a global application object in a single tenant or directory. A service principal is created in each tenant where the application is used, and references the globally unique app object. The service principal object defines what the app can actually do in the specific tenant, who can access the app, and what resources the app can access.
	Ứng dụng - Loại đối tượng chính dịch vụ này là đại diện cục bộ, hay phiên bản ứng dụng, của một đối tượng ứng dụng toàn cầu trong một tenant hoặc thư mục duy nhất. Một đối tượng chính dịch vụ được tạo trong mỗi tenant nơi ứng dụng được sử dụng và tham chiếu đến đối tượng ứng dụng duy nhất trên toàn cầu. Đối tượng chính dịch vụ xác định những gì ứng dụng thực sự có thể làm trong tenant cụ thể, ai có thể truy cập ứng dụng và ứng dụng có thể truy cập những tài nguyên nào.

- **Managed identity** - This type of service principal is used to represent a [managed identity](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview). Managed identities provide an identity for applications to use when connecting to resources that support Microsoft Entra authentication. When a managed identity is enabled, a service principal representing that managed identity is created in your tenant. Service principals representing managed identities can be granted access and permissions, but can't be updated or modified directly.
    Danh tính được quản lý - Loại đối tượng chính dịch vụ này được sử dụng để đại diện cho một danh tính được quản lý. Danh tính được quản lý cung cấp một danh tính để các ứng dụng sử dụng khi kết nối với các tài nguyên hỗ trợ xác thực Microsoft Entra. Khi một danh tính được quản lý được bật, một đối tượng chính dịch vụ đại diện cho danh tính được quản lý đó sẽ được tạo trong tenant của bạn. Các đối tượng dịch vụ đại diện cho danh tính được quản lý có thể được cấp quyền truy cập và quyền hạn, nhưng không thể được cập nhật hoặc sửa đổi trực tiếp.

- **Legacy** - This type of service principal represents a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences. A legacy service principal can have:
	Loại ứng dụng kế thừa (Legacy) - Loại đối tượng dịch vụ này đại diện cho một ứng dụng kế thừa, tức là một ứng dụng được tạo trước khi tính năng đăng ký ứng dụng được giới thiệu hoặc một ứng dụng được tạo thông qua các trải nghiệm kế thừa. Một đối tượng dịch vụ kế thừa có thể có:
    
    - credentials
	    thông tin xác thực
    - service principal names
	    tên đối tượng dịch vụ
    - reply URLs
	    URL phản hồi
    - and other properties that an authorized user can edit, but doesn't have an associated app registration.
		và các thuộc tính khác mà người dùng được ủy quyền có thể chỉnh sửa, nhưng không có đăng ký ứng dụng liên kết.

## Relationship between application objects and service principals

The application object is the _global_ representation of your application for use across all tenants, and the service principal is the _local_ representation for use in a specific tenant. The application object serves as the template from which common and default properties are _derived_ for use in creating corresponding service principal objects.
	Đối tượng ứng dụng là đại diện toàn cục của ứng dụng để sử dụng trên tất cả các tenant, còn nguyên tắc dịch vụ là đại diện cục bộ để sử dụng trong một tenant cụ thể. Đối tượng ứng dụng đóng vai trò là mẫu để từ đó các thuộc tính chung và mặc định được tạo ra để sử dụng trong việc tạo các đối tượng nguyên tắc dịch vụ tương ứng.


An application object has:
	Một đối tượng ứng dụng có:

- A one to one relationship with the software application, and
	Mối quan hệ một-một với ứng dụng phần mềm, và
- A one to many relationships with its corresponding service principal objects.
	Mối quan hệ một-nhiều với các đối tượng nguyên tắc dịch vụ tương ứng của nó.

A service principal must be created in each tenant where the application is used to establish an identity for sign-in and/or access to resources being secured by the tenant. A single-tenant application has only one service principal (in its home tenant), created and consented for use during application registration. A multitenant application also has a service principal created in each tenant where a user from that tenant consented to its use.
	Một nguyên tắc dịch vụ phải được tạo trong mỗi tenant nơi ứng dụng được sử dụng để thiết lập danh tính cho việc đăng nhập và/hoặc truy cập vào các tài nguyên được bảo mật bởi tenant đó. Một ứng dụng đơn tenant chỉ có một nguyên tắc dịch vụ (trong tenant gốc của nó), được tạo và được chấp thuận sử dụng trong quá trình đăng ký ứng dụng. Một ứng dụng đa tenant cũng có một nguyên tắc dịch vụ được tạo trong mỗi tenant nơi người dùng từ tenant đó đã đồng ý sử dụng nó.

# Discover permissions and consent
___

Applications that integrate with the Microsoft identity platform follow an authorization model that gives users and administrators control over how data can be accessed.
	Các ứng dụng tích hợp với nền tảng định danh của Microsoft tuân theo mô hình ủy quyền cho phép người dùng và quản trị viên kiểm soát cách thức truy cập dữ liệu.

The Microsoft identity platform implements the [OAuth 2.0](https://learn.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-protocols) authorization protocol. OAuth 2.0 is a method through which a third-party app can access web-hosted resources on behalf of a user. Any web-hosted resource that integrates with the Microsoft identity platform has a resource identifier, or _application ID URI_.
	Nền tảng định danh của Microsoft triển khai giao thức ủy quyền [OAuth 2.0](https://learn.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-protocols). OAuth 2.0 là một phương thức mà qua đó ứng dụng của bên thứ ba có thể truy cập các tài nguyên được lưu trữ trên web thay mặt người dùng. Bất kỳ tài nguyên được lưu trữ trên web nào tích hợp với nền tảng định danh của Microsoft đều có một mã định danh tài nguyên, hay _URI ID ứng dụng_.

Here are some examples of Microsoft web-hosted resources:
	Dưới đây là một số ví dụ về các tài nguyên được lưu trữ trên web của Microsoft:

- Microsoft Graph: `https://graph.microsoft.com`
- Microsoft 365 Mail API: `https://outlook.office.com`
- Azure Key Vault: `https://vault.azure.net`

The same is true for any third-party resources that are integrated with the Microsoft identity platform. Any of these resources also can define a set of permissions that can be used to divide the functionality of that resource into smaller chunks. When a resource's functionality is chunked into small permission sets, third-party apps can be built to request only the permissions that they need to perform their function. Users and administrators can know what data the app can access.
	Điều tương tự cũng đúng với bất kỳ tài nguyên của bên thứ ba nào được tích hợp với nền tảng định danh của Microsoft. Bất kỳ tài nguyên nào trong số này cũng có thể định nghĩa một tập hợp các quyền có thể được sử dụng để chia chức năng của tài nguyên đó thành các phần nhỏ hơn. Khi chức năng của một tài nguyên được chia thành các tập hợp quyền nhỏ, các ứng dụng của bên thứ ba có thể được xây dựng để chỉ yêu cầu các quyền mà chúng cần để thực hiện chức năng của mình. Người dùng và quản trị viên có thể biết ứng dụng có thể truy cập dữ liệu nào.

In OAuth 2.0, these types of permission sets are called _scopes_. They're also often referred to as _permissions_. In the Microsoft identity platform, a permission is represented as a string value. An app requests the permissions it needs by specifying the permission in the `scope` query parameter. Identity platform supports several well-defined [OpenID Connect scopes](https://learn.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#openid-connect-scopes) and resource-based permissions (each permission is indicated by appending the permission value to the resource's identifier or application ID URI). For example, the permission string `https://graph.microsoft.com/Calendars.Read` is used to request permission to read users calendars in Microsoft Graph.
	Trong OAuth 2.0, các loại tập hợp quyền này được gọi là _phạm vi_. Chúng cũng thường được gọi là _quyền_. Trong nền tảng định danh của Microsoft, một quyền được biểu thị dưới dạng giá trị chuỗi. Một ứng dụng yêu cầu các quyền mà nó cần bằng cách chỉ định quyền trong tham số truy vấn `phạm vi`. Nền tảng định danh hỗ trợ một số phạm vi OpenID Connect được xác định rõ ràng và các quyền dựa trên tài nguyên (mỗi quyền được chỉ định bằng cách thêm giá trị quyền vào mã định danh của tài nguyên hoặc URI ID ứng dụng). Ví dụ, chuỗi quyền `https://graph.microsoft.com/Calendars.Read` được sử dụng để yêu cầu quyền đọc lịch của người dùng trong Microsoft Graph.

An app most commonly requests these permissions by specifying the scopes in requests to the Microsoft identity platform authorize endpoint. However, some high-privilege permissions can be granted only through administrator consent. They can be requested or granted by using the [administrator consent endpoint](https://learn.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#admin-restricted-permissions).
	Thông thường, một ứng dụng sẽ yêu cầu các quyền này bằng cách chỉ định phạm vi trong các yêu cầu gửi đến điểm cuối ủy quyền của nền tảng nhận dạng Microsoft. Tuy nhiên, một số quyền có đặc quyền cao chỉ có thể được cấp thông qua sự đồng ý của quản trị viên. Chúng có thể được yêu cầu hoặc cấp bằng cách sử dụng [điểm cuối đồng ý của quản trị viên](https://learn.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#admin-restricted-permissions).

## Permission types

The Microsoft identity platform supports two types of permissions: _delegated access_ and _app-only access_.
	Nền tảng định danh của Microsoft hỗ trợ hai loại quyền: quyền truy cập được ủy quyền và quyền truy cập chỉ dành cho ứng dụng.

- **Delegated access** are used by apps that have a signed-in user present. For these apps, either the user or an administrator consents to the permissions that the app requests. The app is delegated with the permission to act as a signed-in user when it makes calls to the target resource.
    Quyền truy cập được ủy quyền được sử dụng bởi các ứng dụng có người dùng đã đăng nhập. Đối với các ứng dụng này, người dùng hoặc quản trị viên sẽ đồng ý với các quyền mà ứng dụng yêu cầu. Ứng dụng được ủy quyền để hoạt động như một người dùng đã đăng nhập khi thực hiện các cuộc gọi đến tài nguyên mục tiêu.
- **App-only access permissions** are used by apps that run without a signed-in user present, for example, apps that run as background services or daemons. Only an administrator can consent to app-only access permissions.
    Quyền truy cập chỉ dành cho ứng dụng được sử dụng bởi các ứng dụng chạy mà không cần người dùng đã đăng nhập, ví dụ: các ứng dụng chạy dưới dạng dịch vụ nền hoặc tiến trình nền. Chỉ quản trị viên mới có thể đồng ý với quyền truy cập chỉ dành cho ứng dụng.

## Consent types

Applications in Microsoft identity platform rely on consent in order to gain access to necessary resources or APIs. There are many kinds of consent that your app might need to know about in order to be successful. If you're defining permissions, you'll also need to understand how your users gain access to your app or API.
	Các ứng dụng trong nền tảng định danh của Microsoft dựa vào sự đồng ý để có được quyền truy cập vào các tài nguyên hoặc API cần thiết. Có nhiều loại sự đồng ý mà ứng dụng của bạn có thể cần biết để thành công. Nếu bạn đang xác định quyền, bạn cũng cần hiểu cách người dùng của bạn có được quyền truy cập vào ứng dụng hoặc API của bạn.

There are three consent types: _static user consent_, _incremental and dynamic user consent_, and _admin consent_.
	Có ba loại sự đồng ý: sự đồng ý tĩnh của người dùng, sự đồng ý tăng dần và động của người dùng, và sự đồng ý của quản trị viên.

### Static user consent

In the static user consent scenario, you must specify all the permissions it needs in the app's configuration in the Azure portal. If the user (or administrator, as appropriate) hasn't granted consent for this app, then Microsoft identity platform prompts the user to provide consent at this time. Static permissions also enable administrators to consent on behalf of all users in the organization.
	Trong kịch bản sự đồng ý tĩnh của người dùng, bạn phải chỉ định tất cả các quyền cần thiết trong cấu hình ứng dụng trên cổng Azure. Nếu người dùng (hoặc quản trị viên, tùy trường hợp) chưa cấp quyền cho ứng dụng này, thì nền tảng định danh Microsoft sẽ nhắc người dùng cung cấp sự đồng ý vào thời điểm này. Quyền tĩnh cũng cho phép quản trị viên đồng ý thay mặt tất cả người dùng trong tổ chức.

While static permissions of the app defined in the Azure portal keep the code nice and simple, it presents some possible issues for developers:
	Mặc dù quyền tĩnh của ứng dụng được định nghĩa trong cổng Azure giúp mã đơn giản và dễ hiểu hơn, nhưng nó có thể gây ra một số vấn đề cho nhà phát triển:

- The app needs to request all the permissions it would ever need upon the user's first sign-in. This can lead to a long list of permissions that discourages end users from approving the app's access on initial sign-in.
    Ứng dụng cần yêu cầu tất cả các quyền mà nó sẽ cần khi người dùng đăng nhập lần đầu. Điều này có thể dẫn đến một danh sách dài các quyền, khiến người dùng cuối không muốn chấp thuận quyền truy cập của ứng dụng khi đăng nhập lần đầu.
- The app needs to know all of the resources it would ever access ahead of time. It's difficult to create apps that could access an arbitrary number of resources.
    Ứng dụng cần biết trước tất cả các tài nguyên mà nó sẽ truy cập. Việc tạo ra các ứng dụng có thể truy cập một số lượng tài nguyên tùy ý là rất khó.

### Incremental and dynamic user consent

With the Microsoft identity platform endpoint, you can ignore the static permissions defined in the app registration information in the Azure portal and request permissions incrementally instead. You can ask for a minimum set of permissions upfront and request more over time as the customer uses more app features.
	Với điểm cuối nền tảng định danh Microsoft, bạn có thể bỏ qua các quyền tĩnh được định nghĩa trong thông tin đăng ký ứng dụng trên cổng Azure và thay vào đó yêu cầu quyền tăng dần. Bạn có thể yêu cầu một tập hợp quyền tối thiểu ngay từ đầu và yêu cầu thêm quyền theo thời gian khi khách hàng sử dụng nhiều tính năng hơn của ứng dụng.

To do so, you can specify the scopes your app needs at any time by including the new scopes in the `scope` parameter when requesting an access token - without the need to predefine them in the application registration information. If the user hasn't yet consented to new scopes added to the request, they're prompted to consent only to the new permissions. Incremental, or dynamic consent, only applies to delegated permissions and not to app-only access permissions.
	Để làm như vậy, bạn có thể chỉ định phạm vi quyền mà ứng dụng của bạn cần bất cứ lúc nào bằng cách thêm các phạm vi quyền mới vào tham số phạm vi khi yêu cầu mã truy cập - mà không cần phải xác định trước chúng trong thông tin đăng ký ứng dụng. Nếu người dùng chưa đồng ý với các phạm vi quyền mới được thêm vào yêu cầu, họ sẽ được nhắc chỉ đồng ý với các quyền mới đó. Sự đồng ý tăng dần, hay sự đồng ý động, chỉ áp dụng cho các quyền được ủy quyền chứ không áp dụng cho các quyền truy cập chỉ dành cho ứng dụng.

### Admin consent

Admin consent is required when your app needs access to certain high-privilege permissions. Admin consent ensures that administrators have some other controls before authorizing apps or users to access highly privileged data from the organization.
	Sự đồng ý của quản trị viên là cần thiết khi ứng dụng của bạn cần truy cập vào một số quyền hạn cao. Sự đồng ý của quản trị viên đảm bảo rằng quản trị viên có một số quyền kiểm soát khác trước khi cho phép ứng dụng hoặc người dùng truy cập vào dữ liệu có đặc quyền cao từ tổ chức.

Admin consent done on behalf of an organization still requires the static permissions registered for the app. Set those permissions for apps in the app registration portal if you need an admin to give consent on behalf of the entire organization. This reduces the cycles required by the organization admin to set up the application.
	Sự đồng ý của quản trị viên được thực hiện thay mặt cho tổ chức vẫn yêu cầu các quyền tĩnh đã được đăng ký cho ứng dụng. Hãy thiết lập các quyền đó cho ứng dụng trong cổng đăng ký ứng dụng nếu bạn cần quản trị viên cấp quyền thay mặt cho toàn bộ tổ chức. Điều này giúp giảm bớt các chu kỳ cần thiết để quản trị viên tổ chức thiết lập ứng dụng.

## Requesting individual user consent

In an OpenID Connect or OAuth 2.0 authorization request, an app can request the permissions it needs by using the scope query parameter. For example, when a user signs in to an app, the app sends a request like the following example. Line breaks are added for legibility.
	Trong yêu cầu ủy quyền OpenID Connect hoặc OAuth 2.0, một ứng dụng có thể yêu cầu các quyền cần thiết bằng cách sử dụng tham số truy vấn phạm vi. Ví dụ: khi người dùng đăng nhập vào một ứng dụng, ứng dụng sẽ gửi yêu cầu như ví dụ sau. Các ngắt dòng được thêm vào để dễ đọc.

HTTP

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=00001111-aaaa-2222-bbbb-3333cccc4444
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendars.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

The `scope` parameter is a space-separated list of delegated permissions that the app is requesting. Each permission is indicated by appending the permission value to the resource's identifier (the application ID URI). In the request example, the app needs permission to read the user's calendar and send mail as the user.
	Tham số scope là một danh sách các quyền được ủy quyền mà ứng dụng đang yêu cầu, được phân tách bằng dấu cách. Mỗi quyền được chỉ định bằng cách thêm giá trị quyền vào mã định danh của tài nguyên (URI ID ứng dụng). Trong ví dụ yêu cầu, ứng dụng cần quyền đọc lịch của người dùng và gửi thư với tư cách người dùng.

After the user enters their credentials, the Microsoft identity platform checks for a matching record of _user consent_. If the user hasn't consented to any of the requested permissions in the past, and if the administrator hasn't consented to these permissions on behalf of the entire organization, the Microsoft identity platform asks the user to grant the requested permissions.
	Sau khi người dùng nhập thông tin đăng nhập, nền tảng định danh của Microsoft sẽ kiểm tra xem có bản ghi đồng ý của người dùng phù hợp hay không. Nếu người dùng chưa từng chấp thuận bất kỳ quyền nào được yêu cầu trước đây, và nếu quản trị viên chưa chấp thuận các quyền này thay mặt cho toàn bộ tổ chức, nền tảng định danh của Microsoft sẽ yêu cầu người dùng cấp các quyền được yêu cầu.

# Discover conditional access
___

The Conditional Access feature in Microsoft Entra ID offers one of several ways that you can use to secure your app and protect a service. Conditional Access enables developers and enterprise customers to protect services in a multitude of ways including:
	Tính năng Truy cập Có điều kiện trong Microsoft Entra ID cung cấp một trong số nhiều cách bạn có thể sử dụng để bảo mật ứng dụng và bảo vệ dịch vụ. Truy cập Có điều kiện cho phép các nhà phát triển và khách hàng doanh nghiệp bảo vệ dịch vụ theo nhiều cách, bao gồm:

- [Multifactor authentication](https://learn.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-howitworks)
	[Xác thực đa yếu tố](https://learn.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-howitworks)
- Allowing only Intune enrolled devices to access specific services
	Chỉ cho phép các thiết bị đã đăng ký Intune truy cập các dịch vụ cụ thể
- Restricting user locations and IP ranges
	Hạn chế vị trí người dùng và phạm vi IP

## How does Conditional Access impact an app?

In most common cases, Conditional Access doesn't change an app's behavior or require any changes from the developer. Only in certain cases when an app indirectly or silently requests a token for a service does an app require code changes to handle Conditional Access challenges. It may be as simple as performing an interactive sign-in request.
	Trong hầu hết các trường hợp, Truy cập Có điều kiện không làm thay đổi hành vi của ứng dụng hoặc yêu cầu bất kỳ thay đổi nào từ nhà phát triển. Chỉ trong một số trường hợp nhất định khi một ứng dụng gián tiếp hoặc âm thầm yêu cầu mã thông báo cho một dịch vụ thì ứng dụng mới cần thay đổi mã để xử lý các thách thức Truy cập Có điều kiện. Nó có thể đơn giản như thực hiện yêu cầu đăng nhập tương tác.

Specifically, the following scenarios require code to handle Conditional Access challenges:
	Cụ thể, các trường hợp sau đây yêu cầu mã để xử lý các thử thách Truy cập Có điều kiện:

- Apps performing the on-behalf-of flow
	Ứng dụng thực hiện quy trình thay mặt người khác
- Apps accessing multiple services/resources
	Ứng dụng truy cập nhiều dịch vụ/tài nguyên
- Single-page apps using MSAL.js
	Ứng dụng một trang sử dụng MSAL.js
- Web apps calling a resource
	Ứng dụng web gọi tài nguyên

Conditional Access policies can be applied to the app and also a web API your app accesses. Depending on the scenario, an enterprise customer can apply and remove Conditional Access policies at any time. For your app to continue functioning when a new policy is applied, implement challenge handling.
	Chính sách Truy cập Có điều kiện có thể được áp dụng cho ứng dụng và cả API web mà ứng dụng của bạn truy cập. Tùy thuộc vào trường hợp, khách hàng doanh nghiệp có thể áp dụng và xóa chính sách Truy cập Có điều kiện bất cứ lúc nào. Để ứng dụng của bạn tiếp tục hoạt động khi một chính sách mới được áp dụng, hãy triển khai xử lý thử thách.

## Conditional Access examples

Some scenarios require code changes to handle Conditional Access whereas others work as is. Here are a few scenarios using Conditional Access to do multifactor authentication that gives some insight into the difference.
	Một số trường hợp yêu cầu thay đổi mã để xử lý Truy cập Có điều kiện trong khi những trường hợp khác hoạt động như bình thường. Dưới đây là một vài trường hợp sử dụng Truy cập Có điều kiện để thực hiện xác thực đa yếu tố, giúp bạn hiểu rõ hơn sự khác biệt.

- You're building a single-tenant iOS app and apply a Conditional Access policy. The app signs in a user and doesn't request access to an API. When the user signs in, the policy is automatically invoked and the user needs to perform multifactor authentication.
    Bạn đang xây dựng một ứng dụng iOS đơn người dùng và áp dụng chính sách Truy cập Có điều kiện. Ứng dụng đăng nhập người dùng và không yêu cầu quyền truy cập vào API. Khi người dùng đăng nhập, chính sách sẽ tự động được kích hoạt và người dùng cần thực hiện xác thực đa yếu tố.
- You're building an app that uses a middle tier service to access a downstream API. An enterprise customer at the company using this app applies a policy to the downstream API. When an end user signs in, the app requests access to the middle tier and sends the token. The middle tier performs on-behalf-of flow to request access to the downstream API. At this point, a claims "challenge" is presented to the middle tier. The middle tier sends the challenge back to the app, which needs to comply with the Conditional Access policy.
	Bạn đang xây dựng một ứng dụng sử dụng dịch vụ tầng trung gian để truy cập API hạ nguồn. Một khách hàng doanh nghiệp tại công ty sử dụng ứng dụng này áp dụng một chính sách cho API hạ nguồn. Khi người dùng cuối đăng nhập, ứng dụng yêu cầu quyền truy cập vào tầng trung gian và gửi mã thông báo. Tầng trung gian thực hiện luồng thay mặt để yêu cầu quyền truy cập vào API hạ nguồn. Tại thời điểm này, một "thử thách" xác thực được đưa ra cho tầng trung gian. Tầng trung gian gửi thử thách trở lại ứng dụng, ứng dụng cần phải tuân thủ chính sách Truy cập có điều kiện.