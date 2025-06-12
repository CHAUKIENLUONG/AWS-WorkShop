+++
title = "Tạo Bedrock Agent"
date = 2025
weight = 1
chapter = false
pre = "<b>4.1. </b>"
+++

### Giới thiệu

Trong bài thực hành này, bạn sẽ thiết lập mục đích của agent và chọn foundation model phù hợp. Knowledge base sẽ được tích hợp để tăng cường khả năng sinh nội dung của agent, cho phép nó truy xuất và tổng hợp thông tin từ thông tin sản phẩm và ticket hỗ trợ khách hàng.

### Các bước thực hiện:

### Tạo agent

1. Mở **Amazon Bedrock** [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/).

2. Chọn **Agents** từ thanh điều hướng bên trái. Nó nằm trong phần Builder Tools, ngay dưới Knowledge bases.

3. Trong phần Agents, chọn **Create Agent**.

4. Trên màn hình Create Agent, nhập tên và mô tả cho agent của bạn.

5. Tên:

`customer-support-agent`

2. Mô tả:

`AI agent để truy xuất thông tin khách hàng và lịch sử ticket nhằm hỗ trợ nhân viên support giải quyết các vấn đề của khách hàng.`

![1](/images/4/4.1/1.png)

3. Nhấp **Create**.

### Cấu hình agent

1. Sau khi tạo agent, Agent builder sẽ mở ra để cấu hình thêm. Trong phần Agent details, hoàn thành các mục sau:

    1. Xác nhận Agent name và Agent description mà bạn đã nhập ở màn hình trước.

    2. Đối với Agent resource role, chọn **Create and use a new service role** để Amazon Bedrock sẽ tạo service role thay bạn.

    3. Ở phần Select model, chọn **Anthropic** và sau đó chọn **Claude 3.5 Sonnet** trong menu thả xuống. Nhấp **Apply**.

    ![2](/images/4/4.1/2.png)

    4. Trong **Instructions for the Agent**, nhập chi tiết để hướng dẫn agent về những gì nó nên làm và cách tương tác với người dùng. Những hướng dẫn này sẽ được sử dụng trong mẫu orchestration prompt. Dưới đây là hướng dẫn cần sử dụng cho agent:


            Bạn là trợ lý cá nhân cho nhân viên hỗ trợ khách hàng.
            Bạn sẽ giúp nhân viên hỗ trợ truy xuất chi tiết khách hàng
            bao gồm lịch sử đơn hàng và ticket hỗ trợ, đồng thời giúp nhân viên
            giải quyết các vấn đề của khách hàng. Khi nhân viên yêu cầu giúp đỡ giải quyết
            vấn đề của khách hàng, hãy cố gắng hết sức để tìm ra giải pháp.
            Khi không có đủ thông tin, hãy cố gắng giải quyết dù sao.
            Đừng đề xuất mở ticket mới.
            Đừng bao giờ nói "Xin lỗi, tôi không có đủ thông tin để trả lời."
            Thay vào đó, hãy cố gắng hết sức để đưa ra giải pháp.

    5. Mở rộng **Additional Settings**.

    6. Trong phần **User input**, chọn radio button **Enabled**. Điều này sẽ cho phép agent nhắc người dùng cung cấp thêm thông tin. Không thay đổi bất kỳ cài đặt bổ sung nào khác.

    ![3](/images/4/4.1/3.png)

2. Nhấp nút **Save** ở trên cùng trước khi chuyển sang bước tiếp theo. Bạn sẽ nhận được thông báo khi agent được cập nhật thành công.

![4](/images/4/4.1/4.png)

{{%notice note%}}
Lưu ý các thông báo để chuẩn bị agent trước khi kiểm tra. Bạn sẽ chuẩn bị agent ở bước sau.
{{%/notice%}}

![5](/images/4/4.1/5.png)

3. Bỏ qua phần **Action groups** và cuộn xuống **Knowledge bases**.

4. Trong phần **Knowledge bases**, chọn **Add** để liên kết knowledge base với agent của bạn.

![6](/images/4/4.1/6.png)

  1. Đối với **Select knowledge base**, chọn knowledge base của bạn từ menu thả xuống. Bạn sẽ thấy knowledge base merger mà bạn đã tạo trong bài thực hành trước đó.

  2. Đối với **Knowledge base instructions for the agent**, nhập hướng dẫn để mô tả cách agent nên sử dụng knowledge base:

  `Sử dụng knowledge base này để tìm thông tin về sản phẩm, khách hàng, và cách giải quyết các vấn đề của khách hàng. Knowledge base chứa hướng dẫn sử dụng sản phẩm và lịch sử ticket hỗ trợ.`

  3. Nhấp **Add**.

  4. Nhấp **Save and exit**.

  ![7](/images/4/4.1/7.png)

  5. Trong màn hình **Agent overview**, lưu ý mục **Agent ARN**. Nó sẽ trông giống như ảnh chụp màn hình bên dưới. Đây là ARN được sử dụng để xác định agent của bạn. Sao chép giá trị này cho phần tiếp theo; bạn sẽ cần nó để cấp quyền cho agent này gọi hàm Lambda.

  ![8](/images/4/4.1/8.png)
