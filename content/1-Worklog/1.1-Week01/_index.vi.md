---
title: "Tuần 1"
date: 2026-05-15
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

# Nhật Ký Làm Việc: Xây Dựng & Huấn Luyện Mô Hình Với SageMaker, Lưu Trữ Dữ Liệu Trên S3 Và Triển Khai API Trên EC2

> **Tuần 1 - Thứ Sáu, ngày 15/05/2026:** Tập trung cấu hình môi trường xây dựng và huấn luyện mô hình máy học bằng Amazon SageMaker, quản lý tập dữ liệu cùng artifact qua Amazon S3, và triển khai mô hình hoàn chỉnh thành một API production trên máy chủ Amazon EC2.

---

### Mục tiêu học tập trong tuần

- Khởi tạo và cấu hình **Amazon SageMaker** notebook instance để xây dựng, huấn luyện và đánh giá mô hình học máy.
- Sử dụng **Amazon S3** như một giải pháp lưu trữ bảo mật, độ bền vững cao cho các tập dữ liệu thô và các artifact (trọng số) của mô hình.
- Triển khai mô hình đã huấn luyện thành một **API endpoint trên Amazon EC2** bằng cách sử dụng một framework web mã nguồn mở (FastAPI/Flask).
- Thiết lập quyền truy cập tài nguyên (IAM) và cấu hình mạng để đảm bảo sự tích hợp an toàn, liền mạch giữa SageMaker, S3 và EC2.

---

### Quy Trình Làm Việc Với Máy Học Trên Amazon SageMaker

#### 1. Thiết lập môi trường và Notebook
- Khởi tạo một SageMaker Notebook Instance (sử dụng dòng `ml.t3.medium`) đóng vai trò làm môi trường phát triển thử nghiệm tập trung.
- Gắn IAM Execution Role với các quyền hạn cụ thể (`AmazonSageMakerFullAccess`), cho phép dịch vụ SageMaker tự động đọc dữ liệu huấn luyện từ S3 và ghi ngược kết quả lại S3.

#### 2. Đường ống xây dựng & Huấn luyện mô hình (Training Pipeline)
- Viết các đoạn mã tiền xử lý dữ liệu, làm sạch và chuẩn hóa các đặc trưng (features) trước khi đưa vào huấn luyện.
- Sử dụng các thuật toán tích hợp sẵn của SageMaker (hoặc custom Docker container) để thực thi tiến trình huấn luyện (Training Job).
- Giám sát các chỉ số hiệu năng (loss, accuracy) theo thời gian thực thông qua hệ thống Log của SageMaker được tích hợp trực tiếp với Amazon CloudWatch.
- Đóng gói file mô hình đã tối ưu dưới dạng nén (`model.tar.gz`) và tự động đẩy về bucket S3 được chỉ định sẵn sau khi hoàn tất.

---

### Quản Lý Vòng Đời Dữ Liệu & Artifact Trên Amazon S3

#### 1. Cấu trúc Bucket và Phân lớp lưu trữ
Để hỗ trợ toàn diện cho vòng đời phát triển dự án AI/ML, tôi cấu hình cấu trúc thư mục (Prefix) trong S3 Bucket một cách khoa học:

| Đường dẫn / Thư mục | Loại dữ liệu lưu trữ | Lớp lưu trữ (Storage Class) | Ý nghĩa và mục đích |
|---|---|---|---|
| `/raw-data/` | Tập dữ liệu gốc | S3 Standard | Độ trễ thấp, phục vụ truy cập đọc/ghi liên tục khi khám phá dữ liệu. |
| `/processed-data/` | Dữ liệu đã xử lý | S3 Standard | Dữ liệu sạch đã sẵn sàng để nạp vào các tiến trình huấn luyện. |
| `/model-artifacts/` | File `model.tar.gz` | S3 Standard | Thư mục chứa các tệp trọng số mô hình sau khi train xong. |

#### 2. Kiểm soát an toàn và Độ bền vững dữ liệu
- Tận dụng cam kết độ bền vững dữ liệu lên đến **99.999999999% (11 số 9)** của Amazon S3 để đảm bảo các tệp mô hình quan trọng không bị thất lạc hoặc hư hỏng.
- Áp dụng chính sách **S3 Bucket Policy** nghiêm ngặt, chỉ cho phép duy ứng dụng SageMaker (khi train) và máy chủ EC2 (khi deploy) quyền truy xuất dữ liệu.

---

### Triển Khai API Mô Hình Trên Máy Chủ Amazon EC2

#### 1. Khởi tạo và cấu hình máy chủ EC2
- Khởi chạy một phiên bản máy chủ ảo Amazon EC2 (`t3.medium` hoặc `c6i.large` tùy thuộc vào kích thước cấu trúc của mô hình) chạy hệ điều hành Amazon Linux 2023.
- Cấu hình nhóm bảo mật **Security Group** để mở cổng nhận các traffic web tiêu chuẩn (`80`, `443`) và cổng chạy ứng dụng API tùy chỉnh (`8000`).

#### 2. Quy trình thiết lập và chạy dịch vụ API
- Đồng bộ mã nguồn triển khai (Deployment code) lên EC2, cài đặt môi trường ảo Python (Virtual Environment) và các thư viện phụ thuộc (`boto3`, `torch`/`scikit-learn`, `uvicorn`).
- Sử dụng thư viện `boto3` để viết mã tự động tải tệp `model.tar.gz` mới nhất từ S3 Bucket về máy chủ cục bộ ngay khi ứng dụng API khởi động.
- Sử dụng một bộ quản lý tiến trình production (`systemd` hoặc `pm2`) kết hợp cùng `Nginx` làm Reverse Proxy để phân phối dịch vụ API dự đoán (Prediction Endpoint) ra bên ngoài.

---

### Các Lệnh Tra Cứu Và Vận Hành Qua AWS CLI

Trong suốt quá trình thiết lập hạ tầng huấn luyện và triển khai API, các lệnh AWS CLI dưới đây được áp dụng thường xuyên nhằm kiểm tra trạng thái và xác thực tài nguyên:

```bash
# 1. Liệt kê các SageMaker notebook instance đang hoạt động kèm trạng thái
aws sagemaker list-notebook-instances \
  --query 'NotebookInstances[].{Name:NotebookInstanceName,Status:NotebookInstanceStatus,Type:InstanceType}' \
  --output table

# 2. Đồng bộ hóa thư mục dữ liệu đã xử lý từ local lên S3 bucket
aws s3 sync ./processed-data/ s3://my-ml-model-bucket-2026/processed-data/

# 3. Kiểm tra xem file artifact của mô hình đã được tải lên S3 thành công chưa
aws s3 ls s3://my-ml-model-bucket-2026/model-artifacts/

# 4. Xác thực trạng thái và IP công khai của máy chủ EC2 đang host API
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running" \
  --query 'Reservations[].Instances[].{ID:InstanceId,Type:InstanceType,IP:PublicIpAddress}' \
  --output table

```

---

### Nội Dung Học Tập Đã Hoàn Thành

| Ngày học | Nội dung bài học tập trung | Dịch vụ AWS liên quan |
| --- | --- | --- |
| **15/05/2026** | Xây dựng và Huấn luyện Mô hình Máy học | Amazon SageMaker, CloudWatch Logs |
| **15/05/2026** | Lưu trữ Tập dữ liệu và Trọng số Mô hình | Amazon S3, S3 Bucket Policies |
| **15/05/2026** | Triển khai và Phục vụ API Production | Amazon EC2, VPC Security Groups |

---

### Bài học rút ra từ Tuần 1

1. **Kiến trúc phân tách (Decoupled Architecture):** Tách biệt rõ ràng tầng tính toán hiệu năng cao (SageMaker dùng để train, EC2 dùng làm API inference) khỏi tầng lưu trữ dữ liệu (S3) giúp hệ thống linh hoạt, dễ mở rộng và tối ưu hóa chi phí vận hành.
2. **Quản trị phân quyền liền mạch:** Việc thiết lập chính xác các IAM Role giúp các dịch vụ tự động trao đổi dữ liệu an toàn với S3 mà hoàn toàn không cần phải hardcode (viết chết) các cặp Access Key/Secret Key bên trong mã nguồn ứng dụng.
3. **Tính linh hoạt của Artifact:** Việc đóng gói toàn bộ mô hình thành file nén tập trung `model.tar.gz` trên S3 giúp đơn giản hóa quy trình CI/CD. Khi cần cập nhật phiên bản ứng dụng, máy chủ EC2 chỉ cần kéo tệp mới nhất từ S3 về mà không cần xây dựng lại toàn bộ hạ tầng máy chủ.

---

*Nguồn tài liệu chính: [First Cloud Journey - AWS Study Group*](https://cloudjourney.awsstudygroup.com/)