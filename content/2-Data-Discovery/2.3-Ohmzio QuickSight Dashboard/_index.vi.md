+++
title = "Bảng điều khiển Ohmzio QuickSight"
date = 2025
weight = 3
chapter = false
pre = "<b>2.3. </b>"
+++

### Giới thiệu

Trong phần này, chúng ta sẽ tạo một phân tích về các loại yêu cầu và vấn đề mà khách hàng đang gặp phải, điều này có thể giúp xác định các lĩnh vực cần cải thiện trong sản phẩm và dịch vụ.

### Các bước thực hiện:

### Tạo phân tích mới từ tập dữ liệu

1. Điều hướng đến trang QuickSight [Datasets](https://quicksight.aws.amazon.com/sn/console/signup).

2. Nhấp vào nút menu ba chấm ⋮ bên cạnh tập dữ liệu customer_support_discovery, sau đó chọn **CREATE ANALYSIS**.

![1](../../../images/2/2.3/1.png)

3. Trong cửa sổ **New sheet**, giữ nguyên lựa chọn **Interactive sheet** và nhấp vào nút **CREATE**.

### Phân tích số lượng ticket hỗ trợ theo tháng

1. Hãy bắt đầu bằng việc phân tích số lượng ticket hỗ trợ độc nhất nhận được theo tháng.

2. Nhấp vào biểu đồ trống và thay đổi loại biểu đồ thành biểu đồ đường.

![2](../../../images/2/2.3/2.png)

3. Từ **fields list** trong **primary left pane**:

   * kéo ticket_date vào trường **X axis**
   * kéo ticket_id vào trường **value**

4. Mặc định, bạn sẽ thấy ticket_date được tổng hợp theo ngày. Nhấp vào biểu tượng ba chấm bên cạnh trường ticket_date trong phần **X AXIS** để truy cập menu cấp trường của biểu đồ để thay đổi tổng hợp từ ngày sang tháng.

5. Nhấp vào biểu tượng ba chấm bên cạnh trường ticket_id trong phần **VALUE** để truy cập menu cấp trường của biểu đồ để thay đổi tổng hợp từ count sang count distinct để có được số lượng ticket độc nhất.

![3](../../../images/2/2.3/3.gif)

{{%notice%}}
Phân tích dữ liệu lịch sử cho thấy xu hướng tăng chung về số lượng ticket qua các tháng, cho thấy nhu cầu dịch vụ hỗ trợ ngày càng tăng.
{{%/notice%}}

### Phân tích yêu cầu hỗ trợ theo loại sản phẩm

1. Tiếp theo, hãy xem phân bố yêu cầu hỗ trợ trên các loại sản phẩm khác nhau.

2. Chọn Add trên thanh ứng dụng, sau đó chọn Add visual. Chọn biểu đồ Donut từ menu.

![4](../../../images/2/2.3/4.png)

3. Từ Fields list trong primary left pane thêm các trường cần thiết theo thứ tự sau:

   * kéo category vào trường Group/Color
   * kéo ticket_id vào trường Value

![5](../../../images/2/2.3/5.gif)

{{% notice %}}
Phân tích cho thấy danh mục Lighting có số lượng ticket nhiều nhất.
{{% /notice %}}

### Phân tích sản phẩm có nhiều yêu cầu hỗ trợ nhất

1. Tiếp theo, hãy xem sản phẩm nào có số lượng ticket hỗ trợ nhiều nhất.

2. Chọn Add trên thanh ứng dụng, sau đó chọn Add visual. Chọn **Tree map** từ menu.

![6](../../../images/2/2.3/6.png)

3. Từ Fields list trong primary left pane thêm các trường cần thiết theo thứ tự sau:

   * kéo name[products] vào trường **GROUP BY**

{{% notice info %}}
Bạn có thể thấy name[customers] thay vì name[products]. Bởi vì cả bảng customers và products đều có cột tên "name", QuickSight đổi tên một trong số chúng. Đảm bảo bạn chọn name[products] hoặc chỉ name nếu bạn chỉ thấy name[customers].
{{% /notice %}}

   * kéo ticket_id vào trường **Color**

{{% notice note %}}
Ký hiệu trong ngoặc vuông cho products chỉ ra rằng thuộc tính này xuất phát từ bảng products. Khi join các bảng có cùng tên cột, QuickSight giải quyết điều này bằng cách thêm tên bảng. Nếu bạn join support_tickets với bảng products trước khi join với bảng customers, tên cột của bạn sẽ khác.
{{% /notice %}}

![7](../../../images/2/2.3/7.gif)

{{%notice%}}
Phân tích cho thấy sản phẩm **Ohmzio Smart Plug** có số lượng ticket nhiều nhất.
{{%/notice%}}

### Thêm insights được đề xuất

1. Tiếp theo, hãy thêm các insights được đề xuất.

2. Nhấp vào biểu đồ Tree map để chỉ ra đây là biểu đồ chúng ta muốn dựa vào để tạo insights (khi được chọn, sẽ có khung màu đen xung quanh). Tiếp theo, nhấp vào biểu tượng **Insights** (biểu tượng hình bóng đèn). Panel Insights mở ra và hiển thị danh sách các insights sẵn sàng sử dụng được đề xuất. Cuộn xuống để xem trước các insights mà chúng ta có thể thêm vào bảng điều khiển dựa trên dữ liệu và xu hướng trong biểu đồ Tree map.

![8](../../../images/2/2.3/8.png)

3. Thêm một insight được đề xuất (ví dụ: **Top 3 Products by Ticket Count**) vào phân tích của bạn bằng cách chọn dấu cộng (+) gần tiêu đề insight.

![9](../../../images/2/2.3/9.png)

4. Bạn có thể điều chỉnh kích thước của insights nhỏ hơn và di chuyển chúng lên trên biểu đồ **Tree Map**.

![10](../../../images/2/2.3/10.gif)

{{%notice%}}
Các insights tự động tạo ra cho thấy các sản phẩm Smart Plug và Smart Vent có số lượng ticket nhiều nhất.
{{%/notice%}}
