+++
title = "Khám Phá Dữ Liệu"
date = 2025
weight = 2
chapter = false
pre = "<b>2. </b>"
+++

### Bối Cảnh

Là các chuyên gia công nghệ làm việc trong quá trình sáp nhập gần đây giữa Ampwerks và Ohmzio, chúng ta cần phải hiểu rõ tình trạng dữ liệu của mỗi công ty. Cơ sở dữ liệu của cả Ampwerks và Ohmzio đã được chuyển đến một tài khoản AWS. Ngoài ra, tài khoản của chúng ta đã được đăng ký Amazon QuickSight.

Trong bài thực hành này, chúng ta sẽ cấu hình Amazon QuickSight để khám phá dữ liệu từ cơ sở dữ liệu của Ampwerks và Ohmzio. Dữ liệu chúng ta sẽ sử dụng là tập hợp các thông tin về khách hàng, đơn hàng và sản phẩm. Dưới đây là sơ đồ cơ sở dữ liệu của mỗi công ty:

### Sơ Đồ Cơ Sở Dữ Liệu Ohmzio

    ohmziodb
    ├── products
    │   ├── product_id INT NOT NULL
    │   ├── name VARCHAR(100) NOT NULL
    │   ├── category VARCHAR(50) NOT NULL
    │   ├── description VARCHAR(500) NOT NULL
    │   ├── price DECIMAL(10,2) NOT NULL
    │   └── PRIMARY KEY (product_id)
    ├── customers
    │   ├── customer_id VARCHAR(20) NOT NULL
    │   ├── phone VARCHAR(20)
    │   ├── name VARCHAR(100)
    │   ├── address VARCHAR(200)
    │   ├── city VARCHAR(100)
    │   ├── state VARCHAR(100)
    │   ├── zip VARCHAR(10)
    │   ├── dob DATE
    │   ├── company VARCHAR(200)
    │   ├── job VARCHAR(100)
    │   ├── email VARCHAR(100)
    │   ├── latitude DECIMAL(9,6)
    │   ├── longitude DECIMAL(9,6)
    │   └── PRIMARY KEY (customer_id)
    ├── support_agents
    │   ├── agent_id INT NOT NULL
    │   ├── fname VARCHAR(50) NOT NULL
    │   ├── lname VARCHAR(50) NOT NULL
    │   └── PRIMARY KEY (agent_id)
    ├── order_header
    │   ├── order_id VARCHAR(20) NOT NULL
    │   ├── customer_id VARCHAR(20) NOT NULL
    │   ├── order_date DATE NOT NULL
    │   ├── total DECIMAL(10,2) NOT NULL DEFAULT 0
    │   ├── PRIMARY KEY (order_id)
    │   └── FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
    └── order_items
        ├── order_id VARCHAR(20) NOT NULL
        ├── product_id INT NOT NULL
        ├── unit_price DECIMAL(10,2) NOT NULL
        ├── qty INT NOT NULL
        ├── item_total DECIMAL(10,2) NOT NULL
        ├── PRIMARY KEY (order_id, product_id)
        ├── FOREIGN KEY (order_id) REFERENCES order_header(order_id)
        └── FOREIGN KEY (product_id) REFERENCES products(product_id)

### Sơ Đồ Cơ Sở Dữ Liệu Ampwerks

    ampwerksdb
    ├── products
    │   ├── product_id INT PRIMARY KEY
    │   ├── name VARCHAR(255) NOT NULL
    │   ├── type VARCHAR(255) NOT NULL
    │   ├── price DECIMAL(10,2) NOT NULL
    │   ├── voltage VARCHAR(255)
    │   └── connectors VARCHAR(255)
    ├── customers
    │   ├── customer_id VARCHAR(20) NOT NULL
    │   ├── phone VARCHAR(20)
    │   ├── name VARCHAR(100)
    │   ├── address VARCHAR(200)
    │   ├── city VARCHAR(100)
    │   ├── state VARCHAR(100)
    │   ├── zip VARCHAR(10)
    │   ├── dob DATE
    │   ├── company VARCHAR(200)
    │   ├── job VARCHAR(100)
    │   ├── email VARCHAR(100)
    │   ├── latitude DECIMAL(9,6)
    │   ├── longitude DECIMAL(9,6)
    │   └── PRIMARY KEY (customer_id)
    ├── support_agents
    │   ├── agent_id INT NOT NULL
    │   ├── fname VARCHAR(50) NOT NULL
    │   ├── lname VARCHAR(50) NOT NULL
    │   └── PRIMARY KEY (agent_id)
    ├── order_header
    │   ├── order_id VARCHAR(20) NOT NULL
    │   ├── customer_id VARCHAR(20) NOT NULL
    │   ├── order_date DATE NOT NULL
    │   ├── total DECIMAL(10,2) NOT NULL DEFAULT 0
    │   ├── PRIMARY KEY (order_id)
    │   └── FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
    ├── order_items
    │   ├── order_id VARCHAR(20) NOT NULL
    │   ├── product_id INT NOT NULL
    │   ├── unit_price DECIMAL(10,2) NOT NULL
    │   ├── qty INT NOT NULL
    │   ├── item_total DECIMAL(10,2) NOT NULL
    │   ├── PRIMARY KEY (order_id, product_id)
    │   ├── FOREIGN KEY (order_id) REFERENCES order_header(order_id)
    │   └── FOREIGN KEY (product_id) REFERENCES products(product_id)
    └── support_tickets
        ├── ticket_id VARCHAR(20) NOT NULL
        ├── customer_id VARCHAR(20) NOT NULL
        ├── product_id INT NOT NULL
        ├── agent_id INT NOT NULL
        ├── ticket_date DATE NOT NULL
        ├── PRIMARY KEY (ticket_id)
        ├── FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
        ├── FOREIGN KEY (product_id) REFERENCES products(product_id)
        └── FOREIGN KEY (agent_id) REFERENCES support_agents(agent_id)

### Các Bước Thực Hiện
* Đăng nhập vào bảng điều khiển QuickSight
* Quản lý các tài nguyên nguồn dữ liệu để kích hoạt quyền truy cập
* Tạo bộ dữ liệu mới cho mỗi cơ sở dữ liệu sử dụng công cụ cấu hình dữ liệu trực quan của QuickSight
* Tạo các biểu đồ để khám phá thông tin ban đầu về khách hàng và sản phẩm của mỗi công ty