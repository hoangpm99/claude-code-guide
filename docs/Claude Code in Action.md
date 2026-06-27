Tổng hợp các notes từ khoá học Claude Code in Actions:

1. Coding Assistants (CA) là gì?
Coding Assistants là một hệ thống phức tạp nhằm tận dụng khả năng của mô hình ngôn ngữ để hoàn thành những tác vụ lập trình.

2. Cách hoạt động của Coding Assistants
Khi đưa CA một tác vụ, chúng thường tiếp cận và xử lý chúng theo một quá trình:
- Nắm ngữ cảnh: Hiểu ngữ cảnh xung quanh yêu cầu
- Lên kế hoạch: Quyết định cách xử lý vấn đề 
- Hành động: Thực hiện các bước theo kế hoạch 
![how-coding-assistants work](images\image.png)

3. Tools là gì, cách hoạt động?
- Mô hình ngôn ngữ bản chất chỉ xử lý ngôn ngữ - chúng không có khả năng đọc files hay chạy commands.
- CA hỗ trợ mô hình ngôn ngữ bằng cách cấp cho chúng bộ Tools.
- Khi gửi một yêu cầu cho CA, CA thật ra sẽ tự động chèn thêm vào yêu cầu đó các Instructions để mô hình ngôn ngữ biết cách dùng Tools.
![CA-behind-the-scene](images\image-1.png)
- CA mới là người chạy command. Mô hình ngôn ngữ là để tư duy.
- Điểm mạnh trong CA của Claude là hiểu được Tools làm được gì và sử dụng Tools hiệu quả

