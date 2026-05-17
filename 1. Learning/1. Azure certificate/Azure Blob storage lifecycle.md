Data sets have unique lifecycles. Early in the lifecycle, people access some data often. But the need for access drops drastically as the data ages. Some data stays idle in the cloud and is rarely accessed once stored. Some data expires days or months after creation, while other data sets are actively read and modified throughout their lifetimes.
# Access tiers
___
Azure storage offers different access tiers, allowing you to store blob object data in the most cost-effective manner. Available access tiers include:
	Azure Storage cung cấp các cấp độ truy cập khác nhau, cho phép bạn lưu trữ dữ liệu đối tượng blob một cách tiết kiệm chi phí nhất. Các cấp độ truy cập khả dụng bao gồm:

- **Hot** - An online tier optimized for storing data that is accessed frequently.
	Hot - Cấp độ trực tuyến được tối ưu hóa để lưu trữ dữ liệu được truy cập thường xuyên.
- **Cool** - An online tier optimized for storing data that is infrequently accessed and stored for a minimum of 30 days.
	Cool - Cấp độ trực tuyến được tối ưu hóa để lưu trữ dữ liệu ít được truy cập và được lưu trữ tối thiểu 30 ngày.
- **Cold tier** - An online tier optimized for storing data that is infrequently accessed and stored for a minimum of 90 days. The cold tier has lower storage costs and higher access costs compared to the cool tier.
	Cold tier - Cấp độ trực tuyến được tối ưu hóa để lưu trữ dữ liệu ít được truy cập và được lưu trữ tối thiểu 90 ngày. Cấp độ Cold có chi phí lưu trữ thấp hơn và chi phí truy cập cao hơn so với cấp độ Cool.
- **Archive** - An offline tier optimized for storing data that is rarely accessed and stored for at least 180 days with flexible latency requirements, on the order of hours.
	Archive - Cấp độ ngoại tuyến được tối ưu hóa để lưu trữ dữ liệu hiếm khi được truy cập và được lưu trữ ít nhất 180 ngày với các yêu cầu độ trễ linh hoạt, theo thứ tự giờ.

Data storage limits are set at the account level and not per access tier. You can choose to use all of your limit in one tier or across all three tiers.
	Giới hạn lưu trữ dữ liệu được đặt ở cấp độ tài khoản chứ không phải theo từng cấp độ truy cập. Bạn có thể chọn sử dụng toàn bộ giới hạn của mình trong một cấp độ hoặc trên cả ba cấp độ.

# Manage the data lifecycle
___
Azure Blob Storage lifecycle management offers a rule-based policy that you can use to transition blob data to the appropriate access tiers or to expire data at the end of the data lifecycle.
	Quản lý vòng đời dữ liệu Azure Blob Storage cung cấp chính sách dựa trên quy tắc mà bạn có thể sử dụng để chuyển dữ liệu blob sang các cấp truy cập phù hợp hoặc để hết hạn dữ liệu khi kết thúc vòng đời dữ liệu.

With the lifecycle management policy, you can:
	Với chính sách quản lý vòng đời, bạn có thể:

- Transition blobs from cool to hot immediately when accessed, to optimize for performance.
	Chuyển đổi blob từ trạng thái "lạnh" sang "nóng" ngay lập tức khi được truy cập, để tối ưu hóa hiệu suất.
- Transition current versions of a blob, previous versions of a blob, or blob snapshots to a cooler storage tier if these objects aren't accessed or modified for a period of time, to optimize for cost.
	Chuyển đổi các phiên bản hiện tại của blob, các phiên bản trước đó của blob hoặc ảnh chụp nhanh blob sang cấp lưu trữ "lạnh" hơn nếu các đối tượng này không được truy cập hoặc sửa đổi trong một khoảng thời gian, để tối ưu hóa chi phí.

- Delete current versions of a blob, previous versions of a blob, or blob snapshots at the end of their lifecycles.
	Xóa các phiên bản hiện tại của blob, các phiên bản trước đó của blob hoặc ảnh chụp nhanh blob khi kết thúc vòng đời của chúng.

- Apply rules to an entire storage account, to select containers, or to a subset of blobs using name prefixes or blob index tags as filters.
	Áp dụng các quy tắc cho toàn bộ tài khoản lưu trữ, cho các vùng chứa được chọn hoặc cho một tập hợp con các blob bằng cách sử dụng tiền tố tên hoặc thẻ chỉ mục blob làm bộ lọc.

Consider a scenario where data is frequently accessed during the early stages of the lifecycle, but only occasionally after two weeks. Beyond the first month, the data set is rarely accessed. In this scenario, hot storage is best during the early stages. Cool storage is most appropriate for occasional access. Archive storage is the best tier option after the data ages over a month. By moving data to the appropriate storage tier based on its age with lifecycle management policy rules, you can design the least expensive solution for your needs.
	Hãy xem xét một kịch bản trong đó dữ liệu được truy cập thường xuyên trong giai đoạn đầu của vòng đời, nhưng chỉ thỉnh thoảng sau hai tuần. Sau tháng đầu tiên, tập dữ liệu hiếm khi được truy cập. Trong kịch bản này, lưu trữ "nóng" là tốt nhất trong giai đoạn đầu. Lưu trữ dữ liệu ở mức thấp (cool storage) phù hợp nhất cho việc truy cập không thường xuyên. Lưu trữ dữ liệu lâu dài (archive storage) là lựa chọn tốt nhất sau khi dữ liệu đã cũ hơn một tháng. Bằng cách di chuyển dữ liệu đến cấp lưu trữ phù hợp dựa trên tuổi đời của dữ liệu và áp dụng các quy tắc chính sách quản lý vòng đời, bạn có thể thiết kế giải pháp tiết kiệm chi phí nhất cho nhu cầu của mình.

# Discover Blob storage lifecycle policies
---
A lifecycle management policy is a collection of rules in a JSON document. Each rule definition within a policy includes a filter set and an action set. The filter set limits rule actions to a certain set of objects within a container or objects names. The action set applies the tier or delete actions to the filtered set of objects:
	Chính sách quản lý vòng đời là một tập hợp các quy tắc trong một tài liệu JSON. Mỗi định nghĩa quy tắc trong một chính sách bao gồm một tập hợp bộ lọc và một tập hợp hành động. Tập hợp bộ lọc giới hạn các hành động của quy tắc đối với một tập hợp đối tượng nhất định trong một vùng chứa hoặc tên đối tượng. Tập hợp hành động áp dụng các hành động phân cấp hoặc xóa cho tập hợp đối tượng đã được lọc:

JSON
```
{
  "rules": [
    {
      "name": "rule1",
      "enabled": true,
      "type": "Lifecycle",
      "definition": {...}
    },
    {
      "name": "rule2",
      "type": "Lifecycle",
      "definition": {...}
    }
  ]
}
```

A policy is a collection of rules:

| Parameter name | Parameter type           | Notes                                                                                  |
| -------------- | ------------------------ | -------------------------------------------------------------------------------------- |
| `rules`        | An array of rule objects | At least one rule is required in a policy. You can define up to 100 rules in a policy. |

Each rule within the policy has several parameters:

| Parameter name | Parameter type                            | Notes                                                                                                                                                                                                                                                                                     | Required |
| -------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| `name`         | String                                    | A rule name can include up to 256 alphanumeric characters. Rule name is case-sensitive. It must be unique within a policy.<br><br>Tên quy tắc có thể bao gồm tối đa 256 ký tự chữ và số. Tên quy tắc phân biệt chữ hoa chữ thường. Tên quy tắc phải là duy nhất trong toàn bộ chính sách. | True     |
| `enabled`      | Boolean                                   | An optional boolean to allow a rule to be temporarily disabled. Default value is true.                                                                                                                                                                                                    | False    |
| `type`         | An enum value                             | The current valid type is Lifecycle.                                                                                                                                                                                                                                                      | True     |
| `definition`   | An object that defines the lifecycle rule | Each definition is made up of a filter set and an action set.                                                                                                                                                                                                                             | True     |
# Rules
___
Each rule definition includes a filter set and an action set. The filter set limits rule actions to a certain set of objects within a container or objects names. The action set applies the tier or delete actions to the filtered set of objects.
	Mỗi định nghĩa quy tắc bao gồm một tập hợp bộ lọc và một tập hợp hành động. Tập hợp bộ lọc giới hạn các hành động của quy tắc đối với một tập hợp các đối tượng nhất định trong một vùng chứa hoặc theo tên đối tượng. Tập hợp hành động áp dụng các hành động phân cấp hoặc xóa cho tập hợp các đối tượng đã được lọc.

The following sample rule filters the account to run the actions on objects that exist inside `sample-container` and start with `blob1`.
	Quy tắc mẫu sau lọc tài khoản để chạy các hành động trên các đối tượng tồn tại bên trong `sample-container` và bắt đầu bằng `blob1`.

- Tier blob to cool tier 30 days after last modification
- Tier blob to archive tier 90 days after last modification
- Delete blob 2,555 days (seven years) after last modification
- Delete blob snapshots 90 days after snapshot creation
	- Phân cấp blob thành cấp độ lạnh 30 ngày sau lần sửa đổi cuối cùng
	- Phân cấp blob thành cấp độ lưu trữ 90 ngày sau lần sửa đổi cuối cùng
	- Xóa blob 2.555 ngày (bảy năm) sau lần sửa đổi cuối cùng
	- Xóa ảnh chụp nhanh blob 90 ngày sau khi tạo ảnh chụp nhanh

JSON
```
{
  "rules": [
    {
      "enabled": true,
      "name": "sample-rule",
      "type": "Lifecycle",
      "definition": {
        "actions": {
          "baseBlob": {
            "tierToCool": {
              "daysAfterModificationGreaterThan": 30
            },
            "tierToArchive": {
              "daysAfterModificationGreaterThan": 90,
              "daysAfterLastTierChangeGreaterThan": 7
            },
            "delete": {
              "daysAfterModificationGreaterThan": 2555
            }
          },
          "snapshot": {
            "delete": {
              "daysAfterCreationGreaterThan": 90
            }
          }
        },
        "filters": {
          "blobTypes": [
            "blockBlob"
          ],
          "prefixMatch": [
            "sample-container/blob1"
          ]
        }
      }
    }
  ]
}
```


# Rule filters
___
Filters limit rule actions to a subset of blobs within the storage account. If more than one filter is defined, a logical AND runs on all filters. Filters include:
	Bộ lọc giới hạn các hành động của quy tắc chỉ áp dụng cho một tập hợp con các blob trong tài khoản lưu trữ. Nếu có nhiều hơn một bộ lọc được định nghĩa, phép toán logic AND sẽ được thực thi trên tất cả các bộ lọc. Các bộ lọc bao gồm:

| Filter name    | Type                                                                                                                                                                                                                                                                                                                                               | Is Required |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| blobTypes      | An array of predefined enum values.                                                                                                                                                                                                                                                                                                                | Yes         |
| prefixMatch    | An array of strings for prefixes to be match. Each rule can define up to 10 prefixes. A prefix string must start with a container name.<br><br>Một mảng các chuỗi dùng để so khớp các tiền tố. Mỗi quy tắc có thể định nghĩa tối đa 10 tiền tố. Chuỗi tiền tố phải bắt đầu bằng tên của một vùng chứa.                                             | No          |
| blobIndexMatch | An array of dictionary values consisting of blob index tag key and value conditions to be matched. Each rule can define up to 10 blob index tag condition.<br><br>Một mảng các giá trị từ điển bao gồm các điều kiện về khóa và giá trị của thẻ chỉ mục blob cần được so khớp. Mỗi quy tắc có thể định nghĩa tối đa 10 điều kiện thẻ chỉ mục blob. | No          |

# Rule actions
___
Actions are applied to the filtered blobs when the run condition is met.
	Các hành động được áp dụng cho các blob đã lọc khi điều kiện chạy được đáp ứng.

Lifecycle management supports tiering and deletion of blobs and deletion of blob snapshots. Define at least one action for each rule on blobs or blob snapshots.
	Quản lý vòng đời hỗ trợ phân cấp và xóa blob cũng như xóa ảnh chụp nhanh blob. Xác định ít nhất một hành động cho mỗi quy tắc trên blob hoặc ảnh chụp nhanh blob.

| Action                      | Current Version                            | Snapshot      | Previous Versions |
| --------------------------- | ------------------------------------------ | ------------- | ----------------- |
| tierToCool                  | Supported for `blockBlob`                  | Supported     | Supported         |
| tierToCold                  | Supported for `blockBlob`                  | Supported     | Supported         |
| enableAutoTierToHotFromCool | Supported for `blockBlob`                  | Not supported | Not supported     |
| tierToArchive               | Supported for `blockBlob`                  | Supported     | Supported         |
| delete                      | Supported for `blockBlob` and `appendBlob` | Supported     | Supported         |
The run conditions are based on age. Base blobs use the last modified time to track age, and blob snapshots use the snapshot creation time to track age.
	Các điều kiện chạy dựa trên tuổi đời của các blob cơ bản. Các blob gốc sử dụng thời gian sửa đổi cuối cùng để theo dõi tuổi đời, còn các ảnh chụp nhanh blob sử dụng thời gian tạo ảnh chụp nhanh để theo dõi tuổi đời.

| Action run condition               | Condition value                                                           | Description                                                                                                                                                                                |
| ---------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| daysAfterModificationGreaterThan   | Integer value indicating the age in days                                  | The condition for base blob actions                                                                                                                                                        |
| daysAfterCreationGreaterThan       | Integer value indicating the age in days                                  | The condition for blob snapshot actions                                                                                                                                                    |
| daysAfterLastAccessTimeGreaterThan | Integer value indicating the age in days                                  | The condition for a current version of a blob when access tracking is enabled                                                                                                              |
| daysAfterLastTierChangeGreaterThan | Integer value indicating the age in days after last blob tier change time | The minimum duration in days that a rehydrated blob is kept in hot, cool, or cold tiers before being returned to the archive tier. This condition applies only to `tierToArchive` actions. |

# Implement Blob storage lifecycle policies
___
You can add, edit, or remove a policy by using any of the following methods:

- Azure portal
- Azure PowerShell
- Azure CLI
- REST APIs

The following are the steps and some examples for the Portal and Azure CLI.

## Azure portal
___
There are two ways to add a policy through the Azure portal: Azure portal List view, and Azure portal Code view. Following is an example of how to add a policy in the Azure portal Code view.

### Azure portal Code view
___
1. In the Azure portal, navigate to your storage account.
2. Under **Data management**, select **Lifecycle Management** to view or change lifecycle management policies.
3. Select the **Code View** tab. On this tab, you can define a lifecycle management policy in JSON.

The following JSON is an example of a policy that moves a block blob whose name begins with _log_ to the cool tier if it has been more than 30 days since the blob was modified.

JSON
```
{
  "rules": [
    {
      "enabled": true,
      "name": "move-to-cool",
      "type": "Lifecycle",
      "definition": {
        "actions": {
          "baseBlob": {
            "tierToCool": {
              "daysAfterModificationGreaterThan": 30
            }
          }
        },
        "filters": {
          "blobTypes": [
            "blockBlob"
          ],
          "prefixMatch": [
            "sample-container/log"
          ]
        }
      }
    }
  ]
}
```

## Azure CLI
___
To add a lifecycle management policy with Azure CLI, write the policy to a JSON file, then call the `az storage account management-policy create` command to create the policy.

Azure CLI

```
az storage account management-policy create \
    --account-name <storage-account> \
    --policy @policy.json \
    --resource-group <resource-group>
```

A lifecycle management policy must be read or written in full. Partial updates aren't supported.

# Rehydrate blob data from the archive tier
___
While a blob is in the archive access tier, it's considered to be offline and can't be read or modified. In order to read or modify data in an archived blob, you must first rehydrate the blob to an online tier, either the hot or cool tier. There are two options for rehydrating a blob that is stored in the archive tier:
	Trong khi một blob nằm ở tầng truy cập lưu trữ, nó được coi là ngoại tuyến và không thể đọc hoặc sửa đổi. Để đọc hoặc sửa đổi dữ liệu trong một blob đã được lưu trữ, trước tiên bạn phải khôi phục blob đó vào một tầng trực tuyến, hoặc tầng nóng hoặc tầng lạnh. Có hai tùy chọn để khôi phục một blob được lưu trữ trong tầng lưu trữ:

- **Copy an archived blob to an online tier**: You can rehydrate an archived blob by copying it to a new blob in the hot or cool tier with the [Copy Blob](https://learn.microsoft.com/en-us/rest/api/storageservices/copy-blob) or [Copy Blob from URL](https://learn.microsoft.com/en-us/rest/api/storageservices/copy-blob-from-url) operation. Microsoft recommends this option for most scenarios.
    **Sao chép một blob đã được lưu trữ vào một tầng trực tuyến**: Bạn có thể khôi phục một blob đã được lưu trữ bằng cách sao chép nó vào một blob mới trong tầng nóng hoặc tầng lạnh bằng thao tác [Sao chép Blob](https://learn.microsoft.com/en-us/rest/api/storageservices/copy-blob) hoặc [Sao chép Blob từ URL](https://learn.microsoft.com/en-us/rest/api/storageservices/copy-blob-from-url). Microsoft khuyến nghị tùy chọn này cho hầu hết các trường hợp.
- **Change a blob's access tier to an online tier**: You can rehydrate an archived blob to hot or cool by changing its tier using the [Set Blob Tier](https://learn.microsoft.com/en-us/rest/api/storageservices/set-blob-tier) operation.
    **Thay đổi cấp độ truy cập của blob sang cấp độ trực tuyến**: Bạn có thể khôi phục một blob đã được lưu trữ về trạng thái nóng hoặc lạnh bằng cách thay đổi cấp độ của nó bằng thao tác [Đặt cấp độ Blob](https://learn.microsoft.com/en-us/rest/api/storageservices/set-blob-tier).

Rehydrating a blob from the archive tier can take several hours to complete. Microsoft recommends rehydrating larger blobs for optimal performance. Rehydrating several small blobs concurrently might require extra time.
	Việc khôi phục một blob từ cấp độ lưu trữ có thể mất vài giờ để hoàn tất. Microsoft khuyến nghị nên khôi phục các blob lớn hơn để đạt hiệu suất tối ưu. Việc khôi phục nhiều blob nhỏ cùng lúc có thể cần thêm thời gian.

## Rehydration priority
___
When you rehydrate a blob, you can set the priority for the rehydration operation via the optional `x-ms-rehydrate-priority` header on a [Set Blob Tier](https://learn.microsoft.com/en-us/rest/api/storageservices/set-blob-tier) or **Copy Blob/Copy Blob From URL** operation. Rehydration priority options include:
	Khi bạn khôi phục dữ liệu blob, bạn có thể đặt mức độ ưu tiên cho thao tác khôi phục thông qua tiêu đề tùy chọn `x-ms-rehydrate-priority` trên thao tác [Đặt cấp độ Blob](https://learn.microsoft.com/en-us/rest/api/storageservices/set-blob-tier) hoặc **Sao chép Blob/Sao chép Blob từ URL**. Các tùy chọn ưu tiên khôi phục bao gồm:

- **Standard priority**: The rehydration request is processed in the order it was received and might take up to 15 hours.
	**Ưu tiên tiêu chuẩn**: Yêu cầu khôi phục được xử lý theo thứ tự nhận được và có thể mất đến 15 giờ.
- **High priority**: The rehydration request is prioritized over standard priority requests and might complete in under one hour for objects under 10 GB in size.
	**Ưu tiên cao**: Yêu cầu khôi phục được ưu tiên hơn các yêu cầu ưu tiên tiêu chuẩn và có thể hoàn thành trong vòng chưa đầy một giờ đối với các đối tượng có kích thước dưới 10 GB.

To check the rehydration priority while the rehydration operation is underway, call [Get Blob Properties](https://learn.microsoft.com/en-us/rest/api/storageservices/get-blob-properties) to return the value of the `x-ms-rehydrate-priority` header. The rehydration priority property returns either _Standard_ or _High_.
	Để kiểm tra mức độ ưu tiên khôi phục dữ liệu trong khi quá trình khôi phục đang diễn ra, hãy gọi [Get Blob Properties](https://learn.microsoft.com/en-us/rest/api/storageservices/get-blob-properties) để trả về giá trị của tiêu đề `x-ms-rehydrate-priority`. Thuộc tính ưu tiên khôi phục trả về _Standard_ hoặc _High_.

## Copy an archived blob to an online tier
___
The first option for moving a blob from the archive tier to an online tier is to copy the archived blob to a new destination blob that is in either the hot or cool tier. You can use the [Copy Blob](https://learn.microsoft.com/en-us/rest/api/storageservices/copy-blob) operation to copy the blob. When you copy an archived blob to a new blob in an online tier, the source blob remains unmodified in the archive tier. You must copy the archived blob to a new blob with a different name or to a different container. You can't overwrite the source blob by copying to the same blob.
	Phương án đầu tiên để di chuyển một blob từ tầng lưu trữ sang tầng trực tuyến là sao chép blob đã lưu trữ sang một blob đích mới nằm trong tầng nóng hoặc tầng lạnh. Bạn có thể sử dụng thao tác [Sao chép Blob](https://learn.microsoft.com/en-us/rest/api/storageservices/copy-blob) để sao chép blob. Khi bạn sao chép một blob đã lưu trữ sang một blob mới trong tầng trực tuyến, blob nguồn vẫn không bị thay đổi trong tầng lưu trữ. Bạn phải sao chép blob đã lưu trữ sang một blob mới có tên khác hoặc sang một vùng chứa khác. Bạn không thể ghi đè lên blob nguồn bằng cách sao chép sang cùng một blob.

Rehydrating an archived blob by copying it to an online destination tier is supported within the same storage account only for service versions earlier than 2021-02-12. Beginning with service version 2021-02-12, you can rehydrate an archived blob by copying it to a different storage account, as long as the destination account is in the same region as the source account.
	Việc khôi phục một blob đã lưu trữ bằng cách sao chép nó sang tầng đích trực tuyến chỉ được hỗ trợ trong cùng một tài khoản lưu trữ đối với các phiên bản dịch vụ trước ngày 12/02/2021. Bắt đầu từ phiên bản dịch vụ 2021-02-12, bạn có thể khôi phục dữ liệu blob đã lưu trữ bằng cách sao chép nó sang một tài khoản lưu trữ khác, miễn là tài khoản đích nằm trong cùng khu vực với tài khoản nguồn.

## Change a blob's access tier to an online tier
___
The second option for rehydrating a blob from the archive tier to an online tier is to change the blob's tier by calling **Set Blob Tier**. With this operation, you can change the tier of the archived blob to either hot or cool.
	Phương án thứ hai để khôi phục blob từ cấp độ lưu trữ (archive tier) sang cấp độ trực tuyến (online tier) là thay đổi cấp độ của blob bằng cách gọi hàm **Set Blob Tier**. Với thao tác này, bạn có thể thay đổi cấp độ của blob đã được lưu trữ thành cấp độ nóng (hot tier) hoặc cấp độ lạnh (cool tier).

Once a **Set Blob Tier** request is initiated, it can't be canceled. During the rehydration operation, the blob's access tier setting continues to show as archived until the rehydration process is complete.
	Sau khi yêu cầu **Set Blob Tier** được khởi tạo, nó không thể bị hủy bỏ. Trong quá trình khôi phục, cài đặt cấp độ truy cập của blob vẫn hiển thị là đã lưu trữ cho đến khi quá trình khôi phục hoàn tất.

To learn how to rehydrate a blob by changing its tier to an online tier, see [Rehydrate a blob by changing its tier](https://learn.microsoft.com/en-us/azure/storage/blobs/archive-rehydrate-to-online-tier#rehydrate-a-blob-by-changing-its-tier).
	Để tìm hiểu cách khôi phục blob bằng cách thay đổi cấp độ của nó sang cấp độ trực tuyến, hãy xem [Khôi phục blob bằng cách thay đổi cấp độ của nó](https://learn.microsoft.com/en-us/azure/storage/blobs/archive-rehydrate-to-online-tier#rehydrate-a-blob-by-changing-its-tier).