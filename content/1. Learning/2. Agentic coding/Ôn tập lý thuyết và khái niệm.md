 - **LLM**: Large Language Modal - Mô hình ngôn ngữ lớn
 - **Token**: Đơn vị xử lý của LLM, có thể là một kí tự, một phần của từ, hoặc một từ hoàn chỉnh. Trung bình, 100 token tương đương với khoảng 75 từ tiếng Anh. Các LLM đều có giới hạn về số lượng Token có thể xử lý. Giới hạn này là khác nhau đối với các mô hình khách nhau.
 - Token chia làm 2 loại: Input token (là lượng token được đưa vào làm đầu vào cho LLM), và Output Token (Là lượng token được mô hình trả ra - Bao gồm cả Reasoning Token, tức Token được sinh ra tạm thời trong quá trình mô hình suy luận). Chi phí sự dụng LLM thường được tính toán dựa trên lượng Token Input và Output này.
 - **Prompt**: Câu lệnh, câu hỏi, hoặc đoạn văn bản mà người dùng nhập vào một hệ thống LLM để hướng dẫn nó thực hiện một nhiệm vụ cụ thể.
 - **Context**: Tất cả thông tin được cung cấp cho mô hình LLM trong quá trình xử lý, bao gồm mô tả nhiệm vụ, dữ liệu liên quan, và lịch sử hội thoại (nếu có).
 - Việc cung cấp đầy đủ context có ảnh hưởng thiết yến đến chất lượng phản hồi của LLM.
 - Về cơ bản mô hình LLM chỉ 'biết' những gì nó được học (kiến thức này có thể lỗi thời hoặc không cụ thể cho trường hợp hiện tại) và những gì nằm trong Prompt, mà chúng ta gọi là Context.
 - Context window: Các thuật ngữ như Context window, hay Context length miêu tả lượng thông tin là một LLM có thể xử lý và "ghi nhớ" tại một thời điểm. Nó hoạt động như bộ nhớ làm việc (working memory) của mô hình
 - Đơn bị đo lương cho context window là token.
 - Kích thước context window đã không ngừng tăng trưởng mạnh mẽ trong thời gian vừa qua. Từ mức chỉ 4k khi ChatGPT ra mắt cho đến 16k với GPT-3.5 Turbo, 32k với GPT-4, rồi lên 128k với GPT-4o, 200k với o-series, hay 1m với Gemini 1.5 Pro, và tiếp theo đó là GPT-4.1, Claude Sonnet 4, hay mới đây là Grok 4 Fast, Gemini 2.5 Pro với 2M.
 Một context window đủ lớn cho phép LLM có thể: 
 - Duy trì sự mạch lạc (Coherence) trong những cuộc hội thoại dài hoặc khi phần tích một tài liệu lớn.
 - Tăng cường độ chính xác (Accuracy): Càng nhiều Context liên quan, mô hình càng có khả năng đưa ra câu trả lời chính xác và ít có nguy cơ hallucinate thông tin
 - HIểu biết sâu sắc (Deeper Understanding): Một context window lớn cho phép mô hình năm bắt các mối quan hệ phúc tạp và các phụ thuộc ngữ nghĩa trải dài trên một văn bản lớn, từ đó đưa ra các phân tích toàn diện hơn.

 - AI Agent là một chương trình phần mềm có khả năng tự chủ nhận thức (perceive) môi trường xung quanh, lập kế hoạch (plan), và thực hiện các hành động (act) để đạt được một mục tiêu đã xác được xác định trước.
 - Nếu như LLM là bộ não có khả năng hiểu và tạo ra ngôn ngữ, thì AI Agent là bước tiến hoá tiếp theo: một thức thể hoàn chỉnh có thể sử dụng bộ não đó để hành động một cách tự chủ.
 - Một AI Agent dựa trên LLM thường có một kiến trúc cốt lõi bao gồm các thành phần chính là: Bộ não (Brain - LLM) - Công cụ (Tool use) - Bộ nhớ (Memory)

- MCP, hay Model Context Protocol, là một giao thức được đề xuất bởi Anthropic, vào cuối năm 2024, như là một tiêu chuẩn chung để cung cấp Context cho Model một cách hiệu quả.
- Mục đích của MCP là giúp các modal hành đầu tạo ra phản hồi tốt hơn, phù hợp hơn bằng cách dễ dàng lấy được "context" cần thiết từ các hệ thống bên ngoài.
- Ngày nay, MCP ngày càng trở nên phổ biến, và được hỗ trợ bởi rất nhiều các mô hình LLM tiên tiến.
- MCP Server đóng vai trò như một cầu nối giữa các ứng dụng AI Agent kết nối ra thế giới bên ngoài, để thực thi các tác vụ, hay lấy về thông tin cần thiết.
- Nắm được cách dùng MCP, cách config MCP, sẽ giúp chúng ta mở rộng mạnh mẽ năng lực của các hệ thống Agent.
- 