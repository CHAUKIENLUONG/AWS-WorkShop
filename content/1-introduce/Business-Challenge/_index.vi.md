+++
title = "Thách thức kinh doanh"
date = 2025
weight = 3
chapter = false
pre = "<b>1.2. </b>"
+++

### Thách thức kinh doanh

Ohmzio, một công ty thiết bị nhà thông minh, đã mua lại Ampwerks, một nhà sản xuất phụ kiện xe điện, và hiện cần tích hợp sản phẩm, dữ liệu khách hàng và hệ thống hỗ trợ của Ampwerks vào cơ sở hạ tầng kinh doanh hiện có để hỗ trợ và bán dòng sản phẩm Ampwerks mới một cách hiệu quả. Điều này đòi hỏi phải hợp nhất các cơ sở dữ liệu khách hàng và sản phẩm riêng biệt, xác định cơ hội bán thêm trong danh mục sản phẩm kết hợp và thống nhất hệ thống hỗ trợ để mang lại trải nghiệm khách hàng liền mạch cho cả khách hàng Ohmzio và Ampwerks. Việc tích hợp hiệu quả hoạt động và dữ liệu sẽ là yếu tố quan trọng để hiện thực hóa các lợi ích tiềm năng của thương vụ mua lại.

### Mục tiêu

* Đảm bảo trải nghiệm khách hàng tuyệt vời trong quá trình sáp nhập
* Tích hợp hệ thống hỗ trợ
* Tạo cơ sở kiến thức cho kỹ sư hỗ trợ để cung cấp hỗ trợ khách hàng trên tất cả sản phẩm
* Tận dụng AI tạo sinh để tạo chatbot chuyên gia tư vấn cho kỹ sư hỗ trợ

### Tổng quan giải pháp

![1](../../../images/1/1.2/1.jpg)

### Các bước đã hoàn thành

Dữ liệu sản phẩm và trích xuất từ cả hai hệ thống hỗ trợ đã được lưu trữ trong bucket S3. Hướng dẫn sử dụng sản phẩm có dạng tệp docx và các ticket hỗ trợ đã được trích xuất dưới dạng tệp JSON.

Để tạo hồ sơ khách hàng hợp nhất, dữ liệu khách hàng và đơn hàng từ cả hai cơ sở dữ liệu Aurora của Ohmzio và Amperwerks đã được trích xuất và lưu trữ trong Amazon S3. Amazon Entity Resolution đã được sử dụng để khớp khách hàng và gán định danh khách hàng toàn cầu mới.

Thông tin khách hàng, đơn hàng và hỗ trợ hợp nhất đã được tải vào Amazon DynamoDB để truy xuất nhanh.

### Các bước sẽ thực hiện trong phòng thí nghiệm

Kết nối QuickSight với cơ sở dữ liệu Aurora của Ohmzio để hiểu rõ hơn về sản phẩm và sự cố hỗ trợ.

Sử dụng Amazon Bedrock để xây dựng Cơ sở kiến thức chứa thông tin về sản phẩm và hỗ trợ. Bedrock triển khai Amazon OpenSearch Serverless và sử dụng các mô hình Amazon Titan để tạo vector embeddings của dữ liệu.

Amazon Bedrock Agents được sử dụng để tương tác với cơ sở kiến thức và thực thi các hàm lambda để truy xuất thông tin khách hàng bổ sung.

