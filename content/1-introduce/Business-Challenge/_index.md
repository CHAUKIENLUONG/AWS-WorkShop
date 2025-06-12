+++
title = "Business Challenge"
date = 2025
weight = 3
chapter = false
pre = "<b>1.2. </b>"
+++

### Business Challenge

Ohmzio, a smart home device company, has acquired Ampwerks, an electric vehicle accessories manufacturer, and now needs to integrate Ampwerks' products, customer data, and support systems into their existing business infrastructure in order to effectively support and sell the newly acquired Ampwerks product line. This will require consolidating separate customer and product databases, identifying upsell opportunities across the combined product portfolio, and unifying their support systems to provide a seamless customer experience for both Ohmzio and Ampwerks customers. Effectively integrating operations and data will be critical to realizing the potential benefits of the acquisition.

### Goals

* Ensure a delightful customer experience as we complete the merger
* Integrate support systems
* Create a knowledge base for support engineers to provide customer assistance across all products
* Leverage generative AI to create an expert chatbot to advise our support engineers

### Solution Overview

![1](../../images/1/1.2/1.jpg)

### Steps that have been completed

Product data and extracts from both support systems have been stored in an S3 bucket. The product manuals are available as docx files and the support tickets have been extracted as JSON files.

To create a consolidated customer record, customer and order data from both Ohmzio and Amperwerks Aurora databases has been extracted and stored in Amazon S3. Amazon Entity Resolution was used to match customers and assign a new global customer identifier.

The consolidated customer, order, and support information has been loaded into Amazon DynamoDB for fast retrieval.

### Steps that we will complete in the labs

Connect QuickSight to the Ohmzio Aurora database to gain better understanding of products and support incidents.

Use Amazon Bedrock to build a Knowledge Base containing product and support information. Bedrock deploys Amazon OpenSearch Serverless and uses Amazon Titan models to create vector embeddings of the data.

Amazon Bedrock Agents are used to interact with the knowledge base and execute lambda functions to retrieve additional customer information.

