---
title: "Thiết lập S3 bucket"
weight: 1
chapter: false
pre: " <b> 4.4.1. </b> "
---

### Tên các Bucket
Bạn sẽ cần tạo 3 bucket sau:
* `rag-data-ACCOUNT_ID-REGION` : Lưu trữ dữ liệu cho mô hình (model)
* `user-report-ACCOUNT_ID-REGION` : Lưu trữ hình ảnh báo cáo của người dùng
* `chatbot-image-ACCOUNT_ID-REGION` : Lưu trữ hình ảnh người dùng gửi cho chatbot

---

### Hướng dẫn chi tiết

**1. Mở Amazon S3 Console**
* Truy cập vào [https://console.aws.amazon.com/s3/](https://console.aws.amazon.com/s3/)
* Hoặc: **AWS Management Console** → **Services** → **S3**

![Networking Session](/AWS_Intern-Report/images/picture5.jpg)

**2. Nhấn nút "Create bucket" (Tạo bucket)**

**3. Cấu hình chung (General configuration):**
* **Bucket name:** Nhập `rag-data-ACCOUNT_ID-REGION`
  * *Ví dụ:* `rag-data-123456789012-us-east-1`
* **AWS Region:** Chọn vùng mục tiêu của bạn (Ví dụ: *US East (N. Virginia) us-east-1*)

![Networking Session](/AWS_Intern-Report/images/picture6.jpg)

**4. Quyền sở hữu đối tượng (Object Ownership):**
* Giữ mặc định: **ACLs disabled (recommended)**

**5. Cài đặt Chặn truy cập công khai (Block Public Access):**
* Tích chọn **"Block all public access"**
* Đảm bảo cả 4 tùy chọn con đều được chọn:
  * ✓ Block public access to buckets and objects granted through *new* access control lists (ACLs)
  * ✓ Block public access to buckets and objects granted through *any* access control lists (ACLs)
  * ✓ Block public access to buckets and objects granted through *new* public bucket or access point policies
  * ✓ Block public and cross-account access to buckets and objects through *any* public bucket or access point policies

**6. Quản lý phiên bản (Bucket Versioning):**
* Chọn **"Enable"** (Bật)

![Networking Session](/AWS_Intern-Report/images/picture7.jpg)

**7. Thẻ - Tags (tùy chọn):**
* Thêm thẻ nếu muốn
* *Ví dụ:* `Key=Purpose`, `Value=IncidentResponse`

**8. Mã hóa mặc định (Default encryption):**
* **Encryption type:** Chọn **"Server-side encryption with Amazon S3 managed keys (SSE-S3)"**
* **Bucket Key:** Giữ mặc định (**Enabled**)

**9. Cài đặt nâng cao (Advanced settings):**
* Giữ tất cả mặc định

**10. Nhấn "Create bucket"**

![Networking Session](/AWS_Intern-Report/images/picture8.jpg)

**11. Xác nhận tạo bucket:**
* Bạn sẽ thấy thông báo thành công
* Bucket sẽ xuất hiện trong danh sách S3 bucket của bạn

> **Lưu ý:** Lặp lại các bước từ 2-11 cho 2 bucket còn lại:
> * `user-report-ACCOUNT_ID-REGION`
> * `chatbot-image-ACCOUNT_ID-REGION`

![Networking Session](/AWS_Intern-Report/images/picture9.jpg)

**12. Tạo Quy tắc Vòng đời (Lifecycle Rule):**
- Chọn bucket `chatbot-image-ACCOUNT_ID-REGION` và vào tab **Management**.
- Nhấn **Create lifecycle rule**.
![Networking Session](/AWS_Intern-Report/images/CreateLifecycleRule.png)


**13. Tên và Phạm vi:**
- Nhập tên quy tắc (Ví dụ: `AutoDeleteAfter1Day`).
- Chọn **Apply to all objects in the bucket** (và xác nhận cảnh báo).
![Networking Session](/AWS_Intern-Report/images/CreateLifecycleRule2.png)

**14. Hết hạn phiên bản hiện tại của đối tượng (Expire current versions of objects)**
- **Days after object creation:** 1 ngày.

**15. Xóa vĩnh viễn các phiên bản cũ của đối tượng (Permanently delete noncurrent versions of objects)**
- **Days after objects become noncurrent:** 1 ngày.

**16. Xóa các dấu đánh dấu xóa hết hạn hoặc các tệp tải lên dở dang (Delete expired object delete markers or incomplete multipart uploads)**
- Chọn **Delete incomplete multipart uploads**.
- **Number of days:** 1 ngày.
![Networking Session](/AWS_Intern-Report/images/CreateLifecycleRule3.png)

**17. Nhấn "Create lifecycle rule" để hoàn tất.**