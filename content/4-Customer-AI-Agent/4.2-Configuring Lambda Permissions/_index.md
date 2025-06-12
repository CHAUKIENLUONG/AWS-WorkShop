+++
title = "Configuring Lambda Permissions"
date = 2025
weight = 2
chapter = false
pre = "<b>4.2. </b>"
+++

### Introduction

In this lab, you will configure permissions to allow the agent to execute an **AWS Lambda** function.

**AWS Lambda** is an incredibly powerful and versatile serverless computing service. With Lambda, you don't have to worry about provisioning or managing servers. Lambda automatically scales your application in response to increased traffic or demand, ensuring that your application can handle the workload without any manual intervention.

By combining **AWS Lambda** and **Agents for Amazon Bedrock**, you can build complex, serverless automation and workflow systems. Bedrock agents can be used to trigger Lambda functions, and the Lambda functions can then orchestrate a series of actions, such as updating databases, sending notifications, or invoking other services.

In this lab, we will be using our agent to invoke a lambda function that retrieves customer information from an **Amazon DynamoDB** table.

**Amazon DynamoDB** is a powerful and scalable database service that scales automatically to handle any amount of data and traffic, without the need to provision or manage servers. It can handle up to millions of requests per second, with consistent, single-digit millisecond latency.

For your agent to use a **Lambda** function, you must attach a resource-based policy to the function to provide permissions for the agent.

### Steps

1. Open **AWS Lambda Functions** [console](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions) .

2. In the list of functions, select the function name **BedrockAction**. The function to retrieve customer data has already been created and deployed prior to the lab. We won't be changing any of the code, only setting permissions.

![1](/images/4/4.2/1.png)

3. The Code tab is opened by default. Select Configuration. Next, in the left menu, select **Permissions**. It should be the third item from the top.

![2](/images/4/4.2/2.png)

4. Scroll down to **Resource-based policy statements**.

![3](/images/4/4.2/3.png)

5. Click **Add permissions**.

6. On the **Add permissions** page, configure the following:

    1. Select **AWS service**.

    2. In the Service dropdown, select **Other**.

    3. In the **Statement ID** text box, enter:


    `my-custom-id-0001`

    4. In the *Principal* text box, enter:

    `bedrock.amazonaws.com`

    5. In the **Source ARN** text box paste the Agent ARN you copied after you created your agent. It should look similar to:

    ![4](/images/4/4.2/4.png)

    6. In the **Action** dropdown, select **lambda:InvokeFunction**.

    7. Click **Save**.

    ![5](/images/4/4.2/5.png)

7. Verify that your Lambda Resource-based policy statement was saved.

![6](/images/4/4.2/6.png)