---
title: "Tuần 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Mục tiêu tuần:**
- Khởi chạy và cấu hình hệ thống máy chủ tính toán chuyên dụng dành cho các tác vụ học máy `ML-Forecast-Server`.
- Phát triển các đoạn mã kịch bản Python phục vụ cho việc huấn luyện mô hình dự báo nhu cầu thị trường.
- Triển khai tính năng tự động đóng gói và xuất bản thành phẩm mô hình học máy lên kho lưu trữ Amazon S3.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Khởi chạy máy chủ ảo chuyên dụng `ML-Forecast-Server` sử dụng cấu hình Amazon EC2 instance loại t3.small. | 22/6 |
| Thứ Ba | Thiết lập cài đặt môi trường khoa học dữ liệu Python bao gồm các bộ thư viện Scikit-learn, XGBoost, và LightGBM. | 23/6 |
| Thứ Tư | Viết mã nguồn cốt lõi thực hiện kết nối nạp ma trận đặc trưng lịch sử từ database phân tích `training-db` vào bộ nhớ máy chủ. | 24/6 |
| Thứ Năm | Triển khai các vòng lặp huấn luyện thuật toán hồi quy, áp dụng kỹ thuật đánh giá chéo (cross-validation) và ghi nhật ký hiệu năng. | 25/6 |
| Thứ Sáu | Bổ sung mã nguồn tuần tự hóa dữ liệu để xuất bản tệp mô hình thành phẩm dạng định dạng nén (`.bin`/`.pkl`) trực tiếp lên S3. | 26/6 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Máy chủ huấn luyện học máy chuyên biệt hoạt động ổn định và được bảo vệ nghiêm ngặt bởi nhóm bảo mật mạng riêng.
  - Bài học: Sử dụng máy chủ độc lập cho các tác vụ ML giúp bảo vệ an toàn cho tài nguyên tính toán của các website storefront khỏi tình trạng nghẽn CPU khi chạy thuật toán nặng.
- **Thứ Ba:**
  - Kết quả đạt được: Toàn bộ các gói thư viện khoa học dữ liệu phụ thuộc được thiết lập đồng bộ thông qua môi trường ảo pip virtual environments.
  - Bài học: Cô lập môi trường thực thi giúp đảm bảo mã nguồn huấn luyện mô hình luôn chạy ổn định và nhất quán, tránh lỗi xung đột phiên bản thư viện.
- **Thứ Tư:**
  - Kết quả đạt được: Xác thực kết nối kéo ma trận đặc trưng thành công từ cơ sở dữ liệu phân tích vào cấu trúc dataframe của Python.
  - Bài học: Quy trình nạp dữ liệu trực tiếp vào bộ nhớ giúp giảm thiểu tối đa các hao phí đọc ghi file trung gian trên ổ cứng máy chủ.
- **Thứ Năm:**
  - Kết quả đạt được: Các mô hình hồi quy XGBoost và LightGBM hoàn tất huấn luyện, đạt các chỉ số đánh giá sai số kiểm thử ở mức tối ưu.
  - Bài học: Thực hiện so sánh hiệu năng đồng thời giữa nhiều thuật toán đảm bảo việc lựa chọn ra phiên bản mô hình tối ưu nhất để đưa vào môi trường thực tế.
- **Thứ Sáu:**
  - Kết quả đạt được: Các tệp mô hình học máy thành phẩm được đẩy thành công lên phân vùng đường dẫn lưu trữ tập trung `fashion-retail-model-storage/models/`.
  - Bài học: Lưu trữ tập trung các tệp artifact trên S3 giúp tạo lập một kho quản lý lịch sử các phiên bản mô hình, phục vụ tốt cho công tác triển khai phục vụ API sau này.
