+++
title = "Create a Knowledge Base"
date = 2025
weight = 1
chapter = false
pre = "<b>3.1. </b>"
+++

### Introduction

In this step, we will be creating an Amazon Bedrock: Knowledge Base. The knowledge base will reference an S3 data source that consists of support and product data for both Ohmzio and Ampwerks.

{{%notice note%}}
Please note, AWS is continually making improvements to and expanding Bedrock capabilities. You may notice that the provided screen shots may differ slightly from your experience in the console.
{{%/notice%}}

### Steps:

### Request model access

1. Navigate to the Amazon Bedrock [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/) . Click **Get Started**

   1. If presented with Welcome to Amazon Bedrock! pop-up, proceed by clicking **Manage model access**. If not, proceed to next step.

2. Request model access:

   1. On the left of the screen, click the menu icon to open the services menu.

   2. Click **Model access**

   ![1](/images/3/3.1/1.png)

   3.  In the Model access menu, click Enable specific models --or-- Modify model access.

   {{%notice info%}}
   Do not select Enable all models.
   {{%/notice %}}

   4.  Select the following Base models:

   - Titan Text Embeddings V2
   - Claude 3.5 Sonnet

   {{%notice info%}}
   Please note some base models listed may already have **Access granted**. This will not affect your ability to complete the lab. If a model listed in this step is already granted, proceed requesting access to all other required models.
   {{%/notice %}}

   ![2](/images/3/3.1/2.png)

   Click **Next**.

   5.  In the Review and submit page click **Submit**.

{{%notice%}}
Amazon Bedrock provides a turnkey experience for builders. For example, users are able to leverage several types of foundational models across all of the Bedrock services. This, in turn, provides users the option to select a foundational model that best suits their needs. However, foundational model providers (i.e. Anthropic, Cohere, Stability AI, etc.) require EULA acceptance and reasonable guardrails for model usage prior to implementation. The Model Access console manages these agreements and enables administrators to enforce the principle of least privilage. To learn more about foundational models refer back to [Amazon Bedrock: Knowledge Base](../_index.md) key concepts.
{{%/notice%}}

{{%notice note%}}
After requesting model access, Amazon Bedrock is doing the "undifferentiated heavy lifting" of managing access to these open-source foundational models. Granting access to non-Amazon foundational models may take a few minutes. To verify access has been granted, click the refresh button next to Manage model access.
{{%/notice%}}

### Create Knowledge base

1. Click **Knowledge bases** in the left menu under the Builder tools section.

2. In the Knowledge bases landing page, click **Create knowledge base with vector store**.

![3](/images/3/3.1/3.png)

3. Step 1, provide knowledge base details:

   1. Name the knowledge base:

      `merger-knowledge-base`

   2. Describe the knowledge base:

      `Knowledge base for product and support data for both Ohmzio and Ampwerks.`

   3. Leave the IAM permissions, Query Engine, and other configurations as the default.

   ![4](/images/3/3.1/4.png)

   4.  Click **Next**.

   ![5](/images/3/3.1/5.png)

   ![6](/images/3/3.1/6.png)

4. Step 2, configure data source:

   1. Name the knowledge base data source with the name provided (otherwise the default name will be used), then click **Browse S3** to select S3 URI of source data.

   `merger-knowledge-base-data-source`

   ![7](/images/3/3.1/7.png)

   2.  Click customerdata-{uniqueId} bucket name. Click the radio button next to data/ to select it as the location for the source data. Click Choose.

   {{%notice note%}}
   If you can't find your bucket, make sure you are in the correct AWS region.
   {{%/notice%}}

   ![8](/images/3/3.1/8.png)

   ![9](/images/3/3.1/9.png)

   3.  Verify the S3 URI:

   `s3://customerdata-{uniqueId}/data/`

   4.  Don't change any of the advanced settings.

   5.  Click **Next**.

5.  Step 3, select embeddings model and configure vector store:

   ![10](/images/3/3.1/10.png)

   1.  Under Embeddings model, click Select model and then select **Titan TExt Embeddings V2** model and **On-demand Inference mode**.

   {{%notice%}}
   This is the model that will be used to create the vector embeddings in the vector store.
   {{%/notice%}}

   2.  Under Vector store, Select Quick create a new vector store - Recommended method and Amazon OpenSearch Serverless as the vector store type. This is the default and should already be selected.

   {{%notice%}}
   An Amazon OpenSearch Serverless vector store will be created automatically for you.
   {{%/notice%}}

   Leave the optional configurations unchecked.

   3. Click **Next**.

6. Step 4, Review and create:

   1. Review knowledge base configuration.

   2. Verify the S3 URI is correct:

   `s3://customerdata-{uniqueId}/data/`

   3. Click **Create knowledge base**.

   ![11](/images/3/3.1/11.png)

   {{%notice success%}}
   Wait for the knowledge base to be created. AWS will prepare the vector database in Amazon OpenSearch Serverless. This may take up to 10 minutes to complete.
   {{%/notice%}}

### Sync the Knowledge base

1. Once the knowledge base is created, wait until the knowledge base is successfully created:

![12](/images/3/3.1/12.png)

2. Click **Go to data source** or scroll down to the Data source section. To sync, click the radio button next to the Data source that we created (name should be similar to merger-knowledge-base-data-source). Click **Sync**. This will take a few minutes.

![13](/images/3/3.1/13.png)

{{%notice%}}
Data from your S3 bucket is being read and broken "chunks." By default, Amazon Bedrock automatically splits your source data such that each chunk contains 300 tokens. The selected model, Amazon Titan Embeddings V2, is used to convert your data into vector embeddings for the knowledge base.
{{%/notice%}}

3. When the sync is complete, you should receive another message.

![14](/images/3/3.1/14.png)
