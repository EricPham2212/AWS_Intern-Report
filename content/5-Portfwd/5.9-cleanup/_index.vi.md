---
title: "Dọn dẹp tài nguyên"
weight: 9
chapter: false
pre: " <b> 4.9. </b> "
---

# Dọn dẹp tài nguyên
Sau khi hoàn tất việc triển khai và kiểm thử hệ thống **AnTiScaQ** (hoặc hoàn thành các bài thực hành trong Workshop), bước quản trị cuối cùng và cực kỳ quan trọng là **dọn dẹp tài nguyên (Resource Cleanup)**. Việc vô tình để các dịch vụ cloud tiếp tục chạy ngầm khi không còn sử dụng sẽ dẫn đến chi phí phát sinh ngoài ý muốn trên AWS.

Trong phần này, chúng ta sẽ thực hiện việc **gỡ bỏ an toàn và dọn dẹp toàn bộ hệ sinh thái hạ tầng AWS** đã cấp phát cho dự án, bao gồm:

- **Tính toán & Ứng dụng (Elastic Beanstalk, ECR):**  
  Chấm dứt hoàn toàn môi trường backend và xóa các repository Docker image của ứng dụng.

- **Lưu trữ & Dữ liệu (RDS, S3):**  
  Xóa vĩnh viễn cơ sở dữ liệu MySQL (không tạo bản sao lưu cuối) và dọn dẹp các bucket lưu trữ tài nguyên frontend/static.

- **Mạng & Phân phối (VPC, CloudFront):**  
  Vô hiệu hóa mạng phân phối nội dung toàn cầu và loại bỏ hạ tầng mạng ảo nội bộ của ứng dụng.

- **Giám sát (CloudWatch):**  
  Dọn dẹp và xóa các luồng cảnh báo tự động đã được thiết lập.