Nói một cách đơn giản, Redux là một công cụ quản lý trạng thái. Mặc dù nó được sử dụng chủ yếu với React, nhưng nó có thể được sử dụng với bất kỳ khung hoặc thư viện JavaScript nào khác. Nó rất nhẹ ở mức 2KB (bao gồm cả phụ thuộc), vì vậy bạn không phải lo lắng về việc nó làm cho ứng dụng của bạn có kích thước lớn.

Với Redux, trạng thái ứng dụng của bạn được giữ trong một "store" và mỗi thành phần có thể truy cập bất kỳ trạng thái nào mà nó cần từ "store"này. Sâu hơn một chút để xem tại sao bạn có thể cần một công cụ quản lý trạng thái.

![[Pasted image 20260517101348.png]]

### 1. Cách hoạt động của Redux
Các thành phần của Redux bao gồm:

- **Store:** Store đơn giản là 1 object chứa tất cả state toàn cục của ứng dụng. Nhưng thay vì lưu các state, nó lưu các **reducer**, sẽ được nói sau.
- **Các Action:** Khi ta định nghĩa các action, ta khai báo các tên của hành động trong ứng dụng. Lấy ví dụ ta có 1 state là counter và cần 2 phương thức để tăng và giảm giá trị của counter. Lúc này ta định nghĩa 2 action có tên là '**INCREMENT**' và '**DECREMENT**' và chỉ vậy thôi, việc xử lý thay đổi state của counter sẽ nhường cho **reducer**.
- **Các Reducer:** 1 reducer tương đương với 1 state nhưng kèm theo các mô tả state sẽ thay đổi như thế nào khi các action khác nhau được gọi. Trong ví dụ ta có reducer là **counter**, nó lưu state của **counter** và kiểm tra action vừa được gọi là INCREMENT hay DECREMENT và trả về state mới là state+1 hay state-1 tương ứng.
- **Các Dispatch:** Khi cần dùng 1 action ở component, ta gọi action đó đơn giản bằng cách sử dụng phương thức **dispatch**. VD: dispatch(increment()), dispatch(decrement()).
![[Pasted image 20260517101530.png]]


Cách Redux hoạt động rất đơn giản. Có một "store" trung tâm chứa toàn bộ trạng thái của ứng dụng. Mỗi thành phần có thể truy cập trạng thái được lưu trữ mà không phải gửi từ thành phần này sang thành phần khác.

Có ba phần xây dựng: actions, store, and reducers.