+++
title = "Adding an Action Group"
date = 2025
weight = 3
chapter = false
pre = "<b>4.3. </b>"
+++

### Introduction

Action groups can be defined to further specialize the agent's functionality, allowing it to perform specific actions or procedures. Actions can also retrieve additional information, providing the agent with additional knowledge and capabilities necessary to generate relevant and coherent responses.

### Steps

1. Return to your **Amazon Bedrock Agents** [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/agents) .

2. Select your agent from the list.

3. Select **Edit in Agent Builder**.

![1](/images/4/4.3/1.png)

4. Scroll down to **Action groups**.

{{%notice note%}}
Bedrock may have created a default action group ("UserInputAction") for you. If so, click on the UserInputAction action group and follow the steps below to edit it. If you do not have any existing action group, click Add to create a new one.
{{%/notice%}}

![2](/images/4/4.3/2.png)


5. Click **Add**.

6. On the Create (or Edit) action group page, complete the following:

**See screenshot below**

  1. Enter action group name:

  `agent-action-group`

  2. Description:

  `Actions taken for the agent.`

  3. For **Action group type**, choose **Define with function details**.

  4. For **Action group invocation**, choose **Select an existing Lambda function**.

  5. For **Select Lambda function**, choose **BedrockAction** and $LATEST version.

  6. Enter the details for **Action group function 1**.

  1. Name:

  `GetCustomerDetails`

  2. Description:

  `Retrieve customer by customer id and return the customer details, order history, and support history.`


  3. Confirmation should be Disabled.

  4. Add parameter

   ![3](/images/4/4.3/3.png)
  {{%notice note%}}
  Click the check after editing each parameter attribute.
  {{%/notice%}}

  ![4](/images/4/4.3/4.png)

  1. Name:

  `cust_id`

  2. Description:

  `The ID of the customer.`

  3. Type

  `String`

  4. Required

  `True`

  ![5](/images/4/4.3/5.png)

  ![6](/images/4/4.3/6.png)

  5. Click **Create**.

7. Verify that the action group was created.

![7](/images/4/4.3/7.png)

8. Scroll back to the top and click **Save and exit**.

9. Verify that the agent was updated. 
![8](/images/4/4.3/8.png)