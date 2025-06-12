+++
title = "Customer AI Agent"
date = 2025
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

### Bối cảnh

Phòng IT mới của Ohmzio-Ampwerks đã làm việc để hợp nhất các cơ sở dữ liệu khách hàng thành một cái nhìn tổng hợp duy nhất về khách hàng. Họ đã trích xuất thông tin khách hàng từ cả hai cơ sở dữ liệu và họ đã tận dụng sức mạnh của [AWS Entity Resolution](https://aws.amazon.com/entity-resolution/) để khớp khách hàng và gán một định danh khách hàng duy nhất. Thông tin khách hàng tổng hợp kết quả đã được lưu trữ trong [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) để truy xuất nhanh từ ứng dụng của chúng ta.

### Mục tiêu

**Agents for Amazon Bedrock** có thể hỗ trợ với nhiều loại tác vụ khác nhau. Ví dụ, bạn có thể tạo một agent giúp khách hàng xử lý yêu cầu bồi thường bảo hiểm hoặc một agent giúp khách hàng đặt chỗ du lịch. Hôm nay, bạn sẽ cấu hình một agent để giúp nhóm hỗ trợ cung cấp trải nghiệm khách hàng tốt hơn.

Lab này hướng dẫn bạn qua quá trình sử dụng Agents for Amazon Bedrock để thêm nhiều khả năng hơn vào ứng dụng AI hội thoại của bạn. Sử dụng agents, bạn sẽ điều chỉnh hành vi của ứng dụng bằng cách cung cấp hướng dẫn agent cụ thể. Bạn cũng sẽ cấu hình agent để truy xuất thông tin khách hàng để hỗ trợ thêm với các trường hợp hỗ trợ.

**Các bước Lab**

1. Tạo một agent cho Amazon Bedrock.
2. Thêm action groups vào agent.
3. Kiểm tra agent và xem thông tin trace.

**Một agent bao gồm các thành phần sau:**

1. **Foundation model**. Bạn chọn một foundation model (FM) mà agent gọi để diễn giải input người dùng và các prompt tiếp theo trong quá trình điều phối của nó. Agent cũng gọi FM để tạo phản hồi và các bước tiếp theo trong quá trình của nó.

2. **Instructions**. Bạn viết hướng dẫn mô tả những gì agent được thiết kế để làm. Với advanced prompts, bạn có thể tùy chỉnh thêm hướng dẫn cho agent ở mỗi bước.

3. **Action groups**. Bạn định nghĩa các hành động mà agent nên thực hiện thông qua việc cung cấp các tài nguyên sau:

   - Một OpenAPI schema để định nghĩa các thao tác API mà agent có thể gọi để thực hiện tác vụ của nó.
   - Một Lambda function mà agent có thể thực thi.

4. **Knowledge bases**. Liên kết knowledge bases với một agent. Agent truy vấn knowledge base để có context bổ sung để tăng cường việc tạo phản hồi và input vào các bước của quá trình điều phối.

5. **Prompt templates**. Prompt templates là cơ sở để tạo prompts được cung cấp cho FM. Agents for Amazon Bedrock hiển thị bốn base prompt templates mặc định có thể được chỉnh sửa để tùy chỉnh hành vi của agent.

![1](../../images/4/1.png)

Kiến trúc agent có thể tùy chỉnh và mở rộng này trao quyền cho người dùng tạo ra các trợ lý thông minh được điều chỉnh theo nhu cầu và yêu cầu độc đáo của họ.
