+++
title = "Cài Đặt Workshop"
date = 2025
weight = 2
chapter = false
pre = "<b>1.1. </b>"
+++

### Hướng Dẫn Triển Khai Workshop do AWS Tổ Chức

Nếu bạn đang tham gia sự kiện do AWS tổ chức, hãy chuyển đến [phần tiếp theo](../Business-Challenge/_index.md).

### Hướng Dẫn Triển Khai Workshop Tự Học

Hướng dẫn này sẽ giúp bạn triển khai cơ sở hạ tầng workshop trong tài khoản AWS của riêng bạn. Mẫu workshop tạo ra một số tài nguyên AWS bao gồm cơ sở dữ liệu Aurora, tài nguyên QuickSight và cơ sở hạ tầng hỗ trợ.

Chúng tôi đặc biệt khuyến nghị thực hiện workshop này tại vùng us-west-2 (Oregon).

### Tổng Quan Yêu Cầu Tài Khoản

Trước khi triển khai mẫu CloudFormation, tài khoản của bạn cần:

1. **VPC Mặc Định và Mạng**

- Một VPC mặc định trong vùng bạn chọn
- Ít nhất 2 subnet trong VPC mặc định

2. **Vai Trò IAM**

- Khả năng tạo vai trò IAM mới
- Không có vai trò hiện tại với các tên sau:
  - WorkshopClientRole
  - QSLambdaExecutionRole
  - WSParticipantRole

3. **QuickSight**

- Hoặc có sẵn đăng ký Enterprise Edition hoặc có khả năng tạo mới
- Nếu đã có, phải là Enterprise Edition hoặc Enterprise Edition with Q

4. **Hạn Mức Dịch Vụ**

- Hạn mức khả dụng cho 2 cụm Aurora mới
- Hạn mức khả dụng cho các hàm Lambda
- Quyền tạo bucket S3 và bảng DynamoDB

5. **IAM Identity Center (trước đây là AWS SSO)**

- Nếu bạn sử dụng IAM Identity Center, mẫu phải được triển khai trong cùng vùng nơi nó được kích hoạt

### Quy trình Triển Khai

**Bước 1: Xác Thực Tài Khoản của Bạn**

1. Mở [AWS CloudShell](https://console.aws.amazon.com/cloudshell/home#)
2. Sao chép đoạn mã xác thực sau vào terminal:

`RED='\033[0;31m'; GREEN='\033[0;32m'; YELLOW='\033[1;33m'; NC='\033[0m'; BOLD='\033[1m'; declare -a FINDINGS=(); echo -e "${BOLD}Kiểm Tra Hạ Tầng Workshop${NC}\n"; ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text); REGION=$(aws configure get region); if [ -z "$REGION" ]; then REGION=$(echo $AWS_DEFAULT_REGION); fi; echo -e "${BOLD}ID Tài Khoản:${NC} $ACCOUNT_ID"; echo -e "${BOLD}Vùng:${NC} $REGION\n"; echo -e "${BOLD}Kiểm Tra Đăng Ký QuickSight...${NC}"; QS_SUBSCRIPTION=$(aws quicksight describe-account-subscription --aws-account-id $ACCOUNT_ID 2>/dev/null); if [ ! -z "$QS_SUBSCRIPTION" ]; then echo -e "${GREEN}✓ Đăng ký QuickSight đã tồn tại${NC}"; FINDINGS+=("${GREEN}✓ Đăng ký QuickSight đã tồn tại${NC}"); FINDINGS+=(" --- Đặt ExistingQuickSightSubscription=True"); FINDINGS+=(" --- Đặt DeleteQuickSightOnTermination=false"); EDITION=$(echo "$QS_SUBSCRIPTION" | jq -r '.AccountInfo.Edition'); AUTH_METHOD=$(echo "$QS_SUBSCRIPTION" | jq -r '.AccountInfo.AuthenticationType'); echo " Phiên bản: $EDITION"; echo "  Phương thức xác thực: $AUTH_METHOD"; else echo -e "${YELLOW}→ Không tìm thấy đăng ký QuickSight${NC}"; FINDINGS+=("${YELLOW}→ Không tìm thấy đăng ký QuickSight${NC}"); FINDINGS+=("  --- Đặt ExistingQuickSightSubscription=False"); FINDINGS+=("  --- Đặt DeleteQuickSightOnTermination=true"); fi; echo ""; echo -e "${BOLD}Kiểm Tra VPC Mặc Định...${NC}"; DEFAULT_VPC=$(aws ec2 describe-vpcs --filters Name=is-default,Values=true --query 'Vpcs[0].VpcId' --output text); if [ "$DEFAULT_VPC" != "None" ]; then echo -e "${GREEN}✓ VPC mặc định tồn tại: $DEFAULT_VPC${NC}"; FINDINGS+=("${GREEN}✓ VPC mặc định tồn tại${NC}"); FINDINGS+=(" --- Không cần hành động gì"); SUBNET_COUNT=$(aws ec2 describe-subnets --filters Name=vpc-id,Values=$DEFAULT_VPC --query 'length(Subnets)' --output text); if [ $SUBNET_COUNT -ge 2 ]; then echo -e "${GREEN}✓ Số lượng subnet đủ (Có $SUBNET_COUNT subnet)${NC}"; FINDINGS+=("${GREEN}✓ Số lượng subnet đủ${NC}"); FINDINGS+=("  --- Không cần hành động gì"); else echo -e "${RED}✗ Số lượng subnet không đủ ($SUBNET_COUNT subnet, yêu cầu tối thiểu 2)${NC}"; FINDINGS+=("${RED}✗ Số lượng subnet không đủ${NC}"); FINDINGS+=(" --- Tạo ít nhất 2 subnet trong VPC mặc định"); fi; else echo -e "${RED}✗ Không tìm thấy VPC mặc định${NC}"; FINDINGS+=("${RED}✗ Không tìm thấy VPC mặc định${NC}"); FINDINGS+=(" --- Tạo một VPC mặc định trong vùng này"); fi; echo ""; echo -e "${BOLD}Kiểm Tra Vai Trò IAM...${NC}"; CONFLICT_FOUND=false; CONFLICTING_ROLES=""; for ROLE in "WorkshopClientRole" "QSLambdaExecutionRole" "WSParticipantRole"; do if aws iam get-role --role-name $ROLE --query 'Role.RoleName' --output text 2>/dev/null; then echo -e "${RED}✗ Vai trò đã tồn tại: $ROLE${NC}"; CONFLICT_FOUND=true; CONFLICTING_ROLES="$CONFLICTING_ROLES$ROLE, "; fi; done; if [ "$CONFLICT_FOUND" = true ]; then FINDINGS+=("${RED}✗ Tìm thấy vai trò IAM tồn tại${NC}"); FINDINGS+=(" --- Xóa các vai trò này trước khi triển khai: ${CONFLICTING_ROLES%??}"); else echo -e "${GREEN}✓ Không có vai trò IAM xung đột nào được tìm thấy${NC}"; FINDINGS+=("${GREEN}✓ Không có vai trò IAM xung đột${NC}"); FINDINGS+=("  --- Không cần hành động gì"); fi; echo ""; echo -e "${BOLD}Kiểm Tra Cụm Aurora...${NC}"; CLUSTER_COUNT=$(aws rds describe-db-clusters --query 'length(DBClusters)' --output text); if [ $CLUSTER_COUNT -ge 40 ]; then echo -e "${RED}✗ Hạn mức cụm Aurora có thể đã bị vượt quá${NC}"; FINDINGS+=("${RED}✗ Hạn mức cụm Aurora bị vượt quá${NC}"); FINDINGS+=(" --- Yêu cầu tăng hạn mức hoặc xóa các cụm không sử dụng"); else echo -e "${GREEN}✓ Hạn mức cụm Aurora còn khả dụng${NC}"; FINDINGS+=("${GREEN}✓ Hạn mức cụm Aurora còn khả dụng${NC}"); FINDINGS+=(" --- Không cần hành động gì"); fi; echo ""; echo -e "${BOLD}Kiểm Tra IAM Identity Center (AWS SSO)...${NC}"; if aws sso-admin list-instances 2>/dev/null | grep -q "IdentityStoreId"; then echo -e "${YELLOW}→ IAM Identity Center đã được kích hoạt${NC}"; FINDINGS+=("${YELLOW}→ IAM Identity Center đã được kích hoạt${NC}"); FINDINGS+=(" --- Triển khai workshop trong vùng nơi IAM Identity Center tồn tại"); else echo -e "${GREEN}✓ Không có yêu cầu IAM Identity Center nào được tìm thấy${NC}"; FINDINGS+=("${GREEN}✓ Không có yêu cầu IAM Identity Center${NC}"); FINDINGS+=(" --- Không cần hành động gì"); fi; echo ""; echo -e "\n${BOLD}Tóm Tắt Cuối Cùng và Các Hành Động Cần Thiết:${NC}"; echo "========================================"; for finding in "${FINDINGS[@]}"; do echo -e "$finding"; done; echo -e "\n${BOLD}Cài Đặt Tham Số Mẫu:${NC}"; echo "========================================"; echo "IsSelfPacedWorkshop=true"; if [ ! -z "$QS_SUBSCRIPTION" ]; then echo "ExistingQuickSightSubscription=True"; echo "DeleteQuickSightOnTermination=false"; else echo "ExistingQuickSightSubscription=False"; echo "DeleteQuickSightOnTermination=true"; fi`

1. Nhấn Enter

Đoạn mã sẽ thực hiện tất cả các kiểm tra cần thiết và cung cấp hai phần quan trọng:

**Tóm Tắt Cuối Cùng và Các Hành Động Cần Thiết**

- Dấu kiểm màu xanh (✓) chỉ ra các kiểm tra đã vượt qua
- Dấu X màu đỏ (✗) chỉ ra các vấn đề cần được giải quyết
- Mũi tên màu vàng (→) chỉ ra các mục cần chú ý nhưng có thể không cản trở việc triển khai
- Mỗi phát hiện bao gồm các hành động cụ thể cần thực hiện, nếu có

**Cài Đặt Tham Số Mẫu**

- Hiển thị các giá trị chính xác bạn nên sử dụng cho các tham số mẫu quan trọng
- Các giá trị này dựa trên trạng thái hiện tại của tài khoản bạn

### Bước 2: Giải Quyết Mọi Vấn Đề

Nếu đoạn mã xác thực xác định bất kỳ vấn đề nào:

1. **Dấu X Màu Đỏ (✗)**

- Phải được giải quyết trước khi triển khai
- Thực hiện các mục hành động được cung cấp cho mỗi vấn đề
- Chạy lại đoạn mã xác thực sau khi thực hiện các thay đổi

2. **Mũi Tên Màu Vàng (→)**

- Xem xét các khuyến nghị
- Đảm bảo bạn hiểu các tác động
- Thực hiện hành động nếu cần thiết cho trường hợp sử dụng của bạn

#### Bước 3: Triển Khai Mẫu

1. Tải xuống mẫu để thiết lập cơ sở hạ tầng yêu cầu cho tài khoản: [Mẫu Cloudformation Thiết lập Tài khoản](/account-baseline.yaml)
2. Mở [Cloudformation Console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks?filteringText=&filteringStatus=active&viewNested=true) , và tạo một stack mới.
3. Sao chép các giá trị tham số từ phần "Cài Đặt Tham Số Mẫu" trong đầu ra CloudShell từ Bước 1 của hướng dẫn này, cập nhật các tham số trong CloudFormation console nơi mẫu sẽ được triển khai.
4. Triển khai mẫu CloudFormation
5. Nhập các tham số chính xác như được hiển thị bởi đoạn mã xác thực
6. Xem xét và tạo stack

#### Bước 4: Chuyển Vai Trò

Trong phần còn lại của workshop, bạn sẽ cần sử dụng một vai trò người dùng IAM được tạo bởi mẫu thiết lập cơ sở hạ tầng trong bước trước. Việc sử dụng vai trò này sẽ đảm bảo bạn có đủ quyền để hoàn thành workshop. Nếu người dùng IAM của bạn không thể đảm nhận các vai trò người dùng IAM, vui lòng liên hệ với quản trị viên AWS của bạn.

1. Nhấp vào tên và ID tài khoản của bạn ở góc trên bên phải. Trong menu, chọn **Switch Role**.
![1](/images/1/1.1/1.png)
2. Điền vào mẫu Chuyển Vai:

- Thêm ID Tài Khoản bạn đang sử dụng cho workshop.
- Dán tên vai trò này vào tên vai trò IAM: aidlWSParticipantRole
- Chọn một màu để liên kết với vai trò này.
- Nhấp vào **Switch Role**.
![2](/images/1/1.1/2.png)

3. Xác minh rằng bạn đã đảm nhận đúng vai trò:

- **LƯU Ý**: Bạn có thể thấy một lỗi sau khi đã đảm nhận vai trò thành công. Điều này là bình thường.
- Kiểm tra ở góc trên bên phải để xác minh rằng bạn thấy WSParticipantRole @ [YourAccountID]
- Điều hướng đến [trang chủ console](https://us-west-2.console.aws.amazon.com/console?region=us-west-2)

![3](/images/1/1.1/3.png)

### Những Điều Cần Lưu Ý Quan Trọng

- **Chọn Vùng**: Mẫu tạo ra các tài nguyên theo vùng. Hãy chọn vùng của bạn một cách cẩn thận, đặc biệt nếu bạn sử dụng IAM Identity Center.

- **QuickSight Đã Tồn Tại**: Nếu bạn có một đăng ký QuickSight hiện có:

  - Mẫu sẽ sử dụng đăng ký hiện tại của bạn
  - Đặt tham số theo đầu ra của đoạn mã xác thực
  - Tài nguyên sẽ được thêm vào môi trường QuickSight hiện có của bạn

- **Không Có QuickSight Hiện Tại**: Nếu bạn không có QuickSight:

  - Mẫu sẽ tạo một đăng ký mới
  - Phiên bản Enterprise Edition with Q sẽ được cấu hình
  - Xác thực IAM sẽ được thiết lập

### Dọn Dẹp

- Mẫu tạo ra một bucket S3 sẽ được giữ lại sau khi xóa stack
- Hành vi dọn dẹp QuickSight được kiểm soát bởi tham số DeleteQuickSightOnTermination
- Sử dụng giá trị tham số được đề xuất bởi đoạn mã xác thực
- Các bản sao lưu Aurora có thể được giữ lại tùy thuộc vào cài đặt của bạn

### Nhận Giúp Đỡ

Nếu bạn gặp vấn đề:

1. Chạy lại đoạn mã xác thực để xác minh trạng thái tài khoản của bạn
2. Xem xét bất kỳ thông báo lỗi nào trong console CloudFormation
3. Kiểm tra tài liệu workshop để biết thêm thông tin khắc phục sự cố
4. Nếu bạn đang sử dụng tài khoản AWS do công ty quản lý, vui lòng liên hệ với quản trị viên AWS của bạn.
