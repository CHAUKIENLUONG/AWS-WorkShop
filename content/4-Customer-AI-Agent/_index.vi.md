+++
title = "Customer AI Agent"
date = 2025
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

### Bối cảnh

Phòng IT mới của Ohmzio-Ampwerks đã và đang làm việc để hợp nhất các cơ sở dữ liệu khách hàng thành một cái nhìn tổng thể duy nhất về khách hàng. Họ đã trích xuất thông tin khách hàng từ cả hai cơ sở dữ liệu và họ đã tận dụng sức mạnh của [AWS Entity Resolution](https://aws.amazon.com/entity-resolution/) để khớp thông tin khách hàng và gán một định danh khách hàng duy nhất. Thông tin khách hàng đã được hợp nhất được lưu trữ trong [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) để truy xuất nhanh chóng từ ứng dụng của chúng ta.

### Mục tiêu

**Agents for Amazon Bedrock** có thể hỗ trợ nhiều loại tác vụ khác nhau. Ví dụ, bạn có thể tạo một agent giúp khách hàng xử lý yêu cầu bảo hiểm hoặc một agent giúp khách hàng đặt chỗ du lịch. Hôm nay, bạn sẽ cấu hình một agent để giúp đội ngũ hỗ trợ cung cấp trải nghiệm khách hàng tốt hơn.

Bài thực hành này hướng dẫn bạn qua quy trình sử dụng Agents for Amazon Bedrock để bổ sung thêm khả năng cho ứng dụng AI hội thoại của bạn. Sử dụng agents, bạn sẽ điều chỉnh hành vi của ứng dụng bằng cách cung cấp các hướng dẫn agent cụ thể. Bạn cũng sẽ cấu hình agent để truy xuất thông tin khách hàng nhằm hỗ trợ tốt hơn cho các trường hợp hỗ trợ.

**Các bước thực hành**

1. Tạo một agent cho Amazon Bedrock.
2. Thêm nhóm hành động vào agent.
3. Kiểm tra agent và xem thông tin theo dõi.

**Một agent bao gồm các thành phần sau:**

1. **Mô hình nền tảng**. Bạn chọn một mô hình nền tảng (FM) mà agent sẽ gọi để diễn giải đầu vào của người dùng và các lời nhắc tiếp theo trong quá trình điều phối của nó. Agent cũng gọi FM để tạo ra phản hồi và các bước tiếp theo trong quy trình của nó.

2. **Hướng dẫn**. Bạn viết hướng dẫn mô tả những gì agent được thiết kế để thực hiện. Với các lời nhắc nâng cao, bạn có thể tùy chỉnh thêm hướng dẫn cho agent ở mọi bước.

3. **Nhóm hành động**. Bạn xác định các hành động mà agent nên thực hiện thông qua việc cung cấp các tài nguyên sau:

    * Một schema OpenAPI để xác định các thao tác API mà agent có thể gọi để thực hiện nhiệm vụ của mình.
    * Một hàm Lambda mà agent có thể thực thi.

4. **Cơ sở kiến thức**. Liên kết các cơ sở kiến thức với một agent. Agent truy vấn cơ sở kiến thức để có thêm ngữ cảnh nhằm tăng cường việc tạo phản hồi và đầu vào cho các bước của quy trình điều phối.

5. **Mẫu lời nhắc**. Mẫu lời nhắc là cơ sở để tạo ra các lời nhắc được cung cấp cho FM. Agents for Amazon Bedrock cung cấp sẵn bốn mẫu lời nhắc cơ bản mặc định có thể được chỉnh sửa để tùy chỉnh hành vi của agent của bạn.

![1](../../images/4/1.png)

Kiến trúc agent có thể tùy chỉnh và mở rộng này cho phép người dùng tạo ra các trợ lý thông minh phù hợp với nhu cầu và yêu cầu riêng của họ.
