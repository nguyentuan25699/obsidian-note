# Prompt Engineering
___
- Prompt engineering là tập trung vào các kỹ thuật viết prompt, bao gồm cả các prompt hệ thống - system prompt - đẻ hướng dẫn LLM tạo ra kết quả mong muốn
- Chủ yếu nhấn mạnh vào việc tìm từ ngữ/cú pháp tối ưu cho một lần hồi đáp của mô hình 
- Cùng 1 mô hình, prompt khác nhau có thể cho kết quả khác nhau
- Khi LLM ra đời và bước đầu được người dùng đón nhận, thì Prompt engineering là từ khoá trung tâm của việc ứng dụng AI, hay câu chuyện khai thác sức mạnh của LLM. Công việc "AI Engineering" cũng xoay quanh việc viết Prompt.
# Context Engineering
___
- Sau thời gian hoạt động thì vấn đề không còn chỉ xoay quanh việc "viết prompt như thế nào", mà là quản lý trạng thái toàn cục của Context trong từng vòng lặp suy luận.
- Hiểu một cách đơn giản, trong quá trình Agent vận hành, nó sẽ tự sinh ra dữ liệu (log, memory, tool output, message history, intermediate results,...) Agent sẽ quan sát và tiết tục suy luận dựa trên những dữ liệu đó, để tiếp tục các bước tiếp theo.
=> Cần thiết phải chọn lọc, tái cấu trúc và liên tục cung cấp quyền Context cần thiết qua mỗi bước suy luận của Agent.

# Tại sao Context Engineering quan trọng?
___
## Vấn đề của LLM
Mọi LLM đều có giới hạn về Context có thể xử lý. Mặc dù Context window không dùng mở rộng nhưng nó cũng có những hạn chế:
- Vấn đề chi phí: Dùng càng nhiều token thì tốn càng nhiều chi phí
- Vấn đề performance: Context càng lớn thì thời gian xử lý của LLM càng lâu.
- LLM cũng "mất tập trung": Giống con người, thì mô hình ngôn ngôn ngữ có giới hạn chú ý. Khi context quá dài mô hình sẽ bắt đầu giảm độ chính xác trong việc nhớ thông tin (context rot), theo nghiên cứu, càng thêm nhiều token về ngữ cảnh thì mô hình càng khó truy hồi chi tiết chính xác từ đó.
- "Attention budget" có hạn: Mỗi mô hình chỉ có một "ngân sách chú ý" nhất định cho mỗi lần suy luận. Thêm mỗi token mới tiêu tốn một phần ngân sách đó, làm tăng nguy cơ thông tin quan trọng bị loãng đi. Kiến trúc transformer (là nền tảng của các LLM) bộc mỗi token phải "attend" đến mọi token khác, nên ngữ cảng càng dài thì độ tập trung càng bị trải mỏng.
=> Context quyết định chất lượng tác vụ: Tổ chức ngữ cảng đóng vai trò vô cùng quan trọng, nó có thể làm một mô hình yếu hoạt động hiệu quả hoặc làm giảm độ hiệu quả của một mô hình mạnh mẽ tuỳ thuộc vào cách tổ chức của bạn. Tóm lại, Prompt hay là chưa đủ, cần cấu trúc Context đủ tốt để định hướng được suy luận, ghi nhớ và quyết định của AI Agent.

=> Context Engineering là một môn nghệ thuật trong việc chọn lọc những gì cần đưa vào Context window, từ một vũ trụ thông tin khổng lồ và không ngừng thay đổi.

# Context Engineering - tại sao lại khó?
___
- Đây là một kĩ năng mới, chưa có "giáo trình" chuẩn, đòi hỏi cần vừa làm vừa rút kinh nghiệm, từ các trải nghiệm thực tế thay vì dập khuôn lý thuyết.
- Context luôn thay đổi, rất khó nắm bắt. Trong tác vụ nhiều bước, mỗi vòng lặp tạo thêm nhiều thông tin(hành động, quan sát mới). Cần phải liên tục cập nhật và chọn lọc thông tin cần giữ lại cho lượt suy luận kế tiếp. Việc này mang tính lặp lại mỗi bước suy luận thay vì prompt cố định. Việc này phức tạp vì dữ liệu ngày càng nhiều.
- Như thế nào là đủ?: cân bằng giữa cung cấp đầy đủ thông tin để mô hình hoạt động với việc cắt bỏ những phần ít liên quan để tiết kiệm dung lượng rất khó. Cắt quá mạnh tay có thể loại bỏ nhầm chi tiết quan trọng về sau cần để suy luận, đưa vào quá nhiều thì sẽ vượt quá giới hạn context, hoặc tốn kém chi phí.
- Xác định "cái gì thật sự quan trọng và cần thiết" đòi hỏi nhiều thử nhiệm và trực giác cực kỳ nhạy bén.
- Khi agent trở nên đa năng (nhiều tool, tương tác lâu dài), khối lượng ngữ cảnh phình to và đa dạng, dễ phát sinh lỗi. Ví dụ, nếu cho phép nạp động hàng trăm Tools vào agent, mô hình có thể rối trí và chọn sai hành động. Mặt khác, các lỗi/hành động thất bại phát sinh liên tục - xử lý chúng ra sao trong ngữ cành cũng là một bài toán không đơn giản.
