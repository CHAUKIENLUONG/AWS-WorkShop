+++
title = "Quản lý Tài sản QuickSight"
date = 2025
weight = 1
chapter = false
pre = "<b>2.1. </b>"
+++

### Giới thiệu

Trong phần này, chúng ta sẽ quản lý các tài sản QuickSight để cho phép người dùng QuickSight truy cập các nguồn dữ liệu đã được tạo sẵn. Những nguồn dữ liệu được tạo sẵn này cho phép QuickSight truy cập các cơ sở dữ liệu nguồn.

### Các bước:

### Chia sẻ nguồn dữ liệu với người dùng QuickSight

1. Điều hướng đến [console](https://quicksight.aws.amazon.com/sn/start) Amazon QuickSight.
2. Nếu xuất hiện **What's New in Amazon QuickSight**, nhấp vào đóng.
   ![1](../../../images/2/2.1/1.png)
3. Đăng nhập DataSources
   Truy cập console quản lý QuickSight, nhấp vào biểu tượng **user** nằm trên dải đen phía trên bên phải. Nhấp **Manage QuickSight** từ menu dropdown.

![2](../../../images/2/2.1/2.png)

{{% notice %}}
Đây là console quản trị viên QuickSight. Từ đây, các quản trị viên QuickSight có thể quản lý người dùng, nhóm, tài sản; thiết lập bảo mật tài khoản và quyền để cho phép QuickSight truy cập các tài nguyên AWS khác; quản lý tài nguyên cấp mạng.
{{% /notice %}}

4. Nhấp **Manage assets** trong menu bên trái. Đây là nơi chúng ta sẽ cho phép người dùng của mình truy cập các nguồn dữ liệu đã được tạo sẵn.

5. Trong console Manage assets, nhấp **Data sources** trong phần Browse assets ở dưới cùng.

![3](../../../images/2/2.1/3.png)

6. Hai nguồn dữ liệu chúng ta cần chia sẻ là ohmzio-database và ampwerks-database. Chia sẻ chúng bằng cách tích vào ô bên trái và sau đó nhấp vào nút **SHARE (2)**.

![4](../../../images/2/2.1/4.png)

7. Trong trường User or Group, nhập email sau: `participant-d2e2@amazon.com`. Nhấp vào tên người dùng WSParticipantRole/Participant - ADMIN_PRO để điền vào trường. Nhấp **SHARE (2)**.

   `participant-d2e2@amazon.com`

![5](../../../images/2/2.1/5.png)

![6](../../../images/2/2.1/6.png)

8. Sau khi các tài sản đã được chia sẻ thành công, nhấp **DONE**. Bỏ qua thông báo "What's New in Amazon QuickSight".

### Xác minh các nguồn dữ liệu đã được chia sẻ chính xác

1. Điều hướng lại trang chủ QuickSight bằng cách nhấp vào biểu tượng **QuickSight** trên dải đen phía trên bên trái.

![7](../../../images/2/2.1/7.png)

2. Nhấp **Datasets** trong menu bên trái, sau đó nhấp **New dataset** ở góc trên bên phải.

![8](../../../images/2/2.1/8.png)

3. Trong trang Create a Dataset, trong phần FROM EXISTING DATA SOURCES ở dưới cùng, bạn sẽ thấy hai tùy chọn: ohmzio-database và ampwerks-database.

![9](../../../images/2/2.1/9.png)
