---
title: "Ngày 2"
date: 2026-05-22
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

# Nhật Ký Làm Việc: Tối Ưu Phân Phối Tốc Độ Cao Với CloudFront, Điều Hướng Lưu Lượng Bằng ALB Và Tự Động Mở Rộng Hệ Thống Với Auto Scaling

> **Ngày 2 - Thứ Sáu, ngày 22/05/2026:** Tiến hành nâng cấp hạ tầng API đơn lẻ từ Ngày 1 thành kiến trúc có tính sẵn sàng cao (High Availability) và khả năng co giãn tự động bằng cách cấu hình bộ cân bằng tải Application Load Balancer (ALB), thiết lập Auto Scaling Group cho các máy chủ EC2, và tối ưu hóa tốc độ phản hồi trên toàn cầu thông qua mạng lưới phân phối nội dung AWS CloudFront.

---

### Mục tiêu học tập trong ngày

- Thiết lập **Application Load Balancer (ALB)** để phân phối lưu lượng truy cập API đồng đều đến các máy chủ ảo phía sau.
- Cấu hình **Auto Scaling Group (ASG)** kết hợp cùng Launch Template để tự động tăng/giảm số lượng EC2 instance theo tải thực tế của ứng dụng.
- Triển khai **AWS CloudFront (CDN)** làm lớp giao tiếp ngoài cùng nhằm giảm độ trễ, tối ưu bộ nhớ đệm (Caching) và tăng cường bảo mật cho hệ thống API.
- Thực hiện kiểm thử tính năng Failover (khắc phục sự cố tự động) và các cơ chế co giãn tài nguyên đám mây.

---

### Điều Hướng Lưu Lượng Truy Cập Với Application Load Balancer (ALB)

#### 1. Cấu hình Target Group và Health Check
- Khởi tạo một Target Group dạng `Instances` chạy giao thức HTTP trên cổng `8000` (cổng dịch vụ API từ Ngày 1).
- Cấu hình tính năng **Health Check** (kiểm tra sức khỏe hệ thống) trỏ về đường dẫn `/health` của API với tần suất 30 giây một lần để đảm bảo ALB chỉ điều hướng traffic đến các máy chủ đang hoạt động tốt.

#### 2. Triển khai Load Balancer trong VPC
- Khởi tạo một Application Load Balancer (ALB) hoạt động ở chế độ Internet-facing (công khai).
- Đặt ALB chạy trên nhiều **Availability Zones (AZs)** khác nhau để đảm bảo khả năng chịu lỗi nếu một trung tâm dữ liệu gặp sự cố.
- Cấu hình Security Group cho ALB: chỉ mở cổng HTTP (`80`) và HTTPS (`443`) đón nhận yêu cầu từ người dùng công cộng.

---

### Tự Động Co Giãn Hạ Tầng Với EC2 Auto Scaling

#### 1. Tạo Launch Template (Bản thiết kế máy chủ)
- Tạo một Launch Template chứa cấu hình chuẩn hóa từ máy chủ EC2 của Ngày 1: sử dụng Amazon Linux 2023, loại instance `t3.medium`, mã nguồn API cài sẵn, và IAM Role có quyền kết nối với S3.
- Cấu hình đoạn mã **User Data** (script chạy tự động khi khởi tạo máy chủ) để khi một EC2 mới được dựng lên, nó sẽ tự động chạy lệnh `git pull` cập nhật API, tải file `model.tar.gz` mới nhất từ S3 và kích hoạt dịch vụ FastAPI.

#### 2. Thiết lập Auto Scaling Group (ASG) và Chính sách mở rộng
Tôi đã thiết lập các thông số vận hành cho nhóm tự động co giãn ASG như sau:

| Thông số ASG | Cấu hình mặc định | Ý nghĩa và mục đích vận hành |
|---|---|---|
| **Desired Capacity** | 2 instances | Số lượng máy chủ đích hệ thống luôn duy trì trong trạng thái bình thường. |
| **Minimum Capacity** | 2 instances | Số lượng máy chủ tối thiểu để đảm bảo tính sẵn sàng cao (High Availability). |
| **Maximum Capacity** | 5 instances | Giới hạn tối đa số máy chủ được phép mở rộng để kiểm soát chi phí (OpEx). |

- **Target Tracking Scaling Policy:** Kích hoạt chính sách co giãn tự động dựa trên mức độ sử dụng CPU trung bình (`Average CPU Utilization`). Khi tải CPU của toàn hệ thống vượt ngưỡng **70%**, ASG sẽ tự động kích hoạt khởi tạo thêm máy chủ EC2 mới để gánh tải.

---

### Tối Ưu Hóa Tốc Độ Và Phân Phối Qua AWS CloudFront

#### 1. Cấu hình CloudFront Distribution
- Thiết lập một CloudFront Distribution đóng vai trò làm lớp lá chắn ngoài cùng, cấu hình Endpoint của ALB làm **Origin** (Nguồn phân phối gốc).
- Cấu hình điều hướng toàn bộ lưu lượng HTTP sang HTTPS tại các máy chủ Edge Location của CloudFront để bảo mật đường truyền.

#### 2. Tối ưu bộ nhớ đệm (Cache Behavior Management)
Để cân bằng giữa tốc độ phản hồi và tính chính xác của dữ liệu, tôi thiết lập chính sách cache tách biệt:

| Đường dẫn API (Path) | Cấu hình Cache | Lý do kỹ thuật |
|---|---|---|
| `/static/*` hoặc tệp đồ họa | Caching Enabled (Mặc định 24h) | Giảm tải hoàn toàn cho máy chủ EC2 gốc bằng cách lưu giữ nội dung tĩnh ở Edge Locations gần người dùng. |
| `/predict` (API dự đoán mô hình) | Caching Disabled (Bỏ qua Cache) | Đảm bảo mỗi yêu cầu dự đoán mới gửi lên đều được ALB điều hướng trực tiếp về EC2 để xử lý dữ liệu thời gian thực. |

---

### Các Lệnh Vận Hành Và Giám Sát Qua AWS CLI

Dưới đây là các lệnh CLI phục vụ việc kiểm tra trạng thái hoạt động của bộ cân bằng tải và các tiến trình co giãn tự động:

```bash
# 1. Liệt kê trạng thái sức khỏe của các EC2 instance thuộc Target Group của ALB
aws elbv2 describe-target-health \
  --target-group-arn arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/my-api-tg/abc123xyz

# 2. Kiểm tra thông tin chi tiết và số lượng máy chủ hiện tại của Auto Scaling Group
aws autoscaling describe-auto-scaling-groups \
  --auto-scaling-group-names my-api-asg \
  --query 'AutoScalingGroups[].{Name:AutoScalingGroupName,Desired:DesiredCapacity,Instances:Instances[].InstanceId}'

# 3. Tạo một yêu cầu xóa cache thủ công (Invalidation) trên CloudFront khi cập nhật giao diện
aws cloudfront create-invalidation \
  --distribution-id E1A2B3C4D5E6F7 \
  --paths "/static/*"

# 4. Truy vấn lịch sử hoạt động co giãn (Scaling Activities) để xem ASG đã tăng/giảm máy chủ ra sao
aws autoscaling describe-scaling-activities \
  --auto-scaling-group-name my-api-asg \
  --max-items 3

```

---

### Nội Dung Học Tập Đã Hoàn Thành

| Ngày học | Nội dung bài học tập trung | Dịch vụ AWS liên quan |
| --- | --- | --- |
| **22/05/2026** | Điều phối lưu lượng mạng và Kiểm tra sức khỏe hệ thống | Application Load Balancer (ALB) |
| **22/05/2026** | Tự động hóa quy mô máy chủ theo tải thực tế | EC2 Auto Scaling Group, Launch Templates |
| **22/05/2026** | Mạng lưới phân phối nội dung toàn cầu và Tối ưu hóa Cache | AWS CloudFront (CDN) |

---

### Bài học rút ra từ Ngày 2

1. **Kiến trúc phi trạng thái (Stateless Architecture):** Để Auto Scaling hoạt động hoàn hảo, mã nguồn API chạy trên EC2 phải hoàn toàn "phi trạng thái". Việc Ngày 1 tách biệt tệp mô hình nặng (`model.tar.gz`) sang S3 giúp các máy chủ mới sinh ra từ ASG có thể dễ dàng tải cấu hình về chạy ngay mà không bị ràng buộc dữ liệu cục bộ.
2. **Sự kết hợp giữa ALB và ASG:** Bộ đôi này tạo nên xương sống cho tính sẵn sàng cao. Khi chủ động thử nghiệm tắt (Terminate) một instance EC2, hệ thống tự động phát hiện lỗi nhờ ALB Health Check và ASG lập tức khởi tạo một máy chủ thay thế trong vài phút (Self-healing).
3. **Chiến lược phân lớp hạ tầng:** Đặt CloudFront ở trước ALB giúp tăng tốc độ phản hồi đáng kể cho người dùng cuối trên toàn cầu nhờ mạng lưới mạng lõi của AWS, đồng thời che giấu địa chỉ IP thật của Load Balancer, tạo thêm một lớp bảo mật ngăn chặn các cuộc tấn công DDoS trực diện.

---

*Nguồn tài liệu chính: [First Cloud Journey - AWS Study Group*](https://cloudjourney.awsstudygroup.com/)