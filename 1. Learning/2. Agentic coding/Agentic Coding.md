## AI Driven Development
- AI-Driven Development là phương pháp phát triển mà AI tham gia vào hầu hết các bước - từ viết Code, sinh tài liệu kiểm thử. Lập trình viên chuyển từ "người viết code" sang "người hướng dẫn và giám sát AI"
- Agentic Coding là phong cách lập trình với sự hỗ trợ của AI Agent.
- Thay vì con người đóng vai trò coding chính, và AI support thông qua code completion,.. thì các AI Agent sẽ hoạt động với một mức độ tự chủ cao, tự lên plan, suy nghĩ và thực thi.
- Nguyên lý cốt lõi: Agentic coding không phải chỉ là dùng công cụ cụ thể, mà là một cách tiếp cận. Điều quan trọng nhất là hiển được cách suy nghĩ: biết chia việc AI thé nào, cung cấp thông tin ra sao, kiểm sát thế nào.
- Tư duy mới cho Lập trình viên: thay vì làm hết mọi thứ, hãy dạy cho AI làm việc đó. Muốn dạy tốt thì phải nắm rất vững vấn đề và biết cách diễn đạt thật logic.
## Spec Driven Development
- Spec-Driven Development (SDD) là phương phát phát triển dựa trên đặc tả- tập trung làm specifications thật chi tiết và đầy đủ trước, sau đó code sẽ được AI sinh ra dựa trên spec.
- Thay vì nhảy ngay vào code, điều đầu tiên sẽ "định nghĩa rõ ràng mình muốn xây dựng cái gì và vì sao cần nó" rồi tiếp đến mới xây dựng xem nên "làm nó như thế nào".
- SDD nhằm khắc phục tình trạng vibe coding - lập trình theo cảm hứng mà không có kế  hoạch rõ ràng.
- Vibe-coding dễ đến sản phầm mã nguồn chắp vá, thiếu nhất quán, khó bảo trì và mở rộng.
- SDD đóng vai trò như cầu nối giữa ý định của con người và kết của AI sinh ra, giúp hạn chế việc AI đoán mò yêu cầu.
## Lợi ích của Spec-Driven Development
- Spec là "source of truth" cho dự án, mô tả mục tiêu, yêu cầu và kết quả kỳ vọng thay vì chỉ tập trung vào giải pháp kĩ thuật. Từ đó member dự án và AI đều có cùng 1 hiểu biết thống nhất vè những gì cần xây dựng.
- Tách biệt ý tưởng và công nghệ: Flow thường thấy khi triển khai SDD là xây dựng spec trước, tập trung vào cái cần làm, không phải cách làm. sau đó mới xây dựng technical design dựa trên spec. Do đó có thể tái sự dụng spec ngay cả khi thay đổi công nghệ.
- Có tổ chức, nhất quán và dễ mở rộng: Định nghĩa rõ ràng từ đầu giúp quá trình phát triển trật tự hơn, lặp lại được và dễ mở rộng.
## Spec-Driven Development - Triết lý cố lõi
- Đề cao intent-driven development, trong đó specification cần phải sác định rõ "what" trước "how".
- Tập trung xây dựng specification thật đầy đủ chi tiết, được dẫn dắt bở quy tắc, quy chuẩn, checklist và các quy định tổ chức.
- Thực hiện multi-step refinement, thay vì tạo code thẻo kiểu one-shot prompt.
- Phục thuộc mạnh mẽ vào khả năng của các mô hình AI tối tân trong việc hiểu và diễn giải Specification một các chính xác.

## Vai trò của Context Engineering trong Agentic Coding/SDD
- Nếu chúng ta mong muốn Agent có thể hoạt động như một lập trình viên trong dự án, thì cần phải được cung cấp đầy đủ bối cảnh (yêu cầu, tính năng, kiến trúc hệ thống, coding conventions,...) giống như những thành viên khác trong dự án
- Lúc này, nhiệm vụ của kỹ sư là đảm bảo Agent có đúng và đủ thông tin, trước khi code.
- Trong quá trình phát triển phần mềm, chúng ta gặp nhiều vấn đề context, VD: 
	- Để AI gent được web, cần nhiều thông tin UI(design), logic FE
	- AI gent được BE cần phải thông tin về BE spec, validation, cấu trúc DB.
	- Source code chứa nhiều file lớn nhớ, lượng context của cả folder là rất lớn.
	=> Context engineering đóng vai trò quan trọng trong Agentic coding/SDD, đảm bảo việc cung cấp đẩy đủ thông tin, yêu cầu cần thiết cho AI Agent, để nó gen code sát kì vọng nhất.