+++
title = "Tạo Bedrock Agent"
date = 2025
weight = 1
chapter = false
pre = "<b>4.1. </b>"
+++

### Giới thiệu

Trong lab này, bạn sẽ thiết lập mục đích của agent và chọn foundational model phù hợp. Knowledge base sẽ được tích hợp để tăng cường khả năng sinh của agent, cho phép nó rút ra và tổng hợp thông tin từ thông tin sản phẩm và ticket hỗ trợ khách hàng.

### Các bước:

### Tạo agent

1. Mở [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/) **Amazon Bedrock**.

2. Chọn **Agents** từ navigation pane bên trái. Nó nằm dưới phần Builder Tools, ngay dưới Knowledge bases.

3. Trong phần Agents, chọn **Create Agent**.

4. Trên màn hình Create Agent, nhập tên và mô tả của agent.

   1. Tên:

   `customer-support-agent`

   2. Mô tả:

   `AI agent để truy xuất thông tin khách hàng và lịch sử ticket để hỗ trợ thêm cho các đại diện hỗ trợ giải quyết vấn đề của khách hàng.`

![1](../../../images/4/4.1/1.png)

3. Nhấp **Create**.

### Cấu hình agent

1.  Sau khi tạo agent, Agent builder mở ra để cấu hình thêm. Trong phần Agent details, hoàn thành những điều sau:

    1. Xác minh tên Agent và mô tả Agent mà bạn đã nhập trên màn hình trước.

    2. Đối với Agent resource role, chọn **Create and use a new service role** để Amazon Bedrock sẽ tạo service role thay mặt bạn.

    3. Trong phần Select model, chọn **Anthropic** và sau đó chọn **Claude 3.5 Sonnet** trong dropdown menu. Nhấp **Apply**.

    ![2](../../../images/4/4.1/2.png)

    4.  Trong **Instructions for the Agent**, nhập chi tiết để hướng dẫn agent về những gì nó nên làm và cách nó nên tương tác với người dùng. Những hướng dẫn này sẽ được sử dụng trong orchestration prompt template. Đây là các hướng dẫn để sử dụng cho agent:

            You are a personal assistant for a customer support representative.
            You will help the support representative retrieve customer details
            including order and support ticket history, and help the representative
            resolve customer issues. When the representative asks for help solving
            a customer's problem, please do your best to find a resolution.
            When you don't have enough information, try to resolve it anyway.
            Don't suggest opening a ticket.
            Never say, "Sorry, I don't have enough information to answer that."
            Instead, do your best to come up with a solution.

    5.  Mở rộng **Additional Settings**.

    6.  Dưới **User input**, chọn radio button cho **Enabled**. Điều này sẽ cho phép agent nhắc người dùng về thông tin bổ sung. Không thay đổi bất kỳ cài đặt bổ sung nào khác.

    ![3](../../../images/4/4.1/3.png)

2.  Nhấp nút **Save** ở trên cùng trước khi chuyển sang bước tiếp theo. Bạn sẽ nhận được thông báo khi agent được cập nhật thành công.

![4](../../../images/4/4.1/4.png)

{{%notice note%}}
Lưu ý các thông báo để chuẩn bị agent trước khi kiểm tra. Bạn sẽ chuẩn bị agent ở bước sau.
{{%/notice%}}

![5](../../../images/4/4.1/5.png)

3. Bỏ qua **Action groups** bây giờ và cuộn xuống **Knowledge bases**.

4. Trong phần **Knowledge bases**, chọn **Add** để liên kết knowledge base với agent của bạn.

![6](../../../images/4/4.1/6.png)

1. Đối với **Select knowledge base**, chọn knowledge base của bạn từ dropdown menu. Bạn sẽ thấy merger knowledge base mà bạn đã tạo trong lab trước.

2. Đối với **Knowledge base instructions for the agent**, nhập hướng dẫn để mô tả cách agent nên sử dụng knowledge base:

`Use this knowledge base to find information about products, customers, and how to resolve customer issues. The knowledge base contains product manuals and historical support tickets.`

3. Nhấp **Add**.

4. Nhấp **Save and exit**.

![7](../../../images/4/4.1/7.png)

5. Trong màn hình **Agent overview**, lưu ý mục dưới **Agent ARN**. Nó sẽ trông tương tự như ảnh chụp màn hình bên dưới. Đây là ARN được sử dụng để xác định agent của bạn. Sao chép giá trị này cho phần tiếp theo; bạn sẽ cần nó để cấp quyền cho agent này gọi Lambda function.

![8](../../../images/4/4.1/8.png)
