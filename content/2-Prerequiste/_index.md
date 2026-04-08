---
title : "Proposal"
date: 2026-01-10
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

## 1. Executive Summary
**AnTiScaQ** is an online scam risk detection and warning system built to help users identify suspicious signs at an early stage. The system analyzes multiple types of input data such as **phone numbers, domains, and email content** to assess credibility and issue warnings based on risk levels. Rather than making legal conclusions, AnTiScaQ focuses on warning users, explaining suspicious indicators, and guiding them on how to avoid scams. The system operates based on data collection, community-submitted reports, and a risk-scoring mechanism.

## 2. Problem Statement

### Current Issues
* Online scams are increasing rapidly and becoming more sophisticated, causing major losses for users and businesses.
* The lack of a reliable system makes users more likely to make incorrect decisions.
* Users often have to manually search through browser platforms (Google, Microsoft Edge, ...) or use fragmented databases to verify suspicious phone numbers/links, which is time-consuming and risky.
* Existing tools often lack **content context analysis**.
  * Insufficient data from the **user community**.
  * No **clear explanation of risk levels**.
* The cost of purchasing APIs from enterprise Threat Intelligence platforms (such as Recorded Future, VirusTotal) is too high.
* Reports are often incomplete and **not real-time** when new phishing campaigns emerge.

## Proposed Solution
* **Automated risk detection:** Multi-source analysis (phone numbers, domains, URLs, email content) combined with rule-based methods and AI to detect scam indicators early.

* **AI-powered context analysis:** Use Amazon Bedrock to “understand” content and provide clear explanations of risk levels, helping users make informed decisions more easily.

* **Leveraging community power:** Build a reporting and reputation scoring system based on user contributions, ensuring that data remains continuously updated and reflects real-world conditions.

* **Cost optimization & Scalability:** Apply a Hybrid architecture:
  * Elastic Beanstalk (Docker) for the main backend
  * Lambda for AI & flexible processing → Reducing costs compared to traditional enterprise systems.

* **AWS ecosystem integration:** Use Cognito, RDS, DynamoDB, S3, CloudFront, WAF... to ensure security, performance, and automatic scalability.

* **Simple user experience:** Provide a single platform to replace manual searching, enabling faster and more accurate verification.
  
#### Benefits

* Detect scam risks early from multiple types of input data such as phone numbers, domains, and digital content.
* Provide clear, easy-to-understand risk warnings and support users in making safer decisions.
* Save time by automating the verification and information cross-checking process.
* Improve accuracy by combining system data with community-submitted reports.
* Enhance user safety while browsing the web and interacting with online information sources.
* Help improve awareness, self-protection skills, and digital scam prevention.
* Strengthen security through continuous monitoring and timely alerts.
  
## 3. Solution Architecture

This is the cloud architecture diagram of the system:
<img width="2448" height="1831" alt="aws_architecture drawio" src="https://github.com/user-attachments/assets/d8645511-e074-4cbb-b41f-21e613173038" />

**AWS Services Used**

#### AWS Services Used

| AWS Services | Main Functions |
|---|---|
| AWS Elastic Beanstalk | Deploy and manage the backend application (Spring Boot) as a Docker container. |
| Amazon RDS for MySQL | Relational database for storing structured data (user, report, domain, history, ...). |
| AWS Lambda | Handle serverless tasks (AI chatbot, content analysis, asynchronous processing). |
| Amazon API Gateway | Manage and expose APIs, handle request routing, validation, and endpoint security. |
| Amazon DynamoDB | NoSQL database for temporary/real-time data storage (OTP). |
| AWS Cognito | User authentication and authorization (Authentication & Authorization, supports Google SSO). |
| Amazon S3 | Store files (images, documents, static assets). |
| Amazon CloudFront | CDN for content delivery (frontend, files from S3), reducing latency and increasing page load speed. |
| Amazon Route 53 | Manage DNS and map domains to the system. |
| AWS WAF | Protect APIs from attacks (rate limiting, anti-bot, anti-abuse). |
| Amazon CloudWatch | Monitor the system, store logs, metrics, and send alerts. |
| Amazon SNS | Send notifications (email, SMS) to the system and users. |
| Amazon Bedrock | Provide AI/LLM capabilities for the chatbot and scam content analysis. |
| AWS Secrets Manager | Securely manage sensitive information (API keys, credentials). |
| AWS CodePipeline | Automate the CI/CD pipeline (build → test → deploy). |
| AWS CodeBuild | Service responsible for building and testing code in the CI/CD pipeline. |


## Component Design

**1. Data Collection & Detection Layer**

* **Data sources:** The system receives data from multiple sources, including user-provided information (phone numbers, domains, email content), community-contributed data (reports, feedback), and external services/APIs such as WHOIS or domain lookup sources.
* **Data ingestion:** The backend deployed on Spring Boot and AWS Elastic Beanstalk is responsible for receiving, standardizing, and pre-processing input data, while also triggering analysis workflows whenever new data is generated.

**2. Event Processing Layer**

* **Routing & request handling:** Amazon API Gateway receives requests from the client side, then forwards them to the backend for validation, business logic processing, and request classification.
* **Asynchronous processing:** Tasks that require background execution such as AI analysis, content inspection, or asynchronous processing are offloaded to AWS Lambda. The event-driven mechanism can be integrated with SNS or internal services to optimize the processing flow.

**3. Orchestration & Business Logic Layer**

* **Central orchestration:** The backend acts as the main orchestrator, controlling the entire workflow from input reception and data analysis to result aggregation and response delivery to users.
* **Business processing:** The system aggregates data from multiple sources such as RDS, DynamoDB, and external APIs; then invokes AI services to analyze content, detect suspicious behavior, calculate risk scores, and determine warning levels.

**4. Data Processing & Storage Layer**

* **Data storage:** Amazon RDS for MySQL is used for core relational data such as users, reports, lookup history, and domains; DynamoDB serves data requiring fast access or real-time characteristics; Amazon S3 is used to store files, images, and related documents.
* **Data processing support:** AWS Lambda handles lightweight ETL tasks, data pre-processing, and preparation of input data for AI models or subsequent analysis steps.

**5. AI & Analysis Layer**

* **AI capabilities:** Amazon Bedrock is used to provide intelligent analysis for emails, phone numbers, domains, and suspicious content, while also supporting explanation of warning reasons and operating a scam-prevention advisory chatbot.
* **Secure AI integration:** AWS Lambda acts as an intermediary when interacting with Bedrock, helping control access, process returned results, and ensure that the AI integration flow remains secure and flexible.

**6. Presentation & User Interaction Layer**

* **User interface:** The frontend is built with React and can be deployed via S3 combined with CloudFront to optimize content delivery. The application communicates with the backend through API Gateway under an appropriate security mechanism.
* **Access management:** User authentication and session management are handled through AWS Cognito, supporting JWT and modern identity management mechanisms.

**7. Security & Monitoring Layer**

* **Security & access control:** The system applies AWS Cognito for authentication, combined with AWS WAF, IAM, ACM (SSL/TLS), and Route 53 to strengthen security, manage authorization, and ensure safe network infrastructure.
* **Operational monitoring:** Amazon CloudWatch is used to monitor logs, metrics, and system status; SNS supports alert delivery when incidents occur; meanwhile, AWS Secrets Manager stores and protects sensitive information such as credentials and API keys.

## 4. Technical Implementation Roadmap

**Step 1: Build infrastructure and configure the platform**

* **Networking and security:** Set up AWS network architecture with VPC, separating Public Subnets for public-facing components such as Load Balancer/Internet and Private Subnets for databases. At the same time, configure Internet Gateway, Security Groups, and appropriate access policies to ensure that only necessary services are allowed to connect.
* **Deploy the core backend:** Deploy the Spring Boot backend application to AWS Elastic Beanstalk as a Docker container. Set up Amazon RDS (MySQL) for primary data, DynamoDB for fast-access data such as OTP, and Amazon S3 for storing files, images, or attached documents.
* **Initialize foundational services:** Configure AWS Cognito for user authentication and Google SSO support. At the same time, build the initial platform APIs such as authentication, threat/report data management, and APIs serving the admin dashboard.

**Step 2: Develop public APIs and the Web Portal MVP**

* **Public Lookup API:** Build public lookup APIs for phone numbers, domains, and suspicious content to support quick verification needs from users.
* **Deploy the web interface:** Develop the frontend with React.js and deploy it through Amazon S3 combined with CloudFront to accelerate content delivery.
* **Complete foundational features:** Build the basic scam reporting workflow, the initial statistics dashboard, and configure Route 53 to connect the domain to the system.

**Step 3: Complete data processing and core business logic**

* **Build the processing engine:** Integrate lookup services such as WHOIS/external APIs for domain verification, while also building a risk-scoring mechanism based on rules (rule-based), community data, and content analysis signals.
* **Integrate AI and asynchronous processing:** Use AWS Lambda combined with Amazon Bedrock to process email analysis, suspicious content, advisory chatbot functions, and background tasks following an async model.
  
**Step 4: Expand features and upgrade the frontend**

* **Improve UI/UX:** Refine the user interface with a more detailed dashboard, lookup history, and a more intuitive experience for verification workflows.
* **Expand integration channels:** Develop and integrate a browser extension to support real-time warnings for suspicious websites directly in the browser.
* **Optimize the overall experience:** Fine-tune API performance, reduce response time, and improve the interaction flow between frontend and backend.

**Step 5: Testing, security, and operational optimization**

* **System testing:** Perform all layers of testing including unit test, integration test, and load test to ensure stability before scaling to more users.
* **Strengthen security:** Apply AWS WAF to limit attacks and API abuse, configure IAM Roles following the principle of least privilege, and deploy AWS ACM for SSL/TLS certificate management.
* **Optimize performance and cost:** Enable Auto Scaling for Elastic Beanstalk, optimize caching via CloudFront, and improve query performance on RDS so the system can operate stably at a reasonable cost.

#### Technical Requirements

| Components | Description |
|---|---|
| Frontend & Dashboard | The user interface is built with Next.js, stored as static assets on Amazon S3, and distributed through Amazon CloudFront to optimize global access speed. |
| Backend & Logic Processing | The core logic is developed in Python 3.12, deployed on AWS Lambda, and accessed through Amazon API Gateway to handle requests in a serverless model. |
| Data & Storage | The system uses Amazon DynamoDB for high-speed query tasks, combined with Amazon S3 to securely store files, documents, and related evidence. |
| Infrastructure (IaC) | The entire AWS infrastructure is defined, deployed, and managed automatically as code through AWS Cloud Development Kit (CDK), helping standardize and simplify scaling. |
| Security & Monitoring | The platform applies AWS Cognito for authentication, IAM for authorization management, and Amazon CloudWatch to monitor activity, record logs, and continuously observe the system. |
| CI/CD | Continuous integration and deployment are implemented through AWS CodePipeline, combined with AWS CodeBuild to automatically build and test source code. |

## 5. Roadmap & Deployment Milestones

| Week | Phase | Main Activities | Deliverables |
|---|---|---|---|
| 1-2 | Platform Setup (MVP Core) | Establish the core AWS infrastructure including VPC, Subnet, Security Group; deploy the backend on Elastic Beanstalk combined with RDS; configure Cognito and build the initial core APIs. | Complete authentication functions, Threat API, Report API, and successfully deploy the backend to the cloud environment. |
| 3-4 | API Development & Automation | Build lookup APIs for phone numbers, domains, and URLs; integrate WHOIS; configure the notification system via SNS; set up the CI/CD pipeline. | Stable lookup APIs, a ready Web Portal MVP, and an operational CI/CD pipeline. |
| 5-6 | AI Integration & Advanced Analysis | Connect AWS Lambda with Amazon Bedrock to process content analysis, AI-based risk scoring, and asynchronous processing workflows. | Complete the AI chatbot, content analysis module, and advanced risk scoring mechanism. |
| 7-8 | Dashboard & Extended Integration | Develop the admin dashboard, add statistics APIs, refine the frontend interface, and integrate additional supporting extensions. | A complete management dashboard, improved user interface, and a system ready for use. |
| 9-10 | System Performance Optimization | Optimize operations through Auto Scaling, CloudFront caching, improved database queries, and enhanced API performance. | A more stable system with improved processing speed and overall performance. |
| 11 | Security Hardening | Configure AWS WAF, IAM, SSL/TLS via ACM, enable logging and monitoring with CloudWatch, and review system security configurations. | Complete the security and monitoring layer for the entire platform. |
| 12 | Comprehensive Testing | Perform unit test, integration test, load test, end-to-end testing, and resolve issues identified during evaluation. | A complete testing report and a stable system before the handover stage. |
| 13 | Final Handover | Standardize technical documentation such as API docs, architecture documentation, system demo guides, and organize the GitHub repository. | A complete documentation package, an operational demo, and a project ready for handover. |

## 6. Budget Estimate

**Monthly AWS Cost (Phase 1: ~5,000 API lookups/day)**
*Serverless Architecture - Cost Optimized*

| Services | Configuration | Cost/month |
| :--- | :--- | :--- |
| **AWS Lambda** | 15K invocations, 512MB, 4000ms avg | $0 *(Free tier)* |
↳ Free tier: 1M requests + 400K GB-seconds/month
| **Amazon API Gateway** | 15K REST API requests | $0 |
| **Amazon DynamoDB** | On-demand, 5GB storage, 1M reads, 0.5M write | $0.5 |
| **Amazon S3 Vectors** | 2GB data, PUT/GET | $0.60 |
| **Amazon Bedrock** | Model: Claude Haiku 3, Input Token: 6GB, Output Token: 4GB | $6.5 |
| **Amazon CloudFront** | 10GB transfer, 200K requests | $1.00 |
| **Amazon Route 53** | 1 hosted zone | $0.90 |
| **Amazon CloudWatch**| Basic logs and auth | $0 *(Free tier)* |
| **AWS Secrets Manager**| Proxy key management | $0.4 |
| **AWS Elastic Beanstalk** | t3.micro | $11.68 |
| **Amazon Cognito** | 1000 MAU | $0 |
↳ Free tier: < 50K MAU
| **Amazon RDS for MySQL** | instance db.t4g.micro, gp3 | $21.01 |
| | **TOTAL AWS/MONTH** | **~$42.59** |


## 7. Risk Assessment & Mitigation Measures

| Risks | Impact | Mitigation |
|---|---|---|
| Backend overload and RDS saturation during sudden traffic spikes | High | Configure Auto Scaling for Elastic Beanstalk based on metrics such as CPU, memory, or network. At the same time, use connection pooling for the Spring Boot backend to control the number of connections to RDS and reduce the risk of system bottlenecks. |
| Amazon Bedrock costs rise sharply due to high AI request frequency | High | Apply rate limiting at API Gateway or AWS WAF to control traffic. Limit the model’s output token count and leverage caching for repeated analysis results to reduce unnecessary AI calls. |
| False positives from community-submitted reports | High | Build a trust-scoring mechanism for users who submit reports, while also requiring cross-validation from multiple sources such as WHOIS, a rule-based engine, or internal data before issuing official warnings. |
| Scraper or WHOIS API blocked by IP / request rate limits | Medium | Use a rotating proxy pool and store related sensitive information securely in AWS Secrets Manager. Combine this with a retry strategy using exponential backoff to handle temporary failures from external APIs. |
| Lambda timeout when handling long-running AI or async tasks | Low | Separate heavy AI tasks from the synchronous request flow and move them to an asynchronous processing model through SNS or an event queue. At the same time, optimize Lambda packaging and execution time to reduce timeout risk. |

#### Best Practices for Cost & Performance Optimization

* **Elastic Beanstalk & RDS:** With small instance configurations such as `t3.micro`, MySQL queries should be optimized by designing proper indexes, limiting redundant queries such as the N+1 problem, and controlling the number of backend-to-RDS connections to avoid unnecessary resource consumption.
* **Lambda & Bedrock:** Keep the deployment package lightweight to reduce startup time. Connections such as HTTP clients or database connections should be initialized outside the `handler` to take advantage of execution context reuse and reduce cold start impact. Bedrock costs should also be closely monitored through AWS Budgets.
* **DynamoDB:** If DynamoDB is mainly used for OTP or temporary data, the **TTL (Time to Live)** mechanism should be enabled so the system can automatically delete expired data, thereby saving storage capacity. For the MVP stage, **On-Demand billing** is an appropriate choice for cost optimization.
* **S3 & CloudFront:** **Lifecycle Policies** should be applied on S3 to automatically move less frequently accessed files such as logs or evidence images to lower-cost storage classes such as Glacier. At the same time, caching should be enabled on CloudFront to reduce the number of direct requests to S3.
* **API Gateway & WAF:** Configure **response caching** for 30–60 seconds for public lookup APIs such as phone number or domain checks to reduce backend load. In addition, **throttling** and **WAF rate-based rules** should be configured to limit bots, spam requests, and reduce the risk of resource exhaustion from DDoS attacks.

## 8. Expected Outcomes

### Technical Improvements

* **Automation and fast response:** The system replaces most manual lookup processes with an automated mechanism, allowing detection, analysis, and result delivery in near real time.
* **Enhanced AI capability:** Integrating Amazon Bedrock enables the system to better understand the context of suspicious content, significantly outperforming simple keyword-based or traditional rule-based filtering methods.
* **Flexible and stable infrastructure:** The Hybrid Cloud-Native architecture combining Beanstalk and Lambda allows the platform to scale automatically during traffic surges while maintaining stability and reducing bottlenecks.
* **Improved accuracy:** Cross-referencing data from multiple sources together with a community reputation scoring system helps significantly reduce false positives and improve result reliability.
  
### Business Value

* **Optimized operating cost:** The platform can be operated at low cost in the early stage, creating a clear advantage compared to relying on expensive commercial Threat Intelligence sources.
* **Practical user protection:** The system helps reduce financial loss and personal data exposure risks through early, clear, and easy-to-understand warnings.
* **Time-saving verification:** Users no longer need to manually check across multiple sources and can instead use a centralized platform for faster and more convenient verification.
* **Building a sustainable data ecosystem:** Encouraging users to submit reports helps keep data continuously updated and enriches the system over time without relying entirely on external collection costs.

### Long-term Vision

* **Expand into a digital security ecosystem:** From the initial web portal, the system can further expand into browser extensions, AI chatbots, and other digital touchpoints to protect users more comprehensively.
* **Build a proprietary threat intelligence dataset:** The platform aims to own a specialized scam detection dataset, updated quickly, that can become a strategic asset for B2B collaboration models.
* **Develop AI toward prediction:** In the future, the system will not only stop at detecting existing risks but can also evolve to predict phishing or scam campaigns at an early formation stage.

## 9. Conclusion

The **AnTiScaQ** system with a **Hybrid Cloud-Native** architecture delivers the following outstanding values:

* **Optimized operating cost:** The entire system can be maintained at a low cost, around **27.43 USD/month**, suitable for the MVP stage and scalable according to real demand.
* **No major upfront infrastructure investment required:** The solution makes maximum use of **AWS Free Tier** and internal development resources, significantly reducing startup costs and easing initial investment pressure.
* **High return on investment:** The platform helps reduce dependence on expensive commercial threat intelligence APIs, thereby optimizing long-term costs and improving technology autonomy.
* **Flexible scalability:** The combination of **Elastic Beanstalk** and **AWS Lambda** enables the system to adapt well to sudden traffic surges, especially in situations involving large-scale phishing campaigns.
* **Simplified operations:** Leveraging AWS managed services and serverless services significantly reduces infrastructure administration workload, allowing the development team to focus more on core business functions.
* **Fast deployment speed:** With a roadmap of approximately **13 weeks**, the system can be built, completed, tested, and ready for handover within a relatively short time.

Overall, this is a feasible, effective, and highly applicable approach for building an online scam warning platform. The solution not only leverages the power of AI and community data, but also fits practical deployment requirements where cost, performance, and scalability must all be optimized.
