---
title: "Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Mục tiêu tuần:**
- Triển khai hai cơ sở dữ liệu Amazon RDS PostgreSQL song song cho các tác vụ giao dịch trực tiếp và phân tích.
- Cấu hình các nhóm Subnet cơ sở dữ liệu (DB Subnet Groups) an toàn trên nhiều Availability Zones.
- Thiết lập quy tắc bảo mật mạng để giới hạn quyền truy cập database chỉ cho các máy chủ web được phép.
- Xác minh kết nối từ các máy ảo EC2 trong subnet riêng tư tới các đầu cuối cơ sở dữ liệu.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai (Lên văn phòng) | Triển khai cơ sở dữ liệu giao dịch trung tâm `fashion-rds` sử dụng Amazon RDS PostgreSQL. | 25/5 |
| Thứ Ba | Triển khai cơ sở dữ liệu phân tích chuyên dụng `training-db` sử dụng Amazon RDS PostgreSQL. | 26/5 |
| Thứ Tư | Cấu hình các Security Groups cho cơ sở dữ liệu, chỉ cho phép lưu lượng truy cập từ nhóm bảo mật EC2. | 27/5 |
| Thứ Năm | Thiết lập các DB Subnet Groups để phân bổ các instance cơ sở dữ liệu vào các private subnets trên nhiều AZs. | 28/5 |
| Thứ Sáu | Thực hiện các bài kiểm tra kết nối từ máy ảo EC2 riêng tư tới cả hai endpoint cơ sở dữ liệu. | 29/5 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai (Lên văn phòng):**
  - Kết quả đạt được: RDS `fashion-rds` chạy ổn định trên cấu hình db.t3.micro (dung lượng 20 GiB) và đã bật sao lưu tự động.
  - Bài học: AWS RDS tự động hóa quy trình sao lưu và cập nhật hệ điều hành, giúp giảm thiểu đáng kể công việc quản trị database.
- **Thứ Ba:**
  - Kết quả đạt được: RDS `training-db` được khởi tạo thành công để lưu trữ các tập dữ liệu huấn luyện ML.
  - Bài học: Tách biệt database giao dịch và database phục vụ phân tích/huấn luyện giúp cô lập tải truy vấn, tránh làm chậm ứng dụng web chính.
- **Thứ Tư:**
  - Kết quả đạt được: Thiết lập tường lửa cổng 5432 thành công, chặn hoàn toàn mọi truy cập từ dải IP public.
  - Bài học: Chỉ nên cho phép các máy chủ ứng dụng kết nối tới database thông qua Security Group ID thay vì mở cổng công khai.
- **Thứ Năm:**
  - Kết quả đạt được: Gom nhóm các subnet riêng tư trên các vùng địa lý khác nhau để phục vụ dự phòng.
  - Bài học: DB Subnet Group giúp RDS dễ dàng tạo các bản sao dự phòng (standby instances) ở các vùng khác khi cần thiết.
- **Thứ Sáu:**
  - Kết quả đạt được: Kết nối thành công từ EC2 tới RDS qua lệnh psql và khởi tạo các bảng dữ liệu ban đầu.
  - Bài học: Thử nghiệm kết nối thực tế giúp kiểm chứng tính chính xác của bảng định tuyến subnet và cấu hình nhóm bảo mật.
