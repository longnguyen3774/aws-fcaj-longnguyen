---
title: "Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Mục tiêu tuần:**
- Thiết kế cấu trúc mã nguồn biến đổi dữ liệu phân tán sử dụng ngôn ngữ PySpark (Feature Engineering).
- Triển khai các công thức tính toán đặc trưng chuỗi thời gian phân tán (lượng bán trễ - lags, trung bình trượt - rolling averages).
- Tối ưu hóa hiệu năng các phép toán biến đổi PySpark trên các phân vùng dữ liệu SKU mã sản phẩm lớn.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Khởi tạo cấu trúc nền tảng và thiết lập phiên làm việc SparkSession cho tệp mã nguồn `glue_feature_engineering.py`. | 08/6 |
| Thứ Ba | Áp dụng các kỹ thuật PySpark Window Functions để tính toán các đặc trưng doanh số trễ 7 ngày và 14 ngày. | 09/6 |
| Thứ Tư | Bổ sung các hàm tính toán song song giá trị trung bình trượt 30 ngày và các chỉ số tốc độ tiêu thụ sản phẩm (sales velocity). | 10/6 |
| Thứ Năm | Cấu hình phân vùng dữ liệu tối ưu (partitioning) dựa trên các trường thông tin mã định danh SKU và mã cửa hàng. | 11/6 |
| Thứ Sáu | Thực hiện chạy thử nghiệm cục bộ (local tests) trên cụm dữ liệu giả lập quy mô nhỏ để kiểm tra logic thuật toán. | 12/6 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Môi trường cấu hình làm việc PySpark được tạo lập thành công cùng bộ khởi tạo tham số tối ưu.
  - Bài học: Engine tính toán phân tán của PySpark đem lại hiệu năng vượt trội khi xử lý hàng triệu bản ghi chuỗi thời gian so với các truy vấn SQL tuần tự truyền thống.
- **Thứ Ba:**
  - Kết quả đạt được: Các hàm tính toán giá trị trễ được xác thực hoạt động chính xác trên toàn trục thời gian.
  - Bài học: Sử dụng phân vùng Window chính xác theo từng cặp mặt hàng - vị trí giúp loại bỏ hoàn toàn hiện tượng rò rỉ dữ liệu chéo giữa các SKU.
- **Thứ Tư:**
  - Kết quả đạt được: Các tập đặc trưng trung bình trượt và vận tốc bán hàng được tích hợp thành công vào ma trận dữ liệu đầu ra.
  - Bài học: Chỉ số vận tốc bán hàng hỗ trợ mô hình nhận diện nhanh chóng các biến động đột biến của thị trường thời trang, từ đó nâng cao độ chính xác khi dự báo cầu.
- **Thứ Năm:**
  - Kết quả đạt được: Dữ liệu được phân bổ khoa học theo mã phân loại hàng hóa giúp tăng tốc tiến trình xử lý song song.
  - Bài học: Phân vùng dữ liệu thông minh giúp tối đa hóa công suất xử lý của các nút tính toán (Worker nodes) và giảm thiểu hiện tượng nghẽn mạng do xáo trộn dữ liệu (data shuffling).
- **Thứ Sáu:**
  - Kết quả đạt được: Tiến trình chạy thử hoàn tất thành công, không ghi nhận bất kỳ lỗi cú pháp hay logic xử lý nào.
  - Bài học: Xác thực sớm mã nguồn biến đổi dữ liệu trên tập mẫu giúp tiết kiệm đáng kể thời gian gỡ lỗi và chi phí vận hành dịch vụ trên môi trường thật.
