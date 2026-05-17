A function app provides an execution context in Azure in which your functions run. As such, it's the unit of deployment and management for your functions. A function app is composed of one or more individual functions that are managed, deployed, and scaled together. All of the functions in a function app share the same pricing plan, deployment method, and runtime version. Think of a function app as a way to organize and collectively manage your functions.
	Ứng dụng hàm (Function App) cung cấp ngữ cảnh thực thi trong Azure để các hàm của bạn chạy. Do đó, nó là đơn vị triển khai và quản lý cho các hàm của bạn. Một ứng dụng hàm bao gồm một hoặc nhiều hàm riêng lẻ được quản lý, triển khai và mở rộng quy mô cùng nhau. Tất cả các hàm trong một ứng dụng hàm đều dùng chung gói giá, phương thức triển khai và phiên bản thời gian chạy. Hãy coi ứng dụng hàm như một cách để tổ chức và quản lý các hàm của bạn một cách tập thể.
# Develop and test Azure Functions locally
___
Functions make it easy to use your favorite code editor and development tools to create and test functions on your local computer. Your local functions can connect to live Azure services, and you can debug them on your local computer using the full Functions runtime.
	Functions giúp bạn dễ dàng sử dụng trình soạn thảo mã và công cụ phát triển yêu thích để tạo và kiểm thử các hàm trên máy tính cục bộ của mình. Các hàm cục bộ của bạn có thể kết nối với các dịch vụ Azure đang hoạt động và bạn có thể gỡ lỗi chúng trên máy tính cục bộ bằng cách sử dụng môi trường chạy Functions đầy đủ.

The way in which you develop functions on your local computer depends on your language and tooling preferences. For more information, see [Code and test Azure Functions locally](https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local).
	Cách bạn phát triển các hàm trên máy tính cục bộ phụ thuộc vào ngôn ngữ và công cụ bạn ưa thích. Để biết thêm thông tin, hãy xem phần "Viết mã và kiểm thử Azure Functions cục bộ".
# Local project files
___
A Functions project directory contains the following files in the project root folder, regardless of language:
	Thư mục dự án Functions chứa các tệp sau trong thư mục gốc của dự án, bất kể ngôn ngữ nào:

- `host.json`
- `local.settings.json`
- Other files in the project depend on your language and specific functions.
	Các tệp khác trong dự án phụ thuộc vào ngôn ngữ và các hàm cụ thể của bạn.

The `host.json` metadata file contains configuration options that affect all functions in a function app instance. Other function app configuration options are managed depending on where the function app runs:
	Tệp siêu dữ liệu host.json chứa các tùy chọn cấu hình ảnh hưởng đến tất cả các hàm trong một phiên bản ứng dụng hàm. Các tùy chọn cấu hình ứng dụng hàm khác được quản lý tùy thuộc vào nơi ứng dụng hàm chạy:

- **Deployed to Azure:** Configured in your application settings
	Được triển khai trên Azure: Được cấu hình trong cài đặt ứng dụng của bạn
- **On your local computer:** Configured in the `local.settings.json` file.
	Trên máy tính cục bộ của bạn: Được cấu hình trong tệp local.settings.json.

Configurations in `host.json` related to bindings are applied equally to each function in the function app. You can also override or apply settings per environment using application settings. To learn more, see the [host.json reference](https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json).
	Các cấu hình trong host.json liên quan đến liên kết được áp dụng như nhau cho mỗi hàm trong ứng dụng hàm. Bạn cũng có thể ghi đè hoặc áp dụng cài đặt cho mỗi môi trường bằng cách sử dụng cài đặt ứng dụng. Để tìm hiểu thêm, hãy xem tài liệu tham khảo host.json.

The `local.settings.json` file stores app settings, and settings used by local development tools. Settings in the `local.settings.json` file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.
	Tệp local.settings.json lưu trữ cài đặt ứng dụng và cài đặt được sử dụng bởi các công cụ phát triển cục bộ. Cài đặt trong tệp local.settings.json chỉ được sử dụng khi bạn chạy dự án cục bộ. Khi bạn xuất bản dự án lên Azure, hãy đảm bảo cũng thêm bất kỳ cài đặt cần thiết nào vào cài đặt ứng dụng cho ứng dụng hàm.
# Synchronize settings
___
When you develop your functions locally, any local settings required by your app must also be present in the app settings of the deployed function app. You can also download current settings from the function app to your local project.
	Khi bạn phát triển các hàm cục bộ, bất kỳ cài đặt cục bộ nào mà ứng dụng của bạn yêu cầu cũng phải có trong cài đặt ứng dụng của hàm đã triển khai. Bạn cũng có thể tải xuống các cài đặt hiện tại từ hàm ứng dụng về dự án cục bộ của mình.
# Create triggers and bindings
A trigger defines how a function is invoked and a function must have exactly one trigger. Triggers have associated data, which is often provided as the payload of the function.
	Một trigger xác định cách thức gọi một hàm và một hàm phải có chính xác một trigger. Các trigger có dữ liệu liên kết, thường được cung cấp dưới dạng payload của hàm.

Binding to a function is a way of declaratively connecting another resource to the function; bindings might be connected as _input bindings_, _output bindings_, or both. Data from bindings is provided to the function as parameters.
	Liên kết (binding) với một hàm là một cách khai báo để kết nối một tài nguyên khác với hàm đó; các liên kết có thể được kết nối dưới dạng liên kết đầu vào, liên kết đầu ra hoặc cả hai. Dữ liệu từ các liên kết được cung cấp cho hàm dưới dạng tham số.

You can mix and match different bindings to suit your needs. Bindings are optional and a function might have one or multiple input and/or output bindings.
	Bạn có thể kết hợp các liên kết khác nhau để phù hợp với nhu cầu của mình. Liên kết là tùy chọn và một hàm có thể có một hoặc nhiều liên kết đầu vào và/hoặc đầu ra.

Triggers and bindings let you avoid hardcoding access to other services. Your function receives data (for example, the content of a queue message) in function parameters. You send data (for example, to create a queue message) by using the return value of the function.
	Trigger và binding cho phép bạn tránh việc mã hóa cứng quyền truy cập vào các dịch vụ khác. Hàm của bạn nhận dữ liệu (ví dụ: nội dung của một thông báo trong hàng đợi) trong các tham số của hàm. Bạn gửi dữ liệu (ví dụ: để tạo một thông báo trong hàng đợi) bằng cách sử dụng giá trị trả về của hàm.

When you develop your functions locally, you need to take trigger and binding behaviors into consideration. For HTTP triggers, you can call the HTTP endpoint on the local computer, using `http://localhost/`. For non-HTTP triggered functions, there are several options to run locally:
	Khi bạn phát triển các hàm của mình cục bộ, bạn cần phải xem xét hành vi của trigger và binding. Đối với trigger HTTP, bạn có thể gọi điểm cuối HTTP trên máy tính cục bộ, sử dụng http://localhost/. Đối với các hàm không được kích hoạt bằng HTTP, có một số tùy chọn để chạy cục bộ:

- The easiest way to test bindings during local development is to use connection strings that target live Azure services. You can target live services by adding the appropriate connection string settings in the `Values` array in the local.settings.json file. When you do this, local executions during testing use live service data. Because of this, consider setting-up separate services to use during development and testing, and then switch to different services during production.
	Cách dễ nhất để kiểm tra các liên kết trong quá trình phát triển cục bộ là sử dụng chuỗi kết nối nhắm mục tiêu đến các dịch vụ Azure đang hoạt động. Bạn có thể nhắm mục tiêu đến các dịch vụ đang hoạt động bằng cách thêm các thiết lập chuỗi kết nối thích hợp vào mảng Values ​​trong tệp local.settings.json. Khi bạn làm như vậy, các lần thực thi cục bộ trong quá trình thử nghiệm sẽ sử dụng dữ liệu dịch vụ đang hoạt động. Vì vậy, hãy cân nhắc thiết lập các dịch vụ riêng biệt để sử dụng trong quá trình phát triển và thử nghiệm, sau đó chuyển sang các dịch vụ khác trong quá trình sản xuất.
- For storage-based triggers, you can use the local [Azurite emulator](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azurite) when testing functions with Azure Storage bindings (Queue Storage, Blob Storage, and Table Storage), without having to connect to remote storage services.
	Đối với các trình kích hoạt dựa trên lưu trữ, bạn có thể sử dụng trình giả lập Azurite cục bộ khi kiểm tra các hàm với các liên kết Azure Storage (Queue Storage, Blob Storage và Table Storage), mà không cần phải kết nối với các dịch vụ lưu trữ từ xa.
- You can manually run non-HTTP trigger functions by using special administrator endpoints. For more information, see [Manually run a non HTTP-triggered function](https://learn.microsoft.com/en-us/azure/azure-functions/functions-manually-run-non-http).
	Bạn có thể chạy thủ công các hàm kích hoạt không phải HTTP bằng cách sử dụng các điểm cuối quản trị viên đặc biệt. Để biết thêm thông tin, hãy xem Chạy thủ công một hàm không được kích hoạt bằng HTTP.
# Trigger and binding definitions
___
Triggers and bindings are defined differently depending on the development language and runtime model.
	Các trình kích hoạt và liên kết được định nghĩa khác nhau tùy thuộc vào ngôn ngữ lập trình và mô hình thời gian chạy.

| Language              | Configure triggers and bindings by...                                                                                                                                                                                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| C# class library      | decorating methods and parameters with C# attributes (in-process or isolated worker)<br><br>Bài trí các phương thức và tham số bằng thuộc tính C# (trong tiến trình hoặc trình xử lý độc lập)                                                                                          |
| Java                  | decorating methods and parameters with Java annotations<br><br>Bài trí các phương thức và tham số bằng chú thích Java                                                                                                                                                                  |
| JavaScript/TypeScript | v4 programming model: define inputs/outputs in code using @azure/functions; v3: configure in a per-function function.json<br><br>Mô hình lập trình v4: định nghĩa đầu vào/đầu ra trong mã bằng cách sử dụng @azure/functions; v3: cấu hình trong tệp function.json riêng cho từng hàm. |
| Python                | v2 programming model: define inputs/outputs with decorators; v1: configure in function.json<br><br>Mô hình lập trình v2: định nghĩa đầu vào/đầu ra bằng decorator; v1: cấu hình trong function.json                                                                                    |
| PowerShell            | configure in function.json<br><br>cấu hình trong function.json                                                                                                                                                                                                                         |

For languages that rely on _function.json_ (for example, Node.js v3, Python v1, and PowerShell), the portal provides a UI for adding bindings in the **Integration** tab. You can also edit the file directly in the portal in the **Code + test** tab of your function. For code-first models like Node.js v4 and Python v2, configure bindings in code in your local project; the portal reflects configuration but might not support direct edits.
	Đối với các ngôn ngữ dựa vào function.json (ví dụ: Node.js v3, Python v1 và PowerShell), cổng thông tin cung cấp giao diện người dùng để thêm các liên kết trong tab Tích hợp. Bạn cũng có thể chỉnh sửa trực tiếp tệp này trong cổng thông tin ở tab Mã + kiểm thử của hàm. Đối với các mô hình ưu tiên mã như Node.js v4 và Python v2, hãy cấu hình các liên kết trong mã trong dự án cục bộ của bạn; cổng thông tin sẽ phản ánh cấu hình nhưng có thể không hỗ trợ chỉnh sửa trực tiếp.

In .NET and Java, the parameter type defines the data type for input data. For instance, use `string` to bind to the text of a queue trigger, a byte array to read as binary, and a custom type to deserialize to an object. Since .NET class library functions and Java functions don't rely on _function.json_ for binding definitions, they can't be created and edited in the portal. C# portal editing is based on C# script, which uses _function.json_ instead of attributes.
	Trong .NET và Java, kiểu tham số xác định kiểu dữ liệu cho dữ liệu đầu vào. Ví dụ: sử dụng chuỗi để liên kết với văn bản của trình kích hoạt hàng đợi, mảng byte để đọc dưới dạng nhị phân và kiểu tùy chỉnh để giải mã thành đối tượng. Vì các hàm thư viện lớp .NET và các hàm Java không dựa vào function.json để định nghĩa liên kết, nên chúng không thể được tạo và chỉnh sửa trong cổng thông tin. Chỉnh sửa C# trong cổng thông tin dựa trên tập lệnh C#, sử dụng function.json thay vì thuộc tính.

For languages that are dynamically typed such as JavaScript (using the v3 model) or PowerShell, use the `dataType` property in the _function.json_ file. For example, to read the content of an HTTP request in binary format, set `dataType` to `binary`:
	Đối với các ngôn ngữ kiểu động như JavaScript (sử dụng mô hình v3) hoặc PowerShell, hãy sử dụng thuộc tính `dataType` trong tệp `function.json`. Ví dụ, để đọc nội dung của yêu cầu HTTP ở định dạng nhị phân, hãy đặt `dataType` thành `binary`:

JSON
```
{
    "dataType": "binary",
    "type": "httpTrigger",
    "name": "req",
    "direction": "in"
}
```

Other options for `dataType` are `stream` and `string`.
	Các tùy chọn khác cho `dataType` là `stream` và `string`.
# Binding direction
___
All triggers and bindings have a direction property in the _function.json_ file:
	Tất cả các trình kích hoạt và liên kết đều có thuộc tính `direction` trong tệp `function.json`:

- For triggers, the direction is always `in`
	Đối với trình kích hoạt, hướng luôn là `in`
- Input and output bindings use `in` and `out`
	Các liên kết đầu vào và đầu ra sử dụng `in` và `out`
- Some bindings support a special direction `inout`. If you use `inout`, only the **Advanced editor** is available via the **Integrate** tab in the portal.
	Một số liên kết hỗ trợ hướng đặc biệt `inout`. Nếu bạn sử dụng `inout`, chỉ có trình chỉnh sửa Nâng cao khả dụng thông qua tab Tích hợp trong cổng thông tin.

When you use attributes in a class library to configure triggers and bindings, the direction is provided in an attribute constructor or inferred from the parameter type.
	Khi bạn sử dụng các thuộc tính trong thư viện lớp để cấu hình trình kích hoạt và liên kết, hướng được cung cấp trong hàm tạo thuộc tính hoặc được suy ra từ kiểu tham số.

# Azure Functions trigger and binding examples
___
Suppose you want to write a message to Azure Queue storage whenever an HTTP request is received. You can implement this with an HTTP trigger and a Storage Queue output binding. The configuration approach depends on your language and programming model.
	Giả sử bạn muốn ghi một thông báo vào bộ nhớ Azure Queue mỗi khi nhận được yêu cầu HTTP. Bạn có thể thực hiện điều này bằng cách sử dụng trình kích hoạt HTTP và liên kết đầu ra Storage Queue. Cách cấu hình phụ thuộc vào ngôn ngữ và mô hình lập trình của bạn.

Here's a legacy _function.json_ file for this scenario (applicable to Node.js v3, Python v1, or PowerShell).
	Đây là một tệp function.json cũ cho trường hợp này (áp dụng cho Node.js v3, Python v1 hoặc PowerShell).

JSON
```
{
    "disabled": false,
    "bindings": [
        {
            "type": "httpTrigger",
            "direction": "in",
            "name": "req",
            "authLevel": "function",
            "methods": ["get","post"]
        },
                {
                    "type": "queue",
                    "direction": "out",
                    "name": "outqueue",
                    "queueName": "outqueue",
                    "connection": "AzureWebJobsStorage"
                }
  ]
}
```

The first element in the `bindings` array is the HTTP trigger. The `type` and `direction` properties identify the trigger. The `name` property identifies the function parameter that receives the HTTP request, and `methods` lists the supported HTTP verbs.
	Phần tử đầu tiên trong mảng bindings là trình kích hoạt HTTP. Các thuộc tính type và direction xác định trình kích hoạt. Thuộc tính name xác định tham số hàm nhận yêu cầu HTTP, và methods liệt kê các động từ HTTP được hỗ trợ.

The second element in the `bindings` array is the Storage Queue output binding. The `type` and `direction` properties identify the binding. The `name` property specifies how the function provides the new queue message, the `queueName` identifies the queue, and `connection` refers to the app setting that holds the storage connection string.
	Phần tử thứ hai trong mảng bindings là liên kết đầu ra Storage Queue. Các thuộc tính type và direction xác định liên kết. Thuộc tính name chỉ định cách hàm cung cấp thông báo hàng đợi mới, queueName xác định hàng đợi, và connection đề cập đến cài đặt ứng dụng chứa chuỗi kết nối lưu trữ.
# C# (isolated worker) example
___
This example shows an HTTP-triggered function that writes a message to a Storage Queue using an output binding defined by attributes. For more information, see [C# isolated worker guide](https://learn.microsoft.com/en-us/azure/azure-functions/dotnet-isolated-process-guide).
	Ví dụ này minh họa một hàm được kích hoạt bởi HTTP, ghi một thông báo vào Hàng đợi lưu trữ bằng cách sử dụng liên kết đầu ra được định nghĩa bởi các thuộc tính. Để biết thêm thông tin, hãy xem [hướng dẫn về worker độc lập trong C#](https://learn.microsoft.com/en-us/azure/azure-functions/dotnet-isolated-process-guide).

C#
```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;

public static class HttpToQueue
{
    [Function("HttpToQueue")]
    public static MultiResponse Run(
        [HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req)
    {
        var message = "Processed request";
        return new MultiResponse
        {
            Messages = new[] { message },
            HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.OK)
        };
    }
}

public class MultiResponse
{
    [QueueOutput("outqueue", Connection = "AzureWebJobsStorage")]
    public string[] Messages { get; set; }
    public HttpResponseData HttpResponse { get; set; }
}
```

# Node.js (v4 programming model) example
___
In the v4 Node.js programming model, you configure inputs and outputs in code using `@azure/functions`. For more information, see [Node.js developer guide (v4)](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-node?pivots=nodejs-model-v4#inputs-and-outputs).
	Trong mô hình lập trình Node.js v4, bạn cấu hình đầu vào và đầu ra trong mã bằng cách sử dụng `@azure/functions`. Để biết thêm thông tin, hãy xem [Hướng dẫn dành cho nhà phát triển Node.js (v4)](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-node?pivots=nodejs-model-v4#inputs-and-outputs).

JavaScript
```
import { app, output } from "@azure/functions";

const queueOutput = output.storageQueue({
  queueName: "outqueue",
  connection: "AzureWebJobsStorage"
});

app.http("HttpToQueue", {
  methods: ["GET", "POST"],
  authLevel: "function",
  extraOutputs: [queueOutput],
  handler: async (request, context) => {
    const body = await request.text();
    context.extraOutputs.set(queueOutput, body || "Processed request");
    return { status: 200, body: "Queued" };
  }
});
```

# Python (v2 programming model) example
___
In the v2 Python programming model, you use decorators to define bindings. The runtime generates _function.json_ for you. Visit the [Python developer guide](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-python) for more information.
	Trong mô hình lập trình Python v2, bạn sử dụng decorator để định nghĩa các liên kết. Môi trường runtime sẽ tự động tạo tệp _function.json_ cho bạn. Truy cập [Hướng dẫn dành cho nhà phát triển Python](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-python) để biết thêm thông tin.

Python
```
import azure.functions as func

app = func.FunctionApp()

@app.route(route="HttpToQueue", auth_level=func.AuthLevel.FUNCTION)
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpToQueue(req: func.HttpRequest, msg: func.Out[str]) -> func.HttpResponse:
    body = req.get_body().decode("utf-8") if req.get_body() else "Processed request"
    msg.set(body)
    return func.HttpResponse("Queued", status_code=200)
```

# Connect functions to Azure services
___
As a security best practice, Azure Functions takes advantage of the application settings functionality of Azure App Service to help you more securely store strings, keys, and other tokens required to connect to other services. Application settings in Azure are stored encrypted and accessed at runtime by your app as environment variable `name` `value` pairs. For triggers and bindings that require a connection property, you set the application setting name instead of the actual connection string. You can't configure a binding directly with a connection string or key.
	Để đảm bảo an toàn, Azure Functions tận dụng chức năng cài đặt ứng dụng của Azure App Service để giúp bạn lưu trữ an toàn hơn các chuỗi ký tự, khóa và các mã thông báo khác cần thiết để kết nối với các dịch vụ khác. Cài đặt ứng dụng trong Azure được lưu trữ mã hóa và được ứng dụng của bạn truy cập trong thời gian chạy dưới dạng các cặp giá trị tên biến môi trường. Đối với các trình kích hoạt và liên kết yêu cầu thuộc tính kết nối, bạn đặt tên cài đặt ứng dụng thay vì chuỗi kết nối thực tế. Bạn không thể cấu hình liên kết trực tiếp bằng chuỗi kết nối hoặc khóa.

The default configuration provider uses environment variables. These variables are defined in application settings when running in the Azure and in the local settings file when developing locally.
	Nhà cung cấp cấu hình mặc định sử dụng các biến môi trường. Các biến này được định nghĩa trong cài đặt ứng dụng khi chạy trên Azure và trong tệp cài đặt cục bộ khi phát triển cục bộ.

# Configure an identity-based connection
___
Some connections in Azure Functions are configured to use an identity instead of a secret. Support depends on the extension using the connection. In some cases, a connection string might still be required in Functions even though the service to which you're connecting supports identity-based connections.
	Một số kết nối trong Azure Functions được cấu hình để sử dụng định danh thay vì bí mật. Việc hỗ trợ phụ thuộc vào tiện ích mở rộng sử dụng kết nối. Trong một số trường hợp, chuỗi kết nối vẫn có thể được yêu cầu trong Functions ngay cả khi dịch vụ mà bạn đang kết nối hỗ trợ kết nối dựa trên định danh.
When hosted in the Azure Functions service, identity-based connections use a managed identity. The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential` and `clientID` properties. Configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized.
	Khi được lưu trữ trong dịch vụ Azure Functions, các kết nối dựa trên định danh sử dụng định danh được quản lý. Định danh do hệ thống gán được sử dụng theo mặc định, mặc dù định danh do người dùng gán có thể được chỉ định bằng các thuộc tính `credential` và `clientID`. Việc cấu hình định danh do người dùng gán với ID tài nguyên **không** được hỗ trợ. Khi chạy trong các ngữ cảnh khác, chẳng hạn như phát triển cục bộ, định danh nhà phát triển của bạn sẽ được sử dụng thay thế, mặc dù điều này có thể được tùy chỉnh.
# Grant permission to the identity
___
Identities must have permissions to perform the intended actions. This is typically done by assigning a role in Azure role-based access control, or specifying the identity in an access policy depending on the service to which you're connecting.
	Các định danh phải có quyền thực hiện các hành động dự định. Điều này thường được thực hiện bằng cách gán vai trò trong kiểm soát truy cập dựa trên vai trò của Azure hoặc chỉ định định danh trong chính sách truy cập tùy thuộc vào dịch vụ mà bạn đang kết nối.