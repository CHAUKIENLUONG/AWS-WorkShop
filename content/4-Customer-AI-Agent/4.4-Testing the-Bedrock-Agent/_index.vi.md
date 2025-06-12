+++
title = "Kiểm thử Bedrock Agent"
date = 2025
weight = 4
chapter = false
pre = "<b>4.4. </b>"
+++

## Giới thiệu

Sau khi tạo agent, bạn sẽ có một bản nháp hoạt động để xây dựng agent của mình một cách lặp đi lặp lại. Mỗi khi bạn thay đổi agent, bản nháp sẽ được cập nhật.

Khi quá trình xây dựng agent hoàn tất, bạn có thể tạo một phiên bản và một bí danh. Sau đó, bạn có thể triển khai agent vào ứng dụng của mình bằng cách gọi bí danh đó.

### Kiểm thử bản nháp của bạn

Trong giao diện Amazon Bedrock, bạn mở cửa sổ kiểm thử và cung cấp đầu vào để tạo phản hồi từ agent.

Để giúp khắc phục sự cố về hành vi của agent, **Agents for Amazon Bedrock** cung cấp khả năng xem dấu vết trong một phiên làm việc với agent của bạn. Dấu vết cho thấy quy trình lập luận từng bước của agent.

### Các bước thực hiện

1. Trong hoạt động trước đó, bạn đã thêm nhóm hành động cho agent và bạn vẫn nên ở trang chi tiết agent. Nếu không, hãy quay lại [giao diện **Amazon Bedrock Agents**](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/agents) và chọn agent của bạn từ danh sách.

2. Cửa sổ Kiểm thử sẽ hiển thị ở khung bên phải. Nếu cửa sổ Kiểm thử đã đóng, bạn có thể mở lại bằng cách chọn Test ở đầu trang chi tiết agent.

3. Trước khi kiểm thử agent, bạn phải chuẩn bị nó. Trong cửa sổ Kiểm thử, chọn **Prepare**.

![1](../../../images/4/4.4/1.png)

{{%notice note%}}
Mỗi khi bạn cập nhật bản nháp, bạn phải chuẩn bị agent để đóng gói agent với những thay đổi mới nhất của bạn. Như một phương pháp hay nhất, chúng tôi khuyến nghị bạn luôn kiểm tra thời gian Chuẩn bị lần cuối của agent trong phần Tổng quan Agent của trang Bản nháp để xác minh rằng bạn đang kiểm thử agent với cấu hình mới nhất.
{{%/notice%}}

4. Để kiểm thử agent, nhập tin nhắn và chọn Run. Hãy bắt đầu với một lời chào đơn giản:

`Hi`

5. Trong khi bạn đợi phản hồi được tạo ra hoặc sau khi nó được tạo ra, chọn **Show trace**.

    ![2](../../../images/4/4.4/2.png)

    Dấu vết hiển thị chi tiết cho từng bước của quy trình điều phối agent, bao gồm lời nhắc, cấu hình suy luận và quy trình lập luận của agent cho từng bước và việc sử dụng nhóm hành động và cơ sở kiến thức của nó.

    1. Trong tab **Orchestration and knowledge base**, Mở rộng **Trace Step 1** và cuộn xuống. Chú ý ngữ cảnh bổ sung được cung cấp và cách lời nhắc được thiết kế để tạo ra phản hồi tốt nhất từ mô hình.

    ![3](../../../images/4/4.4/3.png)

    Khi được cung cấp một lời chào đơn giản, agent đáp lại với một lời chào đơn giản cho người dùng.

6. Yêu cầu agent tìm thông tin về khách hàng bằng ID khách hàng.

    `What can you tell me about customer 274877906944?`

    1. Khi agent đang làm việc, nhấp vào Show trace một lần nữa để xem dữ liệu theo dõi mới.

    2. Trong phần Orchestration and knowledge base, Trace Step 2, lưu ý cách agent quyết định gọi hàm.

    ![4](../../../images/4/4.4/4.png)

    3. Trong phản hồi cuối cùng, bạn sẽ thấy chi tiết về khách hàng này, bao gồm sản phẩm đã mua và ticket hỗ trợ từ cả Ampwerks và Ohmzio.

    ![5](../../../images/4/4.4/5.png)

  {{%notice note%}}
  Hãy nhớ rằng đầu ra của bạn có thể trông khác do sự khác biệt trong các mô hình ngôn ngữ lớn.
  {{%/notice%}}

7. Yêu cầu thêm thông tin để giúp khách hàng với vấn đề.

        The customer is having more issues with the Smart Pet Feeder. 
        The smart feeder is dispensing inconsistent amounts of food.

    1. Nhấp vào **Show trace** một lần nữa để xem dữ liệu theo dõi mới.

    2. Chú ý cách agent sử dụng thông tin khách hàng cũng như các ticket hỗ trợ liên quan từ cơ sở kiến thức để tạo phản hồi.
    
    ![6](../../../images/4/4.4/6.png)

    Cũng lưu ý đến [1] trong phản hồi. Nhấp vào chú thích để hiển thị tài liệu cơ sở kiến thức được sử dụng để tìm câu trả lời. Trong trường hợp này, agent đã có thể tìm thấy thông tin liên quan từ các ticket hỗ trợ Ohmzio trước đây.

8. Tiếp tục cuộc đối thoại.

`The customer checked the chute and there are no jams. What else could it be?`

Agent trả lời với các mẹo khắc phục sự cố bổ sung, bao gồm gợi ý hiệu chỉnh lại. Bạn có thể trả lời bằng cách yêu cầu thêm hướng dẫn.

`How do I recalibrate the smart feeder?`

![7](../../../images/4/4.4/7.png)

`The recalibration worked. The feeder is now dispensing the correct amount of food.`

![8](../../../images/4/4.4/8.png)

9. Thử nghiệm bằng cách đặt thêm một vài câu hỏi. Để bắt đầu một cuộc trò chuyện mới, sử dụng các ID khách hàng bổ sung có thể được tìm thấy trong bảng DynamoDB. Dưới đây là một số ID để thử:

        292057776128
        412316860425
        120259084303