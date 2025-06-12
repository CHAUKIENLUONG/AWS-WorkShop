+++
title = "Test the Knowledge Base"
date = 2025
weight = 2
chapter = false
pre = "<b>3.2. </b>"
+++

### Giới thiệu

Sau khi đã tạo cơ sở kiến thức để thực hiện RAG trên các ticket hỗ trợ và dữ liệu sản phẩm cho cả Ohmzio và Ampwerks, chúng ta sẽ sử dụng kỹ thuật prompt để kiểm tra khả năng AI tạo sinh dựa trên dữ liệu đã cung cấp.

### Kỹ thuật Prompt

Như đã định nghĩa trong phần giới thiệu, kỹ thuật prompt là phương pháp thiết kế các câu prompt hiệu quả để hướng dẫn mô hình tạo ra kết quả mong muốn. Dưới đây là một số phương pháp thực hành tốt nhất khi khám phá nguồn dữ liệu với cơ sở kiến thức:

1. Cụ thể hóa: Tính cụ thể giúp mô hình hiểu ngữ cảnh và đưa ra phản hồi chính xác hơn. Ví dụ, thay vì hỏi "hãy cho tôi biết về Đèn thông minh Ohmzio," hãy hỏi "những vấn đề phổ biến nhất với Đèn thông minh Ohmzio là gì?"

2. Sử dụng từ khóa: Đưa các từ khóa liên quan vào prompt để thể hiện ngữ cảnh hoặc lĩnh vực bạn quan tâm. Điều này giúp mô hình điều chỉnh câu trả lời theo chủ đề mong muốn.

3. Cấu trúc prompt: Đối với các truy vấn phức tạp, hãy cấu trúc prompt theo cách logic, từng bước một. Bạn có thể bắt đầu với phần giới thiệu ngắn về chủ đề, tiếp theo là câu hỏi cụ thể hoặc yêu cầu giải thích.

4. Kết hợp ví dụ: Khi tìm kiếm đầu ra sáng tạo hoặc phức tạp, việc cung cấp ví dụ trong prompt có thể hướng dẫn mô hình tạo ra loại phản hồi bạn đang tìm kiếm.

### Các bước thực hiện

1. Điều hướng đến [console](https://console.aws.amazon.com/bedrock/home#) Amazon Bedrock.

2. Nhấp vào **Knowledge bases** trong menu bên trái dưới phần Builder Tools.

3. Nhấp vào nút radio bên cạnh merger-knowledge-base mà chúng ta đã tạo trong phần trước. Sau đó nhấp vào **Test knowledge base**.

![1](../../../images/3/3.2/1.png)

4. Trong cửa sổ Test knowledge base, nhấp vào **Select model**.

![2](../../../images/3/3.2/2.png)

5. Trong cửa sổ pop-up, chọn **Anthropic, Claude 3.5 Sonnet**, và **On-demand**. Nhấp vào **Apply**.

![3](../../../images/3/3.2/3.png)

6. Trong phòng thí nghiệm trước đó, bạn đã sử dụng Amazon QuickSight để phát hiện ra rằng Ổ cắm thông minh có số lượng sự cố hỗ trợ cao nhất. Hãy sử dụng cơ sở kiến thức để khám phá thêm thông tin chi tiết về những sự cố hỗ trợ đó.

   1. Trong bảng điều khiển với ô nhập liệu, sao chép prompt sau và nhấp vào Run:

   `Những vấn đề phổ biến nhất với Ổ cắm thông minh Ohmzio là gì?`

   Đây là một mẫu phản hồi tạo sinh:

   {{%notice note%}}
   Lưu ý rằng kết quả được tạo ra bởi Knowledge Base có thể không hoàn toàn khớp với các mẫu được cung cấp trong hướng dẫn phòng thí nghiệm. Vì việc đào tạo, tinh chỉnh và cải tiến tổng thể cơ sở hạ tầng trừu tượng liên tục được cập nhật để cung cấp trải nghiệm hiệu suất và đáng tin cậy nhất cho người dùng cuối.
   {{%/notice%}}

   ![4](../../../images/3/3.2/4.png)

   Lưu ý rằng phản hồi trong console bao gồm các tham chiếu đến chi tiết nguồn. Chi tiết nguồn có thể được truy cập bằng cách nhấp vào **Details** ở cuối mỗi phản hồi. Điều này cho phép tăng tính minh bạch cho các tuyên bố mà mô hình có thể đưa ra trong một phản hồi nhất định.

   2. Bạn có thể thực hiện những hành động nào để tránh các cuộc gọi hỗ trợ? Sử dụng cơ sở kiến thức để có thêm thông tin chi tiết.

   `Làm thế nào chúng ta có thể cập nhật tài liệu của mình để tránh một số cuộc gọi hỗ trợ không cần thiết?`

   ![5](../../../images/3/3.2/5.png)

   {{%notice%}}
   Cơ sở kiến thức chứa hướng dẫn sử dụng sản phẩm và lịch sử ticket hỗ trợ. Dựa trên thông tin này, LLM tạo ra các hành động có thể được thực hiện để cải thiện tài liệu và giảm số lượng cuộc gọi hỗ trợ.
   {{%/notice%}}
