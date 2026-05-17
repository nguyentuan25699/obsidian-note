- Là CLI Coding Agent vô cùng mạnh mẽ phát triển bởi Anthropic
- Ưu điểm chính của Claude Code là thệ thống agent tông minh kèm một loạt tính năng hỗ trơ tối đa cho Engineer như hook, SubAgent, Slash command và gần đây là Claude Skills
- Ưu điểm khác là Sử dụng trực tiếp API của Anthropic mà không qua Provider trung gian
- Giao hiện CLI cũng giúp cho Claude code có thể hoạt động được trên mọi dự án lập trình mà không phụ thuốc vào IDE nào.
- Có hệ thống Built-in tools manh mẽ cùng khả năng kết hợp với MCP bên ngoài.

# Cách sử dụng
___
## Custom Instruction
___
- Claude.md: là file chưa thông tin quan trọng của toàn dự án như techstack, các yêu cầu đặc biệt tần tuân thủ.
- Khởi tạo CLAUDE.md bằng lệnh /init
- Mỗi thư mục con cũng có thể tạo ra các file CLAUDE.md riêng
- Các file này cần được liên tục review và cập nhập
## Hook
___
- Hook: cho phép user chạy các lệnh shell được config sẵn vào các thời điểm nhất định của một agent lifecycle.
- VD: 
	- Khi agent chuẩn bị chạy tools thì có thể custom PreToolUse hook và chắc các sử dụng nguy hiểm
- Các tạo hook:
	- Chạy command /hook và thực hiện theo hướng dẫ
	- Chỉnh sửa trực tiếp trong file .claude/setting.toml
## Slash command
___
- Slash command: có thể coi là đơn vị cơ bản nhất trong agentic coding trong Claude code. các lệnh này là các chỉ dẫn đơn giản thức hiện một nhiệm vụ cụ thể. Đây có thể là các viên gạch khi bắt đầu xây dự án với Agentic coding
- VD: 
	- Command /add-to-changelog version change_type message sủ dụng để ghi các nội dung vào file CHANGELOG.md
- Cách tạo:
	- Tạo thư mục .claude/commands/ và thêm vào các file markdown tương ứng. Ví dụ .claude/commands/review.md để review code.
- Cách sử dụng:
	- Sử dụng trức tiếp trong CLI với cú pháp /command-name <tham số nếu có>
## Sub Agents
___
- Sub agent: thực hiện các nhiệm vụ chuyên biệt với context, instruction, bộ công cụ riêng độc lập với agent chính. Trong quá trình thực hiện thì agent chính sẽ tự động điều phối đến subagents cần thiết
- VD: Thực hiện nghiên cứu techstack sử dụng các tools websearch
- Cách tạo:
- Thạo thư mục .claude/agents/ và thêm vào các file markdown tương ứng.
- Cách sử dụng
	- Triệu hồi trực tiếp sub agent bằng @agent_name. VD: claude "@db-expert analyze the performance of our user queries"
	- Claude code có thể phối hợp nhiều sub-agent để thức hiện tác vụ phức tạp
- Lưu ý: 
	- Các Sub-agent nên thực hiện 1 nhiệm vụ chuyện biệt và đủ nhỏ
	- Cần có các bước tóm tắt context cho agent chính
	- Định nghĩa rõ các sub-agent có thể chạy song song hoặc phụ thuộc lẫn nhau
## Claude skills
___
- Skills: có thể coi là một bản thiết kế, một workflow tổng thể để Calude code thực hiện một nhiệm vụ phức tạp.
- Khi nào cần dùng Skills: khi cảm thấy đang lặp đi lặp lại cùng một việc nhiều lần => tạo riêng thành skill để tự động hoá.
- Cách tạo ở local: Cót hể tạo file SKILL.md trong thư mục .claude/skills
- Download skills từ market: install bằng lệnh /plugin install <tên skill>
- Cách sử dụng: Skill tự động được gọi khi có tác vụ liên quán hoặc có thể chỉ định trức tiếp cho claude code sử dụng skills. VD: "Use thê 'web app testing' Skill to run our unit tests locally..."