+++
title = "Quicksight Q Data Stories"
date = 2025
weight = 2
chapter = false
pre = "<b>5.2. </b>"
+++

### Giới thiệu
Trong bước này, chúng ta sẽ tạo và kiểm tra một **Q Data story** bằng cách xuất bản dashboard phân tích hỗ trợ khách hàng mà chúng ta đã tạo trong phòng thí nghiệm khám phá dữ liệu. Chúng ta sẽ sử dụng câu lệnh Amazon Q và các biểu đồ để tạo ra một bản nháp có chứa các chi tiết mà bạn cung cấp.

### Các bước thực hiện

1. Quay trở lại menu chính của QuickSight bằng cách nhấp vào liên kết **QuickSight** ở góc trên bên trái.

![1](../../../images/5/5.2/1.png)

2. Nhấp vào menu **Analyses** và mở Analysis customer_support_discovery mà chúng ta đã tạo trong phòng thí nghiệm **Data Discovery**.

![2](../../../images/5/5.2/2.png)

3. Từ thanh menu phía trên, nhấp vào nút **PUBLISH**.

![3](../../../images/5/5.2/3.png)

4. Chọn **Publish new dashboard as**, sau đó nhập tên dashboard.

* **Tên Dashboard**:

`Customer Support Dashboard`

![4](../../../images/5/5.2/4.png)

5. Gần đoạn văn bản cảnh báo, nhấp vào **Link topic. Enable Link Topic for Build Visual and Q&A**. Trong menu thả xuống **Topic**, chọn Trouble Tickets. Nhấp vào **Apply Changes**. Quá trình liên kết có thể mất vài phút, vì vậy hãy nhấp vào **X** ở góc trên bên phải của cửa sổ popup để đóng và tiếp tục.

![5](../../../images/5/5.2/5.png)

6. Nhấp vào nút **Publish Dashboard**.

7. Nhấp vào nút **Build** ở đầu trang dashboard.

![6](../../../images/5/5.2/6.png)

8. Chọn **Data story**. Hoặc, điều hướng đến màn hình bắt đầu của Amazon QuickSight, chọn **Data stories**, sau đó chọn NEW STORY.

![7](../../../images/5/5.2/7.png)

9. Trong màn hình Story xuất hiện, điều hướng đến modal Build data story và sao chép mẫu câu lệnh data story này vào **Describe the data story you need**. Gợi ý: Để có kết quả tốt nhất, đừng đặt câu lệnh dưới dạng câu hỏi. Thay vào đó, hãy nhập data story mà bạn muốn QuickSight xây dựng.

`Giải thích xu hướng của các ticket hỗ trợ theo sản phẩm và khu vực. Đề xuất các lĩnh vực cần có biện pháp khắc phục.`

10. Chọn **Add visuals** để thêm các biểu đồ hỗ trợ cho câu chuyện của bạn.

11. Chọn dashboard **Customer Support Dashboard** từ danh sách **All dashboards** và chọn cả ba biểu đồ của phân tích của bạn, bao gồm **Support Tickets per Month, Tickets by Product Category, Tickets by Product**.

![8](../../../images/5/5.2/8.png)

12. Khi bạn đã hoàn tất việc chọn các biểu đồ, chọn **Add** và sau đó chọn **Build**.

13. Sau khi data story được tạo, bạn có thể xem xét và chỉnh sửa để phù hợp hơn với nhu cầu của bạn. Bạn có thể định dạng văn bản data story, thêm hình ảnh, chỉnh sửa biểu đồ và thêm các khối mới.

![9](../../../images/5/5.2/9.png)