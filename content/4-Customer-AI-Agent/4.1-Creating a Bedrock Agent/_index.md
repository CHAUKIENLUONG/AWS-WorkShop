+++
title = "Creating a Bedrock Agent"
date = 2025
weight = 1
chapter = false
pre = "<b>4.1. </b>"
+++

### Introduction

In this lab, you will setup the agent's purpose and select the appropriate foundation model. The knowledge base will be integrated to augment the agent's generative abilities, enabling it to draw upon and synthesize information from product information and customer support tickets.

### Steps:

### Create the agent

1. Open the **Amazon Bedrock** [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/) .

2. Select **Agents** from the left navigation pane. It is under the Builder Tools section, just below Knowledge bases.

3. In the Agents section, choose **Create Agent**.

4. On the Create Agent screen, enter the name and description of your agent.

5. Name:

`customer-support-agent`

2. Description:

`AI agent to retrieve customer information and ticket history to further help support representatives to resolve customer issues.`

![1](../../images/4/4.1/1.png)

3. Click **Create**.

### Configure the agent

1.  After creating the agent, the Agent builder opens for additional configuration. In the Agent details section, complete the following:

    1. Verify your Agent name and Agent description that you entered on the previous screen.

    2. For the Agent resource role, choose **Create and use a new service role** so that Amazon Bedrock will create the service role on your behalf.

    3. On the Select model section, choose **Anthropic** and then choose **Claude 3.5 Sonnet** in the dropdown menu. Click **Apply**.

    ![2](../../images/4/4.1/2.png)

    4.  In **Instructions for the Agent**, enter details to instruct the agent on what it should do and how it should interact with users. These instructions will be used in the orchestration prompt template. Here are the instructions to use for the agent:

            You are a personal assistant for a customer support representative.
            You will help the support representative retrieve customer details
            including order and support ticket history, and help the representative
            resolve customer issues. When the representative asks for help solving
            a customer's problem, please do your best to find a resolution.
            When you don't have enough information, try to resolve it anyway.
            Don't suggest opening a ticket.
            Never say, "Sorry, I don't have enough information to answer that."
            Instead, do your best to come up with a solution.

    5.  Expand **Additional Settings**.

    6.  Under **User input**, select the radio button for **Enabled**. This will allow the agent to prompt the user for additional information. Don't change any other additional settings.

    ![3](../../images/4/4.1/3.png)

2.  Click the **Save** button at the top before moving to the next step. You will receive a message when the agent is successfully updated.

![4](../../images/4/4.1/4.png)

{{%notice note%}}
Notice the messages to prepare the agent before testing. You will prepare the agent at a later step.
{{%/notice%}}

![5](../../images/4/4.1/5.png)

3. Skip **Action groups** for now and scroll down to **Knowledge bases**.

4. In the **Knowledge bases** section, select **Add** to associate a knowledge base with your agent.

![6](../../images/4/4.1/6.png)

1. For **Select knowledge base**, choose your knowledge base from the dropdown menu. You should see the merger knowledge base you created in an earlier lab.

2. For **Knowledge base instructions for the agent**, enter instructions to describe how the agent should use the knowledge base:

`Use this knowledge base to find information about products, customers, and how to resolve customer issues. The knowledge base contains product manuals and historical support tickets.`

3. Click **Add**.

4. Click **Save and exit**.

![7](../../images/4/4.1/7.png)

5. In the **Agent overview** screen, note the entry under **Agent ARN**. It should look similar to the screenshot below. This is the ARN used to identify your agent. Copy this value for the next section; you will need it in order to grant this agent permission to invoke a Lambda function.

![8](../../images/4/4.1/8.png)
