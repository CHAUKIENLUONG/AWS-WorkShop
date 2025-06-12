+++
title = "Workshop Setup"
date = 2025
weight = 2
chapter = false
pre = "<b>1.1. </b>"
+++

### AWS Hosted Workshop Deployment Guide

If you are participating in an AWS hosted event, proceed to the [next section](../Business-Challenge/_index.md).

### Self-Paced Workshop Deployment Guide

This guide will help you deploy the workshop infrastructure in your own AWS account. The workshop template creates several AWS resources including Aurora databases, QuickSight resources, and supporting infrastructure.

It is strongly recommended that this lab be completed in the us-west-2 (Oregon) region.

### Account Requirements Overview

Before deploying the CloudFormation template, your account needs:

1. **Default VPC and Networking**

- A default VPC in your chosen region
- At least 2 subnets in the default VPC

2. **IAM Roles**

- Ability to create new IAM roles
- No existing roles with these names:
  - WorkshopClientRole
  - QSLambdaExecutionRole
  - WSParticipantRole

3. **QuickSight**

- Either an existing Enterprise Edition subscription or ability to create one
- If existing, must be Enterprise Edition or Enterprise Edition with Q

4. **Service Quotas**

- Available quota for 2 new Aurora clusters
- Available quota for Lambda functions
- Permissions to create S3 buckets and DynamoDB tables

5. **IAM Identity Center (formerly AWS SSO)**

- If you use IAM Identity Center, the template must be deployed in the same region where it's enabled

### Deployment Process

**Step 1: Validate Your Account**

1. Open [AWS CloudShell](https://console.aws.amazon.com/cloudshell/home#)
2. Copy the following validation script into the terminal:

`RED='\033[0;31m'; GREEN='\033[0;32m'; YELLOW='\033[1;33m'; NC='\033[0m'; BOLD='\033[1m'; declare -a FINDINGS=(); echo -e "${BOLD}Workshop Infrastructure Validation Check${NC}\n"; ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text); REGION=$(aws configure get region); if [ -z "$REGION" ]; then REGION=$(echo $AWS_DEFAULT_REGION); fi; echo -e "${BOLD}Account ID:${NC} $ACCOUNT_ID"; echo -e "${BOLD}Region:${NC} $REGION\n"; echo -e "${BOLD}Checking QuickSight Subscription...${NC}"; QS_SUBSCRIPTION=$(aws quicksight describe-account-subscription --aws-account-id $ACCOUNT_ID 2>/dev/null); if [ ! -z "$QS_SUBSCRIPTION" ]; then echo -e "${GREEN}✓ QuickSight subscription exists${NC}"; FINDINGS+=("${GREEN}✓ QuickSight subscription exists${NC}"); FINDINGS+=(" --- Set ExistingQuickSightSubscription=True"); FINDINGS+=(" --- Set DeleteQuickSightOnTermination=false"); EDITION=$(echo "$QS_SUBSCRIPTION" | jq -r '.AccountInfo.Edition'); AUTH_METHOD=$(echo "$QS_SUBSCRIPTION" | jq -r '.AccountInfo.AuthenticationType'); echo " Edition: $EDITION"; echo "  Authentication Method: $AUTH_METHOD"; else echo -e "${YELLOW}→ No QuickSight subscription found${NC}"; FINDINGS+=("${YELLOW}→ No QuickSight subscription found${NC}"); FINDINGS+=("  --- Set ExistingQuickSightSubscription=False"); FINDINGS+=("  --- Set DeleteQuickSightOnTermination=true"); fi; echo ""; echo -e "${BOLD}Checking Default VPC...${NC}"; DEFAULT_VPC=$(aws ec2 describe-vpcs --filters Name=is-default,Values=true --query 'Vpcs[0].VpcId' --output text); if [ "$DEFAULT_VPC" != "None" ]; then echo -e "${GREEN}✓ Default VPC exists: $DEFAULT_VPC${NC}"; FINDINGS+=("${GREEN}✓ Default VPC exists${NC}"); FINDINGS+=(" --- No action needed"); SUBNET_COUNT=$(aws ec2 describe-subnets --filters Name=vpc-id,Values=$DEFAULT_VPC --query 'length(Subnets)' --output text); if [ $SUBNET_COUNT -ge 2 ]; then echo -e "${GREEN}✓ Sufficient subnets found ($SUBNET_COUNT subnets)${NC}"; FINDINGS+=("${GREEN}✓ Sufficient subnets available${NC}"); FINDINGS+=("  --- No action needed"); else echo -e "${RED}✗ Insufficient subnets ($SUBNET_COUNT subnets, minimum 2 required)${NC}"; FINDINGS+=("${RED}✗ Insufficient subnets${NC}"); FINDINGS+=(" --- Create at least 2 subnets in the default VPC"); fi; else echo -e "${RED}✗ No default VPC found${NC}"; FINDINGS+=("${RED}✗ No default VPC found${NC}"); FINDINGS+=(" --- Create a default VPC in this region"); fi; echo ""; echo -e "${BOLD}Checking for existing IAM roles...${NC}"; CONFLICT_FOUND=false; CONFLICTING_ROLES=""; for ROLE in "WorkshopClientRole" "QSLambdaExecutionRole" "WSParticipantRole"; do if aws iam get-role --role-name $ROLE --query 'Role.RoleName' --output text 2>/dev/null; then echo -e "${RED}✗ Role exists: $ROLE${NC}"; CONFLICT_FOUND=true; CONFLICTING_ROLES="$CONFLICTING_ROLES$ROLE, "; fi; done; if [ "$CONFLICT_FOUND" = true ]; then FINDINGS+=("${RED}✗ Existing IAM roles found${NC}"); FINDINGS+=(" --- Delete these roles before deployment: ${CONFLICTING_ROLES%??}"); else echo -e "${GREEN}✓ No conflicting IAM roles found${NC}"; FINDINGS+=("${GREEN}✓ No conflicting IAM roles${NC}"); FINDINGS+=("  --- No action needed"); fi; echo ""; echo -e "${BOLD}Checking Aurora Clusters...${NC}"; CLUSTER_COUNT=$(aws rds describe-db-clusters --query 'length(DBClusters)' --output text); if [ $CLUSTER_COUNT -ge 40 ]; then echo -e "${RED}✗ Aurora cluster quota might be exceeded${NC}"; FINDINGS+=("${RED}✗ Aurora cluster quota exceeded${NC}"); FINDINGS+=(" --- Request quota increase or delete unused clusters"); else echo -e "${GREEN}✓ Aurora cluster quota available${NC}"; FINDINGS+=("${GREEN}✓ Aurora cluster quota available${NC}"); FINDINGS+=(" --- No action needed"); fi; echo ""; echo -e "${BOLD}Checking IAM Identity Center (AWS SSO)...${NC}"; if aws sso-admin list-instances 2>/dev/null | grep -q "IdentityStoreId"; then echo -e "${YELLOW}→ IAM Identity Center enabled${NC}"; FINDINGS+=("${YELLOW}→ IAM Identity Center enabled${NC}"); FINDINGS+=(" --- Deploy workshop in the region where IAM Identity Center exists"); else echo -e "${GREEN}✓ No IAM Identity Center found${NC}"; FINDINGS+=("${GREEN}✓ No IAM Identity Center requirements${NC}"); FINDINGS+=(" --- No action needed"); fi; echo ""; echo -e "\n${BOLD}Final Summary and Required Actions:${NC}"; echo "========================================"; for finding in "${FINDINGS[@]}"; do echo -e "$finding"; done; echo -e "\n${BOLD}Template Parameter Settings:${NC}"; echo "========================================"; echo "IsSelfPacedWorkshop=true"; if [ ! -z "$QS_SUBSCRIPTION" ]; then echo "ExistingQuickSightSubscription=True"; echo "DeleteQuickSightOnTermination=false"; else echo "ExistingQuickSightSubscription=False"; echo "DeleteQuickSightOnTermination=true"; fi`

1. Press Enter

The script will perform all necessary checks and provide two important sections:

**Final Summary and Required Actions**

- Green checkmarks (✓) indicate passing checks
- Red X marks (✗) indicate issues that must be resolved
- Yellow arrows (→) indicate items that need attention but may not block deployment
- Each finding includes specific actions needed, if any

**Template Parameter Settings**

- Shows the exact values you should use for critical template parameters
- These values are based on your account's current state

### Step 2: Address Any Issues

If the validation script identified any issues:

1. **Red X Marks (✗)**

- Must be resolved before deploying
- Follow the provided action items for each
- Run the validation script again after making changes

2. **Yellow Arrows (→)**

- Review the recommendations
- Ensure you understand the implications
- Take action if needed for your use case

#### Step 3: Deploy the Template

1. Download the template to baseline the account with required infrastructure: [Account Baseline Cloudformation Template](https://raw.githubusercontent.com/CHAUKIENLUONG/AWS-WorkShop/refs/heads/main/static/account-baseline.yaml)
2. Open the [Cloudformation Console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks?filteringText=&filteringStatus=active&viewNested=true) , and create a new stack.
3. Copy the parameter values from the "Template Parameter Settings" section in the CloudShell output from Step 1 of this guide, update the parameters in the CloudFormation console where the template will be deployed.
4. Deploy the CloudFormation template
5. Enter the parameters exactly as shown by the validation script
6. Review and create the stack

#### Step 4: Switch Roles

For the remainder of the workshop, you will need to use an IAM user role created by the baseline template in the previous step. Using this role will ensure you have the necessary permissions to complete the workshop. If your IAM user is unable to asume IAM user roles, please contact your AWS administrator.

1. Click on your user name and account ID in the upper right. In the menu, select **Switch Role**.
![1](../../images/1/1.1/1.png)
2. Fill in the Switch Role form:

- Add in the Account ID you are using for the workshop.
- Paste this role name into the IAM role name: aidlWSParticipantRole
- Select a color to associate with this role.
- Click **Switch Role**.
![2](../../images/1/1.1/2.png)

3. Verify you have correctly assumed the role:

- **NOTE**: You may see an error after successfully assuming the role. This is to be expected.
- Check in the upper right to verify you see WSParticipantRole @ [YourAccountID]
- Navigate to the [console homepage](https://us-west-2.console.aws.amazon.com/console?region=us-west-2)

![3](../../images/1/1.1/3.png)

### Important Considerations

- **Region Selection**: The template creates regional resources. Choose your region carefully, especially if you use IAM Identity Center.

- **Existing QuickSight**: If you have an existing QuickSight subscription:

  - The template will use your existing subscription
  - Set parameters according to the validation script output
  - Resources will be added to your existing QuickSight environment

- **No Existing QuickSight**: If you don't have QuickSight:

  - The template will create a new subscription
  - Enterprise Edition with Q will be configured
  - IAM authentication will be set up

### Cleanup

- The template creates an S3 bucket that is retained after stack deletion
- QuickSight cleanup behavior is controlled by the DeleteQuickSightOnTermination parameter
- Use the parameter value recommended by the validation script
- Aurora snapshots may be retained depending on your settings

### Getting Help

If you encounter issues:

1. Run the validation script again to verify your account state
2. Review any error messages in the CloudFormation console
3. Check the workshop documentation for additional troubleshooting
4. If you are using a company-managed AWS account, please reach out to your AWS administrator.
