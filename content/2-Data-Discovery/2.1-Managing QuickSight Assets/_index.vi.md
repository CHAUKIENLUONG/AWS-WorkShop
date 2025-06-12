+++
title = "Create IAM Role"
date = 2024
weight = 1
chapter = false
pre = "<b>2.1. </b>"
+++

## Create IAM Role

In this step, we'll navigate to the IAM Console interface and create a role for the Glue service. This role will allow AWS Glue to access data in S3 and create necessary objects in the Glue Catalog.

1. Access the [AWS Management Console](https://aws.amazon.com/console/)

   - Search for **IAM**
   - Select **IAM** to enter the **IAM Dashboard**

   ![IAM](../../../images/1/iam-service-cropped.png)

2. In the IAM Dashboard

   - Select **Role**
   - Select **Create role**

   ![IAM](../../../images/1/create_iam_role_cropped.png?width=90pc)

3. In the **Create role** interface, at the **Select trusted entity** step

   - Select **AWS Service**
   - Under _Service or use case_ select **Glue**
   - Select **Next**

   ![IAM](../../../images/1/create_iam_role_detail.png?width=90pc)

4. In the **Create role** interface, at the **Add Permission** step

   - Search and select **AmazonS3FullAccess**

   ![AmazonS3FullAccess](../../../images/1/add_s3_permission_2step.png?width=90pc)

   - Search and select **AWSGlueServiceRole**
   - Select **Next**

   ![AWSGlueServiceRole](../../../images/1/add_glue_permission.png?width=90pc)

5. In the **Create role** interface, at the **Name, review and create** step

   - Under **Role name**, enter `AWSGlueServiceRoleDefault`
     ![AWSGlueServiceRole](../../../images/1/name_role.png?width=90pc)
   - Review the role information at **Select trusted entity** and **Add Permission**
     ![AWSGlueServiceRole](../../../images/1/review_role.png?width=90pc)
   - Select **Create role**
     ![AWSGlueServiceRole](../../../images/1/create_role_submit.png?width=90pc)

6. Successful role creation interface:
   ![AWSGlueServiceRole](../../../images/1/create_role_success.png?width=90pc)
