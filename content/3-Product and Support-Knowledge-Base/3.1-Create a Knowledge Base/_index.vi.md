+++
title = "Tạo cơ sở kiến thức"
date = 2025
weight = 1
chapter = false
pre = "<b>3.1. </b>"
+++

### Giới thiệu

Trong bước này, chúng ta sẽ tạo một Amazon Bedrock: Knowledge Base. Cơ sở kiến thức sẽ tham chiếu đến nguồn dữ liệu S3 bao gồm dữ liệu hỗ trợ và sản phẩm cho cả Ohmzio và Ampwerks.

{{%notice note%}}
Xin lưu ý, AWS liên tục cải tiến và mở rộng khả năng của Bedrock. Bạn có thể nhận thấy rằng các ảnh chụp màn hình được cung cấp có thể hơi khác so với trải nghiệm của bạn trong giao diện điều khiển.
{{%/notice%}}

### Các bước thực hiện:

### Yêu cầu truy cập mô hình

1. Điều hướng đến [giao diện điều khiển](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/) Amazon Bedrock. Nhấp vào **Get Started**

   1. Nếu xuất hiện cửa sổ Welcome to Amazon Bedrock!, tiếp tục bằng cách nhấp vào **Manage model access**. Nếu không, chuyển sang bước tiếp theo.

2. Yêu cầu truy cập mô hình:

   1. Ở bên trái màn hình, nhấp vào biểu tượng menu để mở menu dịch vụ.

   2. Nhấp vào **Model access**

   ![1](../../../images/3/3.1/1.png)

   3. Trong menu Model access, nhấp vào Enable specific models --hoặc-- Modify model access.

   {{%notice info%}}
   Không chọn Enable all models.
   {{%/notice %}}

   4. Chọn các mô hình cơ bản sau:

   - Titan Text Embeddings V2
   - Claude 3.5 Sonnet

   {{%notice info%}}
   Xin lưu ý một số mô hình cơ bản được liệt kê có thể đã được **Access granted**. Điều này sẽ không ảnh hưởng đến khả năng hoàn thành bài thực hành của bạn. Nếu một mô hình được liệt kê trong bước này đã được cấp quyền, hãy tiếp tục yêu cầu truy cập vào tất cả các mô hình cần thiết khác.
   {{%/notice %}}

   ![2](../../../images/3/3.1/2.png)

   Nhấp vào **Next**.

   5. Trong trang Review and submit nhấp vào **Submit**.

{{%notice%}}
Amazon Bedrock cung cấp trải nghiệm chìa khóa trao tay cho người xây dựng. Ví dụ, người dùng có thể tận dụng một số loại mô hình nền tảng trên tất cả các dịch vụ Bedrock. Điều này, đến lượt nó, cung cấp cho người dùng tùy chọn để chọn một mô hình nền tảng phù hợp nhất với nhu cầu của họ. Tuy nhiên, các nhà cung cấp mô hình nền tảng (tức là Anthropic, Cohere, Stability AI, v.v.) yêu cầu chấp nhận EULA và các biện pháp bảo vệ hợp lý cho việc sử dụng mô hình trước khi triển khai. Giao diện điều khiển Model Access quản lý các thỏa thuận này và cho phép quản trị viên thực thi nguyên tắc đặc quyền tối thiểu. Để tìm hiểu thêm về các mô hình nền tảng, hãy xem lại các khái niệm chính về [Amazon Bedrock: Knowledge Base](../_index.md).
{{%/notice%}}

{{%notice note%}}
Sau khi yêu cầu truy cập mô hình, Amazon Bedrock đang thực hiện "công việc nặng nhọc không khác biệt" của việc quản lý truy cập vào các mô hình nền tảng mã nguồn mở này. Việc cấp quyền truy cập vào các mô hình nền tảng không phải của Amazon có thể mất vài phút. Để xác minh quyền truy cập đã được cấp, hãy nhấp vào nút làm mới bên cạnh Manage model access.
{{%/notice%}}

### Tạo cơ sở kiến thức

1. Nhấp vào **Knowledge bases** trong menu bên trái dưới phần Builder tools.

2. Trong trang Knowledge bases, nhấp vào **Create knowledge base with vector store**.

![3](../../../images/3/3.1/3.png)

3. Bước 1, cung cấp chi tiết cơ sở kiến thức:

   1. Đặt tên cho cơ sở kiến thức:

      `merger-knowledge-base`

   2. Mô tả cơ sở kiến thức:

      `Cơ sở kiến thức cho dữ liệu sản phẩm và hỗ trợ cho cả Ohmzio và Ampwerks.`

   3. Giữ nguyên quyền IAM, Query Engine và các cấu hình khác theo mặc định.

   ![4](../../../images/3/3.1/4.png)

   4. Nhấp vào **Next**.

   ![5](../../../images/3/3.1/5.png)

   ![6](../../../images/3/3.1/6.png)

4. Bước 2, cấu hình nguồn dữ liệu:

   1. Đặt tên cho nguồn dữ liệu cơ sở kiến thức với tên được cung cấp (nếu không tên mặc định sẽ được sử dụng), sau đó nhấp vào **Browse S3** để chọn S3 URI của dữ liệu nguồn.

   `merger-knowledge-base-data-source`

   ![7](../../../images/3/3.1/7.png)

   2. Nhấp vào tên bucket customerdata-{uniqueId}. Nhấp vào nút radio bên cạnh data/ để chọn nó làm vị trí cho dữ liệu nguồn. Nhấp Choose.

   {{%notice note%}}
   Nếu bạn không thể tìm thấy bucket của mình, hãy đảm bảo bạn đang ở đúng vùng AWS.
   {{%/notice%}}

   ![8](../../../images/3/3.1/8.png)

   ![9](../../../images/3/3.1/9.png)

   3. Xác minh S3 URI:

   `s3://customerdata-{uniqueId}/data/`

   4. Không thay đổi bất kỳ cài đặt nâng cao nào.

   5. Nhấp vào **Next**.

5. Bước 3, chọn mô hình embeddings và cấu hình vector store:

   ![10](../../../images/3/3.1/10.png)

   1. Dưới phần Embeddings model, nhấp vào Select model và sau đó chọn mô hình **Titan Text Embeddings V2** và **On-demand Inference mode**.

   {{%notice%}}
   Đây là mô hình sẽ được sử dụng để tạo các vector embeddings trong vector store.
   {{%/notice%}}

   2. Dưới phần Vector store, Chọn Quick create a new vector store - Recommended method và Amazon OpenSearch Serverless làm loại vector store. Đây là mặc định và nên đã được chọn sẵn.

   {{%notice%}}
   Một vector store Amazon OpenSearch Serverless sẽ được tạo tự động cho bạn.
   {{%/notice%}}

   Để nguyên các cấu hình tùy chọn không được chọn.

   3. Nhấp vào **Next**.

6. Bước 4, Xem xét và tạo:

   1. Xem xét cấu hình cơ sở kiến thức.

   2. Xác minh S3 URI là chính xác:

   `s3://customerdata-{uniqueId}/data/`

   3. Nhấp vào **Create knowledge base**.

   ![11](../../../images/3/3.1/11.png)

   {{%notice success%}}
   Đợi cho cơ sở kiến thức được tạo. AWS sẽ chuẩn bị cơ sở dữ liệu vector trong Amazon OpenSearch Serverless. Quá trình này có thể mất đến 10 phút để hoàn thành.
   {{%/notice%}}

### Đồng bộ hóa cơ sở kiến thức

1. Sau khi cơ sở kiến thức được tạo, đợi cho đến khi cơ sở kiến thức được tạo thành công:

![12](../../../images/3/3.1/12.png)

2. Nhấp vào **Go to data source** hoặc cuộn xuống phần Data source. Để đồng bộ hóa, nhấp vào nút radio bên cạnh Data source mà chúng ta đã tạo (tên nên giống với merger-knowledge-base-data-source). Nhấp vào **Sync**. Quá trình này sẽ mất vài phút.

![13](../../../images/3/3.1/13.png)

{{%notice%}}
Dữ liệu từ bucket S3 của bạn đang được đọc và chia thành "các khối". Theo mặc định, Amazon Bedrock tự động chia dữ liệu nguồn của bạn sao cho mỗi khối chứa 300 token. Mô hình đã chọn, Amazon Titan Embeddings V2, được sử dụng để chuyển đổi dữ liệu của bạn thành vector embeddings cho cơ sở kiến thức.
{{%/notice%}}

3. Khi quá trình đồng bộ hóa hoàn tất, bạn sẽ nhận được một thông báo khác.

![14](../../../images/3/3.1/14.png)
