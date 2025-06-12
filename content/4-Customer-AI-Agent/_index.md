+++
title = "Customer AI Agent"
date = 2025
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

### Background

The new Ohmzio-Ampwerks IT department has been working to merge the customer databases into a single, consolidated view of customers. They have extracted customer information from both databases and they have leveraged the power of [AWS Entity Resolution](https://aws.amazon.com/entity-resolution/) to match customers and assign a unique customer identifier. The resulting consolidated customer information has been stored in [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) for fast retrieval from our application.

### Objective

**Agents for Amazon Bedrock** can assist with a wide variety of tasks. For example, you can create an agent that helps customers process insurance claims or an agent that helps customers make travel reservations. Today, you will configure an agent to help the support team provide a better customer experience.

This lab walks you through the process of using Agents for Amazon Bedrock to add more capabilities to your conversational AI application. Using agents, you will adjust the behavior of your application by providing specific agent instructions. You will also configure your agent to retrieve customer information to further assist with support cases.

**Lab Steps**

1.Create an agent for Amazon Bedrock.
2. Add action groups to the agent.
3. Test the agent and view the trace information.

**An agent consists of the following components:**

1. **Foundation model**. You choose a foundation model (FM) that the agent invokes to interpret user input and subsequent prompts in its orchestration process. The agent also invokes the FM to generate responses and follow-up steps in its process.

2. **Instructions**. You write instructions that describe what the agent is designed to do. With advanced prompts, you can further customize instructions for the agent at every step.

3. **Action groups**. You define the actions that the agent should perform through providing the following resources:

    * An OpenAPI schema to define the API operations that the agent can invoke to perform its tasks.
    * A Lambda function that the agent can execute.

4. **Knowledge bases**. Associate knowledge bases with an agent. The agent queries the knowledge base for extra context to augment response generation and input into steps of the orchestration process.

5. **Prompt templates**. Prompt templates are the basis for creating prompts to be provided to the FM. Agents for Amazon Bedrock exposes the default four base prompt templates that can be edited to customize your agent's behavior.

![1](/images/4/1.png)

This customizable and extensible agent architecture empowers users to create intelligent assistants tailored to their unique needs and requirements.
