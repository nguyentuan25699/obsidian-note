## 1. Synchronous & IO blocking
### a. Synchronous programming
Lập trình đồng bộ (synchronous programming) là cách lập trình mà các câu lệnh chạy tuần tự nhau, lệnh trước chạy xong thì lệnh sau mới có thể chạy.


> Task A > Task B > Task C
> Task X > Task Y so slowwwwwwwwww > Task Z

Như vậy, khi xử lý các tác vụ IO như đọc file, query database, chờ network,... nói chung là những công việc tốn thời gian, thì trong synchronous chương trình phải chờ đợi những việc kia hoàn thành xong thì mới chạy tiếp, do đó dẫn tới hiện tượng IO blocking.

### b. IO blocking
Là hiện tượng xảy ra với code đồng bộ, khi thực hiện một tác vụ quá lâu (như ví dụ trên). Do đó, các câu lệnh sau phải chờ đợi một thời gian dài, và trình duyệt có thể không phản ứng với các sự kiện UI.

Nếu ứng dụng hay trang web không phản hồi những sự kiện UI thì hệ điều hành sẽ nghĩ rằng ứng dụng đang bị treo. Khi đó con trỏ chuột có thể thành hình tròn xoay xoay, hoặc tệ hơn là ứng dụng bị lỗi "Not responding" (trên Windows). Đối với web thì nó có thể bị crash, người dùng không thể tương tác, không thể làm gì khác ngoài chờ đợi.

## 2. Asynchronous & non-blocking
### a. Asynchronous programming
Để khắc phục vấn đề blocking của synchronous, người ta đưa ra khái niệm lập trình bất đồng bộ (không đồng bộ - asynchronous programming). Về cơ bản, bất đồng bộ là các câu lệnh chạy có thể không theo thứ tự, lệnh chạy trước có thể kết thúc sau câu lệnh chạy sau.

> Task A > Task B > Task B end > ......... > Task A end

Bất đồng bộ không làm chương trình chạy nhanh hơn, đúng ra nó chỉ tránh lãng phí thời gian chờ đợi vô ích các tác vụ IO, network,... trong khi những tác vụ đấy thực hiện thì làm việc khác, khi nào chúng xong sẽ có cơ chế để thông báo lại cho mình.

Bất đồng bộ có hai dạng:
- Asynchronous trong đơn luồng (single-threaded)
- Asynchronous trong đa luồng (multi-threaded)

Đối với bất đồng bộ đa luồng, thì có thể thực thi nhiều công việc cùng lúc (mỗi việc thuộc một thread).
Đối với ngôn ngữ đơn luồng như JS thì bất đồng bộ có một số điểm đặc biệt, sẽ được trình bày sau.

### b. Non-blocking

Bất đồng bộ giải quyết được vấn đề blocking của đồng bộ, được gọi là non-blocking. Nghĩa là khi chạy một tác vụ nặng (IO, network,...) thì những lệnh tiếp theo được phép chạy ngay mà không cần chờ tác vụ kia hoàn thành.

## 3. JavaScript asynchronous?
Người ta thường nói JavaScript là ngôn ngữ bất đồng bộ, nhưng thực tế không hẳn như vậy.

### a. JS luôn đồng bộ & blocking
Đúng là JS có những cơ chế hỗ trợ lập trình bất đồng bộ (callback, promise, async/await), nhưng bản thân JS runtime hoàn toàn không phải. Bạn không thể nào viết một hàm với callback, promise hay async/await và hi vọng nó hoạt động asynchronous và non-blocking.

> Một vòng lặp vô tận trong JS luôn dẫn tới blocking, dù bạn có code bất đồng bộ kiểu nào đi chăng nữa.

Code JS là đơn luồng và hoàn toàn đồng bộ. Chỉ có những tác vụ sử dụng WebAPIs (do browser) như [[AJAX]], timeout,... thì JS mới thực thi chúng dạng bất đồng bộ. (hoặc một số API như [[AJAX]] của [[jQuery]] cho phép cả hai chế độ).

Do việc gọi và dùng các hàm WebAPIs tương tự như code bình thường, nên có thể bạn hiểu nhầm code JS cũng là bất đồng bộ.

> Chỉ có những hàm gọi WebAPIs mới có thể bất đồng bộ. Bạn không thể nào viết một hàm trong JS và yêu cầu nó chạy bất đồng bộ và non-blocking.

### b. Callback, promise,... là gì?

> Callback, promise hay async/await, chúng chỉ là những kĩ thuật **hỗ trợ** trong việc xử lý các tác vụ bất đồng bộ (của WebAPIs)
> Bản thân chúng **không dùng** để **tạo ra** các hàm bất đồng bộ.

Hỗ trợ ở đây có nghĩa, khi bạn thực hiện một hàm bất đồng bộ, đôi lúc bạn sẽ cần **đợi** nó hoàn thành để **làm thêm việc gì đó**. Nhưng nếu đợi nó bằng cách cho nó chạy dạng đồng bộ thì bị blocking.

Do đó, các kĩ thuật như callback hay promise được sinh ra để thực hiện các công việc mà yêu cầu hàm bất đồng bộ hoàn thành.

Ví dụ, bạn cần đợi hàm AJAX (bất đồng bộ) thực hiện xong để lấy dữ liệu, nhưng không muốn web bị blocking. Bình thường, nếu lấy dữ liệu ngay thì sẽ không lấy được do AJAX chưa thực hiện xong. Do đó, bạn dùng callback (hoặc promise) để giúp bạn thực hiện **lấy dữ liệu** ngay sau khi AJAX **hoàn thành**. Nghĩa là một callback dùng lấy dữ liệu nhận được sẽ được gọi.


## 4. Concepts
### a. Execution context

Hiểu đơn giản, execution context là môi trường mà hàm thực thi. Một execution context chứa code của một hàm và tất cả những thứ liên quan mà hàm cần dùng (biến cục bộ, inner function,...).

Execution context có 3 loại:
- Global context: là context của hàm main (bạn nào học C/C++ sẽ biết). Đây là context được tạo ra đầu tiên, được đẩy vào call stack đầu tiên. Mặc dù JS không có hàm main, nhưng ngầm định là có.
- Function context: context chứa một function nào đó. Chú ý, nếu function được gọi nhiều lần, thì sẽ có bấy nhiêu lần context được tạo ra.
- Eval context: context chứa code trong hàm `eval()`. Hàm này bị bỏ và không dùng vì không an toàn.

### b. Call stack
Stack là cấu trúc dữ liệu dạng LIFO (Last In First Out), là thứ gì đưa vào stack sau sẽ được lấy ra đầu tiên. Có thể tưởng tượng nó như một chồng đĩa, đĩa nào nằm trên cùng (được đặt vào sau cuối) thì sẽ được lấy ra đầu tiên.

Call stack cũng là một stack, và nó chứa tất cả execution context trong chương trình. Như ví dụ trên thì chồng đĩa là call stack, thì những cái đĩa là các execution context. Và chỉ có context nằm trên cùng (trên đỉnh) của stack thì mới được thực thi.

Quy trình hoạt động của call stack:

- Khi chương trình chạy, context của hàm main được đẩy vào đầu tiên.
- Lúc này, chỉ có main context nên nó nằm ở top của call stack, và nó được chạy
- Khi main chạy tới lời gọi function khác, thì context của function đó được tạo ra và đẩy ngay vào stack
- Function được gọi đang nằm trên top, nên hàm main tạm dừng và function bắt đầu thực thi
- Nếu function gọi một function khác nữa, thì cứ tiếp tục như vậy.
- Sau khi function thực thi xong, thì context của nó sẽ được lấy ra khỏi stack. Lúc này context tiếp theo (đã trở thành top) sẽ được thực thi tiếp.
- Cứ như vậy cho tới khi hàm main lấy ra khỏi call stack
- Khi call stack rỗng, thì chương trình xong (nhưng chưa kết thúc được vì có thể còn các callback chưa xử lý trong queue).

Vì JS là đơn luồng, nên nó chỉ có một callstack. Điều đó đồng nghĩa với việc tại một thời điểm, chỉ có một lệnh trên cùng (top) của call stack được thực thi.

### c. Task queue
Queue là cấu trúc dữ liệu hơi khác với stack, có dạng FIFO (First In First Out), vào trước ra trước. Tưởng tượng giống như khi xếp hàng vậy.

Task queue (hay còn gọi là callback queue) là nơi chứa các callback đi kèm với các hàm bất đồng bộ.

Quy trình hoạt động:

- Khi gọi hàm bất đồng bộ (thuộc WebAPIs) kèm theo callback, thì nó sẽ đưa context vào cho WebAPIs xử lý.
- Khi WebAPIs xử lý xong, thì callback sẽ được đẩy vào callback queue.
- Các callback sẽ lần lượt được event loop đẩy vào call stack (chỉ khi stack rỗng thì 1 callback sẽ được đẩy vào), cứ như thế cho tới khi queue rỗng.

Ngoài task queue, còn có job queue, là một queue thứ 2 nhưng dùng xử lý các callback của promise. Và job queue có độ ưu tiên cao hơn callback queue, do đó các job sẽ được chạy trước callback.

### d. Web APIs & C++ APIs
WebAPIs (hoặc C++ API bên Node.js) là những API được trình duyệt hoặc platform cung cấp cho JavaScript sử dụng. Các API có thể kể tới như:

- WebAPIs: AJAX, DOM, các hàm của browser API như `setTimeout()`,...
- Node.js C++ API: các hàm file system, query database,...

JS sử dụng các hàm này tương tự như việc gọi hàm bình thường, nhưng thường thì các hàm này sẽ gọi theo kiểu bất đồng bộ (mặc dù một số API cho phép dùng cả 2 kiểu). Và nên dùng bất đồng bộ vì thường những thao tác với WebAPIs đều khá tốn thời gian.

Quy trình hoạt động:

- Khi có một yêu cầu (lời gọi hàm) tới WebAPIs, thì nó sẽ xử lý công việc đó. Yêu cầu API có thể gửi kèm theo một callback (hoặc promise).
- Khi công việc được xử lý xong, callback tương ứng (nếu có) sẽ được đẩy vào task queue, và sẽ được thực thi (đối với promise thì đẩy vào job queue)

Có hai chú ý như sau:

- WebAPIs do browser thực thi, và browser thường chia thành các thread cho mỗi nhiệm vụ. Do đó, bản thân JS là đơn luồng, nhưng các hàm WebAPIs là đa luồng do trình duyệt thực thi.
- Thứ tự đẩy callback vào queue phụ thuộc vào task nào xong trước sẽ được đẩy vào trước. Ví dụ hai hàm `setTimeout(fn, 1000)` tuy gọi sau `setTimeout(fn, 3000)` nhưng callback của nó sẽ được đẩy vào task queue trước (do thời gian hoàn thành ngắn hơn).

### e. Event loop
Về cơ bản event loop là một vòng lặp vô tận của V8 engine, chỉ để thực hiện hai việc:

- Kiểm tra call stack có rỗng không
- Nếu stack rỗng rồi thì lấy một context trong queue đẩy thêm vào stack.
- Khi context đẩy vào stack thực hiện xong, stack lại rỗng thì tiếp tục lấy trong queue ra đẩy vào, cứ tiếp tục như thế tới khi queue rỗng hết.
- Job queue ưu tiên cao hơn task queue (callback queue), nên những context trong job queue được lấy ra trước.
- Bên trong task queue, những task dùng render UI thì sẽ được lấy ra trước

## 5. Problems

### a. Stack overflow

Vấn đề đầu tiên cần tránh là stack overflow. Đây là tình trạng stack bị đầy do chứa quá nhiều execution context. Như code ví dụ sau.

```js
function foo() {
    foo();
}
foo();
```

Hàm `foo()` thực hiện gọi lại chính nó mà không có điều kiện dừng lại, nên sẽ tới lúc nào đó trong call stack toàn là `foo() foo() foo()...` nhiều tới mức làm đầy stack.

Khi đó, trình duyệt sẽ báo lỗi Range Error.

Cách tránh thì đơn giản thôi, tránh việc gọi hàm vô tận, thường xảy ra khi đệ quy không có điều kiện dừng như trên.

