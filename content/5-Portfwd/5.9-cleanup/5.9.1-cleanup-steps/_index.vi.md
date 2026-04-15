---
title: "Các bước dọn dẹp"
weight: 1
chapter: false
pre: " <b> 4.9.1. </b> "
---

# Dọn dẹp tài nguyên
Để tránh phát sinh chi phí ngoài ý muốn sau khi hoàn thành Workshop, hãy xóa các tài nguyên theo thứ tự sau:

**1. VPC**: Đi tới VPC, chọn VPC của ứng dụng này, nhấn **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deletevpc.png)

**2. RDS for MySQL**: Đi tới RDS, tab Databases, chọn database, nhấn **Delete**.
Bỏ chọn **Create final snapshot**, **Retain automated backups**, tích chọn **I acknowledge ...**

![Cleanup Session](/AWS_Intern-Report/images/deleterds.png)

![Cleanup Session](/AWS_Intern-Report/images/deleterds1.png)

**3. ECR**: Đi tới ECR, tab **Repositories**, chọn repository chứa docker image của ứng dụng. Nhấn **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deleteecr.png)

**4. Elastic Beanstalk**: Đi tới Elastic Beanstalk, tab **Environments**, chọn environment. Sau đó, nhấn **Terminate environment**

![Cleanup Session](/AWS_Intern-Report/images/deleteelb.png)

**5. DynamoDB**: Chọn table -> Delete
![Clean Session](/AWS_Intern-Report/images/delete_dynamo.png)

**6. Bedrock Knowledge Base**: Chọn knowledge base -> Delete
![Clean Session](/AWS_Intern-Report/images/deletekb.png)

**7. S3**: Chọn bucket -> Empty bucket -> Delete
![Clean Session](/AWS_Intern-Report/images/delete_s3.png)

**8. Cloudfront**: Đi tới Cloudfront, chọn distribution. Chọn **Disable**, sau đó nhấn **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deletecloudfront.png)

**9. CloudWatch**: Đi tới CloudWatch, tab **Alarms**, chọn alarm vừa thiết lập, nhấn **Delete**

![Cleanup Session](/AWS_Intern-Report/images/deletecloudwatch.png)