+++
title = "Cơ sở kiến thức về Sản phẩm và Hỗ trợ"
date = 2025
weight = 3
chapter = false
pre = "<b>3. </b>"
+++

### Bối cảnh
Sau khi phát hiện những phát hiện ban đầu quan trọng trong dữ liệu bằng phân tích mô tả trong QuickSight, hãy tận dụng khả năng AI tổng hợp để tăng cường quy trình khám phá dữ liệu. Để đảm bảo quá trình sáp nhập diễn ra suôn sẻ, việc hiểu rõ những khó khăn mà khách hàng gặp phải với sản phẩm là điều quan trọng nhất. Chúng ta sẽ sử dụng kết hợp các dịch vụ AI tổng hợp của AWS và các phương pháp tối ưu kỹ thuật prompt để tạo ra kết quả.

### Kỹ thuật Prompt

Kỹ thuật prompt là một phương pháp được sử dụng trong lĩnh vực trí tuệ nhân tạo (AI), đặc biệt với các mô hình AI tổng hợp như Large Language Models (LLMs), để tạo ra các đầu vào (prompts) hướng dẫn mô hình tạo ra các kết quả mong muốn. Nó bao gồm việc thiết kế, tinh chỉnh và kiểm tra các prompt để giao tiếp hiệu quả nhiệm vụ hoặc câu hỏi với mô hình theo cách tối đa hóa khả năng nhận được phản hồi chính xác, phù hợp và mạch lạc.

Bằng cách áp dụng các phương pháp tối ưu trong việc thiết kế prompt được sử dụng trong cơ sở kiến thức, chúng ta có thể nhận được kết quả có giá trị cao tối ưu. Ngoài ra, kỹ thuật prompt hiệu quả đòi hỏi phải hiểu rõ về dữ liệu huấn luyện, khả năng và giới hạn của mô hình. Các prompt phải đủ cụ thể để tạo ra phản hồi mong muốn nhưng cũng đủ linh hoạt để cho phép mô hình tạo ra các kết quả sáng tạo hoặc sâu sắc.

### Dữ liệu Sản phẩm và Hỗ trợ

Bạn đã được cung cấp dữ liệu sản phẩm và hỗ trợ cho cả Ohmzio và Ampwerks. Dữ liệu hiện được lưu trữ trong Amazon S3 Bucket.

    s3://customerdata
    └── data/
        ├── ampwerks/
        │   ├── productinfo/
        │   │   └── <product-documentation>.docx
        │   └── support/
        │       └── <support-tickets>.json
        └── ohmzio/
            ├── productinfo/
            │   └── <product-documentation>.docx
            └── support/
                └── <support-tickets>.json

Đối với mỗi công ty, thư mục productinfo/ chứa các tệp .docx cho từng sản phẩm họ bán. Mỗi tài liệu chứa mô tả chi tiết về sản phẩm, hướng dẫn và câu hỏi thường gặp.

Thư mục support/ chứa các tệp .json cho mọi ticket hỗ trợ khách hàng. Các ticket hỗ trợ này chứa các tương tác giữa đại diện hỗ trợ và khách hàng yêu cầu hỗ trợ về sản phẩm họ đã mua.

Dữ liệu productinfo/ và support/ sẽ cung cấp dữ liệu ngữ cảnh có liên quan cao cho mô hình nền tảng. Điều này sẽ cho phép mô hình cung cấp phản hồi dựa trên các tương tác thực tế và giảm thiểu ảo giác.

{{%notice%}}
**ảo giác**: (liên quan đến trí tuệ nhân tạo) là phản hồi được tạo ra bởi AI chứa thông tin sai hoặc gây hiểu lầm được trình bày như sự thật.
{{%/notice%}}

### Amazon Bedrock: Knowledge Bases

Để tăng cường nỗ lực khám phá, bạn sẽ sử dụng Amazon Bedrock: Knowledge Bases để tạo nguồn dữ liệu được chỉ định cụ thể (dữ liệu sản phẩm và hỗ trợ cho cả hai công ty) để thực hiện Retrieval Augmented Generation (RAG) với Foundation Model (FM) trên nguồn dữ liệu chúng ta xác định. Đây là kiến trúc logic của kiến trúc RAG sử dụng Knowledge Bases và các khái niệm chính:

![1](../../images/3/1.png)

* **Retrieval Augmented Generation (RAG)** là một phương pháp trong trí tuệ nhân tạo kết hợp khả năng của hai thành phần chính: hệ thống truy xuất và mô hình tổng hợp. Phương pháp này đặc biệt được sử dụng trong các tác vụ xử lý ngôn ngữ tự nhiên (NLP), như trả lời câu hỏi, tạo nội dung và hệ thống đối thoại. Mục tiêu của RAG là nâng cao chất lượng, độ phù hợp và độ chính xác của đầu ra của mô hình tổng hợp bằng cách kết hợp động kiến thức bên ngoài được truy xuất trong thời gian thực.

* **Large Language Model (LLM)** là một mô hình học sâu rất lớn được huấn luyện trước trên lượng dữ liệu khổng lồ. Transformer cơ bản là một tập hợp các mạng nơ-ron bao gồm bộ mã hóa và giải mã với khả năng tự chú ý. Bộ mã hóa và giải mã trích xuất ý nghĩa từ chuỗi văn bản và hiểu mối quan hệ giữa các từ và cụm từ trong đó. Điều này cho phép LLM cực kỳ linh hoạt. Một mô hình có thể thực hiện các nhiệm vụ hoàn toàn khác nhau như trả lời câu hỏi, tóm tắt tài liệu, dịch ngôn ngữ và hoàn thành câu.

* **Foundation Model (FM)** có phạm vi rộng hơn và bao gồm không chỉ các mô hình ngôn ngữ mà còn bất kỳ loại mô hình học sâu nào được huấn luyện trước trên tập dữ liệu lớn và có thể được tinh chỉnh cho nhiều nhiệm vụ khác nhau. Khái niệm này mở rộng ra ngoài văn bản để bao gồm các mô hình được đào tạo trên hình ảnh, âm thanh và hơn thế nữa.

* **Vector Store** trong bối cảnh AI tổng hợp đề cập đến cơ sở dữ liệu hoặc hệ thống lưu trữ chứa các vector đa chiều, là biểu diễn của các mục dữ liệu (như văn bản, hình ảnh hoặc âm thanh) dưới dạng máy có thể xử lý và hiểu hiệu quả. Các vector này thường được tạo ra thông qua quá trình embedding, trong đó các mục dữ liệu được chuyển đổi thành các vector có kích thước cố định, nắm bắt các thuộc tính ngữ nghĩa và mối quan hệ của dữ liệu gốc trong không gian vector liên tục.

{{%notice%}}
Khi được sử dụng với RAG, mô hình AI tổng hợp có thể truy vấn vector store để truy xuất thông tin liên quan dựa trên truy vấn đầu vào. Thông tin này sau đó có thể được sử dụng để tạo ra phản hồi vừa phù hợp vừa được cập nhật bằng dữ liệu cụ thể.
{{%/notice%}}

### Các bước

* Tạo Amazon Bedrock: Knowledge Base
* Kiểm tra knowledge base
* Sử dụng kỹ thuật prompt để trích xuất dữ liệu về sản phẩm và dịch vụ