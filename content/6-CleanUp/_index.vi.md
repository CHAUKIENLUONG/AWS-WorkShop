+++
title = "Dọn Dẹp"
date = 2025
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

### Hướng dẫn

Nếu bạn đã thực hiện phòng lab này trên một tài khoản không do AWS cung cấp, hãy làm theo các bước sau để gỡ bỏ các tài nguyên của workshop.

1. Xóa Bedrock Agent và Action Groups đã tạo ở [4.1 Tạo Bedrock Agent](../4-Customer-AI-Agent/4.1-Creating%20a%20Bedrock%20Agent/_index.md).

2. Xóa Bedrock Knowledge Base đã tạo ở [3.1 Tạo Knowledge Base](../3-Product%20and%20Support-Knowledge-Base/3.1-Create%20a%20Knowledge%20Base/_index.md).

3. Xóa dữ liệu mẫu của workshop -- (Tùy chọn) Truy cập [S3 Console](https://us-west-2.console.aws.amazon.com/s3?region=us-west-2) và xóa bucket được tạo bởi template của workshop. Tên bucket sẽ là `customerdata-<stackid>`. Nếu bạn muốn giữ lại dữ liệu gốc, có thể bỏ qua bước này.

{{%notice info%}}
Nếu bỏ qua bước này, bucket S3 chứa toàn bộ dữ liệu mẫu sẽ vẫn còn trong tài khoản. Điều này sẽ phát sinh thêm khoảng ~24 MB dung lượng lưu trữ vào chi phí S3 hiện tại.
{{%/notice%}}

4. Xóa hạ tầng cơ bản -- Truy cập [CloudFormation](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks?filteringText=&filteringStatus=active&viewNested=true) và xóa stack ds-genai-workshop đã được triển khai cho workshop.
