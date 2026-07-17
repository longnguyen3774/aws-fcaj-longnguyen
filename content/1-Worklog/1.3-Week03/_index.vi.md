---
title: "Tuần 3"
date: 2026-05-04
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

**Mục tiêu tuần:**
- Khởi tạo cấu trúc lược đồ (schema) cho cơ sở dữ liệu giao dịch chính và cơ sở dữ liệu phân tích.
- Cấp phát các phân vùng lưu trữ Amazon S3 đóng vai trò làm vùng đệm dữ liệu (landing zone).
- Thiết lập hệ thống cảnh báo Amazon CloudWatch cơ sở để giám sát toàn bộ hạ tầng.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Thiết kế chi tiết lược đồ quan hệ database PostgreSQL phục vụ cho lưu trữ giao dịch cửa hàng. | 04/5 |
| Thứ Ba | Xây dựng cấu trúc bảng phân tích dành riêng cho các tập đặc trưng (feature store) trong database huấn luyện. | 05/5 |
| Thứ Tư | Cấp phát bucket Amazon S3 chính mang tên `fashion-retail-model-storage` cùng các phân vùng đệm dữ liệu. | 06/5 |
| Thứ Năm | Cấu hình các quy tắc chính sách kiểm soát quyền truy cập S3 Bucket Policies và bật mã hóa phía máy chủ (SSE-S3). | 07/5 |
| Thứ Sáu | Thiết lập các ngưỡng cảnh báo chi phí và hạ tầng cơ sở trên nền tảng Amazon CloudWatch. | 08/5 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Lược đồ giao dịch storefront được hoàn thiện với đầy đủ ràng buộc khóa ngoại và chỉ mục (index).
  - Bài học: Xây dựng các chỉ mục tối ưu ngay từ đầu giúp đẩy nhanh tốc độ thực thi cho các tác vụ trích xuất dữ liệu của AWS Glue sau này.
- **Thứ Ba:**
  - Kết quả đạt được: Lược đồ kho đặc trưng phân tích được tối ưu hóa chuyên biệt cho dữ liệu dạng chuỗi thời gian (time-series).
  - Bài học: Lược đồ phân tích cần được thiết kế gọn gàng nhằm tăng tốc khả năng đọc dữ liệu khi cung cấp đầu vào cho các mô hình học máy.
- **Thứ Tư:**
  - Kết quả đạt được: Các phân vùng S3 lưu trữ được thiết lập khoa học dưới các tiền tố cụ thể (`/landing`, `/features`, `/models`).
  - Bài học: Tổ chức cấu trúc thư mục (prefix) khoa học trên S3 giúp đơn giản hóa việc phân quyền truy cập và đường dẫn cho các script ETL.
- **Thứ Năm:**
  - Kết quả đạt được: Các tính năng mã hóa và chặn truy cập công khai được kích hoạt trên toàn bộ các bucket.
  - Bài học: Chính sách chặn truy cập công khai (Block Public Access) tuyệt đối bảo vệ an toàn cho các dữ liệu thương mại nhạy cảm của doanh nghiệp.
- **Thứ Sáu:**
  - Kết quả đạt được: Hệ thống cảnh báo được kích hoạt thành công đối với các ngưỡng ngân sách và hiệu năng CPU máy chủ.
  - Bài học: Giám sát chi phí sớm giúp kiểm soát ngân sách vận hành hạ tầng cloud, tránh các chi phí phát sinh ngoài ý muốn.
