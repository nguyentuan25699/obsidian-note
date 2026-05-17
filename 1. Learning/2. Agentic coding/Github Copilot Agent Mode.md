## Giới thiệu
- Là coding agent được phát triển bở Github, thử nhiệm vào 06/2021, chính thức vào 06/2022
- Ban đầu chỉ ở mức độ hỏi đáp và hoàn thành mã, nhưng đến 2025 phát triển thành Coding Agent có tình tự chủ cao
- Có thể hoạt động tự chủ trên workspace. Khi assign issue cho nó thì sẽ tự hoạt động và trả ra PR
## Mục đích
- Hỗ trợ trong hầu hết khía cạnh lập trình: Hỏi code, debug, Code, Refactor, tạo PR, viết Doc, comment, review...
- Ask mode: thiết kế để hỏi đáp mà không thực thi việc implement (như giải thích tính năng xxx trong function yy)
- Edit mode: thực hiện chỉnh sửa cụ thể chính xác tại vị trí nhất định (như bôi đen và yêu cầu Copilot chỉnh sửa)
- Agent mode: Thực hiện tác vụ phức tạp, nhiều bước và liên quan đến nhiều tập tin, thậm chí tạo ra tệp mới.
## Điểm nổi bật
- Agent mode có thể thực hiện nhiều tác vụ nhiều công đoạn như research -> plan -> implement -> test trong một agent request giúp tiết kiệm chi phí sử dụng.
- Cho phép custom các chatmode (là các agent chuyên biệt), slash command tuỳ thuộc vào mục đích của developer.
- Hệ thống built-in tools mạnh mẽ cho phép tìm kiếm codebase, đọc/ghi file, có thể custom các tools riêng cũng như kết nối với MCP bên ngoài.
- Chat extension đã được open source giúp cộng đồng có thể phát triển thêm các tính năng customize cho phù hợp.
## Customize Github  Copilot - Instruction
- Mục đích: tạo các file hướng dẫn tuỳ chỉnh cho dự án, cho team giúp Copilot luôn follow theo các hướng dẫn cụ thể.
- Cách tạo: 
	- Với các instruction tổng quát, hay điền vào file .github/copilot-instruction.md
	- Với các tác vụ đặc biệt hãy tạo các files tương ứng đặt vào thư mục .github/instructions, VD: .github/instructions/go.instruction.md
- Sử dụng: các instruction sẽ được áp dụng trong phạm vi toàn bộ dự án ngay khi cấu hình xong.
## Customize Github Copilot - Chatmode
- Mục đích: Tạo ra các agent chuyên biệt dùng cho từng hoạt động, mục đích cụ thể, chỉ định các tools, model và các hướng dẫn thực hiện cụ thể
- Các tạo: 
	- Sử dụng Command Pallêt để Install manually
	- Copy các file .chatmode.md vào trong thư mục .github/chatmodes
- Các sử dụng: khi cài đặt xong, ở cửa sổ chat có thể chọn chatmode để sử dụng.
## Customize Github Copilot - Slash command
- Mục đích: tạo ra các prompt sẵn sàng sử dụng cho các tác vụ cụ thể như viết specs, viếc docs.
- Cách tạo: 
	- Sử dụng VS cde hoặc VS Insiders để cài đặt
	- Copy các file * .prompt.md vào trong thư mục .github/prompts
- Cách sử dụng: ngay sau khi cài đặt, có thê thử dụng theo cú pháp /prompt-name trong cửa sổ chat của VSCode.
  