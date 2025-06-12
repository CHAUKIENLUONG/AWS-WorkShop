+++
title = "Creating QuickSight Datasets"
date = 2025
weight = 2
chapter = false
pre = "<b>2.2. </b>"
+++

### Introduction

In this section, we will be creating a dataset to analyze customer ticket inquiries to help identify opportunities for product improvements using the ohmzio-database data source. After connecting to a new data source, Amazon QuickSight stores the connection information. It adds the data source to the **FROM EXISTING DATA SOURCES** section of the **Create a Dataset** page. You can use these existing data sources to create new datasets without re-specifying connection information.

### Steps:

### Create the data set

1. Navigate to the new [dataset](https://quicksight.aws.amazon.com/sn/data-sets/new?state=hashArgs%23&isauthcode=true&code=eyJ6aXAiOiJERUYiLCJlbmMiOiJBMjU2R0NNIiwiYWxnIjoiZGlyIn0..O7pGUvtHMj8_63Rz.03xVmsBwAbdbk2NKk61fTWdb_bd0V3_aQQaoiNHXirQ7KTVN0PL8AvBcsn5Y1FD-zCTQRaRUM2vbjbv_vWc-OxIiHgZcNFdGT5CBKvpQKFvi4ZQjMlGG6BZUFzN3C-qdBFv6gLztdZbuSp65hsCd6PLG0YgCLIb3FcsOKIA-E70DNZO1FtctmLc96tJ05mtBfqhz7HAVWepc9DFNlWd3sNgH5jaqGvhW1BbFDJubvwH13qGf03hGlNEWPtz3GeP1sPZxJ9pX087YI8gKD9smC28ZIZ3Aw5MAM3081r-sP8LBCziIAWnGVdwXbO8aJBErlym1GElE1qww0ICVWtBsLy7eDThvVRMtS2m1QOYwi-Tg1o89hLPQMwBBFwlCVksg5hu6mEeSxW5EnUzs3V7red3oYaE20KNajdvCYHT8Y1SMMbL1eaOokJp7TtzilokdxeTzaGRPcksWfUCzBkmpRn5CtyWvUxi5FpgCPp7YEbj1cE5luQ2ESp3i-PravbTb9_9k2ctlPsx65VfDtkQw3GuaRWMU8Najp4nao3K2RFimYulLbtTU5pvoHutsW1m7zc_FZEX-s5dIhmlumSW57RYg6Duqx2ctEfdnKC5QDZWDdDX-24de4pv0RoSm73a8uJWrNj9z4zbjo6ag0ZAt-YoX62jCvIVDChQz8wHwceDwWjmYiP0lbpnz1Uh-5l-IZvVaFZOiCp4k5K7lSrBsz-KYm1ob7e0VXaqSI9TSz1AqROBJZy_K5CpPcuRlyI9rCPT54tSXwAxUDkpyVEv8ChZi1mkYx7YW-siTIrMB_YrKRX4Xw-N9rgS65P-ied6vVNxQLp0yUlH3kmMSTGnXF5M3aCOZrcOm6jv413tStprdhVqlCrMNLEA79QT4RjKocfcttFNVtC1LytQAAOyBw1M7NLGEPSejwNL6H6KI54BSzw19BG_W2l4H7RhqztdAAm5KXH_RcQGp1k6O3Jd_n1uTL7lAyUQ1zL9i9JGAzg6Cv7zldAAQEDxWc263grSB01qO059F0N7ik41eUn6Lu67FKtQB46080sRpwKHnGQeLnV5Oxqt8UgnmHiGYs3pH58lwQ4jSdTVLfh2eaOO37dCNeHkqHP8z4ccbwK7P0R_fytxykl6zII28LDceKa8Pi7ZXnURs6dWE6Vy_elB0o0h0z8Mp0n7XMEWBQOcUTBVSpnJ9zuHJjpaJmMKLF1JAxHOEigOQu4vdgu8lJ0h5RIeCf0AWvkotnFWTgFxZW6Se1Y-zVIXBf_E0_DjeFUUZOjEYjMsqioXkh2v_LXOcyqnFUtRKPr_tMouMMK_I_H8pdxzC3IvI4y5l96M-kjVIxciaCmxuXQdzEJ5h3GtI3echy7JrkZvxixyN1lgZotepHwS2OB7r8GZ3JRQHNppwkFZ_8es7IrOoE351JEqR85Kx8Tx-2XqfVfZSxTT8BV34pwLTUti06giPnzcM3HUMHjorydsoBBVqmIvfsgECkp9wcrEL7Jr0fWtfy7GM2RV4yZU86oEAJfmc4JmmdqS9JHMWHW3BjwRJPWLgL0DBHxWCN9eG2g585yA0aBgeVqCSKR7OXzCLdHV8aRjd2nlQa56fipQd733emlINXesxbGygxdWtRPS8eIIOxFdsJV8MRbiGEKf6__NQYk1M_vhM9jzvuGzJjcRxWsnMEv_AmEpoODdK5iLyJnF7OIvjUPluCUWnnp86be3YBq4.HobmVbKnFnBBqm-q63dPCQ)  (if not already there).

![1](../../images/2/2.2/1.png)

2. In the FROM EXISTING DATA SOURCES section of the Create a Dataset page, choose the ohmzio-database, and then choose **Create dataset**.

![2](../../images/2/2.2/2.png)

![3](../../images/2/2.2/3.png)

3. On the **Choose your table** screen, connect to ohmziodb schema from **Schema: contain sets of tables** option and select support_tickets table from **Tables: contain the data you can visualize.**

![4](../../images/2/2.2/4.png)

4. To prepare the data before creating an analysis, choose **Edit/Preview** data to open data preparation.

![5](../../images/2/2.2/5.png)

5. Join the support_tickets table with the customers and products tables.

   1. Click the **Add data** button located in the top right corner of the screen.

   ![6](../../images/2/2.2/6.png)

   2. Select **Data source** from the drop down menu.

   ![7](../../images/2/2.2/7.png)

   3. Select **ohmzio-database** as the data source.

   ![8](../../images/2/2.2/8.png)

   4. Select **ohmziodb** as the schema containing the tables.

   ![9](../../images/2/2.2/9.png)

   5. Click the checkbox next to the customers and products tables., Click the **Select** button to select both tables.

   ![10](../../images/2/2.2/10.png)

   6. You will now see the additional tables added with two red dots indicating that the joins have not been configured. Click each set of red dots to access the join configuration options.

   ![11](../../images/2/2.2/11.png)

   7. For customers, populate the join clause by selecting **customer_id** as the join column for both the support_tickets and customers tables. Choose the recommended join type of **Left** and make sure you click the Apply button to save your changes.

   ![12](../../images/2/2.2/12.png)

   8. For products, populate the join clause by selecting **product_id** as the join column for both the support_tickets and products tables. Choose the recommended join type of **Left** and make sure you click the Apply button to save your changes.

   ![13](../../images/2/2.2/13.png)

### Update field types

1. You can flag geographic fields in your data, so that Amazon QuickSight can display them on a map. On the left side of the **Fields** pane, look for geographic columns city, state, zip, latitude, and longitude.

2. Click the ellipsis menu button ⋮ next to City field. Click **Change data** type and choose **City** under the Geospatial data type subsection. Repeat for the following:

**State** field will map to **State** Geospatial data type
**Zip** field will map to **Postcode** Geospatial data type
**Latitude** field will map to **Latitude** Geospatial data type
**Longitude** field will map to **Longitude** Geospatial data type

![14](../../images/2/2.2/14.png)

{{%notice%}}
You will notice the field icon will update for each field once it is updated to a geospatial data type.
{{%/notice%}}

3. To make your dataset name more intuitive and descriptive change the dataset name from support_tickets to customer_support_discovery. To update, click into the text field with the current title and update with the following:


   `customer_support_discovery`

![15](../../images/2/2.2/15.png)

4. Click on **Save & Publish** (in top blue ribbon, on right side) to save your changes and publish the dataset.

![16](../../images/2/2.2/16.png)

5. Navigate back to the QuickSight landing page by clicking the **QuickSight** icon in the top black ribbon on the left side.

![17](../../images/2/2.2/17.png)

6. Click on **Datasets** in the left menu to see your published dataset customer_support_discovery.

![18](../../images/2/2.2/18.png)