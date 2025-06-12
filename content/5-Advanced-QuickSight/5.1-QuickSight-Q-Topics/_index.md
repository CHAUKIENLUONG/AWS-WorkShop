+++
title = "QuickSight Q Topics"
date = 2025
weight = 1
chapter = false
pre = "<b>5.1. </b>"
+++

### Introduction

In this step, we will create and test a **Q Topic** on the customer_support_discovery dataset that we created in the data discovery lab. The **Q topic** will accelerate data-driven decisions with humanistic Q&A, which includes:

* AI-generated narrative that highlights key insights
* Multi-visual answer to your question along with supporting visuals to add valuable context
* AI-generated and author-reviewed suggested questions and automated data previews

### Steps
### Review fields:

1. Navigate to the Amazon QuickSight [console](https://quicksight.aws.amazon.com/sn/start) .

2. To enable natural language query of your data, you first have to **create a topic**.

    1. On the QuickSight start page, choose **Topics**.

    2. On the Topics page that opens, choose **New topic** at upper right.

    ![1](../../images/5/5.1/1.png)
  {{%notice note%}}
  If you don't have the option to create a new topic, refresh the page. QuickSight needs your updated credentials.
  {{%/notice%}}

    3. On the **New topic** page that opens, enter **Topic name, Description**, and check **Use new generative Q&A experience**.

      * **Topic Name**:

      `Trouble Tickets`

      * **Topic Description**:

      `Explore ticket data`

      ![2](../../images/5/5.1/2.png)

    4. Click **Continue**. On **Select a dataset** screen choose the customer_support_discovery dataset and then choose **Create**.

  {{%notice note%}}
  The process of creating the QuickSight topic may take few minutes to complete depending on the size of your datasets. This step sets up the supporting resources needed for your QuickSight topic. Do not navigate away from this page until the topic has been fully created.
  {{%/notice%}}

3. After creating the topic, you should be taken directly to the topic's workspace. If you closed the popup window during topic creation, follow the additional steps below. Otherwise proceed with the topic review.

    1. Find the topic under **Amazon Q Topics** page.

    ![3](../../images/5/5.1/3.png)

    2. Click on Trouble Tickets topic name to open that topic's workspace.

4. You will review your topic settings by clicking on **Start Review** button on **Summary** tab of Trouble Tickets topic.

![4](../../images/5/5.1/4.png)

5. In the popup window, click **DISMISS ALL TASKS**. When asked to confirm, click** DISMISS ALL TASKS AGAIN**.

![5](../../images/5/5.1/5.png)

6. Create **Calculated Fields** to count the number of tickets, customers, and products.

    1. Select the **Data** tab, then **Data Fields**. Click the **Add calculated field** 
    button. 
    
    ![6](../../images/5/5.1/6.png)

    2. Enter **Name** in the calculations editor as :

    `Distinct Tickets Count`

    3. Search distinct_count function from Functions list available on the right and double-click on it to add it the workspace. Place your cursor inside the parenthesis in the workspace, and search ticket id from Fields list available on the right and double-click on it to add it the workspace.

    As an alternative, you can manually enter the calculation.

    `distinct_count({Ticket Id})`

    ![7](../../images/5/5.1/7.png)

    4. Save your calculation by choosing **Save** at upper right.

    5. Repeat the above steps to add two more **Calculated Fields**.

        1. Distinct Customers Count

        `Distinct Customers Count`

        `distinct_count({Customer Id})`

        ![8](../../images/5/5.1/8.png)

        2. Distinct Products Count
  
        `Distinct Products Count`

        `distinct_count({Product Id})`

      ![9](../../images/5/5.1/9.png)

7. In the **Data Fields** section, adjust the filter to show **All fields**.

![10](../../images/5/5.1/10.png)

8. In the **Data Fields** section, under **Include**, toggle the button ON and OFF to include/exclude fields for your topic. Start by excluding the unique identifiers: **Agent Id, Customer Id**, and **Product Id**.

9. For the included fields, add synonyms and details that Q will use to link fields to user questions. Include **Ticket Date**. Click the **+** sign to add the following synonyms to **Ticket Date**:

* **case date**
* **open date**
* **support date**

10. Click the **V** on the far right of the data field to expand it. Make sure the **Ticket Date** has a Role of **Dimension** and a Semantic Type of **Date**. Enter a description.

![11](../../images/5/5.1/11.png)

11. Use the table below to complete the review of the data fields in the Q topic. Include:

* **Category**
* **Company**
* **City**
* **Description**
* **Name**
* **Name Products**
* **State**
* **Ticket Date**

{{%notice note%}}
Remember, your field names for "Customer Name" and "Product Name" may be different if your join was performed in a different order.
{{%/notice%}}

| **Include** | **Friendly name** | **Synonyms** | **Details** | **Description** |
|---------|--------------|----------|----------|-------------|
| No | Address | | | |
| No | Agent Id | | | |
| Yes | Category | product category, product type | Dimension | The type of product. |
| Yes | City | town | Dimension, Location, City | The city where the customer lives. |
| Yes | Company | corporation, organization | Dimension, Organization | The customer's employer. |
| No | Customer Id | | | |
| No | Customer Id Customers | | | |
| Yes | Description | product description, product details | Dimension, Descriptive Text | Detailed product description. |
| Yes | Distinct Customers Count | customers, number of customers | Measure | The quantity of customers. |
| Yes | Distinct Products Count | number of products, products | Measure | The quantity of products. |
| Yes | Distinct Tickets Count | number of tickets, support cases | Measure | The quantity of support tickets. |
| No | Dob | | | |
| No | Email | | | |
| No | Job | | | |
| No | Latitude | | | |
| No | Longitude | | | |
| Yes | Name | customer name, customer | Dimension, Person | The customer's full name. |
| Yes | Name Products | product name, item, device, product | Dimension | Name of product. |
| No | Price | | | |
| No | Phone | | | |
| No | Product Id | | | |
| No | Product Id Products | | | |
| Yes | State | commonwealth | Dimension, Location, State | The state where the customer lives. |
| Yes | Ticket Date | case date, open date, support date | Dimension, Date | Date support ticket was opened. |
| No | Ticket Id | | | |
| No | Zip | | | |

### Review changes:

1. After updating the data fields, filter the view to show only the included fields. 

![12](../../images/5/5.1/12.png)

2. Verify that your included data fields match the image below. 

![13](../../images/5/5.1/13.png)

### Test your topic:

1. In the the center of the top blue bar on your **topic** screen, click **Ask a question about Trouble Tickets**. Let's use this **topic** to uncover additional insights by asking questions in natural language. 

![14](../../images/5/5.1/14.png)

2. In the **Amazon Q** bar, copy the following prompt, and click **ASK**

`Number of tickets by product type?`

Here is a sample generative response: 

![15](../../images/5/5.1/15.png)

{{%notice note%}}
If the topic returns a blank window, try refreshing the page and resubmitting the question.
{{%/notice%}}

Experiment by asking a few more questions.

`Which products had the most support cases last year?`

`Which products had the most issues in December?`

`Which location had the most most support cases?`

{{%notice note%}}
Tip - To help you form questions, think Who, What, Where, When and Why.
{{%/notice%}}

4. When you are finished asking questions, close **Ask Questions** screen by clicking behind the popup window. This will return to the **Trouble Tickets** summary tab.

![16](../../images/5/5.1/16.png)

5. Click on **User Activity** tab to see user statistics. This will provide data on every question asked and how well Q responded. In this tab you can analyze topic performance and update topic details based on feedback. 

![17](../../images/5/5.1/17.png)