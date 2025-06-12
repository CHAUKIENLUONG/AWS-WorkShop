+++
title = "Conclusion"
date = 2025
weight = 5
chapter = false
pre = "<b>4.5. </b>"
+++

### Congratulations!

You have just completed setting up an **Agent for Amazon Bedrock**!

### Summary

In this lab, you:

1. Created an agent for Amazon Bedrock.
2. Provided instructions and configured the agent to use your knowledge base.
3. Added an action group to the agent.
4. Configured a lambda function to invoke from your agent.
5. Tested the agent and analyzed tracing information.

### Next Steps

To explore additional customer data to use as agent inputs, you can browse the **Amazon DynamoDB** table directly. Use this link to browse the [all-customers table](https://us-west-2.console.aws.amazon.com/dynamodbv2/home?region=us-west-2#item-explorer?maximize=true&operation=SCAN&table=all-customers) .

![1](../../images/4/4.5/1.png)

In the lab, you configured an action group to call a Lamdba function. The sample lamba function retrieved additional customer information from **Amazon DynamoDB** and returned it to the agent for additional customer-specific context.

Amazon Bedrock Agents empower you to construct autonomous agents that can perform tasks on your behalf. Agents automatically call the necessary APIs to transact with your systems and processes to fulfill the request, determining along the way if they can proceed or if they need to gather more information.

How can you use Agents to automate tasks within your organization?

### Additional Learning

[What is Retrieval-Augmented Generation? ](https://aws.amazon.com/what-is/retrieval-augmented-generation/)

[Agents for Amazon Bedrock ](https://aws.amazon.com/bedrock/agents/)

[How Agents for Amazon Bedrock works ](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-how.html)