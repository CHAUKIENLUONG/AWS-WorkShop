+++
title = "Dashboard QuickSight Ohmzio"
date = 2025
weight = 3
chapter = false
pre = "<b>2.3. </b>"
+++

### Giới thiệu

Trong phần này, chúng ta sẽ tạo một phân tích để phân tích các loại yêu cầu và vấn đề mà khách hàng đang đưa ra, điều này có thể giúp xác định các lĩnh vực cần cải thiện trong sản phẩm và dịch vụ.

### Các bước:

### Tạo phân tích mới từ dataset

1. Điều hướng đến trang [Datasets](https://quicksight.aws.amazon.com/sn/console/signup) QuickSight.

2. Nhấp vào nút menu ellipsis ⋮ bên cạnh dataset customer_support_discovery, sau đó chọn **CREATE ANALYSIS**.

![1](../../../images/2/2.3/1.png)

3. Trên pop-up **New sheet**, để **Interactive sheet** được chọn và nhấp nút **CREATE**.

### Phân tích khối lượng ticket hỗ trợ theo tháng

1. Hãy bắt đầu bằng cách phân tích khối lượng ticket hỗ trợ duy nhất nhận được theo cơ sở hàng tháng.

2. Nhấp vào visual trống và thay đổi loại visual thành biểu đồ đường.

![2](../../../images/2/2.3/2.png)

3. Từ **danh sách fields** trong **primary left pane**:

   - kéo ticket_date vào trường **X axis**
   - kéo ticket_id vào trường **value**

4. Theo mặc định, bạn sẽ thấy ticket_date được tổng hợp theo ngày. Nhấp vào ellipsis bên cạnh trường ticket_date từ phần **X AXIS** của visual để truy cập menu field cấp visual để thay đổi tổng hợp từ ngày sang tháng.

5. Nhấp vào ellipsis bên cạnh trường ticket_id từ phần **VALUE** của visual để truy cập menu field cấp visual để thay đổi tổng hợp từ count sang count distinct để lấy số lượng ticket duy nhất.

![3](../../../images/2/2.3/3.gif)

{{%notice%}}
Phân tích dữ liệu lịch sử cho thấy tổng thể xu hướng tăng lên trong khối lượng ticket qua các tháng, cho thấy nhu cầu ngày càng tăng cho các dịch vụ hỗ trợ.
{{%/notice%}}

### Phân tích yêu cầu hỗ trợ theo loại sản phẩm

1. Tiếp theo hãy xem phân phối các yêu cầu hỗ trợ trên các loại sản phẩm khác nhau.

2. Chọn Add trên thanh ứng dụng, sau đó chọn Add visual. Chọn **Donut chart** từ menu.

![4](../../../images/2/2.3/4.png)

3. Từ danh sách Fields trong primary left pane thêm các trường cần thiết theo thứ tự sau:

   - kéo category vào trường **Group/Color**
   - kéo ticket_id vào trường **Value**

![5](../../../images/2/2.3/5.gif)

{{% notice %}}
Phân tích cho thấy danh mục **Lighting** có khối lượng ticket nhiều nhất.
{{% /notice %}}

### Phân tích sản phẩm có nhiều yêu cầu hỗ trợ nhất

1. Tiếp theo hãy xem sản phẩm nào có số lượng ticket hỗ trợ nhiều nhất.

2. Chọn Add trên thanh ứng dụng, sau đó chọn Add visual. Chọn **Tree map** từ menu.

![6](../../../images/2/2.3/6.png)

3. Từ danh sách Fields trong primary left pane thêm các trường cần thiết theo thứ tự sau:

   - kéo name[products] vào trường **GROUP BY**

{{% notice info %}}
Bạn có thể thấy name[customers] thay vì name[products]. Vì cả bảng customers và products đều có cột có tên "name", Quicksight đổi tên một trong số chúng. Hãy đảm bảo bạn chọn name[products] hoặc chỉ name nếu bạn chỉ thấy name[customers].
{{% /notice %}}

- kéo ticket_id vào trường **Color**

{{% notice note %}}
Ký hiệu ngoặc vuông cho products cho biết thuộc tính có nguồn gốc từ bảng products. Khi join các bảng có cùng tên cột, QuickSight giải quyết điều này bằng cách thêm tên bảng. Nếu bạn join support_tickets với bảng products trước khi join với bảng customers, tên cột của bạn sẽ khác.
{{% /notice %}}

![7](../../../images/2/2.3/7.gif)

{{%notice%}}
Phân tích cho thấy sản phẩm **Ohmzio Smart Plug** có khối lượng ticket nhiều nhất.
{{%/notice%}}

### Thêm insights được gợi ý

1. Tiếp theo hãy thêm các insights được gợi ý.

2. Nhấp vào visual Tree map để chỉ ra đây là visual chúng ta muốn dựa insights từ đó (khi được chọn, sẽ có hộp đen xung quanh chu vi). Tiếp theo, nhấp vào biểu tượng **Insights** (biểu tượng hình bóng đèn). Panel Insights mở ra và hiển thị danh sách các insights được gợi ý sẵn sàng sử dụng. Cuộn xuống để xem trước các insights chúng ta có thể thêm vào dashboard dựa trên dữ liệu và xu hướng trong visual Tree map.

![8](../../../images/2/2.3/8.png)

3. Thêm một insight được gợi ý (như **Top 3 Products by Ticket Count**) vào phân tích của bạn bằng cách chọn dấu cộng (+) gần tiêu đề insight.

![9](../../../images/2/2.3/9.png)

4. Bạn có thể thay đổi kích thước insights để nhỏ hơn và di chuyển chúng lên trên visual **Tree Map** của bạn.

![10](../../../images/2/2.3/10.gif)

{{%notice%}}
Các insights được tạo tự động cho thấy rằng sản phẩm Smart Plug và Smart Vent có khối lượng ticket nhiều nhất.
{{%/notice%}}
