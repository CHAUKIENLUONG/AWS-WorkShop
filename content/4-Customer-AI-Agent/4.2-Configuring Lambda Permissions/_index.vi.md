+++
title = "Cấu hình quyền cho Lambda"
date = 2025
weight = 2
chapter = false
pre = "<b>4.2. </b>"
+++

### Giới thiệu

Trong bài lab này, bạn sẽ cấu hình các quyền để cho phép agent thực thi một hàm **AWS Lambda**.

**AWS Lambda** là một dịch vụ điện toán serverless mạnh mẽ và linh hoạt. Với Lambda, bạn không cần phải lo lắng về việc cung cấp hoặc quản lý máy chủ. Lambda tự động mở rộng ứng dụng của bạn để đáp ứng lưu lượng hoặc nhu cầu tăng cao, đảm bảo ứng dụng của bạn có thể xử lý khối lượng công việc mà không cần can thiệp thủ công.

Bằng cách kết hợp **AWS Lambda** và **Agents for Amazon Bedrock**, bạn có thể xây dựng các hệ thống tự động hóa và quy trình làm việc phức tạp, không cần máy chủ. Các agent Bedrock có thể được sử dụng để kích hoạt các hàm Lambda, và các hàm Lambda sau đó có thể điều phối một loạt các hành động, như cập nhật cơ sở dữ liệu, gửi thông báo, hoặc gọi các dịch vụ khác.

Trong bài lab này, chúng ta sẽ sử dụng agent của mình để gọi một hàm lambda nhằm truy xuất thông tin khách hàng từ bảng **Amazon DynamoDB**.

**Amazon DynamoDB** là một dịch vụ cơ sở dữ liệu mạnh mẽ và có khả năng mở rộng tự động để xử lý bất kỳ lượng dữ liệu và lưu lượng truy cập nào, mà không cần cung cấp hoặc quản lý máy chủ. Nó có thể xử lý lên đến hàng triệu yêu cầu mỗi giây, với độ trễ ổn định ở mức vài mili giây.

Để agent của bạn có thể sử dụng hàm **Lambda**, bạn phải gắn một chính sách dựa trên tài nguyên vào hàm để cấp quyền cho agent.

### Các bước thực hiện

1. Mở [bảng điều khiển](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions) **AWS Lambda Functions**.

2. Trong danh sách các hàm, chọn tên hàm **BedrockAction**. Hàm để truy xuất dữ liệu khách hàng đã được tạo và triển khai trước bài lab. Chúng ta sẽ không thay đổi bất kỳ mã nào, chỉ thiết lập quyền.

![1](../../../images/4/4.2/1.png)

3. Tab Code được mở theo mặc định. Chọn Configuration. Tiếp theo, trong menu bên trái, chọn **Permissions**. Nó sẽ là mục thứ ba từ trên xuống.

![2](../../../images/4/4.2/2.png)

4. Cuộn xuống phần **Resource-based policy statements**.

![3](../../../images/4/4.2/3.png)

5. Nhấp vào **Add permissions**.

6. Trên trang **Add permissions**, cấu hình các mục sau:

    1. Chọn **AWS service**.

    2. Trong danh sách Service, chọn **Other**.

    3. Trong ô **Statement ID**, nhập:


    `my-custom-id-0001`

    4. Trong ô *Principal*, nhập:

    `bedrock.amazonaws.com`

    5. Trong ô **Source ARN**, dán ARN của Agent mà bạn đã sao chép sau khi tạo agent. Nó sẽ có dạng tương tự như:

    ![4](../../../images/4/4.2/4.png)

    6. Trong danh sách **Action**, chọn **lambda:InvokeFunction**.

    7. Nhấp **Save**.

    ![5](../../../images/4/4.2/5.png)

7. Xác minh rằng chính sách dựa trên tài nguyên Lambda của bạn đã được lưu.

![6](../../../images/4/4.2/6.png)