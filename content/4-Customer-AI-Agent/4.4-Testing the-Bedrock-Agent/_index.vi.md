+++
title = "Kiểm tra Bedrock Agent"
date = 2025
weight = 4
chapter = false
pre = "<b>4.4. </b>"
+++

## Giới thiệu

Sau khi bạn tạo một agent, bạn sẽ có một bản nháp hoạt động mà bạn có thể sử dụng để xây dựng agent một cách lặp lại. Mỗi khi bạn thay đổi agent, bản nháp hoạt động sẽ được cập nhật.

Khi việc xây dựng agent hoàn tất, bạn có thể tạo một version và alias. Sau đó bạn có thể triển khai agent vào ứng dụng của mình bằng cách gọi alias.

### Kiểm tra bản nháp hoạt động

Trong Amazon Bedrock console, bạn mở cửa sổ test và cung cấp input để tạo ra phản hồi của agent.

Để giúp khắc phục sự cố hành vi của agent, **Agents for Amazon Bedrock** cung cấp khả năng xem trace trong quá trình phiên làm việc với agent. Trace hiển thị quá trình lý luận từng bước của agent.

### Các bước

1. Trong hoạt động trước, bạn đã thêm action group cho agent và bạn vẫn nên ở trên trang chi tiết agent. Nếu không, quay lại [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/agents) **Amazon Bedrock Agents** và chọn agent của bạn từ danh sách.

2. Cửa sổ Test nên ở trong pane bên phải. Nếu cửa sổ Test bị đóng, bạn có thể mở lại bằng cách chọn Test ở đầu trang chi tiết agent.

3. Trước khi kiểm tra agent, bạn phải chuẩn bị nó. Trong cửa sổ Test, chọn **Prepare**.

![1](../../../images/4/4.4/1.png)

{{%notice note%}}
Mỗi khi bạn cập nhật bản nháp hoạt động, bạn phải chuẩn bị agent để đóng gói agent với những thay đổi mới nhất của bạn. Như một thực hành tốt nhất, chúng tôi khuyến nghị bạn luôn kiểm tra Last prepared time của agent trong phần Agent overview của trang Working draft để xác minh rằng bạn đang kiểm tra agent với cấu hình mới nhất.
{{%/notice%}}

4. Để kiểm tra agent, nhập một tin nhắn và chọn Run. Hãy bắt đầu với một lời chào đơn giản:

`Hi`

5. Trong khi bạn chờ phản hồi được tạo hoặc sau khi nó được tạo, chọn **Show trace**.

   ![2](../../../images/4/4.4/2.png)

   Trace hiển thị chi tiết cho mỗi bước của quá trình điều phối agent, bao gồm prompt, cấu hình inference, và quá trình lý luận của agent cho mỗi bước và việc sử dụng action groups và knowledge bases.

   1. Trong tab **Orchestration and knowledge base**, Mở rộng **Trace Step 1** và cuộn xuống. Lưu ý context bổ sung được cung cấp và cách prompt được thiết kế để tạo ra phản hồi tốt nhất từ model.

   ![3](../../../images/4/4.4/3.png)

   Khi được cung cấp một lời chào đơn giản, agent phản hồi với một lời chào đơn giản lại cho người dùng.

6. Yêu cầu agent tìm thông tin về một khách hàng sử dụng customer ID.

   `What can you tell me about customer 274877906944?`

   1. Khi agent đang hoạt động, nhấp Show trace lại để xem dữ liệu tracing mới.

   2. Trong **Orchestration and knowledge base, Trace Step 2**, lưu ý cách agent quyết định gọi function.

   ![4](../../../images/4/4.4/4.png)

   3. Trong phản hồi cuối cùng, bạn sẽ thấy chi tiết cho khách hàng này, bao gồm sản phẩm đã mua và support tickets từ cả Ampwerks và Ohmzio.

   ![5](../../../images/4/4.4/5.png)

{{%notice note%}}
Hãy nhớ, output của bạn có thể trông khác dựa trên sự khác biệt trong các large language models.
{{%/notice%}}

7.  Yêu cầu thêm thông tin để giúp khách hàng với một vấn đề.

        The customer is having more issues with the Smart Pet Feeder.
        The smart feeder is dispensing inconsistent amounts of food.

    1. Nhấp **Show trace** lại để xem dữ liệu tracing mới.

    2. Lưu ý cách agent sử dụng thông tin khách hàng cũng như support tickets liên quan từ knowledge base để tạo phản hồi.

    ![6](../../../images/4/4.4/6.png)

    Cũng lưu ý **[1]** trong phản hồi. Nhấp vào footnote để hiển thị tài liệu knowledge base được sử dụng để tìm câu trả lời. Trong trường hợp này, agent đã có thể tìm thông tin liên quan từ các Ohmzio support tickets trong quá khứ.

8.  Tiếp tục cuộc hội thoại.

`The customer checked the chute and there are no jams. What else could it be?`

Agent phản hồi với các mẹo khắc phục sự cố bổ sung, bao gồm gợi ý về recalibration. Bạn có thể phản hồi bằng cách yêu cầu thêm hướng dẫn.

`How do I recalibrate the smart feeder?`

![7](../../../images/4/4.4/7.png)

`The recalibration worked. The feeder is now dispensing the correct amount of food.`

![8](../../../images/4/4.4/8.png)

9.  Thử nghiệm bằng cách hỏi thêm một vài câu hỏi. Để bắt đầu cuộc hội thoại mới, sử dụng các customer ID bổ sung có thể tìm thấy trong bảng DynamoDB. Đây là một vài ID để thử:

        292057776128
        412316860425
        120259084303
