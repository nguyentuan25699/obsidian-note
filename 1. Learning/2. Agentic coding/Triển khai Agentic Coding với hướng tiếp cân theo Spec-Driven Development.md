# Spec-Driven Development vs Tranditional Development
___
- Thường viết code trước, rồi mới viết spec và các tài liệu liên quan sau. SDD đảo ngược quy trình đó
- SDD đặt spec làm trung tâm - AI sẽ tự động viết code dựa trên spec này.
# Flow của Spec-Driven Development
___
Khó có một flow tiêu chuẩn, tuỳ vào cá nhân, tổ chức, dự án, nhưng có những bước cơ bản như sau: 
Writing spec -> Planning -> Breaking Tasks -> Implementing
## Bước 1 - Viết đặc tả (Spec)
- Định nghĩa dự án cần làm gì và tại sao. Bước này tập trung vào góc độ nghiệp vụ: Liệt kê mục tiêu, nhu cầu người dùng,...
## Bước 2 - Lập kế hoạch (Planning)
- Đặc tả ý tưởng thành giải pháp kĩ thật cụ thể, File `plan.md` sẽ mô tả kiến trúc hệ thống, các phần chính, luồng dữ liệu, công nghệ, API, cơ sở dữ liệu... phù hợp với yêu cầu đề ra.
## Bước 3 - Lên nhiệm vụ triển khai (Breaking Task)
- Phân ra kế hoạch kỹ thuật thành các việc cụ thể để thực thi
- Mỗi tác vụ có thể được mô tả trong 1 file .md dưới thư mục tasks/ (hoặc 1 file task tổng hợp) với đủ bối cảnh và tiêu chí để hoàn thành.
- VD: Tạo khung dự án, xây dựng từng module/ chức năng theo đặc tả, viết test cho mỗi phần, kiểm thử tích hợp, hoàn thiện tài liệu...
## Bước 4 - Implement
- AI Agent sẽ thực hiện task lần lượt cho đến khi hoàn thành việc được giao
=> Nếu có thay đổi yêu cầu, cần cập nhật lại spec => plan => sinh ra task mới để đảm bảo mọi thứ nhất quán

# Spec-Driven Development toolset
___
## Amazon Kiro
- Bởi Amazon tháng 7/2025
- Là bản fork của VS Code, hướng tới đưa coder ra khỏi vide coding.
- Kiro hỗ trợ trực tiếp SDD: Coder mô tả yêu cầu bằng ngôn ngữ tự nhiên, Kiro sẽ tạo ra user stories kèm acceptance criteria, technical design document và danh sách coding task để thực hiện yêu cầu.
- Sau khi được review bởi lập trình viên thì sẽ được chuyển giao cho AI coding agent để implement lần lượt.
## Github Speckit
- Bởi Github tháng 9/2025
- Cung cấp một bộ cấu trúc mẫu để mô tả dự án phần mềm theo đặc tả mà công cụ AI có thể hiểu được.
- Github cung cấp dòng lệnh Specify CLI giúp khởi tạo nhanh cấu trúc SpecKit. Chỉ với 1 lệnh, CLI sẽ tạo thư mục `.specify` cùng các file mẫu (spec.md, plan.md, thư mục task) và cả các tệp prompt để tích hợp với các AI Coding agent khác nhau như Github copilot, Claude, Gemini, Cursor...
- Speckit mang lại 'tính nhất quán ở quy mô lớn' - cả đội ngũ phát triển cũng như AI Assistant đều  làm việc trên cùng 1 bộ hướng dẫn
- Toàn bộ đặc tả và kế hoạch được quản lý dưới thư mục .specify/ trong repository dự án
	- .specify/spec.md: tập tin markdown chứa đặc tả mục tiêu và yêu cầu của dự án. Đây là nguồn thông tin về cái gì cần xây dựng VD: liệt kê các tính năng, user stories, tiêu chí chấp nhận, ...
	- .specify/plan.md: tập tin markdown ghi lại phương thức kĩ thuật và kiến trúc cho dự án. Phác thảo cách thức sẽ thực hiện yêu cầu: kiến trúc hệ thống, thành phần, công nghệ, thư viện, cấu trúc data, API...
	- .specify/tasks/ : Chứa tập tin nhiệm vụ cụ thể. Mỗi file trong thư mục là một công việc nhỏ, như là 1 ticket hoặc user story kĩ thật. Mô tả chi tiết yêu cầu task để coder hoặc AI thực hiện.
	- .specify/constitution.md (optional): Tập tin ghi nguyên tắc, chuẩn mực của dự án. VD: hiệu suất, bảo mật, giao diện, coding style,...
- Tạo tệp cấu hình phù hợp với coding agent AI như Copilot Claude,...