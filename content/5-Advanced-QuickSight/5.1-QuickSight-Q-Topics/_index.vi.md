+++
title = "QuickSight Q Topics"
date = 2025
weight = 1
chapter = false
pre = "<b>5.1. </b>"
+++

### Giới thiệu

Trong bước này, chúng ta sẽ tạo và kiểm tra một **Q Topic** trên dataset customer_support_discovery mà chúng ta đã tạo trong lab khám phá dữ liệu. **Q topic** sẽ tăng tốc các quyết định dựa trên dữ liệu với Q&A nhân văn, bao gồm:

- Tường thuật được tạo bởi AI làm nổi bật các insights chính
- Câu trả lời đa hình ảnh cho câu hỏi của bạn cùng với các hình ảnh hỗ trợ để thêm context có giá trị
- Các câu hỏi được gợi ý được tạo bởi AI và được tác giả xem xét cùng với các bản xem trước dữ liệu tự động

### Các bước

### Xem xét các trường:

1.  Điều hướng đến [console](https://quicksight.aws.amazon.com/sn/start) Amazon QuickSight.

2.  Để bật truy vấn ngôn ngữ tự nhiên cho dữ liệu của bạn, bạn trước tiên phải **tạo một topic**.

    1. Trên trang bắt đầu QuickSight, chọn **Topics**.

    2. Trên trang Topics mở ra, chọn **New topic** ở góc trên bên phải.

    ![1](../../../images/5/5.1/1.png)
    
  {{%notice note%}}
  Nếu bạn không có tùy chọn tạo topic mới, hãy làm mới trang. QuickSight cần thông tin đăng nhập cập nhật của bạn.
  {{%/notice%}}

  3. Trên trang **New topic** mở ra, nhập **Topic name, Description**, và tích **Use new generative Q&A experience**.

       - **Topic Name**:

       `Trouble Tickets`

       - **Topic Description**:

       `Explore ticket data`

       ![2](../../../images/5/5.1/2.png)

  4. Nhấp **Continue**. Trên màn hình **Select a dataset** chọn dataset customer_support_discovery và sau đó chọn **Create**.

{{%notice note%}}
Quá trình tạo QuickSight topic có thể mất vài phút để hoàn thành tùy thuộc vào kích thước của datasets của bạn. Bước này thiết lập các tài nguyên hỗ trợ cần thiết cho QuickSight topic của bạn. Không điều hướng khỏi trang này cho đến khi topic được tạo hoàn toàn.
{{%/notice%}}

3. Sau khi tạo topic, bạn sẽ được đưa trực tiếp đến workspace của topic. Nếu bạn đóng cửa sổ popup trong quá trình tạo topic, làm theo các bước bổ sung bên dưới. Nếu không, tiếp tục với việc xem xét topic.

   1. Tìm topic dưới trang **Amazon Q Topics**.

   ![3](../../../images/5/5.1/3.png)

   2. Nhấp vào tên topic Trouble Tickets để mở workspace của topic đó.

4. Bạn sẽ xem xét cài đặt topic bằng cách nhấp vào nút **Start Review** trên tab **Summary** của topic Trouble Tickets.

![4](../../../images/5/5.1/4.png)

5. Trong cửa sổ popup, nhấp **DISMISS ALL TASKS**. Khi được hỏi để xác nhận, nhấp **DISMISS ALL TASKS AGAIN**.

![5](../../../images/5/5.1/5.png)

6. Tạo **Calculated Fields** để đếm số lượng tickets, customers, và products.

   1. Chọn tab **Data**, sau đó **Data Fields**. Nhấp nút **Add calculated field**.

   ![6](../../../images/5/5.1/6.png)

   2. Nhập **Name** trong trình soạn thảo tính toán như:

   `Distinct Tickets Count`

   3. Tìm kiếm function **distinct_count** từ danh sách **Functions** có sẵn bên phải và nhấp đúp vào nó để thêm vào workspace. Đặt con trỏ của bạn bên trong dấu ngoặc trong workspace, và tìm kiếm **ticket id** từ danh sách **Fields** có sẵn bên phải và nhấp đúp vào nó để thêm vào workspace.

   Như một lựa chọn thay thế, bạn có thể nhập tính toán thủ công.

   `distinct_count({Ticket Id})`

   ![7](../../../images/5/5.1/7.png)

   4. Lưu tính toán của bạn bằng cách chọn **Save** ở góc trên bên phải.

   5. Lặp lại các bước trên để thêm hai **Calculated Fields** nữa.

      1. Distinct Customers Count

      `Distinct Customers Count`

      `distinct_count({Customer Id})`

      ![8](../../../images/5/5.1/8.png)

      2. Distinct Products Count

      `Distinct Products Count`

      `distinct_count({Product Id})`

   ![9](../../../images/5/5.1/9.png)

7. Trong phần **Data Fields**, điều chỉnh bộ lọc để hiển thị **All fields**.

![10](../../../images/5/5.1/10.png)

8. Trong phần **Data Fields**, dưới **Include**, bật tắt nút ON và OFF để bao gồm/loại trừ các trường cho topic của bạn. Bắt đầu bằng cách loại trừ các định danh duy nhất: **Agent Id, Customer Id**, và **Product Id**.

9. Đối với các trường được bao gồm, thêm synonyms và chi tiết mà Q sẽ sử dụng để liên kết các trường với câu hỏi của người dùng. Bao gồm **Ticket Date**. Nhấp dấu **+** để thêm các synonyms sau vào **Ticket Date**:

- **case date**
- **open date**
- **support date**

10. Nhấp **V** ở bên phải xa nhất của data field để mở rộng nó. Đảm bảo **Ticket Date** có Role là **Dimension** và Semantic Type là **Date**. Nhập mô tả.

![11](../../../images/5/5.1/11.png)

11. Sử dụng bảng bên dưới để hoàn thành việc xem xét các data fields trong Q topic. Bao gồm:

- **Category**
- **Company**
- **City**
- **Description**
- **Name**
- **Name Products**
- **State**
- **Ticket Date**

{{%notice note%}}
Hãy nhớ, tên trường của bạn cho "Customer Name" và "Product Name" có thể khác nếu join của bạn được thực hiện theo thứ tự khác.
{{%/notice%}}

| **Include** | **Friendly name**        | **Synonyms**                         | **Details**                 | **Description**                     |
| ----------- | ------------------------ | ------------------------------------ | --------------------------- | ----------------------------------- |
| No          | Address                  |                                      |                             |                                     |
| No          | Agent Id                 |                                      |                             |                                     |
| Yes         | Category                 | product category, product type       | Dimension                   | The type of product.                |
| Yes         | City                     | town                                 | Dimension, Location, City   | The city where the customer lives.  |
| Yes         | Company                  | corporation, organization            | Dimension, Organization     | The customer's employer.            |
| No          | Customer Id              |                                      |                             |                                     |
| No          | Customer Id Customers    |                                      |                             |                                     |
| Yes         | Description              | product description, product details | Dimension, Descriptive Text | Detailed product description.       |
| Yes         | Distinct Customers Count | customers, number of customers       | Measure                     | The quantity of customers.          |
| Yes         | Distinct Products Count  | number of products, products         | Measure                     | The quantity of products.           |
| Yes         | Distinct Tickets Count   | number of tickets, support cases     | Measure                     | The quantity of support tickets.    |
| No          | Dob                      |                                      |                             |                                     |
| No          | Email                    |                                      |                             |                                     |
| No          | Job                      |                                      |                             |                                     |
| No          | Latitude                 |                                      |                             |                                     |
| No          | Longitude                |                                      |                             |                                     |
| Yes         | Name                     | customer name, customer              | Dimension, Person           | The customer's full name.           |
| Yes         | Name Products            | product name, item, device, product  | Dimension                   | Name of product.                    |
| No          | Price                    |                                      |                             |                                     |
| No          | Phone                    |                                      |                             |                                     |
| No          | Product Id               |                                      |                             |                                     |
| No          | Product Id Products      |                                      |                             |                                     |
| Yes         | State                    | commonwealth                         | Dimension, Location, State  | The state where the customer lives. |
| Yes         | Ticket Date              | case date, open date, support date   | Dimension, Date             | Date support ticket was opened.     |
| No          | Ticket Id                |                                      |                             |                                     |
| No          | Zip                      |                                      |                             |                                     |

### Xem xét thay đổi:

1. Sau khi cập nhật data fields, lọc view để chỉ hiển thị các trường được bao gồm.

![12](../../../images/5/5.1/12.png)

2. Xác minh rằng data fields được bao gồm của bạn khớp với hình ảnh bên dưới.

![13](../../../images/5/5.1/13.png)

### Kiểm tra topic của bạn:

1. Ở giữa thanh xanh phía trên trên màn hình **topic** của bạn, nhấp **Ask a question about Trouble Tickets**. Hãy sử dụng **topic** này để khám phá thêm insights bằng cách đặt câu hỏi bằng ngôn ngữ tự nhiên.

![14](../../../images/5/5.1/14.png)

2. Trong thanh **Amazon Q**, sao chép prompt sau, và nhấp **ASK**

`Number of tickets by product type?`

Đây là một phản hồi sinh mẫu:

![15](../../../images/5/5.1/15.png)

{{%notice note%}}
Nếu topic trả về cửa sổ trống, hãy thử làm mới trang và gửi lại câu hỏi.
{{%/notice%}}

3. Thử nghiệm bằng cách hỏi thêm một vài câu hỏi.

`Which products had the most support cases last year?`

`Which products had the most issues in December?`

`Which location had the most most support cases?`

{{%notice note%}}
**Mẹo** - Để giúp bạn hình thành câu hỏi, hãy nghĩ Who, What, Where, When và Why.
{{%/notice%}}

4. Khi bạn hoàn thành việc đặt câu hỏi, đóng màn hình **Ask Questions** bằng cách nhấp phía sau cửa sổ popup. Điều này sẽ quay lại tab **Trouble Tickets** summary.

![16](../../../images/5/5.1/16.png)

5. Nhấp vào tab **User Activity** để xem thống kê người dùng. Điều này sẽ cung cấp dữ liệu về mọi câu hỏi được hỏi và Q phản hồi tốt như thế nào. Trong tab này bạn có thể phân tích hiệu suất topic và cập nhật chi tiết topic dựa trên phản hồi.

![17](../../../images/5/5.1/17.png)
