# Giới thiệu
- Là một loạt công cụ coding agent được tạo ra bởi OpenAI
- Có thể hoạt động cả trên local qua Codex CLI hoặc trên cloud
- Codex CLI là một coding agent chạy trên terminal có thể đọc hiển toàn bộ mã nguồn cho dự án và thực hiện thay đổi nhiều file cũng lúc và chạy các câu lệnh hệ thống.
- Cho phép liên kết với Github repo để có thể assign task trên cloud. mỗi tác vụ của codex sẽ được chạy trên một môi trường sandbox riêng biệt giúp dễ dàng quản lý các thay đổi và cho phép song song nhiều tác vụ.
# Customize
## Instruction
- Sử dụng tệp đặc biệt là AGENTS.md lưu thông tin các hướng dẫn...
- Cần review và cập nhật thường xuyên
- Có thể dùng /init để tự tạo file này.
## Agent trong codex
- Lựa chọn modal: sử dụng lệnh /model để hiển thị các modal được  support.
- Lựa chọn các agent: codex không chia thành sub-agent hay custom chatmode như copilot hay claude code, chỉ có 1 agent để thực hiện tác vụ, tuy nhiên có thể chọn các agent để thực hiện.
- ## Codex trên cloud
- Được tích hợp trong các gói ChatGPT plus, pro, business, edu và enterprise
- Có thể liên kết từ giao diện web hoặc app điện thoại với Git repo, assign task cho Codex để chúng thực hiện và tạo PR.