+++
title = "Kết luận"
date = 2025
weight = 5
chapter = false
pre = "<b>4.5. </b>"
+++

### Chúc mừng!

Bạn vừa hoàn thành việc thiết lập **Agent for Amazon Bedrock**!

### Tổng kết

Trong bài thực hành này, bạn đã:

1. Tạo một agent cho Amazon Bedrock.
2. Cung cấp hướng dẫn và cấu hình agent để sử dụng cơ sở kiến thức của bạn.
3. Thêm một nhóm hành động vào agent.
4. Cấu hình hàm lambda để gọi từ agent của bạn.
5. Kiểm tra agent và phân tích thông tin theo dõi.

### Các bước tiếp theo

Để khám phá thêm dữ liệu khách hàng để sử dụng làm đầu vào cho agent, bạn có thể duyệt bảng **Amazon DynamoDB** trực tiếp. Sử dụng liên kết này để duyệt [bảng all-customers](https://us-west-2.console.aws.amazon.com/dynamodbv2/home?region=us-west-2#item-explorer?maximize=true&operation=SCAN&table=all-customers).

![1](/images/4/4.5/1.png)

Trong bài thực hành, bạn đã cấu hình một nhóm hành động để gọi hàm Lambda. Hàm Lambda mẫu đã truy xuất thông tin khách hàng bổ sung từ **Amazon DynamoDB** và trả về cho agent để bổ sung ngữ cảnh cụ thể cho khách hàng.

Amazon Bedrock Agents cho phép bạn xây dựng các agent tự động có thể thực hiện các tác vụ thay mặt bạn. Các agent tự động gọi các API cần thiết để giao dịch với hệ thống và quy trình của bạn nhằm thực hiện yêu cầu, xác định trong quá trình đó xem họ có thể tiếp tục hay cần thu thập thêm thông tin.

Bạn có thể sử dụng Agents để tự động hóa các tác vụ trong tổ chức của mình như thế nào?

### Tài liệu bổ sung

[Retrieval-Augmented Generation là gì?](https://aws.amazon.com/what-is/retrieval-augmented-generation/)

[Agents for Amazon Bedrock](https://aws.amazon.com/bedrock/agents/)

[Cách thức hoạt động của Agents for Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-how.html)