---
title: "Ngày 3"
date: 2026-05-25
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

# Nhật Ký Làm Việc: Khởi Tạo Cơ Sở Dữ Liệu RDS Postgres, Tự Động Hóa Biến Đổi Dữ Liệu Với AWS Glue Và Lập Lịch Cron Job Bằng EventBridge

> **Ngày 3 - Thứ Hai, ngày 25/05/2026:** Tập trung xây dựng lớp lưu trữ dữ liệu có cấu trúc bằng Amazon RDS Postgres, thiết kế đường ống trích xuất và biến đổi dữ liệu (ETL) tự động thông qua AWS Glue, và thiết lập cơ chế kích hoạt theo lịch trình thời gian sử dụng Amazon EventBridge.

---

### Mục tiêu học tập trong ngày

- Khởi tạo và cấu hình một cơ sở dữ liệu quan hệ **Amazon RDS PostgreSQL** bảo mật và tối ưu cho ứng dụng.
- Xây dựng quy trình **ETL (Extract, Transform, Load)** với **AWS Glue** để tự động thu thập và biến đổi dữ liệu thô từ S3 trước khi nạp vào database.
- Tự động hóa lịch trình thực thi toàn bộ hệ thống bằng các quy tắc **Amazon EventBridge (thay thế CloudWatch Events)**.
- Kiểm tra tính toàn vẹn của dữ liệu sau biến đổi và phân quyền IAM an toàn giữa các dịch vụ.

---

### Quản Trị Cơ Sở Dữ Liệu Với Amazon RDS PostgreSQL

#### 1. Khởi tạo và Phân nhóm mạng (Subnet Group)
- Khởi chạy một database instance **Amazon RDS PostgreSQL** bản stable, cấu hình lớp lưu trữ `db.t3.micro` thuộc diện Free Tier để thử nghiệm.
- Tạo một **DB Subnet Group** chuyên biệt gom nhóm các Private Subnet trong VPC, đảm bảo cơ sở dữ liệu hoàn toàn cô lập khỏi Internet.
- Thiết lập cơ chế **Auto Minor Version Upgrade** để hệ thống tự động vá các lỗi bảo mật nhỏ của PostgreSQL.

#### 2. Cấu hình bảo mật nâng cao
- Thiết lập **Security Group cho RDS**: Chỉ cho phép các kết nối inbound ở cổng tiêu chuẩn `5432` đi đến từ Security Group của nhóm máy chủ EC2 (từ Ngày 2) và môi trường AWS Glue.
- Kích hoạt tính năng **Storage Encryption** (Mã hóa dữ liệu khi lưu trữ) sử dụng khóa KMS mặc định của AWS.

---

### Trích Xuất Và Biến Đổi Dữ Liệu Tự Động Với AWS Glue

#### 1. Khám phá dữ liệu với Glue Crawler & Data Catalog
- Khởi tạo một **AWS Glue Crawler** để tự động quét qua thư mục dữ liệu thô `/raw-data/` trên S3 Bucket (từ Ngày 1).
- Crawler tự động phân tích cấu trúc tệp dữ liệu (JSON/CSV) và ánh xạ schema vào một bảng dữ liệu logic nằm trong **AWS Glue Data Catalog**.

#### 2. Thiết kế Glue ETL Job (Python/Spark)
- Xây dựng một **Glue ETL Job** (sử dụng mã nguồn Python/PySpark) thực hiện các tác vụ xử lý dữ liệu nâng cao:
  - Loại bỏ các bản ghi trùng lặp (Drop Duplicates) và xử lý các giá trị bị khuyết (Null values).
  - Chuẩn hóa định dạng ngày tháng và chuyển đổi kiểu dữ liệu của các đặc trưng (Features) để phù hợp với mô hình ML.
- Đầu ra của Glue Job cấu hình kết nối JDBC (Java Database Connectivity) để ghi trực tiếp các bản ghi đã làm sạch vào các bảng (Tables) bên trong cơ sở dữ liệu **RDS Postgres**.

---

### Tự Động Hóa Lịch Trình Thực Thi Bằng Amazon EventBridge

#### 1. Cấu hình EventBridge Rule (Schedule)
- Thay vì chạy các tác vụ ETL thủ công, tôi thiết lập một **EventBridge Rule** hoạt động theo dạng **Schedule** (Lịch trình) để biến hệ thống thành một đường ống dữ liệu tự động hoàn toàn.
- Sử dụng biểu thức **Cron Expression** (`cron(0 1 * * ? *)`) để lên lịch kích hoạt hệ thống đều đặn vào lúc 01:00 AM mỗi ngày khi lượng tải hệ thống thấp.

#### 2. Điều phối mục tiêu (Target Mapping)
- Cấu hình Target của EventBridge Rule trỏ trực tiếp đến AWS Glue Job vừa khởi tạo ở bước trước.
- Thiết lập **Retry Policy** (Chính sách thử lại) tối đa 3 lần và cấu hình Dead-Letter Queue (DLQ) qua SQS để lưu giữ các sự kiện bị lỗi nếu Glue Job không thể kích hoạt thành công.

---

### Các Lệnh Vận Hành Và Giám Sát Qua AWS CLI

Dưới đây là các lệnh CLI hỗ trợ việc kiểm tra trạng thái của cơ sở dữ liệu, kích hoạt đường ống dữ liệu và giám sát lịch trình:

```bash
# 1. Kiểm tra trạng thái hoạt động và Endpoint kết nối của cơ sở dữ liệu RDS Postgres
aws rds describe-db-instances \
  --db-instance-identifier my-postgres-db \
  --query 'DBInstances[].{Status:DBInstanceStatus,Endpoint:Endpoint.Address,Port:Endpoint.Port}'

# 2. Kích hoạt thủ công một AWS Glue Crawler để quét dữ liệu mới trên S3
aws glue start-crawler --name my-s3-raw-data-crawler

# 3. Kích hoạt trực tiếp một Glue ETL Job từ Terminal và kiểm tra mã thực thi
aws glue start-job-run --job-name my-data-transform-job

# 4. Kiểm tra trạng thái hoạt động (Bật/Tắt) của quy tắc lập lịch EventBridge
aws events describe-rule --name daily-etl-schedule-rule \
  --query '{Name:Name,State:State,Schedule:ScheduleExpression}'

```

---

### Nội Dung Học Tập Đã Hoàn Thành

| Ngày học | Nội dung bài học tập trung | Dịch vụ AWS liên quan |
| --- | --- | --- |
| **25/05/2026** | Quản trị cơ sở dữ liệu quan hệ bảo mật và cô lập mạng | Amazon RDS PostgreSQL, KMS |
| **25/05/2026** | Khám phá dữ liệu tự động và xây dựng đường ống ETL | AWS Glue (Crawler, Data Catalog, Job) |
| **25/05/2026** | Lập lịch Cron Job và điều phối sự kiện serverless | Amazon EventBridge |

---

### Bài học rút ra từ Ngày 3

1. **Nguyên tắc cô lập cơ sở dữ liệu:** Tuyệt đối không để cơ sở dữ liệu RDS tiếp xúc trực tiếp với Internet công cộng (`Publicly Accessible = No`). Chỉ cho phép truy cập thông qua Security Group nội bộ từ EC2 hoặc Glue giúp thu hẹp tối đa bề mặt tấn công mạng.
2. **Sức mạnh của Meta-data:** AWS Glue Data Catalog đóng vai trò cực kỳ quan trọng như một cuốn từ điển dữ liệu trung tâm. Nó giúp lập chỉ mục cấu hình dữ liệu trên S3 mà không cần di chuyển dữ liệu thật, giúp các tác vụ phân tích và huấn luyện ML sau này trở nên rõ ràng và có cấu trúc.
3. **Chuyển đổi sang Serverless Event-driven:** Việc thay thế các tập lệnh cron-job truyền thống chạy trên máy chủ bằng EventBridge giúp hệ thống loại bỏ hoàn toàn chi phí duy trì máy chủ bật 24/7. Toàn bộ hạ tầng kích hoạt và biến đổi dữ liệu (Glue + EventBridge) chỉ tính phí trên từng giây thực thi, tối ưu hóa triệt để chi phí vận hành (OpEx).

---

*Nguồn tài liệu chính: [First Cloud Journey - AWS Study Group*](https://cloudjourney.awsstudygroup.com/)