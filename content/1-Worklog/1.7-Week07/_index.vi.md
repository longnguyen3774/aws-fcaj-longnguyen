---
title: "Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

**Mục tiêu tuần:**
- Khởi tạo kho dữ liệu AWS Glue Data Catalog và thiết lập các kết nối mạng JDBC liên quan.
- Xây dựng và hoàn thiện mã nguồn Python Shell ETL để phục vụ trích xuất dữ liệu thô tự động từ database.
- Kiểm chứng tính an toàn của quy trình truyền tải dữ liệu từ RDS PostgreSQL về phân vùng đệm S3 Landing Zone.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Cấu hình thiết lập các kết nối AWS Glue Connections liên kết an toàn tới cả hai cơ sở dữ liệu `fashion-rds` và `training-db`. | 01/6 |
| Thứ Ba | Phát triển hoàn thiện kịch bản mã nguồn `de-fashion-rds-extract` chạy trong môi trường AWS Glue Python Shell. | 02/6 |
| Thứ Tư | Cấu hình phân quyền truy cập dữ liệu S3 IAM Data Access dành riêng cho vai trò thực thi (execution role) của AWS Glue. | 03/6 |
| Thứ Năm | Tiến hành các lượt chạy thử nghiệm thủ công đầu tiên đối với script trích xuất dữ liệu Python. | 04/6 |
| Thứ Sáu | Xác thực tính toàn vẹn của dữ liệu thô dạng CSV đã đẩy về vùng lưu trữ đệm trong S3. | 05/6 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Các kết nối của Glue Catalog được xác thực thành công, giao tiếp trơn tru tới hệ thống RDS.
  - Bài học: Glue Connection quản lý an toàn thông tin chuỗi kết nối JDBC thông qua cấu hình mạng bảo mật nội bộ VPC.
- **Thứ Ba:**
  - Kết quả đạt được: Script Python Shell được viết hoàn chỉnh giúp truy vấn nhanh chóng lịch sử giao dịch bán hàng hàng ngày từ cửa hàng.
  - Bài học: Môi trường Python Shell là một lựa chọn tối ưu chi phí và gọn nhẹ để kéo các tập giao dịch nhỏ mà không phải chịu hao phí tài nguyên khởi động của cụm mã nguồn Spark.
- **Thứ Tư:**
  - Kết quả đạt được: Vai trò thực thi hệ thống được cấp phép ghi dữ liệu chuẩn xác vào các phân vùng đệm S3 mục tiêu.
  - Bài học: Giới hạn quyền hạn tài nguyên chặt chẽ đảm bảo quy trình ETL không thể thực hiện các hành vi đọc hoặc ghi dữ liệu trái phép ngoài phạm vi dự án.
- **Thứ Năm:**
  - Kết quả đạt được: Dữ liệu từ các bảng PostgreSQL được bóc tách thành công và đẩy thẳng lên hệ thống lưu trữ S3.
  - Bài học: Xây dựng các cơ chế bắt ngoại lệ (exception handling) tốt giúp tiến trình xử lý không bị treo hoặc chết âm thầm khi chạy tự động theo lịch.
- **Thứ Sáu:**
  - Kết quả đạt được: Các tập dữ liệu giao dịch thô khớp hoàn toàn về số lượng dòng (row count) so với bảng nguồn tại database.
  - Bài học: Đối soát dữ liệu đầu cuối đảm bảo quy trình nạp nhập dữ liệu ban đầu cho chuỗi cung ứng MLOps luôn đạt độ tin cậy tuyệt đối.
