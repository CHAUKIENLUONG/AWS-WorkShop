+++
title = "Clean Up"
date = 2025
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

### Instructions

If this lab was run in an account not provided by AWS, follow these steps to tear-down the workshop resources.

1. Remove Bedrock Agent and Action Groups created in [4.1 Creating a Bedrock Agent](../4-Customer-AI-Agent/4.1-Creating%20a%20Bedrock%20Agent/_index.md).

2. Remove Bedrock Knowledge Base created in [3.1 Create a Knowlege Base](../3-Product%20and%20Support-Knowledge-Base/3.1-Create%20a%20Knowledge%20Base/_index.md).

3. Remove workshop sample data -- (Optional) Navigate to the [S3 Console](https://us-west-2.console.aws.amazon.com/s3?region=us-west-2) , and delete the bucket created by the workshop template. The name of the bucket will be `customerdata-<stackid>`. If keeping the source data is preferred, this step can be skipped.

{{%notice info%}}
If this step is skipped, the S3 bucket containing all sample data will remain in the account. This will accrue additional ~24 MB of storage to existing S3 storage costs.
{{%/notice%}}

4. Remove baseline infrastructure -- Navigate to [CloudFormation](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks?filteringText=&filteringStatus=active&viewNested=true)  and delete the ds-genai-workshop stack deployed for the workshop.