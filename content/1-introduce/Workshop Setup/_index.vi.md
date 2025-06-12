+++
title = "Thiết lập Workshop"
date = 2025
weight = 2
chapter = false
pre = "<b>1.1. </b>"
+++

### Hướng dẫn Triển khai Workshop được AWS Tổ chức

Nếu bạn đang tham gia sự kiện được AWS tổ chức, hãy tiếp tục đến [phần tiếp theo](../Business-Challenge/_index.md).

### Hướng dẫn Triển khai Workshop Tự học

Hướng dẫn này sẽ giúp bạn triển khai cơ sở hạ tầng workshop trong tài khoản AWS của riêng bạn. Template workshop tạo ra nhiều tài nguyên AWS bao gồm cơ sở dữ liệu Aurora, tài nguyên QuickSight và cơ sở hạ tầng hỗ trợ.

Rất khuyến nghị rằng lab này nên được hoàn thành ở khu vực us-west-2 (Oregon).

### Tổng quan Yêu cầu Tài khoản

Trước khi triển khai template CloudFormation, tài khoản của bạn cần:

1. **VPC và Mạng Mặc định**

- Một VPC mặc định trong khu vực bạn chọn
- Ít nhất 2 subnet trong VPC mặc định

2. **IAM Roles**

- Khả năng tạo IAM roles mới
- Không có roles hiện có với những tên này:
  - WorkshopClientRole
  - QSLambdaExecutionRole
  - WSParticipantRole

3. **QuickSight**

- Hoặc một subscription Enterprise Edition hiện có hoặc khả năng tạo một cái mới
- Nếu đã có, phải là Enterprise Edition hoặc Enterprise Edition with Q

4. **Service Quotas**

- Quota khả dụng cho 2 cluster Aurora mới
- Quota khả dụng cho Lambda functions
- Quyền tạo S3 buckets và DynamoDB tables

5. **IAM Identity Center (trước đây là AWS SSO)**

- Nếu bạn sử dụng IAM Identity Center, template phải được triển khai trong cùng khu vực nơi nó được bật

### Quy trình Triển khai

**Bước 1: Xác thực Tài khoản của Bạn**

1. Mở [AWS CloudShell](https://console.aws.amazon.com/cloudshell/home#)
2. Sao chép script xác thực sau vào terminal:

`RED='\033[0;31m'; GREEN='\033[0;32m'; YELLOW='\033[1;33m'; NC='\033[0m'; BOLD='\033[1m'; declare -a FINDINGS=(); echo -e "${BOLD}Kiểm tra Xác thực Cơ sở hạ tầng Workshop${NC}\n"; ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text); REGION=$(aws configure get region); if [ -z "$REGION" ]; then REGION=$(echo $AWS_DEFAULT_REGION); fi; echo -e "${BOLD}Account ID:${NC} $ACCOUNT_ID"; echo -e "${BOLD}Region:${NC} $REGION\n"; echo -e "${BOLD}Kiểm tra Subscription QuickSight...${NC}"; QS_SUBSCRIPTION=$(aws quicksight describe-account-subscription --aws-account-id $ACCOUNT_ID 2>/dev/null); if [ ! -z "$QS_SUBSCRIPTION" ]; then echo -e "${GREEN}✓ Subscription QuickSight tồn tại${NC}"; FINDINGS+=("${GREEN}✓ Subscription QuickSight tồn tại${NC}"); FINDINGS+=(" --- Đặt ExistingQuickSightSubscription=True"); FINDINGS+=(" --- Đặt DeleteQuickSightOnTermination=false"); EDITION=$(echo "$QS_SUBSCRIPTION" | jq -r '.AccountInfo.Edition'); AUTH_METHOD=$(echo "$QS_SUBSCRIPTION" | jq -r '.AccountInfo.AuthenticationType'); echo " Edition: $EDITION"; echo "  Phương thức Xác thực: $AUTH_METHOD"; else echo -e "${YELLOW}→ Không tìm thấy subscription QuickSight${NC}"; FINDINGS+=("${YELLOW}→ Không tìm thấy subscription QuickSight${NC}"); FINDINGS+=("  --- Đặt ExistingQuickSightSubscription=False"); FINDINGS+=("  --- Đặt DeleteQuickSightOnTermination=true"); fi; echo ""; echo -e "${BOLD}Kiểm tra VPC Mặc định...${NC}"; DEFAULT_VPC=$(aws ec2 describe-vpcs --filters Name=is-default,Values=true --query 'Vpcs[0].VpcId' --output text); if [ "$DEFAULT_VPC" != "None" ]; then echo -e "${GREEN}✓ VPC mặc định tồn tại: $DEFAULT_VPC${NC}"; FINDINGS+=("${GREEN}✓ VPC mặc định tồn tại${NC}"); FINDINGS+=(" --- Không cần hành động"); SUBNET_COUNT=$(aws ec2 describe-subnets --filters Name=vpc-id,Values=$DEFAULT_VPC --query 'length(Subnets)' --output text); if [ $SUBNET_COUNT -ge 2 ]; then echo -e "${GREEN}✓ Tìm thấy đủ subnets ($SUBNET_COUNT subnets)${NC}"; FINDINGS+=("${GREEN}✓ Có đủ subnets${NC}"); FINDINGS+=("  --- Không cần hành động"); else echo -e "${RED}✗ Không đủ subnets ($SUBNET_COUNT subnets, tối thiểu cần 2)${NC}"; FINDINGS+=("${RED}✗ Không đủ subnets${NC}"); FINDINGS+=(" --- Tạo ít nhất 2 subnets trong VPC mặc định"); fi; else echo -e "${RED}✗ Không tìm thấy VPC mặc định${NC}"; FINDINGS+=("${RED}✗ Không tìm thấy VPC mặc định${NC}"); FINDINGS+=(" --- Tạo VPC mặc định trong khu vực này"); fi; echo ""; echo -e "${BOLD}Kiểm tra IAM roles hiện có...${NC}"; CONFLICT_FOUND=false; CONFLICTING_ROLES=""; for ROLE in "WorkshopClientRole" "QSLambdaExecutionRole" "WSParticipantRole"; do if aws iam get-role --role-name $ROLE --query 'Role.RoleName' --output text 2>/dev/null; then echo -e "${RED}✗ Role tồn tại: $ROLE${NC}"; CONFLICT_FOUND=true; CONFLICTING_ROLES="$CONFLICTING_ROLES$ROLE, "; fi; done; if [ "$CONFLICT_FOUND" = true ]; then FINDINGS+=("${RED}✗ Tìm thấy IAM roles hiện có${NC}"); FINDINGS+=(" --- Xóa các roles này trước khi triển khai: ${CONFLICTING_ROLES%??}"); else echo -e "${GREEN}✓ Không tìm thấy IAM roles xung đột${NC}"; FINDINGS+=("${GREEN}✓ Không có IAM roles xung đột${NC}"); FINDINGS+=("  --- Không cần hành động"); fi; echo ""; echo -e "${BOLD}Kiểm tra Aurora Clusters...${NC}"; CLUSTER_COUNT=$(aws rds describe-db-clusters --query 'length(DBClusters)' --output text); if [ $CLUSTER_COUNT -ge 40 ]; then echo -e "${RED}✗ Quota Aurora cluster có thể bị vượt quá${NC}"; FINDINGS+=("${RED}✗ Quota Aurora cluster bị vượt quá${NC}"); FINDINGS+=(" --- Yêu cầu tăng quota hoặc xóa clusters không sử dụng"); else echo -e "${GREEN}✓ Quota Aurora cluster khả dụng${NC}"; FINDINGS+=("${GREEN}✓ Quota Aurora cluster khả dụng${NC}"); FINDINGS+=(" --- Không cần hành động"); fi; echo ""; echo -e "${BOLD}Kiểm tra IAM Identity Center (AWS SSO)...${NC}"; if aws sso-admin list-instances 2>/dev/null | grep -q "IdentityStoreId"; then echo -e "${YELLOW}→ IAM Identity Center được bật${NC}"; FINDINGS+=("${YELLOW}→ IAM Identity Center được bật${NC}"); FINDINGS+=(" --- Triển khai workshop trong khu vực nơi IAM Identity Center tồn tại"); else echo -e "${GREEN}✓ Không tìm thấy IAM Identity Center${NC}"; FINDINGS+=("${GREEN}✓ Không có yêu cầu IAM Identity Center${NC}"); FINDINGS+=(" --- Không cần hành động"); fi; echo ""; echo -e "\n${BOLD}Tóm tắt Cuối cùng và Hành động Cần thiết:${NC}"; echo "========================================"; for finding in "${FINDINGS[@]}"; do echo -e "$finding"; done; echo -e "\n${BOLD}Cài đặt Tham số Template:${NC}"; echo "========================================"; echo "IsSelfPacedWorkshop=true"; if [ ! -z "$QS_SUBSCRIPTION" ]; then echo "ExistingQuickSightSubscription=True"; echo "DeleteQuickSightOnTermination=false"; else echo "ExistingQuickSightSubscription=False"; echo "DeleteQuickSightOnTermination=true"; fi`

1. Nhấn Enter

Script sẽ thực hiện tất cả các kiểm tra cần thiết và cung cấp hai phần quan trọng:

**Tóm tắt Cuối cùng và Hành động Cần thiết**

- Dấu tích xanh (✓) cho biết các kiểm tra đạt
- Dấu X đỏ (✗) cho biết các vấn đề phải được giải quyết
- Mũi tên vàng (→) cho biết các mục cần chú ý nhưng có thể không chặn triển khai
- Mỗi phát hiện bao gồm các hành động cụ thể cần thiết, nếu có

**Cài đặt Tham số Template**

- Hiển thị các giá trị chính xác bạn nên sử dụng cho các tham số template quan trọng
- Các giá trị này dựa trên trạng thái hiện tại của tài khoản

### Bước 2: Giải quyết Các Vấn đề

Nếu script xác thực xác định bất kỳ vấn đề nào:

1. **Dấu X Đỏ (✗)**

- Phải được giải quyết trước khi triển khai
- Làm theo các mục hành động được cung cấp cho mỗi vấn đề
- Chạy lại script xác thực sau khi thực hiện thay đổi

2. **Mũi tên Vàng (→)**

- Xem xét các khuyến nghị
- Đảm bảo bạn hiểu các tác động
- Thực hiện hành động nếu cần cho trường hợp sử dụng của bạn

#### Bước 3: Triển khai Template

1. Tải xuống template để thiết lập cơ bản tài khoản với cơ sở hạ tầng cần thiết: [Account Baseline Cloudformation Template](https://raw.githubusercontent.com/CHAUKIENLUONG/AWS-WorkShop/refs/heads/main/static/account-baseline.yaml)
2. Mở [Cloudformation Console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks?filteringText=&filteringStatus=active&viewNested=true) và tạo stack mới.
3. Sao chép các giá trị tham số từ phần "Cài đặt Tham số Template" trong đầu ra CloudShell từ Bước 1 của hướng dẫn này, cập nhật các tham số trong CloudFormation console nơi template sẽ được triển khai.
4. Triển khai template CloudFormation
5. Nhập các tham số chính xác như được hiển thị bởi script xác thực
6. Xem xét và tạo stack

#### Bước 4: Chuyển đổi Roles

Đối với phần còn lại của workshop, bạn sẽ cần sử dụng IAM user role được tạo bởi template baseline trong bước trước. Sử dụng role này sẽ đảm bảo bạn có các quyền cần thiết để hoàn thành workshop. Nếu IAM user của bạn không thể assume IAM user roles, vui lòng liên hệ với AWS administrator của bạn.

1. Nhấp vào tên người dùng và ID tài khoản ở góc trên bên phải. Trong menu, chọn **Switch Role**.
   ![1](../../../images/1/1.1/1.png)
2. Điền vào form Switch Role:

- Thêm Account ID bạn đang sử dụng cho workshop.
- Dán tên role này vào IAM role name: aidlWSParticipantRole
- Chọn màu để liên kết với role này.
- Nhấp **Switch Role**.
  ![2](../../../images/1/1.1/2.png)

3. Xác minh bạn đã assume role một cách chính xác:

- **LƯU Ý**: Bạn có thể thấy lỗi sau khi assume role thành công. Điều này là bình thường.
- Kiểm tra ở góc trên bên phải để xác minh bạn thấy WSParticipantRole @ [YourAccountID]
- Điều hướng đến [trang chủ console](https://us-west-2.console.aws.amazon.com/console?region=us-west-2)

![3](../../../images/1/1.1/3.png)

### Các Cân nhắc Quan trọng

- **Lựa chọn Khu vực**: Template tạo ra các tài nguyên theo khu vực. Chọn khu vực của bạn một cách cẩn thận, đặc biệt nếu bạn sử dụng IAM Identity Center.

- **QuickSight Hiện có**: Nếu bạn có subscription QuickSight hiện có:

  - Template sẽ sử dụng subscription hiện có của bạn
  - Đặt các tham số theo đầu ra script xác thực
  - Tài nguyên sẽ được thêm vào môi trường QuickSight hiện có của bạn

- **Không có QuickSight Hiện có**: Nếu bạn không có QuickSight:

  - Template sẽ tạo subscription mới
  - Enterprise Edition with Q sẽ được cấu hình
  - Xác thực IAM sẽ được thiết lập

### Dọn dẹp

- Template tạo ra S3 bucket được giữ lại sau khi xóa stack
- Hành vi dọn dẹp QuickSight được kiểm soát bởi tham số DeleteQuickSightOnTermination
- Sử dụng giá trị tham số được khuyến nghị bởi script xác thực
- Aurora snapshots có thể được giữ lại tùy thuộc vào cài đặt của bạn

### Nhận Trợ giúp

Nếu bạn gặp vấn đề:

1. Chạy lại script xác thực để xác minh trạng thái tài khoản
2. Xem xét bất kỳ thông báo lỗi nào trong CloudFormation console
3. Kiểm tra tài liệu workshop để biết thêm thông tin khắc phục sự cố
4. Nếu bạn đang sử dụng tài khoản AWS được quản lý bởi công ty, vui lòng liên hệ với AWS administrator của bạn.
