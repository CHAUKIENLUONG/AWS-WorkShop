+++
title = "Cấu hình Quyền Lambda"
date = 2025
weight = 2
chapter = false
pre = "<b>4.2. </b>"
+++

### Giới thiệu

Trong lab này, bạn sẽ cấu hình quyền để cho phép agent thực thi một **AWS Lambda** function.

**AWS Lambda** là một dịch vụ tính toán serverless cực kỳ mạnh mẽ và linh hoạt. Với Lambda, bạn không phải lo lắng về việc cung cấp hoặc quản lý servers. Lambda tự động mở rộng ứng dụng của bạn để đáp ứng với lưu lượng hoặc nhu cầu tăng lên, đảm bảo rằng ứng dụng của bạn có thể xử lý khối lượng công việc mà không cần can thiệp thủ công.

Bằng cách kết hợp **AWS Lambda** và **Agents for Amazon Bedrock**, bạn có thể xây dựng các hệ thống tự động hóa và workflow serverless phức tạp. Bedrock agents có thể được sử dụng để kích hoạt Lambda functions, và các Lambda functions sau đó có thể điều phối một chuỗi các hành động, chẳng hạn như cập nhật databases, gửi thông báo, hoặc gọi các dịch vụ khác.

Trong lab này, chúng ta sẽ sử dụng agent của mình để gọi một lambda function truy xuất thông tin khách hàng từ bảng **Amazon DynamoDB**.

**Amazon DynamoDB** là một dịch vụ database mạnh mẽ và có thể mở rộng, tự động mở rộng để xử lý bất kỳ lượng dữ liệu và lưu lượng nào, mà không cần cung cấp hoặc quản lý servers. Nó có thể xử lý tới hàng triệu requests mỗi giây, với độ trễ nhất quán, một chữ số millisecond.

Để agent của bạn sử dụng một **Lambda** function, bạn phải đính kèm một resource-based policy vào function để cung cấp quyền cho agent.

### Các bước

1. Mở [console](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions) **AWS Lambda Functions**.

2. Trong danh sách functions, chọn tên function **BedrockAction**. Function để truy xuất dữ liệu khách hàng đã được tạo và triển khai trước lab. Chúng ta sẽ không thay đổi bất kỳ code nào, chỉ thiết lập quyền.

![1](../../../images/4/4.2/1.png)

3. Tab Code được mở theo mặc định. Chọn Configuration. Tiếp theo, trong menu bên trái, chọn **Permissions**. Nó nên là mục thứ ba từ trên xuống.

![2](../../../images/4/4.2/2.png)

4. Cuộn xuống **Resource-based policy statements**.

![3](../../../images/4/4.2/3.png)

5. Nhấp **Add permissions**.

6. Trên trang **Add permissions**, cấu hình những điều sau:

   1. Chọn **AWS service**.

   2. Trong dropdown Service, chọn **Other**.

   3. Trong hộp văn bản **Statement ID**, nhập:

   `my-custom-id-0001`

   4. Trong hộp văn bản **Principal**, nhập:

   `bedrock.amazonaws.com`

   5. Trong hộp văn bản **Source ARN** dán Agent ARN mà bạn đã sao chép sau khi tạo agent. Nó sẽ trông tương tự như:

   ![4](../../../images/4/4.2/4.png)

   6. Trong dropdown **Action**, chọn **lambda:InvokeFunction**.

   7. Nhấp **Save**.

   ![5](../../../images/4/4.2/5.png)

7. Xác minh rằng Lambda Resource-based policy statement của bạn đã được lưu.

![6](../../../images/4/4.2/6.png)
