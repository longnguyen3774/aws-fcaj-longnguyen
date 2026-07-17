---
title: "Tuần 9"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**Mục tiêu tuần:**
- Triển khai toàn bộ quy trình biến đổi đặc trưng lên dịch vụ quản trị AWS Glue Spark.
- Cấu hình cơ chế kết nối nạp dữ liệu đầu ra từ Spark ngược trở lại vào cơ sở dữ liệu analytical `training-db`.
- Thực hiện đo đạc hiệu năng và tối ưu hóa chi phí cho toàn chuỗi ETL tổng thể.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Tải tệp mã nguồn xử lý hoàn chỉnh `glue_feature_engineering.py` lên kho lưu trữ scripts an toàn của AWS Glue. | 15/6 |
| Thứ Ba | Cấu hình phân bổ tài nguyên cho AWS Glue Spark Job với mức thiết lập ban đầu tối thiểu là 2 Data Processing Units (DPUs). | 16/6 |
| Thứ Tư | Tích hợp thư viện ghi JDBC driver PostgreSQL vào mã nguồn Spark để đẩy trực tiếp dữ liệu sau xử lý vào database `training-db`. | 17/6 |
| Thứ Năm | Tiến hành chạy thử nghiệm liên hoàn toàn bộ chuỗi gồm hai tiến trình ETL liên tiếp nhau. | 18/6 |
| Thứ Sáu | Phân tích thời gian chạy, biểu đồ tiêu thụ RAM và tinh chỉnh lại định lượng cấp phát DPU tối ưu cho hệ thống. | 19/6 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Mã nguồn xử lý dữ liệu được quản lý phiên bản rõ ràng và lưu trữ an toàn trong bucket triển khai hệ thống.
  - Bài học: Quản lý phiên bản script chặt chẽ ngăn chặn rủi ro vô tình ghi đè mã nguồn lỗi làm gián đoạn chuỗi cung ứng dữ liệu sản xuất.
- **Thứ Ba:**
  - Kết quả đạt được: Cấp phát tài nguyên ban đầu hợp lý giúp kiểm soát tốt chi phí sử dụng hạ tầng cloud.
  - Bài học: Khởi đầu từ mức cấu hình tài nguyên nhỏ giúp dễ dàng tìm ra điểm cân bằng tối ưu giữa tốc độ chạy và chi phí hóa đơn AWS phát sinh.
- **Thứ Tư:**
  - Kết quả đạt được: Dữ liệu kết quả từ Spark được ghi nhận nạp nhập thành công vào các bảng chứa dữ liệu huấn luyện phân tách.
  - Bài học: Ghi trực tiếp kết quả vào một database phân tích riêng biệt bảo vệ tuyệt đối hiệu năng hệ thống giao dịch của khách hàng mua hàng.
- **Thứ Năm:**
  - Kết quả đạt được: Chuỗi quy trình chạy liên tiếp hoàn tất thành thục: Dữ liệu di chuyển mượt mà từ database nguồn qua S3, rồi nạp về `training-db`.
  - Bài học: Hệ thống ETL tuần tự, độc lập và rõ ràng tạo tiền đề vững chắc cho việc xây dựng các kiến trúc tự động hóa thông minh tiếp theo.
- **Thứ Sáu:**
  - Kết quả đạt được: Chuỗi pipeline xử lý tổng thể được tinh chỉnh tối ưu thời gian chạy xuống dưới 20 phút, đáp ứng hoàn hảo yêu cầu bài toán ngân sách.
  - Bài học: Tối ưu hóa các thông số vận hành giúp hạ tầng cloud luôn vận hành hiệu quả ngay cả khi khối lượng dữ liệu kinh doanh của doanh nghiệp mở rộng mạnh mẽ.
