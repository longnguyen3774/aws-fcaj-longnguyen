---
title: "Tuần 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

**Mục tiêu tuần:**
- Phát triển tầng dịch vụ tính toán không máy chủ (Serverless) phục vụ dự báo trực tuyến sử dụng nền tảng AWS Lambda.
- Xuất bản hàm dự báo Lambda ra môi trường bên ngoài dưới dạng một endpoint kết nối thông qua dịch vụ Amazon API Gateway.
- Xác thực độ trễ phản hồi thấp và tính chính xác của kết quả dự báo trả về từ endpoint API.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Viết mã nguồn xử lý logic dự báo cho hàm AWS Lambda, tiếp nhận đầu vào thông tin mã sản phẩm và thực hiện sinh dự đoán. | 29/6 |
| Thứ Ba | Đóng gói mã nguồn dự báo kèm theo các thư viện phụ thuộc rút gọn thành một lớp triển khai mã nguồn tối ưu Lambda Layer. | 30/6 |
| Thứ Tư | Khởi tạo dịch vụ Amazon API Gateway loại HTTP API đóng vai trò làm cổng tiếp nhận yêu cầu public cho hệ thống không máy chủ. | 01/7 |
| Thứ Năm | Cấu hình các quy tắc kích hoạt Lambda và biến môi trường trỏ đường dẫn nạp động tệp mô hình học máy trực tiếp từ S3. | 02/7 |
| Thứ Sáu | Thực hiện các bài kiểm tra đo đạc thời gian phản hồi (latency) và kiểm thử tải đồng thời sử dụng các công cụ kiểm thử API chuyên dụng. | 03/7 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Hàm Lambda viết xong, có khả năng nạp nhanh tệp mô hình từ S3 và thực hiện tính toán trả về số lượng cầu dự báo cho SKU mặt hàng.
  - Bài học: Mô hình kiến trúc serverless loại bỏ hoàn toàn các gánh nặng chi phí phần cứng và công sức bảo trì hệ thống máy chủ chạy thường trực 24/7.
- **Thứ Ba:**
  - Kết quả đạt được: Kích thước gói mã nguồn triển khai được tối ưu hóa nén gọn thành công nhằm tăng tốc thời gian khởi động của hàm không máy chủ.
  - Bài học: Giữ kích thước gói mã nguồn gọn nhẹ giúp giảm thiểu tối đa hiện tượng trễ khởi động lạnh (cold start latency) khi có yêu cầu đột biến gọi vào hệ thống.
- **Thứ Tư:**
  - Kết quả đạt được: Cổng kết nối API Gateway chính thức hoạt động trực tuyến, cung cấp một URL kết nối an toàn, bảo mật và tự động mở rộng theo tải.
  - Bài học: API Gateway tự động co giãn công suất xử lý một cách linh hoạt, đảm bảo đáp ứng mượt mà các đợt bùng nổ traffic tra cứu từ ứng dụng bán hàng.
- **Thứ Năm:**
  - Kết quả đạt được: Hàm Lambda thực hiện tải và ánh xạ thành công mô hình từ kho chứa S3 để đưa ra phản hồi kết quả chính xác.
  - Bài học: Cơ chế nạp động mô hình cho phép các kỹ sư dễ dàng cập nhật phiên bản dự báo mới chỉ bằng thao tác thay thế tệp tin trên S3 mà không cần cấu hình lại code API.
- **Thứ Sáu:**
  - Kết quả đạt được: Thời gian phản hồi trung bình của API giữ vững ở mức dưới 150ms xuyên suốt toàn bộ các bài kiểm tra mô phỏng lượng truy cập lớn.
  - Bài học: Tốc độ phản hồi API cực nhanh đảm bảo hệ thống website storefront và các nhà quản trị có được trải nghiệm mượt mà, không bị gián đoạn khi xem thông tin dự báo cầu.
