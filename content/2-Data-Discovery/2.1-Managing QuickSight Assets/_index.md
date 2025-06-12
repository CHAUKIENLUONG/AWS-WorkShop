+++
title = "Managing QuickSight Assets"
date = 2025
weight = 1
chapter = false
pre = "<b>2.1. </b>"
+++

### Introduction

In this section, we will be managing QuickSight assets to enable QuickSight users to access data sources that have already been created. These pre-made data sources enable QuickSight to access the source databases.

### Steps:

### Share data sources with QuickSight users

1. Navigate to the Amazon QuickSight [console](https://quicksight.aws.amazon.com/sn/start).
2. If presented with **What's New in Amazon QuickSight**, click close.
![1](../../images/2/2.1/1.png)
3. DataSources Login
   Access the QuickSight management console, click the **user** icon located on the top black ribbon on the right hand side. Click **Manage QuickSight** from the dropdown menu.

![2](../../images/2/2.1/2.png)

{{% notice %}}
This is the QuickSight administrator console. From here, QuickSight administrators can manage users, groups, assets; set account security and permissions to enable QuickSight access to other AWS resources; manage network level resources.
{{% /notice %}}

4. Click **Manage assets** on the left menu. Here is where we will enable our user to access the data sources that have been already created.

5. In the Manage assets console, click **Data sources** in the bottom Browse assets section.

![3](../../images/2/2.1/3.png)

6. The two data sources we need to share are the ohmzio-database and ampwerks-database data sources. Share these by checking the box on the left and then clicking on the **SHARE (2)** button.

![4](../../images/2/2.1/4.png)

7. In the User or Group field, enter the following email: `participant-d2e2@amazon.com`. Click on the username WSParticipantRole/Participant - ADMIN_PRO to populate the field. Click **SHARE (2)**.

   `participant-d2e2@amazon.com`

![5](../../images/2/2.1/5.png)

![6](../../images/2/2.1/6.png)

8. Once the assets have been shared successfully, click DONE. Ignore the "What's New in Amazon QuickSight" prompt.

### Verify the data sources were shared correctly

1. Navigate back to the QuickSight landing page by clicking the **QuickSight** icon in the top black ribbon on the left side.

![7](../../images/2/2.1/7.png)

2. Click **Datasets** in the left menu, then click **New dataset** in the upper right hand corner.

![8](../../images/2/2.1/8.png)

3. In the Create a Dataset landing page, in the bottom section FROM EXISTING DATA SOURCES you should see two option: ohmzio-database and ampwerks-database.

![9](../../images/2/2.1/9.png)
