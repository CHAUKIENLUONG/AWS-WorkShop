+++
title = "Tạo Knowledge Base"
date = 2025
weight = 1
chapter = false
pre = "<b>3.1. </b>"
+++

### Giới thiệu

Trong bước này, chúng ta sẽ tạo một Amazon Bedrock: Knowledge Base. Knowledge base sẽ tham chiếu đến một nguồn dữ liệu S3 bao gồm dữ liệu hỗ trợ và sản phẩm cho cả Ohmzio và Ampwerks.

{{%notice note%}}
Xin lưu ý, AWS đang liên tục cải thiện và mở rộng khả năng của Bedrock. Bạn có thể nhận thấy rằng các ảnh chụp màn hình được cung cấp có thể khác một chút so với trải nghiệm của bạn trong console.
{{%/notice%}}

### Các bước:

### Yêu cầu quyền truy cập model

1. Điều hướng đến [console](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/) Amazon Bedrock. Nhấp **Get Started**

   1. Nếu xuất hiện pop-up Welcome to Amazon Bedrock!, tiếp tục bằng cách nhấp **Manage model access**. Nếu không, tiếp tục đến bước tiếp theo.

2. Yêu cầu quyền truy cập model:

   1. Ở bên trái màn hình, nhấp vào biểu tượng menu để mở menu dịch vụ.

   2. Nhấp **Model access**

   ![1](../../../images/3/3.1/1.png)

   3. Trong menu Model access, nhấp **Enable specific models** --or-- **Modify model access**.

   {{%notice info%}}
   **Không** chọn **Enable all models**.
   {{%/notice %}}

   4. Chọn các Base models sau:

   - Titan Text Embeddings V2
   - Claude 3.5 Sonnet

   {{%notice info%}}
   Xin lưu ý một số base models được liệt kê có thể đã có **Access granted**. Điều này sẽ không ảnh hưởng đến khả năng hoàn thành lab của bạn. Nếu một model được liệt kê trong bước này đã được cấp quyền, tiếp tục yêu cầu quyền truy cập cho tất cả các model khác được yêu cầu.
   {{%/notice %}}

   ![2](../../../images/3/3.1/2.png)

   Nhấp **Next**.

   5. Trong trang Review and submit nhấp **Submit**.

{{%notice%}}
Amazon Bedrock cung cấp trải nghiệm turnkey cho các nhà phát triển. Ví dụ, người dùng có thể tận dụng nhiều loại foundational models trên tất cả các dịch vụ Bedrock. Điều này, đến lượt nó, cung cấp cho người dùng tùy chọn chọn một foundational model phù hợp nhất với nhu cầu của họ. Tuy nhiên, các nhà cung cấp foundational model (tức là Anthropic, Cohere, Stability AI, v.v.) yêu cầu chấp nhận EULA và các guardrails hợp lý cho việc sử dụng model trước khi triển khai. Console Model Access quản lý các thỏa thuận này và cho phép quản trị viên thực thi nguyên tắc least privilege. Để tìm hiểu thêm về foundational models, tham khảo lại các khái niệm chính [Amazon Bedrock: Knowledge Base](../_index.md).
{{%/notice%}}

{{%notice note%}}
Sau khi yêu cầu quyền truy cập model, Amazon Bedrock đang thực hiện "undifferentiated heavy lifting" của việc quản lý quyền truy cập vào các foundational models mã nguồn mở này. Cấp quyền truy cập cho các foundational models không phải Amazon có thể mất vài phút. Để xác minh quyền truy cập đã được cấp, nhấp nút refresh bên cạnh Manage model access.
{{%/notice%}}

### Tạo Knowledge base

1. Nhấp **Knowledge bases** trong menu bên trái dưới phần Builder tools.

2. Trong trang Knowledge bases, nhấp **Create knowledge base with vector store**.

![3](../../../images/3/3.1/3.png)

3. Bước 1, cung cấp chi tiết knowledge base:

   1. Đặt tên knowledge base:

      `merger-knowledge-base`

   2. Mô tả knowledge base:

      `Knowledge base for product and support data for both Ohmzio and Ampwerks.`

   3. Để nguyên IAM permissions, Query Engine, và các cấu hình khác như mặc định.

   ![4](../../../images/3/3.1/4.png)

   4. Nhấp **Next**.

   ![5](../../../images/3/3.1/5.png)

   ![6](../../../images/3/3.1/6.png)

4. Bước 2, cấu hình nguồn dữ liệu:

   1. Đặt tên knowledge base data source với tên được cung cấp (nếu không tên mặc định sẽ được sử dụng), sau đó nhấp **Browse S3** để chọn S3 URI của dữ liệu nguồn.

   `merger-knowledge-base-data-source`

   ![7](../../../images/3/3.1/7.png)

   2. Nhấp vào tên bucket **customerdata-{uniqueId}**. Nhấp radio button bên cạnh data/ để chọn nó làm vị trí cho dữ liệu nguồn. Nhấp **Choose**.

   {{%notice note%}}
   Nếu bạn không thể tìm thấy bucket của mình, hãy đảm bảo bạn đang ở đúng AWS region.
   {{%/notice%}}

   ![8](../../../images/3/3.1/8.png)

   ![9](../../../images/3/3.1/9.png)

   3. Xác minh S3 URI:

   `s3://customerdata-{uniqueId}/data/`

   4. Không thay đổi bất kỳ cài đặt nâng cao nào.

   5. Nhấp **Next**.

5. Bước 3, chọn embeddings model và cấu hình vector store:

   ![10](../../../images/3/3.1/10.png)

   1. Dưới Embeddings model, nhấp Select model và sau đó chọn model **Titan Text Embeddings V2** và **On-demand Inference mode**.

   _Đây là model sẽ được sử dụng để tạo vector embeddings trong vector store._

   2. Dưới Vector store, Chọn Quick create a new vector store - Recommended method và Amazon OpenSearch Serverless làm loại vector store. Đây là mặc định và nên đã được chọn.

   _Một Amazon OpenSearch Serverless vector store sẽ được tạo tự động cho bạn._

   Để nguyên các cấu hình tùy chọn không được chọn.

   3. Nhấp **Next**.

6. Bước 4, Review and create:

   1. Xem xét cấu hình knowledge base.

   2. Xác minh S3 URI là chính xác:

   `s3://customerdata-{uniqueId}/data/`

   3. Nhấp **Create knowledge base**.

   ![11](../../../images/3/3.1/11.png)

   {{%notice success%}}
   Chờ knowledge base được tạo. AWS sẽ chuẩn bị vector database trong Amazon OpenSearch Serverless. Điều này có thể mất tới 10 phút để hoàn thành.
   {{%/notice%}}

### Đồng bộ Knowledge base

1. Khi knowledge base được tạo, chờ cho đến khi knowledge base được tạo thành công:

![12](../../../images/3/3.1/12.png)

2. Nhấp **Go to data source** hoặc cuộn xuống phần Data source. Để đồng bộ, nhấp radio button bên cạnh Data source mà chúng ta đã tạo (tên nên tương tự merger-knowledge-base-data-source). Nhấp **Sync**. Điều này sẽ mất vài phút.

![13](../../../images/3/3.1/13.png)

{{%notice%}}
Dữ liệu từ S3 bucket của bạn đang được đọc và chia thành các "chunks." Theo mặc định, Amazon Bedrock tự động chia dữ liệu nguồn của bạn sao cho mỗi chunk chứa 300 tokens. Model được chọn, Amazon Titan Embeddings V2, được sử dụng để chuyển đổi dữ liệu của bạn thành vector embeddings cho knowledge base.
{{%/notice%}}

3. Khi đồng bộ hoàn tất, bạn sẽ nhận được một thông báo khác.

![14](../../../images/3/3.1/14.png)
