---
title : "Bản đề xuất"
date: 2026-01-10
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

## 1. Tóm tắt điều hành
**AnTiScaQ** là một hệ thống kiểm tra và cảnh báo nguy cơ lừa đảo trực tuyến, được xây dựng nhằm giúp người dùng phát hiện sớm các dấu hiệu đáng ngờ. Hệ thống phân tích nhiều loại dữ liệu đầu vào như **số điện thoại, tên miền và nội dung email** để đánh giá độ uy tín và đưa ra cảnh báo theo mức độ rủi ro. Thay vì đưa ra kết luận mang tính pháp lý, AnTiScaQ tập trung vào việc cảnh báo, giải thích các dấu hiệu nghi vấn và hướng dẫn người dùng cách phòng tránh. Hệ thống hoạt động dựa trên việc thu thập dữ liệu, tiếp nhận báo cáo từ cộng đồng và áp dụng cơ chế chấm điểm rủi ro.

## 2. Tuyên bố vấn đề

### Vấn đề hiện tại
* Lừa đảo trực tuyến đang gia tăng nhanh chóng và ngày càng tinh vi, gây ra thiệt hại lớn cho người dùng và doanh nghiệp.
* Thiếu vắng một hệ thống đáng tin cậy, khiến người dùng dễ đưa ra quyết định sai lầm.
* Người dùng thường phải tìm kiếm thủ công qua các nền tảng trình duyệt (Google, Microsoft Edge, ...) hoặc dùng các cơ sở dữ liệu phân mảnh để kiểm tra số điện thoại/đường link đáng ngờ, gây tốn thời gian và rủi ro.
* Các công cụ hiện có thường thiếu **khả năng phân tích ngữ cảnh nội dung**.
  * Thiếu hụt dữ liệu từ **cộng đồng người dùng**.
  * Không cung cấp **giải thích rõ ràng về mức độ rủi ro**.
* Chi phí quá đắt đỏ để mua API từ các nền tảng Threat Intel doanh nghiệp (như Recorded Future, VirusTotal).
* Báo cáo thường bị thiếu sót, **không theo thời gian thực (not real-time)** khi các chiến dịch phishing mới bùng nổ.

## Giải pháp đề xuất
* **Tự động hóa phát hiện rủi ro:** Phân tích đa nguồn (số điện thoại, domain, URL, nội dung email) kết hợp rule-based và AI để phát hiện sớm các dấu hiệu lừa đảo.

* **Phân tích ngữ cảnh bằng AI:** Sử dụng Amazon Bedrock để “hiểu” nội dung và cung cấp giải thích rõ ràng về mức độ rủi ro, giúp người dùng dễ dàng ra quyết định.

* **Khai thác sức mạnh cộng đồng:** Xây dựng hệ thống báo cáo và chấm điểm uy tín dựa trên đóng góp của người dùng, giúp dữ liệu luôn được cập nhật và phản ánh đúng thực tế.

* **Tối ưu chi phí & Khả năng mở rộng:** Áp dụng kiến trúc Hybrid:
  * Elastic Beanstalk (Docker) cho backend chính
  * Lambda cho AI & linh hoạt xử lý → Giảm thiểu chi phí so với các hệ thống enterprise truyền thống.

* **Tích hợp hệ sinh thái AWS:** Sử dụng Cognito, RDS, DynamoDB, S3, CloudFront, WAF... để đảm bảo bảo mật, hiệu năng và khả năng tự động mở rộng.

* **Trải nghiệm người dùng đơn giản:** Cung cấp một nền tảng duy nhất thay thế việc tìm kiếm thủ công, giúp kiểm tra nhanh chóng và chính xác.
  
#### Lợi ích

* Phát hiện sớm nguy cơ lừa đảo từ nhiều loại dữ liệu đầu vào như số điện thoại, tên miền và nội dung số.
* Đưa ra cảnh báo rủi ro rõ ràng, dễ hiểu và hỗ trợ người dùng ra quyết định an toàn hơn.
* Tiết kiệm thời gian nhờ tự động hóa quá trình kiểm tra và đối chiếu thông tin.
* Nâng cao độ chính xác thông qua việc kết hợp dữ liệu hệ thống với báo cáo từ cộng đồng.
* Tăng cường an toàn cho người dùng khi duyệt web và tương tác với các nguồn thông tin trực tuyến.
* Hỗ trợ cải thiện nhận thức, kỹ năng tự bảo vệ và phòng tránh lừa đảo số.
* Củng cố bảo mật nhờ cơ chế theo dõi liên tục và cảnh báo kịp thời.
  
## 3. Kiến trúc giải pháp

Đây là sơ đồ kiến trúc đám mây của hệ thống:
<img width="2448" height="1831" alt="aws_architecture drawio" src="https://github.com/user-attachments/assets/d8645511-e074-4cbb-b41f-21e613173038" />

**Dịch vụ AWS sử dụng**

#### Dịch vụ AWS sử dụng

| Dịch vụ AWS | Chức năng chính |
|---|---|
| AWS Elastic Beanstalk | Triển khai và quản lý ứng dụng backend (Spring Boot) dưới dạng Docker container. |
| Amazon RDS for MySQL | Cơ sở dữ liệu quan hệ, lưu trữ dữ liệu có cấu trúc (user, report, domain, history, ...). |
| AWS Lambda | Xử lý các tác vụ serverless (AI chatbot, phân tích nội dung, xử lý bất đồng bộ). |
| Amazon API Gateway | Quản lý và expose API, xử lý định tuyến request, validation và bảo mật endpoint. |
| Amazon DynamoDB | NoSQL database, lưu trữ dữ liệu tạm/thời gian thực (OTP). |
| AWS Cognito | Xác thực và phân quyền người dùng (Authentication & Authorization, hỗ trợ SSO Google). |
| Amazon S3 | Lưu trữ file (ảnh, tài liệu, static assets). |
| Amazon CloudFront | CDN phân phối nội dung (frontend, file từ S3), giảm độ trễ và tăng tốc độ tải trang. |
| Amazon Route 53 | Quản lý DNS, mapping domain tới hệ thống. |
| AWS WAF | Bảo vệ API khỏi các đợt tấn công (rate limiting, chống bot, chống abuse). |
| Amazon CloudWatch | Giám sát hệ thống, lưu log, metrics và gửi cảnh báo (alert). |
| Amazon SNS | Gửi thông báo (email, SMS) cho hệ thống và người dùng. |
| Amazon Bedrock | Cung cấp AI/LLM cho chatbot và phân tích nội dung lừa đảo. |
| AWS Secrets Manager | Quản lý bảo mật thông tin nhạy cảm (API keys, credentials). |
| AWS CodePipeline | Tự động hóa CI/CD pipeline (build → test → deploy). |
| AWS CodeBuild | Service chịu trách nhiệm build và test code trong CI/CD pipeline. |


## Thiết kế thành phần

**1. Lớp Thu Thập Dữ Liệu & Nhận Diện (Data Collection & Detection Layer)**

* **Nguồn dữ liệu:** Hệ thống tiếp nhận dữ liệu từ nhiều nguồn khác nhau, bao gồm thông tin do người dùng cung cấp (số điện thoại, tên miền, nội dung email), dữ liệu đóng góp từ cộng đồng (báo cáo, phản hồi), và các dịch vụ/API bên ngoài như WHOIS hoặc nguồn tra cứu domain.
* **Tiếp nhận dữ liệu:** Backend triển khai trên Spring Boot và AWS Elastic Beanstalk chịu trách nhiệm tiếp nhận, chuẩn hóa và tiền xử lý dữ liệu đầu vào, đồng thời kích hoạt các tiến trình phân tích khi phát sinh dữ liệu mới.

**2. Lớp Xử Lý Sự Kiện (Event Processing Layer)**

* **Định tuyến & xử lý yêu cầu:** Amazon API Gateway tiếp nhận request từ phía client, sau đó chuyển tiếp đến backend để thực hiện validation, xử lý nghiệp vụ và phân loại yêu cầu phù hợp.
* **Xử lý bất đồng bộ:** Những tác vụ cần xử lý nền như phân tích AI, kiểm tra nội dung, hoặc xử lý không đồng bộ sẽ được chuyển sang AWS Lambda. Cơ chế event-driven có thể kết hợp với SNS hoặc các service nội bộ để tối ưu luồng xử lý.

**3. Lớp Điều Phối & Xử Lý Nghiệp Vụ (Orchestration & Business Logic Layer)**

* **Điều phối trung tâm:** Backend đóng vai trò là bộ điều phối chính, kiểm soát toàn bộ quy trình từ tiếp nhận input, phân tích dữ liệu đến tổng hợp và trả kết quả cho người dùng.
* **Xử lý nghiệp vụ:** Hệ thống tổng hợp dữ liệu từ nhiều nguồn như RDS, DynamoDB và các API bên ngoài; sau đó gọi các dịch vụ AI để phân tích nội dung, phát hiện hành vi đáng ngờ, tính toán điểm rủi ro và xác định mức cảnh báo.

**4. Lớp Xử Lý Dữ Liệu & Lưu Trữ (Data Processing & Storage Layer)**

* **Lưu trữ dữ liệu:** Amazon RDS for MySQL được sử dụng cho dữ liệu quan hệ chính như người dùng, báo cáo, lịch sử tra cứu và domain; DynamoDB phục vụ các dữ liệu cần truy xuất nhanh hoặc mang tính thời gian thực; Amazon S3 dùng để lưu trữ tệp, hình ảnh và tài liệu liên quan.
* **Hỗ trợ xử lý dữ liệu:** AWS Lambda đảm nhiệm các tác vụ ETL nhẹ, tiền xử lý dữ liệu và chuẩn bị dữ liệu đầu vào cho các mô hình AI hoặc các bước phân tích tiếp theo.

**5. Lớp AI & Phân Tích (AI & Analysis Layer)**

* **Năng lực AI:** Amazon Bedrock được sử dụng để cung cấp khả năng phân tích thông minh đối với email, số điện thoại, tên miền và các nội dung nghi ngờ, đồng thời hỗ trợ giải thích lý do cảnh báo và vận hành chatbot tư vấn phòng tránh lừa đảo.
* **Tích hợp AI an toàn:** AWS Lambda đóng vai trò trung gian khi giao tiếp với Bedrock, giúp kiểm soát truy cập, xử lý kết quả trả về và đảm bảo luồng tích hợp AI được an toàn, linh hoạt.

**6. Lớp Trình Bày & Tương Tác Người Dùng (Presentation & User Interaction Layer)**

* **Giao diện người dùng:** Frontend được xây dựng bằng React và có thể triển khai qua S3 kết hợp CloudFront để tối ưu phân phối nội dung. Ứng dụng giao tiếp với backend thông qua API Gateway theo cơ chế bảo mật phù hợp.
* **Quản lý truy cập:** Việc xác thực người dùng và quản lý phiên đăng nhập được thực hiện thông qua AWS Cognito, hỗ trợ JWT và các cơ chế quản lý danh tính hiện đại.

**7. Lớp Bảo Mật & Giám Sát (Security & Monitoring Layer)**

* **Bảo mật & kiểm soát truy cập:** Hệ thống áp dụng AWS Cognito cho xác thực, kết hợp AWS WAF, IAM, ACM (SSL/TLS) và Route 53 để tăng cường bảo mật, quản lý phân quyền và đảm bảo an toàn cho hạ tầng mạng.
* **Giám sát vận hành:** Amazon CloudWatch được sử dụng để theo dõi logs, metrics và trạng thái hệ thống; SNS hỗ trợ gửi cảnh báo khi có sự cố; trong khi đó, AWS Secrets Manager lưu trữ và bảo vệ các thông tin nhạy cảm như credentials và API keys.

## 4. Lộ trình Khai triển Kỹ thuật

**Bước 1: Xây dựng hạ tầng và cấu hình nền tảng**

* **Mạng và bảo mật:** Thiết lập kiến trúc mạng trên AWS với VPC, phân tách Public Subnet cho các thành phần public-facing như Load Balancer/Internet và Private Subnet cho cơ sở dữ liệu. Đồng thời cấu hình Internet Gateway, Security Groups và các chính sách truy cập phù hợp để đảm bảo chỉ các dịch vụ cần thiết mới được phép kết nối.
* **Triển khai backend cốt lõi:** Đưa ứng dụng backend Spring Boot lên AWS Elastic Beanstalk dưới dạng Docker container. Thiết lập Amazon RDS (MySQL) cho dữ liệu chính, DynamoDB cho các dữ liệu cần truy xuất nhanh như OTP, và Amazon S3 để lưu trữ tệp, hình ảnh hoặc tài liệu đính kèm.
* **Khởi tạo dịch vụ nền:** Cấu hình AWS Cognito cho xác thực người dùng và hỗ trợ Google SSO. Đồng thời xây dựng các API nền tảng ban đầu như xác thực, quản lý dữ liệu threat/report và các API phục vụ dashboard quản trị.

**Bước 2: Phát triển API công khai và Web Portal MVP**

* **Public Lookup API:** Xây dựng các API tra cứu công khai cho số điện thoại, tên miền và nội dung nghi ngờ nhằm phục vụ nhu cầu kiểm tra nhanh từ người dùng.
* **Triển khai giao diện web:** Phát triển frontend bằng React.js và triển khai thông qua Amazon S3 kết hợp với CloudFront để tăng tốc phân phối nội dung.
* **Hoàn thiện tính năng nền tảng:** Xây dựng luồng báo cáo lừa đảo cơ bản, dashboard thống kê ban đầu và cấu hình Route 53 để kết nối domain với hệ thống.

**Bước 3: Hoàn thiện xử lý dữ liệu và nghiệp vụ lõi**

* **Xây dựng engine xử lý:** Tích hợp các dịch vụ tra cứu như WHOIS/API bên ngoài để kiểm tra domain, đồng thời xây dựng cơ chế chấm điểm rủi ro dựa trên luật (rule-based), dữ liệu cộng đồng và các tín hiệu phân tích nội dung.
* **Tích hợp AI và xử lý bất đồng bộ:** Sử dụng AWS Lambda kết hợp với Amazon Bedrock để xử lý phân tích email, nội dung nghi ngờ, chatbot tư vấn và các tác vụ xử lý nền theo mô hình async.
  
**Bước 4: Mở rộng tính năng và nâng cấp frontend**

* **Cải thiện UI/UX:** Hoàn thiện giao diện người dùng với dashboard chi tiết hơn, lịch sử tra cứu và trải nghiệm trực quan hơn cho các luồng kiểm tra.
* **Mở rộng kênh tích hợp:** Phát triển và tích hợp browser extension để hỗ trợ cảnh báo website nghi ngờ theo thời gian thực ngay trên trình duyệt.
* **Tối ưu trải nghiệm tổng thể:** Điều chỉnh hiệu năng API, giảm thời gian phản hồi và cải thiện luồng tương tác giữa frontend và backend.

**Bước 5: Kiểm thử, bảo mật và tối ưu vận hành**

* **Kiểm thử hệ thống:** Thực hiện đầy đủ các lớp kiểm thử gồm unit test, integration test và load test để đảm bảo tính ổn định trước khi mở rộng người dùng.
* **Tăng cường bảo mật:** Áp dụng AWS WAF để hạn chế tấn công và lạm dụng API, cấu hình IAM Roles theo nguyên tắc phân quyền tối thiểu, đồng thời triển khai AWS ACM để quản lý chứng chỉ SSL/TLS.
* **Tối ưu hiệu năng và chi phí:** Bật Auto Scaling cho Elastic Beanstalk, tối ưu cache qua CloudFront và cải thiện hiệu suất truy vấn trên RDS để hệ thống vận hành ổn định với chi phí hợp lý.

#### Yêu cầu Kỹ thuật

| Thành phần | Mô tả |
|---|---|
| Frontend & Bảng điều khiển | Giao diện người dùng được xây dựng bằng Next.js, lưu trữ dưới dạng static assets trên Amazon S3 và phân phối thông qua Amazon CloudFront để tối ưu tốc độ truy cập toàn cầu. |
| Backend & Xử lý Logic | Phần logic cốt lõi được phát triển bằng Python 3.12, triển khai trên AWS Lambda và được truy cập thông qua Amazon API Gateway để xử lý request theo mô hình serverless. |
| Dữ liệu & Lưu trữ | Hệ thống sử dụng Amazon DynamoDB cho các tác vụ truy vấn tốc độ cao, đồng thời kết hợp với Amazon S3 để lưu trữ an toàn các tệp tin, tài liệu và bằng chứng liên quan. |
| Cơ sở hạ tầng (IaC) | Toàn bộ hạ tầng AWS được định nghĩa, triển khai và quản lý tự động bằng mã thông qua AWS Cloud Development Kit (CDK), giúp chuẩn hóa và dễ mở rộng. |
| Bảo mật & Giám sát | Nền tảng áp dụng AWS Cognito cho xác thực, IAM cho quản lý phân quyền, đồng thời sử dụng Amazon CloudWatch để giám sát hoạt động, ghi log và theo dõi hệ thống liên tục. |
| CI/CD | Quy trình tích hợp và triển khai liên tục được thực hiện qua AWS CodePipeline, kết hợp AWS CodeBuild để tự động build và kiểm thử mã nguồn. |

## 5. Lộ trình & Mốc triển khai

| Tuần | Giai đoạn | Hoạt động chính | Sản phẩm bàn giao |
|---|---|---|---|
| 1-2 | Xây dựng nền tảng (MVP Core) | Thiết lập hạ tầng AWS cơ bản gồm VPC, Subnet, Security Group; triển khai backend trên Elastic Beanstalk kết hợp RDS; cấu hình Cognito và xây dựng các API cốt lõi ban đầu. | Hoàn thiện chức năng xác thực, Threat API, Report API và triển khai backend thành công trên môi trường cloud. |
| 3-4 | Phát triển API & tự động hóa | Xây dựng các API tra cứu cho số điện thoại, domain và URL; tích hợp WHOIS; cấu hình hệ thống thông báo qua SNS; thiết lập pipeline CI/CD. | Các API tra cứu hoạt động ổn định, Web Portal MVP sẵn sàng và pipeline CI/CD được đưa vào vận hành. |
| 5-6 | Tích hợp AI & mở rộng phân tích | Kết nối AWS Lambda với Amazon Bedrock để xử lý phân tích nội dung, chấm điểm rủi ro bằng AI và triển khai các luồng xử lý bất đồng bộ. | Hoàn thành chatbot AI, mô-đun phân tích nội dung và cơ chế risk scoring nâng cao. |
| 7-8 | Dashboard & tích hợp mở rộng | Phát triển admin dashboard, bổ sung API thống kê, hoàn thiện giao diện frontend và tích hợp thêm extension hỗ trợ. | Dashboard quản trị hoàn chỉnh, giao diện người dùng được cải thiện và sẵn sàng sử dụng. |
| 9-10 | Tối ưu hiệu năng hệ thống | Tối ưu khả năng vận hành thông qua Auto Scaling, CloudFront caching, cải thiện truy vấn cơ sở dữ liệu và nâng cấp hiệu năng API. | Hệ thống vận hành ổn định hơn, tốc độ xử lý và hiệu năng tổng thể được nâng cao. |
| 11 | Tăng cường bảo mật | Cấu hình AWS WAF, IAM, SSL/TLS qua ACM, bật logging và monitoring với CloudWatch, đồng thời rà soát các cấu hình an toàn hệ thống. | Hoàn thiện lớp bảo mật và giám sát cho toàn bộ nền tảng. |
| 12 | Kiểm thử toàn diện | Thực hiện unit test, integration test, load test, kiểm thử end-to-end và xử lý các lỗi phát sinh trong quá trình đánh giá. | Báo cáo kiểm thử hoàn chỉnh, hệ thống đạt mức ổn định trước giai đoạn bàn giao. |
| 13 | Hoàn tất bàn giao | Chuẩn hóa tài liệu kỹ thuật như API docs, tài liệu kiến trúc, hướng dẫn demo hệ thống và tổ chức lại repository GitHub. | Bộ tài liệu hoàn chỉnh, bản demo vận hành được và dự án sẵn sàng bàn giao. |

## 6. Ước tính ngân sách

**Chi phí AWS hàng tháng (Phase 1: ~5,000 API lookups/ngày)**
*Kiến trúc Serverless - Chi phí tối ưu*

| Dịch vụ | Cấu hình | Chi phí/tháng |
| :--- | :--- | :--- |
| **AWS Lambda** | 15K invocations, 512MB, 4000ms avg | $0 *(Free tier)* |
↳ Free tier: 1M requests + 400K GB-seconds/month
| **Amazon API Gateway** | 15K REST API requests | $0 |
| **Amazon DynamoDB** | On-demand, 5GB storage, 1M reads, 0.5M write | $0.5 |
| **Amazon S3 Vectors** | 2GB data, PUT/GET | $0.60 |
| **Amazon Bedrock** | Model: Claude Haiku 3, Input Token: 6GB, Output Token: 4GB | $6.5 |
| **Amazon CloudFront** | 10GB transfer, 200K requests | $1.00 |
| **Amazon Route 53** | 1 hosted zone | $0.90 |
| **Amazon CloudWatch**| Log và Auth cơ bản | $0 *(Free tier)* |
| **AWS Secrets Manager**| Quản lý key proxy | $0.4 |
| **AWS Elastic Beanstalk** | t3.micro | $11.68 |
| **Amazon Cognito** | 1000 MAU | $0 |
↳ Free tier: < 50K MAU
| **Amazon RDS for MySQL** | instance db.t4g.micro, gp3 | $21.01 |
| | **TỔNG AWS/THÁNG** | **~$42.59** |


## 7. Đánh giá rủi ro & Biện pháp giảm thiểu

| Rủi ro | Ảnh hưởng | Giảm thiểu |
|---|---|---|
| Quá tải backend và RDS khi lưu lượng tăng đột biến | Cao | Thiết lập Auto Scaling cho Elastic Beanstalk dựa trên các chỉ số như CPU, memory hoặc network. Đồng thời sử dụng connection pooling cho backend Spring Boot để kiểm soát số lượng kết nối tới RDS và hạn chế nguy cơ nghẽn hệ thống. |
| Chi phí Amazon Bedrock tăng mạnh do tần suất gọi AI cao | Cao | Áp dụng rate limiting tại API Gateway hoặc AWS WAF để kiểm soát lưu lượng. Giới hạn số lượng token đầu ra của mô hình và tận dụng cơ chế cache đối với các kết quả phân tích lặp lại nhằm giảm số lần gọi AI không cần thiết. |
| False positive từ dữ liệu báo cáo cộng đồng | Cao | Xây dựng cơ chế chấm điểm độ tin cậy cho người dùng gửi báo cáo, đồng thời yêu cầu đối chiếu với nhiều nguồn như WHOIS, rule-based engine hoặc dữ liệu nội bộ trước khi phát sinh cảnh báo chính thức. |
| Scraper hoặc WHOIS API bị chặn IP / giới hạn tần suất truy cập | Trung bình | Sử dụng rotating proxy pool và lưu trữ thông tin nhạy cảm liên quan trong AWS Secrets Manager. Kết hợp thêm retry strategy với exponential backoff để xử lý các lỗi tạm thời từ API bên ngoài. |
| Lambda timeout khi xử lý tác vụ AI hoặc async kéo dài | Thấp | Tách các tác vụ AI nặng ra khỏi luồng request đồng bộ, chuyển sang mô hình xử lý bất đồng bộ thông qua SNS hoặc hàng đợi sự kiện. Đồng thời tối ưu package và thời gian thực thi của Lambda để giảm nguy cơ timeout. |

#### Best Practices tối ưu chi phí & Hiệu năng

* **Elastic Beanstalk & RDS:** Với cấu hình instance nhỏ như `t3.micro`, cần tối ưu truy vấn MySQL bằng cách thiết kế index hợp lý, hạn chế truy vấn dư thừa như lỗi N+1 và kiểm soát số lượng kết nối từ backend tới RDS để tránh tiêu tốn tài nguyên không cần thiết.
* **Lambda & Bedrock:** Giữ package triển khai gọn nhẹ để giảm thời gian khởi tạo. Các kết nối như HTTP client hoặc database connection nên được khởi tạo ngoài `handler` để tận dụng khả năng tái sử dụng execution context và giảm ảnh hưởng của cold start. Đồng thời nên theo dõi sát chi phí Bedrock thông qua AWS Budgets.
* **DynamoDB:** Nếu DynamoDB chủ yếu được dùng cho OTP hoặc dữ liệu tạm thời, nên bật cơ chế **TTL (Time to Live)** để hệ thống tự động xóa dữ liệu hết hạn, từ đó tiết kiệm dung lượng lưu trữ. Với giai đoạn MVP, chế độ **On-Demand billing** là lựa chọn phù hợp để tối ưu chi phí.
* **S3 & CloudFront:** Nên áp dụng **Lifecycle Policies** trên S3 để tự động chuyển các tệp ít truy cập như log hoặc ảnh bằng chứng sang các lớp lưu trữ chi phí thấp hơn như Glacier. Đồng thời bật cache trên CloudFront để giảm số lượng request truy cập trực tiếp về S3.
* **API Gateway & WAF:** Thiết lập **response caching** trong khoảng 30–60 giây cho các API tra cứu công khai như kiểm tra số điện thoại hoặc domain để giảm tải cho backend. Ngoài ra, cần cấu hình **throttling** và **WAF rate-based rules** nhằm hạn chế bot, spam request và giảm nguy cơ bị khai thác tài nguyên bởi các đợt tấn công DDoS.

## 8. Kết quả kỳ vọng

### Cải tiến kỹ thuật

* **Tự động hóa và phản hồi nhanh:** Hệ thống thay thế phần lớn quy trình tra cứu thủ công bằng cơ chế xử lý tự động, cho phép phát hiện, phân tích và trả kết quả gần như theo thời gian thực.
* **Nâng cao năng lực AI:** Việc tích hợp Amazon Bedrock giúp hệ thống hiểu tốt hơn ngữ cảnh của nội dung nghi ngờ, từ đó vượt xa các phương pháp lọc đơn giản dựa trên từ khóa hoặc rule-based truyền thống.
* **Hạ tầng linh hoạt và ổn định:** Kiến trúc Hybrid Cloud-Native kết hợp giữa Beanstalk và Lambda giúp nền tảng tự động mở rộng khi lưu lượng tăng cao, đồng thời duy trì sự ổn định và hạn chế nghẽn cổ chai.
* **Cải thiện độ chính xác:** Cơ chế đối chiếu dữ liệu từ nhiều nguồn cùng với hệ thống chấm điểm uy tín cộng đồng giúp giảm đáng kể tỷ lệ cảnh báo sai và nâng cao độ tin cậy của kết quả.
  
### Giá trị kinh doanh

* **Tối ưu chi phí vận hành:** Nền tảng có thể được vận hành với mức chi phí thấp trong giai đoạn đầu, tạo lợi thế rõ rệt so với việc phụ thuộc vào các nguồn Threat Intelligence thương mại có giá cao.
* **Bảo vệ người dùng thiết thực:** Hệ thống hỗ trợ giảm thiểu thiệt hại tài chính và rủi ro lộ lọt thông tin cá nhân nhờ các cảnh báo sớm, rõ ràng và dễ hiểu.
* **Tiết kiệm thời gian tra cứu:** Người dùng không cần kiểm tra thủ công qua nhiều nguồn khác nhau mà có thể sử dụng một nền tảng tập trung để tra cứu nhanh và thuận tiện hơn.
* **Hình thành hệ sinh thái dữ liệu bền vững:** Việc khuyến khích người dùng đóng góp báo cáo giúp dữ liệu được cập nhật liên tục, làm giàu hệ thống theo thời gian mà không phụ thuộc hoàn toàn vào chi phí thu thập bên ngoài.

### Tầm nhìn dài hạn

* **Mở rộng thành hệ sinh thái bảo mật số:** Từ web portal ban đầu, hệ thống có thể phát triển thêm sang tiện ích trình duyệt, chatbot AI và các điểm chạm số khác để bảo vệ người dùng toàn diện hơn.
* **Xây dựng kho dữ liệu threat intelligence riêng:** Nền tảng hướng tới việc sở hữu tập dữ liệu nhận diện lừa đảo mang tính đặc thù, cập nhật nhanh và có thể trở thành tài sản chiến lược cho các mô hình hợp tác B2B.
* **Phát triển AI theo hướng dự báo:** Trong tương lai, hệ thống không chỉ dừng ở việc phát hiện rủi ro hiện có mà còn có thể tiến tới dự báo sớm các chiến dịch phishing hoặc lừa đảo mới ngay từ giai đoạn hình thành.

## 9. Kết luận

Hệ thống **AnTiScaQ** với kiến trúc **Hybrid Cloud-Native** mang lại các giá trị nổi bật sau:

* **Chi phí vận hành tối ưu:** Toàn bộ hệ thống có thể được duy trì với mức chi phí thấp, khoảng **27.43 USD/tháng**, phù hợp với giai đoạn MVP và mở rộng dần theo nhu cầu thực tế.
* **Không cần đầu tư hạ tầng ban đầu lớn:** Giải pháp tận dụng tối đa **AWS Free Tier** cùng nguồn lực phát triển nội bộ, giúp giảm đáng kể chi phí khởi tạo và hạn chế áp lực đầu tư ban đầu.
* **Hiệu quả đầu tư cao:** Nền tảng giúp giảm sự phụ thuộc vào các API threat intelligence thương mại đắt đỏ, từ đó tối ưu chi phí dài hạn và nâng cao khả năng chủ động công nghệ.
* **Khả năng mở rộng linh hoạt:** Sự kết hợp giữa **Elastic Beanstalk** và **AWS Lambda** cho phép hệ thống thích ứng tốt với các đợt tăng tải đột biến, đặc biệt trong các tình huống xuất hiện chiến dịch phishing quy mô lớn.
* **Đơn giản hóa vận hành:** Việc tận dụng các dịch vụ managed services và serverless của AWS giúp giảm đáng kể khối lượng công việc quản trị hạ tầng, cho phép nhóm phát triển tập trung nhiều hơn vào nghiệp vụ cốt lõi.
* **Tốc độ triển khai nhanh:** Với lộ trình khoảng **13 tuần**, hệ thống có thể được xây dựng, hoàn thiện, kiểm thử và sẵn sàng bàn giao trong thời gian tương đối ngắn.

Nhìn chung, đây là một hướng tiếp cận khả thi, hiệu quả và có tính ứng dụng cao cho việc xây dựng một nền tảng cảnh báo lừa đảo trực tuyến. Giải pháp không chỉ tận dụng được sức mạnh của AI và dữ liệu cộng đồng, mà còn phù hợp với bài toán triển khai thực tế khi cần tối ưu cả chi phí, hiệu năng và khả năng mở rộng.
