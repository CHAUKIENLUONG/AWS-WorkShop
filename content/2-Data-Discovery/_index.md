+++
title = "Data Discovery"
date = 2025
weight = 2
chapter = false
pre = "<b>2. </b>"
+++

### Background

As technologists working on the recent Ampwerks and Ohmzio merger, it is up to us to understand the state of each company's data. Both Ampwerks and Ohmzio databases have been migrated to an AWS account. Additionally, our account has been subscribed to Amazon QuickSight.

In this lab, we will configure Amazon QuickSight to allow us to explore data from Ampwerks and Ohmzio databases. The data we will use for this lab is a collection of customer, order, and product data. Here is the schema for each of the databases:

### Ohmzio Database Schema

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

### Ampwerks Database Schema

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

### Steps
* Log into QuickSight console
* Manage data source assets to enable access
* Create new datasets for each database using the QuickSight visual data configuration tool
* Create visuals to uncover initial customer and product insights for each company