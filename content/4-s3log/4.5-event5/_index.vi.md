---
title: "Sự Kiện 5"
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---
# Cloud Mastery 2026 - #3

**Thời gian:** 11 Tháng 4, 2026     
**Địa điểm:** Lô E2a-7, Đường D1, Khu Công nghệ cao, Phường Long Thạnh Mỹ, Thành phố Thủ Đức, TP.HCM

---

### Giới thiệu sự kiện
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/5e9851cf-f26b-438d-a7c8-290b6404ed75" />


Sự kiện "Cloud Mastery 2026 - #3" đã mang đến những kiến thức chuyên sâu về cách xây dựng cơ sở hạ tầng mạng an toàn, bền bỉ và được kiến trúc tốt trên đám mây. Xuyên suốt ba phiên thảo luận, các chuyên gia đã hướng dẫn người tham dự chi tiết cách thiết kế Virtual Private Clouds (VPC), quản lý các thực tiễn tốt nhất của Identity and Access Management (IAM), và triển khai các chiến lược bảo vệ ứng dụng và mạng lưới toàn diện chống lại các mối đe dọa không gian mạng hiện đại.

#### 09:00 AM - 10:00 AM | Networking on AWS (Mạng trên AWS)
**Diễn giả:** Lâm An Thịnh & Nguyễn Phan Quốc Việt

[cite_start]Phiên đầu tiên đã giải quyết các nền tảng cốt lõi của mạng lưới đám mây, minh họa cách cấu trúc và bảo mật luồng lưu lượng trong môi trường AWS[cite: 14].


<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/e52e57f8-c096-4fbd-a0c5-ae3e1853fa61" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/352d1767-a913-485b-92e4-37459c48d9f9" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/28a0338b-1ef5-430d-a908-aefec99adfff" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/492efcda-6d91-447c-be6c-b45dc4d6a0ac" />

**Những điểm chính:**
* [cite_start]**Nền tảng Mạng AWS:** Khám phá các khái niệm nền tảng về VPC, CIDR, Subnets, và tầm quan trọng của việc kiểm soát "Bán kính ảnh hưởng" (Blast Radius)[cite: 15, 16, 29].
* [cite_start]**Định tuyến Lưu lượng:** Trình bày chi tiết vai trò của Internet Gateways (IGW), Route Tables, và Elastic IPs trong việc quản lý lưu lượng vào và ra[cite: 17, 40, 41].
* [cite_start]**NAT Gateway:** Làm nổi bật sự khác biệt giữa Zonal và Regional NAT Gateways, giải thích cách các cơ chế SNAT và PAT cung cấp quyền truy cập internet an toàn, chỉ dành cho chiều đi ra (outbound-only) đối với các subnet riêng tư[cite: 66, 70, 71, 79].
* [cite_start]**Security Groups vs. NACL:** Phân biệt giữa Security Groups (có trạng thái - stateful, cấp độ ENI, các quy tắc chỉ cho phép) và Network ACLs (không trạng thái - stateless, cấp độ subnet, được đánh giá theo thứ tự số với sự hỗ trợ từ chối rõ ràng)[cite: 112, 116, 120, 126, 128, 142].

---

#### 10:00 AM - 11:00 AM | Identity & Access Management (Quản lý Danh tính & Truy cập)
**Diễn giả:** Huỳnh Hoàng Long & Đặng Thị Minh Thư

Phiên thứ hai tập trung vào việc giải quyết các thách thức của kiểm soát truy cập, nhấn mạnh phương pháp tiếp cận zero-trust và quản lý quyền hạn tập trung trong AWS.

<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/188a4990-33e2-4e0b-93e4-3d372b61bfd2" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/6aaab23c-7db5-49c8-8df4-5e140243bb43" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/bfbb0007-179a-4908-bf0a-19607e5976ef" />


**Những điểm chính:**
* [cite_start]**Thực tiễn tốt nhất của IAM:** Nhấn mạnh nguyên tắc đặc quyền tối thiểu, bật MFA cho tất cả người dùng, xóa root access keys, và thay đổi mật khẩu thường xuyên[cite: 351, 352, 359, 360].
* [cite_start]**Single Sign-On (SSO):** Thảo luận về việc sử dụng SSO để tích hợp nhiều tài khoản, cung cấp một lần đăng nhập cho nhiều ứng dụng và quản lý truy cập tập trung[cite: 362, 363, 364].
* [cite_start]**SCPs vs. Permission Boundaries:** Giải thích rằng Service Control Policies (SCPs) hoạt động như các chính sách cấp tổ chức để lọc các quyền hạn tối đa [cite: 370, 372][cite_start], trong khi Permission Boundaries áp dụng các giới hạn cụ thể cho Người dùng/Vai trò (Users/Roles) trong một tài khoản cá nhân[cite: 377].
* [cite_start]**Phổ Danh tính (Credential Spectrum):** Khuyến nghị tránh sử dụng Access Keys dài hạn của IAM User, thay vào đó là sử dụng các thông tin xác thực ngắn hạn do AWS Security Token Service (STS) tạo ra[cite: 380, 381, 383].

---

#### 11:00 AM - 12:00 PM | AWS Network & Application Protection (Bảo vệ Mạng & Ứng dụng AWS)
**Diễn giả:** Lâm Tuấn Kiệt

Phiên cuối cùng đã mang đến một góc nhìn mới về việc che chắn khối lượng công việc khỏi các lỗ hổng và lưu lượng truy cập độc hại bằng cách sử dụng các dịch vụ bảo mật bản địa của AWS.

<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/3b4e2681-6f10-4c31-a72f-bedccb351dc5" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/f49fb917-d87f-4fef-b6c0-3a5d4ed6c1cd" />
<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/df24d53b-56a8-46ec-b2f8-509dc27392b4" />

**Những điểm chính:**
* [cite_start]**AWS WAF (Web Application Firewall):** Bảo vệ các ứng dụng web khỏi các lỗ hổng web phổ biến bằng cách lọc các yêu cầu HTTP/HTTPS, đặc biệt là ngăn chặn các cuộc tấn công như SQL Injection và Cross-Site Scripting (XSS)[cite: 405, 406, 408, 409].
* [cite_start]**AWS Shield:** Cung cấp khả năng bảo vệ được quản lý chống lại các cuộc tấn công DDoS để đảm bảo tính khả dụng cao, cung cấp cả bậc Standard miễn phí và bậc Advanced để tăng cường bảo vệ[cite: 417, 419, 420].
* [cite_start]**AWS Network Firewall:** Triển khai các ranh giới bảo mật trong VPCs, cung cấp cả bộ lọc lưu lượng có trạng thái (stateful) và không trạng thái (stateless) cùng với ngăn chặn xâm nhập[cite: 428, 430, 431].
* [cite_start]**AWS Firewall Manager:** Đóng vai trò là một công cụ quản lý bảo mật tập trung trên các tài khoản AWS, tự động triển khai các quy tắc cho WAF, Shield, và Network Firewall để đảm bảo tính nhất quán của các chính sách nhiều tài khoản[cite: 439, 440, 444].
