Instrumenting and monitoring your apps helps you maximize their availability and performance.
	Việc tích hợp và giám sát ứng dụng giúp bạn tối đa hóa tính khả dụng và hiệu suất của chúng.

After completing this module, you'll be able to:
	Sau khi hoàn thành mô-đun này, bạn sẽ có thể:

- Describe how Application Insights works and how it collects events and metrics.
	Mô tả cách Application Insights hoạt động và cách nó thu thập các sự kiện và số liệu.
- Instrument an app for monitoring, and perform availability tests.
	Tích hợp ứng dụng để giám sát và thực hiện các bài kiểm tra tính khả dụng.
- Use Application Map to help you monitor performance and troubleshoot issues.
	Sử dụng Application Map để giúp bạn giám sát hiệu suất và khắc phục sự cố.

# Explore Application Insights
___

Application Insights is an extension of Azure Monitor and provides Application Performance Monitoring (APM) features. APM tools are useful to monitor applications from development, through test, and into production in the following ways:
	Application Insights là một phần mở rộng của Azure Monitor và cung cấp các tính năng Giám sát Hiệu suất Ứng dụng (APM). Các công cụ APM rất hữu ích để giám sát các ứng dụng từ giai đoạn phát triển, thử nghiệm cho đến khi đưa vào sản xuất theo các cách sau:

- Proactively understand how an application is performing.
	Chủ động hiểu được hiệu suất của ứng dụng.
- Reactively review application execution data to determine the cause of an incident.
	Phản ứng bằng cách xem xét dữ liệu thực thi ứng dụng để xác định nguyên nhân của sự cố.

In addition to collecting metrics and application telemetry data, which describe application activities and health, Application Insights can also be used to collect and store application trace logging data.
	Ngoài việc thu thập các chỉ số và dữ liệu đo từ xa của ứng dụng, mô tả các hoạt động và tình trạng của ứng dụng, Application Insights cũng có thể được sử dụng để thu thập và lưu trữ dữ liệu nhật ký theo dõi ứng dụng.

The log trace is associated with other telemetry to give a detailed view of the activity. Adding trace logging to existing apps only requires providing a destination for the logs; the logging framework rarely needs to be changed.
	Dấu vết nhật ký được liên kết với các dữ liệu đo từ xa khác để cung cấp cái nhìn chi tiết về hoạt động. Việc thêm tính năng ghi nhật ký theo dõi vào các ứng dụng hiện có chỉ cần cung cấp đích đến cho nhật ký; khung ghi nhật ký hiếm khi cần phải thay đổi.

## Application Insights feature overview

Features include, but not limited to:
	Các tính năng bao gồm, nhưng không giới hạn ở:

| Feature                            | Description                                                                                                                                                                                                                                                                                                                                            |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Live Metrics                       | Observe activity from your deployed application in real time with no effect on the host environment.<br><br>Quan sát hoạt động của ứng dụng đã triển khai trong thời gian thực mà không ảnh hưởng đến môi trường máy chủ.                                                                                                                              |
| Availability                       | Also known as _Synthetic Transaction Monitoring_, probe your applications external endpoints to test the overall availability and responsiveness over time.<br><br>Còn được gọi là _Giám sát giao dịch tổng hợp_, công cụ này sẽ kiểm tra các điểm cuối bên ngoài của ứng dụng để đánh giá tính khả dụng và khả năng phản hồi tổng thể theo thời gian. |
| GitHub or Azure DevOps integration | Create GitHub or Azure DevOps work items in context of Application Insights data.<br><br>Tạo các mục công việc GitHub hoặc Azure DevOps trong ngữ cảnh dữ liệu Application Insights.                                                                                                                                                                   |
| Usage                              | Understand which features are popular with users and how users interact and use your application<br><br>Hiểu rõ những tính năng nào được người dùng yêu thích và cách người dùng tương tác và sử dụng ứng dụng của bạn.                                                                                                                                |
| Smart Detection                    | Automatic failure and anomaly detection through proactive telemetry analysis.<br><br>Tự động phát hiện lỗi và bất thường thông qua phân tích dữ liệu đo từ xa chủ động.                                                                                                                                                                                |
| Application Map                    | A high level top-down view of the application architecture and at-a-glance visual references to component health and responsiveness.<br><br>Tổng quan cấp cao về kiến ​​trúc ứng dụng và các thông tin trực quan về tình trạng hoạt động và khả năng phản hồi của các thành phần.                                                                      |
| Distributed Tracing                | Search and visualize an end-to-end flow of a given execution or transaction.<br><br>Tìm kiếm và trực quan hóa toàn bộ quy trình thực thi hoặc giao dịch.                                                                                                                                                                                               |

## What Application Insights monitors

Application Insights collects Metrics and application Telemetry data, which describe application activities and health, as well as trace logging data.
	Application Insights thu thập các chỉ số và dữ liệu đo lường ứng dụng, mô tả hoạt động và tình trạng của ứng dụng, cũng như dữ liệu nhật ký theo dõi.

- **Request rates, response times, and failure rates** - Find out which pages are most popular, at what times of day, and where your users are. See which pages perform best. If your response times and failure rates go high when there are more requests, then perhaps you have a resourcing problem.
	**Tỷ lệ yêu cầu, thời gian phản hồi và tỷ lệ lỗi** - Tìm hiểu trang nào phổ biến nhất, vào thời điểm nào trong ngày và người dùng của bạn ở đâu. Xem trang nào hoạt động tốt nhất. Nếu thời gian phản hồi và tỷ lệ lỗi tăng cao khi có nhiều yêu cầu, thì có thể bạn đang gặp vấn đề về tài nguyên.
- **Dependency rates, response times, and failure rates** - Find out whether external services are slowing you down.
	**Tỷ lệ phụ thuộc, thời gian phản hồi và tỷ lệ lỗi** - Tìm hiểu xem các dịch vụ bên ngoài có làm chậm hoạt động của bạn hay không.
- **Exceptions** - Analyze the aggregated statistics, or pick specific instances and drill into the stack trace and related requests. Both server and browser exceptions are reported.
	**Ngoại lệ** - Phân tích số liệu thống kê tổng hợp, hoặc chọn các trường hợp cụ thể và xem chi tiết dấu vết ngăn xếp và các yêu cầu liên quan. Cả ngoại lệ máy chủ và trình duyệt đều được báo cáo.
- **Page views and load performance** - reported by your users' browsers.
	**Lượt xem trang và hiệu suất tải** - được báo cáo bởi trình duyệt của người dùng.
- **AJAX calls** from web pages - rates, response times, and failure rates.
	**Các cuộc gọi AJAX** từ các trang web - tỷ lệ, thời gian phản hồi và tỷ lệ lỗi.
- **User and session counts**.
	**Số lượng người dùng và phiên**.
- **Performance counters** from your Windows or Linux server machines, such as CPU, memory, and network usage.
	**Bộ đếm hiệu năng** từ máy chủ Windows hoặc Linux của bạn, chẳng hạn như CPU, bộ nhớ và mức sử dụng mạng.
- **Host diagnostics** from Docker or Azure.
	**Chẩn đoán máy chủ** từ Docker hoặc Azure.
- **Diagnostic trace logs** from your app - so that you can correlate trace events with requests.
	**Nhật ký theo dõi chẩn đoán** từ ứng dụng của bạn - để bạn có thể đối chiếu các sự kiện theo dõi với các yêu cầu.
- **Custom events and metrics** that you write yourself in the client or server code, to track business events such as items sold or games won.
	**Các sự kiện và số liệu tùy chỉnh** do chính bạn viết trong mã máy khách hoặc máy chủ, để theo dõi các sự kiện kinh doanh như số mặt hàng đã bán hoặc số trò chơi đã thắng.

## Getting started with Application Insights

Application Insights is one of the many services hosted within Microsoft Azure, and telemetry is sent there for analysis and presentation. It's free to sign up, and if you choose the basic pricing plan of Application Insights, there's no charge until your application has grown to have substantial usage.
	Application Insights là một trong nhiều dịch vụ được lưu trữ trong Microsoft Azure, và dữ liệu đo lường được gửi đến đó để phân tích và trình bày. Việc đăng ký là miễn phí, và nếu bạn chọn gói giá cơ bản của Application Insights, bạn sẽ không phải trả phí cho đến khi ứng dụng của bạn phát triển và có mức sử dụng đáng kể.

There are several ways to get started monitoring and analyzing app performance:
	Có một số cách để bắt đầu giám sát và phân tích hiệu suất ứng dụng:

- **At run time:** instrument your web app on the server. Ideal for applications already deployed. Avoids any update to the code.
	**Trong thời gian chạy:** tích hợp công cụ vào ứng dụng web của bạn trên máy chủ. Lý tưởng cho các ứng dụng đã được triển khai. Tránh mọi cập nhật mã.
- **At development time:** add Application Insights to your code. Allows you to customize telemetry collection and send more telemetry.
	**Trong quá trình phát triển:** thêm Application Insights vào mã của bạn. Cho phép bạn tùy chỉnh việc thu thập dữ liệu đo lường và gửi nhiều dữ liệu đo lường hơn.
- **Instrument your web pages** for page view, AJAX, and other client-side telemetry.
	**Tích hợp công cụ vào các trang web của bạn** để thu thập dữ liệu đo lường lượt xem trang, AJAX và các dữ liệu đo lường phía máy khách khác.
- **Analyze mobile app usage** by integrating with Visual Studio App Center.
	**Phân tích việc sử dụng ứng dụng di động** bằng cách tích hợp với Visual Studio App Center.
- **Availability tests** - ping your website regularly from our servers.
	**Kiểm tra tính khả dụng** - thường xuyên kiểm tra trạng thái trang web của bạn từ máy chủ của chúng tôi.

# Discover log-based metrics
___

Application Insights log-based metrics let you analyze the health of your monitored apps, create powerful dashboards, and configure alerts. There are two kinds of metrics:
	Các chỉ số dựa trên nhật ký của Application Insights cho phép bạn phân tích tình trạng hoạt động của các ứng dụng được giám sát, tạo bảng điều khiển mạnh mẽ và cấu hình cảnh báo. Có hai loại chỉ số:

- **Log-based metrics** behind the scene are translated into [Kusto queries](https://learn.microsoft.com/en-us/azure/kusto/query/) from stored events.
	**Chỉ số dựa trên nhật ký** được dịch thành [truy vấn Kusto](https://learn.microsoft.com/en-us/azure/kusto/query/) từ các sự kiện đã lưu trữ.
- **Standard metrics** are stored as preaggregated time series.
	**Chỉ số tiêu chuẩn** được lưu trữ dưới dạng chuỗi thời gian được tổng hợp trước.

Since _standard metrics_ are preaggregated during collection, they have better performance at query time. Standard metrics are a better choice for dashboarding and in real-time alerting. The _log-based metrics_ have more dimensions, which makes them the superior option for data analysis and ad-hoc diagnostics. Use the [namespace selector](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/metrics-getting-started#create-your-first-metric-chart) to switch between log-based and standard metrics in [metrics explorer](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/metrics-getting-started).
	Vì các chỉ số tiêu chuẩn được tổng hợp trước trong quá trình thu thập, chúng có hiệu suất tốt hơn khi truy vấn. Chỉ số tiêu chuẩn là lựa chọn tốt hơn cho việc tạo bảng điều khiển và cảnh báo thời gian thực. Các chỉ số dựa trên nhật ký có nhiều chiều hơn, điều này làm cho chúng trở thành lựa chọn vượt trội hơn cho việc phân tích dữ liệu và chẩn đoán tức thời. Sử dụng [bộ chọn không gian tên](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/metrics-getting-started#create-your-first-metric-chart) để chuyển đổi giữa các chỉ số dựa trên nhật ký và các chỉ số tiêu chuẩn trong [trình khám phá chỉ số](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/metrics-getting-started).

## Log-based metrics

Developers can use the SDK to send events manually (by writing code that explicitly invokes the SDK) or they can rely on the automatic collection of events from autoinstrumentation. In either case, the Application Insights backend stores all collected events as logs, and the Application Insights blades in the Azure portal act as an analytical and diagnostic tool for visualizing event-based data from logs.
	Các nhà phát triển có thể sử dụng SDK để gửi sự kiện theo cách thủ công (bằng cách viết mã gọi trực tiếp SDK) hoặc họ có thể dựa vào việc thu thập sự kiện tự động từ công cụ tự động đo lường. Trong cả hai trường hợp, hệ thống phụ trợ Application Insights sẽ lưu trữ tất cả các sự kiện đã thu thập dưới dạng nhật ký, và các bảng Application Insights trong cổng Azure hoạt động như một công cụ phân tích và chẩn đoán để trực quan hóa dữ liệu dựa trên sự kiện từ nhật ký.

Using logs to retain a complete set of events can bring great analytical and diagnostic value. For example, you can get an exact count of requests to a particular URL with the number of distinct users who made these calls. Or you can get detailed diagnostic traces, including exceptions and dependency calls for any user session. Having this type of information can significantly improve visibility into the application health and usage, allowing to cut down the time necessary to diagnose issues with an app.
	Việc sử dụng nhật ký để lưu giữ toàn bộ tập hợp sự kiện có thể mang lại giá trị phân tích và chẩn đoán tuyệt vời. Ví dụ, bạn có thể nhận được số lượng chính xác các yêu cầu đến một URL cụ thể cùng với số lượng người dùng khác nhau đã thực hiện các cuộc gọi này. Hoặc bạn có thể nhận được các dấu vết chẩn đoán chi tiết, bao gồm các ngoại lệ và các cuộc gọi phụ thuộc cho bất kỳ phiên người dùng nào. Việc có loại thông tin này có thể cải thiện đáng kể khả năng hiển thị về tình trạng và mức sử dụng ứng dụng, cho phép giảm thời gian cần thiết để chẩn đoán các sự cố với ứng dụng.

At the same time, collecting a complete set of events may be impractical (or even impossible) for applications that generate a large volume of telemetry. For situations when the volume of events is too high, Application Insights implements several telemetry volume reduction techniques, such as sampling and filtering that reduces the number of collected and stored events. Unfortunately, lowering the number of stored events also lowers the accuracy of the metrics that, behind the scenes, must perform query-time aggregations of the events stored in logs.
	Đồng thời, việc thu thập toàn bộ tập hợp sự kiện có thể không thực tế (hoặc thậm chí không thể) đối với các ứng dụng tạo ra một lượng lớn dữ liệu đo lường. Trong trường hợp khối lượng sự kiện quá lớn, Application Insights triển khai một số kỹ thuật giảm khối lượng dữ liệu đo từ xa, chẳng hạn như lấy mẫu và lọc để giảm số lượng sự kiện được thu thập và lưu trữ. Tuy nhiên, việc giảm số lượng sự kiện được lưu trữ cũng làm giảm độ chính xác của các chỉ số, vốn phải thực hiện tổng hợp các sự kiện được lưu trữ trong nhật ký tại thời điểm truy vấn.

## Preaggregated metrics

The preaggregated metrics aren't stored as individual events with lots of properties. Instead, they're stored as preaggregated time series, and only with key dimensions. This feature makes the new metrics superior at query time: retrieving data happens faster and requires less compute power. It also enables new scenarios such as near real-time alerting on dimensions of metrics, more responsive dashboards, and more.
	Các chỉ số được tổng hợp trước không được lưu trữ dưới dạng các sự kiện riêng lẻ với nhiều thuộc tính. Thay vào đó, chúng được lưu trữ dưới dạng chuỗi thời gian được tổng hợp trước, và chỉ với các chiều dữ liệu chính. Tính năng này giúp các chỉ số mới vượt trội hơn khi truy vấn: việc truy xuất dữ liệu diễn ra nhanh hơn và yêu cầu ít sức mạnh tính toán hơn. Nó cũng cho phép các kịch bản mới như cảnh báo gần thời gian thực trên các chiều dữ liệu, bảng điều khiển phản hồi nhanh hơn, v.v.

The newer SDKs ([Application Insights 2.7](https://www.nuget.org/packages/Microsoft.ApplicationInsights/2.7.2) SDK or later for .NET) preaggregate metrics during collection. This applies to [standard metrics sent by default](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/metrics-supported#microsoftinsightscomponents) so the accuracy isn't affected by sampling or filtering. It also applies to custom metrics sent using [GetMetric](https://learn.microsoft.com/en-us/azure/azure-monitor/app/api-custom-events-metrics#getmetric) resulting in less data ingestion and lower cost.
	Các SDK mới hơn ([Application Insights 2.7](https://www.nuget.org/packages/Microsoft.ApplicationInsights/2.7.2) SDK trở lên cho .NET) tổng hợp trước các chỉ số trong quá trình thu thập. Điều này áp dụng cho [các chỉ số tiêu chuẩn được gửi theo mặc định](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/metrics-supported#microsoftinsightscomponents) nên độ chính xác không bị ảnh hưởng bởi việc lấy mẫu hoặc lọc. Điều này cũng áp dụng cho các chỉ số tùy chỉnh được gửi bằng [GetMetric](https://learn.microsoft.com/en-us/azure/azure-monitor/app/api-custom-events-metrics#getmetric), dẫn đến việc thu thập dữ liệu ít hơn và chi phí thấp hơn.

For the SDKs that don't implement preaggregation the Application Insights backend still populates the new metrics by aggregating the events received by the Application Insights event collection endpoint. While you don't benefit from the reduced volume of data transmitted over the wire, you can still use the preaggregated metrics and experience better performance and support of the near real-time dimensional alerting with SDKs that don't preaggregate metrics during collection.
	Đối với các SDK không triển khai tính năng tổng hợp trước, hệ thống phụ trợ Application Insights vẫn sẽ điền các chỉ số mới bằng cách tổng hợp các sự kiện nhận được bởi điểm cuối thu thập sự kiện Application Insights. Mặc dù bạn không được hưởng lợi từ việc giảm lượng dữ liệu truyền qua mạng, bạn vẫn có thể sử dụng các chỉ số đã được tổng hợp trước và trải nghiệm hiệu suất tốt hơn cũng như hỗ trợ cảnh báo chiều gần thời gian thực với các SDK không tổng hợp trước các chỉ số trong quá trình thu thập.

It's worth mentioning that the collection endpoint preaggregates events before ingestion sampling, which means that [ingestion sampling](https://learn.microsoft.com/en-us/azure/azure-monitor/app/sampling) will never impact the accuracy of preaggregated metrics, regardless of the SDK version you use with your application.
	Điều đáng lưu ý là điểm cuối thu thập dữ liệu sẽ tổng hợp trước các sự kiện trước khi lấy mẫu để nhập dữ liệu, điều này có nghĩa là [lấy mẫu khi nhập dữ liệu](https://learn.microsoft.com/en-us/azure/azure-monitor/app/sampling) sẽ không bao giờ ảnh hưởng đến độ chính xác của các số liệu được tổng hợp trước, bất kể phiên bản SDK bạn sử dụng với ứng dụng của mình là gì.

# Instrument an app for monitoring
___

At a basic level, "instrumenting" is simply enabling an application to capture telemetry. There are two methods to instrument your application:
	Ở mức độ cơ bản, "cài đặt công cụ" chỉ đơn giản là cho phép một ứng dụng thu thập dữ liệu đo lường. Có hai phương pháp để cài đặt công cụ cho ứng dụng của bạn:

- Automatic instrumentation (autoinstrumentation)
	Cài đặt tự động (autoinstrumentation)
- Manual instrumentation
	Cài đặt thủ công

**Autoinstrumentation** enables telemetry collection through configuration without touching the application's code. Although it's more convenient, it tends to be less configurable. It's also not available in all languages. See [Autoinstrumentation supported environments and languages](https://learn.microsoft.com/en-us/azure/azure-monitor/app/codeless-overview). When autoinstrumentation is available, it's the easiest way to enable Azure Monitor Application Insights.
	**Cài đặt tự động** cho phép thu thập dữ liệu đo lường thông qua cấu hình mà không cần chỉnh sửa mã ứng dụng. Mặc dù tiện lợi hơn, nhưng phương pháp này thường ít tùy chỉnh hơn. Nó cũng không khả dụng trong tất cả các ngôn ngữ. Xem [Môi trường và ngôn ngữ được hỗ trợ bởi cài đặt tự động](https://learn.microsoft.com/en-us/azure/azure-monitor/app/codeless-overview). Khi cài đặt tự động khả dụng, đây là cách dễ nhất để kích hoạt Azure Monitor Application Insights.

**Manual instrumentation** is coding against the Application Insights or OpenTelemetry API. In the context of a user, it typically refers to installing a language-specific SDK in an application. This means that you have to manage the updates to the latest package version by yourself. You can use this option if you need to make custom dependency calls or API calls that aren't captured by default with autoinstrumentation. There are two options for manual instrumentation:
	**Cài đặt thủ công** là lập trình dựa trên API của Application Insights hoặc OpenTelemetry. Trong ngữ cảnh của người dùng, nó thường đề cập đến việc cài đặt SDK dành riêng cho ngôn ngữ trong ứng dụng. Điều này có nghĩa là bạn phải tự quản lý việc cập nhật lên phiên bản gói mới nhất. Bạn có thể sử dụng tùy chọn này nếu cần thực hiện các lệnh gọi phụ thuộc tùy chỉnh hoặc các lệnh gọi API không được ghi lại theo mặc định bằng tính năng tự động đo lường. Có hai tùy chọn để đo lường thủ công:

- [Application Insights SDKs](https://learn.microsoft.com/en-us/azure/azure-monitor/app/asp-net-core)
- [Azure Monitor OpenTelemetry Distros](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-enable).

## Enabling via Application Insights SDKs

You only need to install the Application Insights SDK in the following circumstances:
	Bạn chỉ cần cài đặt SDK Application Insights trong các trường hợp sau:

- You require custom events and metrics
	Bạn cần các sự kiện và số liệu tùy chỉnh
- You require control over the flow of telemetry
	Bạn cần kiểm soát luồng dữ liệu đo lường
- Auto-Instrumentation isn't available (typically due to language or platform limitations)
	Tính năng Tự động giám sát không khả dụng (thường do hạn chế về ngôn ngữ hoặc nền tảng)

To use the SDK, you install a small instrumentation package in your app and then instrument the web app, any background components, and JavaScript within the web pages. The app and its components don't have to be hosted in Azure. The instrumentation monitors your app and directs the telemetry data to an Application Insights resource by using a unique token.
	Để sử dụng SDK, bạn cài đặt một gói giám sát nhỏ trong ứng dụng của mình, sau đó giám sát ứng dụng web, bất kỳ thành phần chạy nền nào và JavaScript trong các trang web. Ứng dụng và các thành phần của nó không cần phải được lưu trữ trên Azure. Quá trình giám sát sẽ theo dõi ứng dụng của bạn và chuyển hướng dữ liệu đo lường đến tài nguyên Application Insights bằng cách sử dụng một mã thông báo duy nhất.

A list of SDK versions and names is hosted on GitHub. For more information, visit [SDK Version](https://github.com/microsoft/ApplicationInsights-dotnet/blob/develop/docs/versions_and_names.md).
	Danh sách các phiên bản và tên SDK được lưu trữ trên GitHub. Để biết thêm thông tin, hãy truy cập [Phiên bản SDK](https://github.com/microsoft/ApplicationInsights-dotnet/blob/develop/docs/versions_and_names.md).

## Enable via OpenTelemetry

Microsoft worked with project stakeholders from two previously popular open-source telemetry projects, [OpenCensus](https://opencensus.io/) and [OpenTracing](https://opentracing.io/). Together, we helped to create a single project, OpenTelemetry. OpenTelemetry includes contributions from all major cloud and Application Performance Management (APM) vendors and lives within the [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/). Microsoft is a Platinum Member of the CNCF.
	Microsoft đã hợp tác với các bên liên quan từ hai dự án đo lường từ xa mã nguồn mở phổ biến trước đây, [OpenCensus](https://opencensus.io/) và [OpenTracing](https://opentracing.io/). Cùng nhau, chúng tôi đã giúp tạo ra một dự án duy nhất, OpenTelemetry. OpenTelemetry bao gồm các đóng góp từ tất cả các nhà cung cấp điện toán đám mây và Quản lý Hiệu suất Ứng dụng (APM) lớn và thuộc [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/). Microsoft là Thành viên Bạch kim của CNCF.

Some legacy terms in Application Insights are confusing because of the industry convergence on OpenTelemetry. The following table highlights these differences. OpenTelemetry terms are replacing Application Insights terms.
	Một số thuật ngữ cũ trong Application Insights gây nhầm lẫn do sự hội tụ của ngành công nghiệp về OpenTelemetry. Bảng sau đây nêu bật những khác biệt này. Các thuật ngữ của OpenTelemetry đang thay thế các thuật ngữ của Application Insights.

|Application Insights|OpenTelemetry|
|---|---|
|Autocollectors|Instrumentation libraries|
|Channel|Exporter|
|Codeless / Agent-based|Autoinstrumentation|
|Traces|Logs|
|Requests|Server Spans|
|Dependencies|Other Span Types (Client, Internal, etc.)|
|Operation ID|Trace ID|
|ID or Operation Parent ID|Span ID|

# Select an availability test
___

After you deploy your web app or website, you can set up recurring tests to monitor availability and responsiveness. Application Insights sends web requests to your application at regular intervals from points around the world. It can alert you if your application isn't responding or responds too slowly. You can create up to 100 availability tests per Application Insights resource.
	Sau khi triển khai ứng dụng web hoặc trang web của bạn, bạn có thể thiết lập các bài kiểm tra định kỳ để theo dõi tính khả dụng và khả năng phản hồi. Application Insights gửi các yêu cầu web đến ứng dụng của bạn theo định kỳ từ các điểm trên khắp thế giới. Nó có thể cảnh báo bạn nếu ứng dụng của bạn không phản hồi hoặc phản hồi quá chậm. Bạn có thể tạo tối đa 100 bài kiểm tra tính khả dụng cho mỗi tài nguyên Application Insights.

Availability tests don't require any changes to the website you're testing and work for any HTTP or HTTPS endpoint that's accessible from the public internet. You can also test the availability of a REST API that your service depends on.
	Các bài kiểm tra tính khả dụng không yêu cầu bất kỳ thay đổi nào đối với trang web bạn đang kiểm tra và hoạt động với bất kỳ điểm cuối HTTP hoặc HTTPS nào có thể truy cập được từ internet công cộng. Bạn cũng có thể kiểm tra tính khả dụng của API REST mà dịch vụ của bạn phụ thuộc vào.

You can create up to 100 availability tests per Application Insights resource, and there are three types of availability tests:
	Bạn có thể tạo tối đa 100 bài kiểm tra tính khả dụng cho mỗi tài nguyên Application Insights, và có ba loại bài kiểm tra tính khả dụng:

- **Standard test:** This is a type of availability test that checks the availability of a website by sending a single request, similar to the deprecated URL ping test. In addition to validating whether an endpoint is responding and measuring the performance, Standard tests also include TLS/SSL certificate validity, proactive lifetime check, HTTP request verb (for example, `GET`,`HEAD`, and `POST`), custom headers, and custom data associated with your HTTP request.
    **Kiểm tra tiêu chuẩn:** Đây là loại kiểm tra tính khả dụng kiểm tra tính khả dụng của một trang web bằng cách gửi một yêu cầu duy nhất, tương tự như bài kiểm tra ping URL đã lỗi thời. Ngoài việc xác thực xem điểm cuối có phản hồi hay không và đo lường hiệu suất, các bài kiểm tra Tiêu chuẩn cũng bao gồm tính hợp lệ của chứng chỉ TLS/SSL, kiểm tra thời gian tồn tại chủ động, động từ yêu cầu HTTP (ví dụ: `GET`, `HEAD` và `POST`), tiêu đề tùy chỉnh và dữ liệu tùy chỉnh liên quan đến yêu cầu HTTP của bạn.
- **Custom TrackAvailability test:** If you decide to create a custom application to run availability tests, you can use the [TrackAvailability()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) method to send the results to Application Insights.
    **Kiểm tra TrackAvailability tùy chỉnh:** Nếu bạn quyết định tạo một ứng dụng tùy chỉnh để chạy các bài kiểm tra tính khả dụng, bạn có thể sử dụng phương thức [TrackAvailability()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) để gửi kết quả đến Application Insights.
- [URL ping test (classic)](https://learn.microsoft.com/en-us/azure/azure-monitor/app/monitor-web-app-availability): You can create this test through the portal to validate whether an endpoint is responding and measure performance associated with that response. You can also set custom success criteria coupled with more advanced features, like parsing dependent requests and allowing for retries.
	[Kiểm tra ping URL (cổ điển)](https://learn.microsoft.com/en-us/azure/azure-monitor/app/monitor-web-app-availability): Bạn có thể tạo bài kiểm tra này thông qua cổng thông tin để xác thực xem điểm cuối có phản hồi hay không và đo lường hiệu suất liên quan đến phản hồi đó. Bạn cũng có thể thiết lập các tiêu chí thành công tùy chỉnh kết hợp với các tính năng nâng cao hơn, chẳng hạn như phân tích các yêu cầu phụ thuộc và cho phép thử lại.

# Troubleshoot app performance by using Application Map
___

Application Map helps you spot performance bottlenecks or failure hotspots across all components of your distributed application. Each node on the map represents an application component or its dependencies; and has health key performance indicator and alerts status. You can select through from any component to more detailed diagnostics, such as Application Insights events. If your app uses Azure services, you can also select through to Azure diagnostics, such as SQL Database Advisor recommendations.
	Bản đồ ứng dụng giúp bạn phát hiện các điểm nghẽn hiệu năng hoặc điểm nóng lỗi trên tất cả các thành phần của ứng dụng phân tán. Mỗi nút trên bản đồ đại diện cho một thành phần ứng dụng hoặc các phần phụ thuộc của nó; và có chỉ số hiệu năng chính và trạng thái cảnh báo. Bạn có thể chọn từ bất kỳ thành phần nào để xem chẩn đoán chi tiết hơn, chẳng hạn như các sự kiện Application Insights. Nếu ứng dụng của bạn sử dụng các dịch vụ Azure, bạn cũng có thể chọn xem chẩn đoán Azure, chẳng hạn như các đề xuất của SQL Database Advisor.

Components are independently deployable parts of your distributed/microservices application. Developers and operations teams have code-level visibility or access to telemetry generated by these application components.
	Các thành phần là các phần có thể triển khai độc lập của ứng dụng phân tán/microservices của bạn. Các nhà phát triển và nhóm vận hành có khả năng xem mã hoặc truy cập vào dữ liệu đo từ xa được tạo bởi các thành phần ứng dụng này.

- Components are different from "observed" external dependencies such as SQL, Event Hubs, etc. which your team/organization may not have access to (code or telemetry).
	Các thành phần khác với các phần phụ thuộc bên ngoài "được quan sát" như SQL, Event Hubs, v.v., mà nhóm/tổ chức của bạn có thể không có quyền truy cập (mã hoặc dữ liệu đo từ xa).
- Components run on any number of server/role/container instances.
	Các thành phần chạy trên bất kỳ số lượng phiên bản máy chủ/vai trò/container nào.
- Components can be separate Application Insights instrumentation keys (even if subscriptions are different) or different roles reporting to a single Application Insights instrumentation key. The preview map experience shows the components regardless of their configuration.
	Các thành phần có thể là các khóa công cụ Application Insights riêng biệt (ngay cả khi đăng ký khác nhau) hoặc các vai trò khác nhau báo cáo cho một khóa công cụ Application Insights duy nhất. Trải nghiệm bản đồ xem trước hiển thị các thành phần bất kể cấu hình của chúng.

You can see the full application topology across multiple levels of related application components. Components could be different Application Insights resources, or different roles in a single resource. The app map finds components by following HTTP dependency calls made between servers with the Application Insights SDK installed.
	Bạn có thể xem toàn bộ cấu trúc ứng dụng trên nhiều cấp độ của các thành phần ứng dụng liên quan. Các thành phần có thể là các tài nguyên Application Insights khác nhau, hoặc các vai trò khác nhau trong cùng một tài nguyên. Bản đồ ứng dụng tìm các thành phần bằng cách theo dõi các cuộc gọi phụ thuộc HTTP được thực hiện giữa các máy chủ đã cài đặt SDK Application Insights.

This experience starts with progressive discovery of the components. When you first load the application map, a set of queries is triggered to discover the components related to this component. A button at the top-left corner updates with the number of components in your application as they're discovered.
	Trải nghiệm này bắt đầu bằng việc khám phá dần dần các thành phần. Khi bạn tải bản đồ ứng dụng lần đầu tiên, một tập hợp các truy vấn sẽ được kích hoạt để khám phá các thành phần liên quan đến thành phần này. Một nút ở góc trên bên trái sẽ cập nhật số lượng thành phần trong ứng dụng của bạn khi chúng được khám phá.

Selecting **Update map components** refreshes with all components discovered until that point. Depending on the complexity of your application, this may take a minute to load.
	Chọn **Cập nhật các thành phần bản đồ** sẽ làm mới với tất cả các thành phần đã được khám phá cho đến thời điểm đó. Tùy thuộc vào độ phức tạp của ứng dụng, quá trình này có thể mất một phút để tải.

If all of the components are roles within a single Application Insights resource, then this discovery step isn't required. The initial load for such an application has all its components.
	Nếu tất cả các thành phần đều là các vai trò trong cùng một tài nguyên Application Insights, thì bước khám phá này không cần thiết. Lần tải ban đầu cho một ứng dụng như vậy đã có tất cả các thành phần của nó.

![Application Map screenshot showing the initial load of an app where all of the components are roles within a single Application Insights resource.](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/media/application-map.png)

One of the key objectives with this experience is to be able to visualize complex topologies with hundreds of components. Select on any component to see related insights and go to the performance and failure triage experience for that component.
	Một trong những mục tiêu chính của trải nghiệm này là khả năng hình dung các cấu trúc phức tạp với hàng trăm thành phần. Chọn bất kỳ thành phần nào để xem thông tin chi tiết liên quan và chuyển đến trải nghiệm phân tích hiệu năng và lỗi cho thành phần đó.

![Screenshot showing component details in the Application Map.](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/media/application-map-component.png)

Application Map uses the cloud role name property to identify the components on the map. You can manually set or override the cloud role name and change what gets displayed on the Application Map.
	Bản đồ ứng dụng sử dụng thuộc tính tên vai trò đám mây để xác định các thành phần trên bản đồ. Bạn có thể thiết lập hoặc ghi đè tên vai trò đám mây theo cách thủ công và thay đổi những gì được hiển thị trên Bản đồ ứng dụng.