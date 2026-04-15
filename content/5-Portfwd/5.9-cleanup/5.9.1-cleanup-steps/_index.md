---
title: "Clean up resources"
weight: 1
chapter: false
pre: " <b> 4.9.1. </b> "
---

# Clean up resources
To avoid unexpected costs after completing the Workshop, delete resources in the following order:

**1. VPC**: Go to VPC, choose VPC for this application, click **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deletevpc.png)

**2. RDS for MySQL**: Go to RDS, tab Databases, choose database , click **Delete**.
Uncheck **Create final snapshot**, **Retain automated backups**, check **I acknowledge ...**

![Cleanup Session](/AWS_Intern-Report/images/deleterds.png)

![Cleanup Session](/AWS_Intern-Report/images/deleterds1.png)

**3. ECR**: Go to ECR, tab **Repositories**, choose repository that contains docker image of application. Choose **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deleteecr.png)

**4. Elastic Beanstalk**: Go to Elastic Beanstalk, tab **Environments**, choose environment . Then, click **Terminare environment**

![Cleanup Session](/AWS_Intern-Report/images/deleteelb.png)

**5.**DynamoDB**: Choose table -> Delete
![Clean Session](/AWS_Intern-Report/images/delete_dynamo.png)

**6. Bedrock Knowledge Base**: Choose knowledge base -> Delete
![Clean Session](/AWS_Intern-Report/images/deletekb.png)

**6. **S3**: Choose bucket -> Empty bucket -> Delete
![Clean Session](/AWS_Intern-Report/images/delete_s3.png)

**8. Cloudfront**: Go to Cloudfront, choose distribution. Choose **Disable**, then **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deletecloudfront.png)

**9. CloudWatch**: Go to CloudWatch, tab **Alarms**, choose the alarm just set, click **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deletecloudwatch.png)

