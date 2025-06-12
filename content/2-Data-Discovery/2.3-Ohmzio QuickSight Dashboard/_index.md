+++
title = "Ohmzio QuickSight Dashboard"
date = 2025
weight = 3
chapter = false
pre = "<b>2.3. </b>"
+++

### Introduction

In this section, we will create an analysis for analyzing the types of inquiries and issues customers are raising, which can help identify areas for improvement in products and services.

### Steps:

### Create new analysis from a dataset

1. Navigate to the QuickSight [Datasets](https://quicksight.aws.amazon.com/sn/console/signup)  page.

2. Click the ellipsis menu button ⋮ next to customer_support_discovery dataset, and then choose **CREATE ANALYSIS**.

![1](../../images/2/2.3/1.png)

3. On the **New sheet** pop-up, leave **Interactive sheet** selected and click the **CREATE** button.

### Analyze monthly support ticket volume

1. Let's start by analyzing the volume of unique support tickets received on a monthly basis.

2. Click the empty visual and change the visual type to line chart.

![2](../../images/2/2.3/2.png)

3. From the **fields list** in **primary left pane**:

   * drag ticket_date to **X axis** field
   * drag ticket_id to **value** field

4. By default, you will see that ticket_date is aggregated by day. Click the ellipsis against ticket_date field from the **X AXIS** section of the visual to access the visual-level field menu to change the aggregation from day to month.

5. Click the ellipsis against ticket_id field from the **VALUE** section of visual to access the visual-level field menu to change the aggregation from count to count distinct to get count of unique tickets.

![3](../../images/2/2.3/3.gif)

{{%notice%}}
The analysis of historical data reveals overall an upward trend in ticket volume over the months, indicating an increasing demand for support services.
{{%/notice%}}

### Analyze support requests by product type

1. Next let's view the distribution of support requests across various product types.

2. Choose Add on the application bar, and then choose Add visual. Select the Donut chart from the menu.

![4](../../images/2/2.3/4.png)

3. From the Fields list in primary left pane add necessary fields in the following order:

   * drag category to Group/Color field
   * drag ticket_id to Value field

![5](../../images/2/2.3/5.gif)

{{% notice %}}
The analysis show Lighting category has most volume of tickets.
{{% /notice %}}
### Analyze product with highest support requests

1. Next let's view which product has most number of support tickets.

2. Choose Add on the application bar, and then choose Add visual. Select **Tree map** from the menu.

![6](../../images/2/2.3/6.png)

3 From the Fields list in primary left pane add necessary fields in the following order:

   * drag name[products] to the **GROUP BY** field well

{{% notice info %}}
You may see name[customers] instead of name[products]. Because both the customers and the products tables have a column titled “name”, Quicksight renames one of them. Make sure you select name[products] or just name if you only see name[customers].
{{% /notice %}}

   * drag ticket_id to **Color** field well

{{% notice note %}}
The bracket notation for products indicates that the attribute originates from the products table. When joining tables that have the same column names, QuickSight resolves this by adding the table name. If you joined support_tickets with the products table before you joined with the customers table, your column names will be different.
{{% /notice %}}

![7](../../images/2/2.3/7.gif)

{{%notice%}}
The analysis shows **Ohmzio Smart Plug** product has most volume of tickets.
{{%/notice%}}

### Add suggested insights

1. Next let's add suggested insights.

2. Click on the Tree map visual to indicate this is the visual we want to base our insights from (once selected, will have a black box around perimeter). Next, click the **Insights** icon (light bulb shaped icon). The Insights panel opens and displays a list of ready-to-use suggested insights. Scroll down to preview the insights we can add to our dashboard based on the data and trends in the Tree map visual.

![8](../../images/2/2.3/8.png)

3. Add a suggested insight (such as, **Top 3 Products by Ticket Count**) to your analysis by choosing the plus sign (+) near the insight title.

![9](../../images/2/2.3/9.png)

4. You can resize the insights to be smaller, and move them on top of your **Tree Map** visual.

![10](../../images/2/2.3/10.gif)

{{%notice%}}
The auto-generated insights reveal that the Smart Plug and Smart Vent products have the most volume of tickets.
{{%/notice%}}
