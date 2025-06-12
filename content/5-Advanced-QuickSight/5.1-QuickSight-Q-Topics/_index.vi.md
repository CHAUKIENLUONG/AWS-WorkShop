+++
title = "QuickSight Q Topics"
date = 2025
weight = 1
chapter = false
pre = "<b>5.1. </b>"
+++

### Giới thiệu

Trong bước này, chúng ta sẽ tạo và kiểm tra một **Q Topic** trên bộ dữ liệu customer_support_discovery mà chúng ta đã tạo trong phòng thí nghiệm khám phá dữ liệu. **Q topic** sẽ đẩy nhanh các quyết định dựa trên dữ liệu với Q&A theo ngôn ngữ tự nhiên, bao gồm:

* Tường thuật được tạo bởi AI làm nổi bật các thông tin quan trọng
* Câu trả lời đa hình ảnh cho câu hỏi của bạn cùng với hình ảnh hỗ trợ để thêm ngữ cảnh có giá trị
* Câu hỏi gợi ý được tạo bởi AI và được tác giả xem xét cùng với bản xem trước dữ liệu tự động

### Các bước thực hiện
### Xem xét các trường:

1. Điều hướng đến [bảng điều khiển](https://quicksight.aws.amazon.com/sn/start) Amazon QuickSight.

2. Để kích hoạt truy vấn ngôn ngữ tự nhiên cho dữ liệu của bạn, trước tiên bạn phải **tạo một topic**.

    1. Trên trang khởi động QuickSight, chọn **Topics**.

    2. Trên trang Topics mở ra, chọn **New topic** ở góc trên bên phải.

    ![1](/images/5/5.1/1.png)
  {{%notice note%}}
  Nếu bạn không thấy tùy chọn tạo topic mới, hãy làm mới trang. QuickSight cần thông tin xác thực cập nhật của bạn.
  {{%/notice%}}

    3. Trên trang **New topic** mở ra, nhập **Tên chủ đề, Mô tả**, và đánh dấu chọn **Sử dụng trải nghiệm Q&A tạo sinh mới**.

      * **Tên chủ đề**:

      `Vé sự cố`

      * **Mô tả chủ đề**:

      `Khám phá dữ liệu vé`

      ![2](/images/5/5.1/2.png)

    4. Nhấp vào **Tiếp tục**. Trên màn hình **Chọn bộ dữ liệu**, chọn bộ dữ liệu customer_support_discovery và sau đó chọn **Tạo**.

  {{%notice note%}}
  Quá trình tạo chủ đề QuickSight có thể mất vài phút để hoàn thành tùy thuộc vào kích thước của các bộ dữ liệu của bạn. Bước này thiết lập các tài nguyên hỗ trợ cần thiết cho chủ đề QuickSight của bạn. Đừng điều hướng ra khỏi trang này cho đến khi chủ đề đã được tạo hoàn toàn.
  {{%/notice%}}

3. Sau khi tạo chủ đề, bạn sẽ được đưa trực tiếp đến không gian làm việc của chủ đề. Nếu bạn đã đóng cửa sổ popup trong quá trình tạo chủ đề, hãy làm theo các bước bổ sung bên dưới. Nếu không, hãy tiếp tục với việc xem xét chủ đề.

    1. Tìm chủ đề dưới trang **Amazon Q Topics**.

    ![3](/images/5/5.1/3.png)

    2. Nhấp vào tên chủ đề Vé sự cố để mở không gian làm việc của chủ đề đó.

4. Bạn sẽ xem xét cài đặt chủ đề của mình bằng cách nhấp vào nút **Bắt đầu xem xét** trên tab **Tóm tắt** của chủ đề Vé sự cố.

![4](/images/5/5.1/4.png)

5. Trong cửa sổ popup, nhấp vào **BỎ QUA TẤT CẢ CÁC NHIỆM VỤ**. Khi được yêu cầu xác nhận, nhấp vào **BỎ QUA TẤT CẢ CÁC NHIỆM VỤ MỘT LẦN NỮA**.

![5](/images/5/5.1/5.png)

6. Tạo **Trường Tính toán** để đếm số lượng vé, khách hàng và sản phẩm.

    1. Chọn tab **Dữ liệu**, sau đó là **Trường Dữ liệu**. Nhấp vào nút **Thêm trường tính toán**.
    
    ![6](/images/5/5.1/6.png)

    2. Nhập **Tên** trong trình chỉnh sửa tính toán như sau:

    `Số lượng vé duy nhất`

    3. Tìm kiếm hàm distinct_count từ danh sách Các hàm có sẵn ở bên phải và nhấp đúp vào nó để thêm nó vào không gian làm việc. Đặt con trỏ của bạn bên trong dấu ngoặc đơn trong không gian làm việc, và tìm kiếm mã vé từ danh sách Các trường có sẵn ở bên phải và nhấp đúp vào nó để thêm nó vào không gian làm việc.

    Là một sự thay thế, bạn có thể nhập thủ công phép tính.

    `distinct_count({Ticket Id})`

    ![7](/images/5/5.1/7.png)

    4. Lưu phép tính của bạn bằng cách chọn **Lưu** ở góc trên bên phải.

    5. Lặp lại các bước trên để thêm hai **Trường Tính toán** nữa.

        1. Số lượng Khách hàng duy nhất

        `Số lượng Khách hàng duy nhất`

        `distinct_count({Customer Id})`

        ![8](/images/5/5.1/8.png)

        2. Số lượng Sản phẩm duy nhất
  
        `Số lượng Sản phẩm duy nhất`

        `distinct_count({Product Id})`

      ![9](/images/5/5.1/9.png)

7. Trong phần **Trường Dữ liệu**, điều chỉnh bộ lọc để hiển thị **Tất cả các trường**.

![10](/images/5/5.1/10.png)

8. Trong phần **Trường Dữ liệu**, dưới **Bao gồm**, chuyển đổi nút BẬT và TẮT để bao gồm/loại trừ các trường cho chủ đề của bạn. Bắt đầu bằng cách loại trừ các định danh duy nhất: **Agent Id, Customer Id**, và **Product Id**.

9. Đối với các trường đã bao gồm, thêm các từ đồng nghĩa và chi tiết mà Q sẽ sử dụng để liên kết các trường với các câu hỏi của người dùng. Bao gồm **Ngày vé**. Nhấp vào dấu **+** để thêm các từ đồng nghĩa sau vào **Ngày vé**:

* **ngày trường hợp**
* **ngày mở**
* **ngày hỗ trợ**

10. Nhấp vào **V** ở bên phải xa của trường dữ liệu để mở rộng nó. Đảm bảo rằng **Ngày vé** có Vai trò là **Kích thước** và Loại Ngữ nghĩa là **Ngày**. Nhập một mô tả.

![11](/images/5/5.1/11.png)

11. Sử dụng bảng bên dưới để hoàn thành việc xem xét các trường dữ liệu trong chủ đề Q. Bao gồm:

* **Danh mục**
* **Công ty**
* **Thành phố**
* **Mô tả**
* **Tên**
* **Tên Sản phẩm**
* **Tiểu bang**
* **Ngày vé**

{{%notice note%}}
Nhớ rằng, tên trường của bạn cho "Tên Khách hàng" và "Tên Sản phẩm" có thể khác nếu phép nối của bạn được thực hiện theo một thứ tự khác.
{{%/notice%}}

| **Bao gồm** | **Tên thân thiện** | **Từ đồng nghĩa** | **Chi tiết** | **Mô tả** |
|---------|--------------|----------|----------|-------------|
| Không | Địa chỉ | | | |
| Không | Agent Id | | | |
| Có | Danh mục | loại sản phẩm, kiểu sản phẩm | Kích thước | Loại sản phẩm. |
| Có | Thành phố | thị trấn | Kích thước, Địa điểm, Thành phố | Thành phố nơi khách hàng sinh sống. |
| Có | Công ty | tập đoàn, tổ chức | Kích thước, Tổ chức | Nhà tuyển dụng của khách hàng. |
| Không | Customer Id | | | |
| Không | Customer Id Customers | | | |
| Có | Mô tả | mô tả sản phẩm, chi tiết sản phẩm | Kích thước, Văn bản mô tả | Mô tả chi tiết sản phẩm. |
| Có | Số lượng Khách hàng duy nhất | khách hàng, số lượng khách hàng | Đo lường | Số lượng khách hàng. |
| Có | Số lượng Sản phẩm duy nhất | số lượng sản phẩm, sản phẩm | Đo lường | Số lượng sản phẩm. |
| Có | Số lượng Vé duy nhất | số lượng vé, trường hợp hỗ trợ | Đo lường | Số lượng vé hỗ trợ. |
| Không | Dob | | | |
| Không | Email | | | |
| Không | Công việc | | | |
| Không | Vĩ độ | | | |
| Không | Kinh độ | | | |
| Có | Tên | tên khách hàng, khách hàng | Kích thước, Người | Họ và tên đầy đủ của khách hàng. |
| Có | Tên Sản phẩm | tên sản phẩm, mặt hàng, thiết bị, sản phẩm | Kích thước | Tên sản phẩm. |
| Không | Giá | | | |
| Không | Điện thoại | | | |
| Không | Product Id | | | |
| Không | Product Id Products | | | |
| Có | Tiểu bang | bang | Kích thước, Địa điểm, Tiểu bang | Bang nơi khách hàng sinh sống. |
| Có | Ngày vé | ngày trường hợp, ngày mở, ngày hỗ trợ | Kích thước, Ngày | Ngày vé hỗ trợ được mở. |
| Không | Ticket Id | | | |
| Không | Mã bưu điện | | | |

### Xem xét các thay đổi:

1. Sau khi cập nhật các trường dữ liệu, lọc chế độ xem để chỉ hiển thị các trường đã bao gồm. 

![12](/images/5/5.1/12.png)

2. Xác minh rằng các trường dữ liệu đã bao gồm của bạn khớp với hình ảnh bên dưới. 

![13](/images/5/5.1/13.png)

### Kiểm tra chủ đề của bạn:

1. Ở giữa thanh màu xanh lam ở đầu màn hình **chủ đề** của bạn, nhấp vào **Hỏi một câu hỏi về Vé sự cố**. Hãy sử dụng **chủ đề** này để khám phá thêm thông tin chi tiết bằng cách đặt câu hỏi bằng ngôn ngữ tự nhiên. 

![14](/images/5/5.1/14.png)

2. Trong thanh **Amazon Q**, sao chép đoạn văn bản sau, và nhấp vào **HỎI**

`Số lượng vé theo loại sản phẩm?`

Dưới đây là một phản hồi tạo sinh mẫu: 

![15](/images/5/5.1/15.png)

{{%notice note%}}
Nếu chủ đề trả về một cửa sổ trống, hãy thử làm mới trang và gửi lại câu hỏi.
{{%/notice%}}

Thử nghiệm bằng cách đặt một vài câu hỏi nữa.

`Những sản phẩm nào có nhiều trường hợp hỗ trợ nhất trong năm ngoái?`

`Những sản phẩm nào có nhiều sự cố nhất vào tháng Mười Hai?`

`Địa điểm nào có nhiều trường hợp hỗ trợ nhất?`

{{%notice note%}}
Mẹo - Để giúp bạn hình thành câu hỏi, hãy nghĩ đến Ai, Cái gì, Ở đâu, Khi nào và Tại sao.
{{%/notice%}}

4. Khi bạn đã hoàn thành việc đặt câu hỏi, hãy đóng màn hình **Hỏi Các Câu Hỏi** bằng cách nhấp ra ngoài cửa sổ popup. Điều này sẽ trở lại tab tóm tắt **Vé sự cố**.

![16](/images/5/5.1/16.png)

5. Nhấp vào tab **Hoạt động Người dùng** để xem thống kê người dùng. Điều này sẽ cung cấp dữ liệu về mọi câu hỏi đã được đặt và mức độ phản hồi của Q. Trong tab này, bạn có thể phân tích hiệu suất chủ đề và cập nhật chi tiết chủ đề dựa trên phản hồi. 

![17](/images/5/5.1/17.png)