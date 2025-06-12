+++
title = "Testing the Bedrock Agent"
date = 2025
weight = 4
chapter = false
pre = "<b>4.4. </b>"
+++

## Introduction

After you create an agent, you will have a working draft that you can use to iteratively build your agent. Each time you make changes to your agent, the working draft is updated.

When the agent build is complete, you can create a version and an alias. You can then deploy your agent to your applications by calling the alias.

### Testing your working draft

In the Amazon Bedrock console, you open up a test window and provide inputs to generate agent responses.

To help troubleshoot your agent's behavior, **Agents for Amazon Bedrock** provides the ability to view the trace during a session with your agent. The trace shows the agent's step-by-step reasoning process.

### Steps

1. During the previous activity, you added the action group for your agent and you should still be on the agent details page. If not, return to your **Amazon Bedrock Agents** [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/agents)  and select your agent from the list.

2. The Test window should be in a pane on the right. If the Test window is closed, you can reopen it by selecting Test at the top of the agent details page.

3. Before testing the agent, you must prepare it. In the Test window, select **Prepare**.

![1](/images/4/4.4/1.png)

{{%notice note%}}
Every time you update the working draft, you must prepare the agent to package the agent with your latest changes. As a best practice, we recommend that you always check your agent's Last prepared time in the Agent overview section of the Working draft page to verify that you're testing your agent with the latest configurations.
{{%/notice%}}

4. To test the agent, enter a message and choose Run. Let's start with a simple greeting:

`Hi`

5. While you wait for the response to generate or after it is generated, select **Show trace**. 

    ![2](/images/4/4.4/2.png)

    Trace shows details for each step of the agent's orchestration process, including the prompt, inference configurations, and agent's reasoning process for each step and usage of its action groups and knowledge bases.

    1. In the **Orchestration and knowledge base** tab, Expand **Trace Step 1** and scroll down. Notice the additional context provided and how the prompt is engineered to create the best response from the model.

    ![3](/images/4/4.4/3.png)

    When provided with a the simple greeting, the agent responds with a simple greeting back to the user.

6. Ask the agent to find information about a customer using the customer ID.

    `What can you tell me about customer 274877906944?`

    1. As the agent is working, click Show trace again to view the new tracing data.

    2. In the Orchestration and knowledge base, Trace Step 2, note how the agent decided to invoke the function.

    ![4](/images/4/4.4/4.png)

    3. In the final response, you should see the details for this customer, including products purchased and support tickets from both Ampwerks and Ohmzio.

    ![5](/images/4/4.4/5.png)

  {{%notice note%}}
  Remember, your output may look different based on variances in the large language models.
  {{%/notice%}}

7. Ask for more information to help the customer with an issue.

        The customer is having more issues with the Smart Pet Feeder. 
        The smart feeder is dispensing inconsistent amounts of food.

    1. Click **Show trace** again to view the new tracing data.

    2. Notice how the agent uses the customer information as well as related support tickets from the knowledge base to create a response. 
    
    ![6](/images/4/4.4/6.png)

    Also notice the [1] in the response. Click the footnote to show the knowledge base document used to find the answer. In this instance, the agent was able to find relevant information from past Ohmzio support tickets.

8. Continue the dialog.

`The customer checked the chute and there are no jams. What else could it be?`

The agent responds with additional troubleshooting tips, including a suggestion for recalibration. You can respond by asking for more instructions.

`How do I recalibrate the smart feeder?`

![7](/images/4/4.4/7.png)

`The recalibration worked. The feeder is now dispensing the correct amount of food.`

![8](/images/4/4.4/8.png)

9. Experiment by asking a few more questions. To start a new conversation, use additional customer IDs that can be found in the DynamoDB table. Here are a few to try:

        292057776128
        412316860425
        120259084303