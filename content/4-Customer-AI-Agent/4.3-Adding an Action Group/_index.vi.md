+++
title = "Thêm Action Group"
date = 2025
weight = 3
chapter = false
pre = "<b>4.3. </b>"
+++

### Giới thiệu

Action groups có thể được định nghĩa để chuyên biệt hóa thêm chức năng của agent, cho phép nó thực hiện các hành động hoặc quy trình cụ thể. Actions cũng có thể truy xuất thông tin bổ sung, cung cấp cho agent kiến thức và khả năng bổ sung cần thiết để tạo ra các phản hồi liên quan và mạch lạc.

### Các bước

1. Quay lại [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/agents) **Amazon Bedrock Agents**.

2. Chọn agent của bạn từ danh sách.

3. Chọn **Edit in Agent Builder**.

![1](../../../images/4/4.3/1.png)

4. Cuộn xuống **Action groups**.

{{%notice note%}}
Bedrock có thể đã tạo một action group mặc định ("UserInputAction") cho bạn. Nếu vậy, nhấp vào action group UserInputAction và làm theo các bước bên dưới để chỉnh sửa nó. Nếu bạn không có action group nào hiện có, nhấp Add để tạo một cái mới.
{{%/notice%}}

![2](../../../images/4/4.3/2.png)

5. Nhấp **Add**.

6. Trên trang Create (hoặc Edit) action group, hoàn thành những điều sau:

**Xem ảnh chụp màn hình bên dưới**

1. Nhập tên action group:

`agent-action-group`

2. Mô tả:

`Actions taken for the agent.`

3. Đối với **Action group type**, chọn **Define with function details**.

4. Đối với **Action group invocation**, chọn **Select an existing Lambda function**.

5. Đối với **Select Lambda function**, chọn **BedrockAction** và phiên bản $LATEST.

6. Nhập chi tiết cho **Action group function 1**.

   1. Tên:

   `GetCustomerDetails`

   2. Mô tả:

   `Retrieve customer by customer id and return the customer details, order history, and support history.`

   3. Confirmation nên được Disabled.

   4. Thêm parameter

   ![3](../../../images/4/4.3/3.png)

{{%notice note%}}
Nhấp vào dấu tích sau khi chỉnh sửa mỗi thuộc tính parameter.
{{%/notice%}}

![4](../../../images/4/4.3/4.png)

1. Tên:
   `cust_id`
2. Mô tả:
   `The ID of the customer.`
3. Loại
   `String`
4. Bắt buộc
   `True`
   ![5](../../../images/4/4.3/5.png)
   ![6](../../../images/4/4.3/6.png)
5. Nhấp **Create**.

6. Xác minh rằng action group đã được tạo.

![7](../../../images/4/4.3/7.png)

8. Cuộn lại lên trên và nhấp **Save and exit**.

9. Xác minh rằng agent đã được cập nhật.
   ![8](../../../images/4/4.3/8.png)
