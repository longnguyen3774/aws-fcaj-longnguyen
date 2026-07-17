---
title: "Tuần 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Mục tiêu tuần:**
- Cấu hình mạng lưới phân phối nội dung Amazon CloudFront CDN để tối ưu hóa truyền tải tài nguyên tĩnh.
- Triển khai bộ cân bằng tải External Application Load Balancer để điều phối traffic công cộng từ Internet.
- Triển khai bộ cân bằng tải Internal Application Load Balancer để bảo mật kết nối nội bộ giữa các microservices.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Khởi tạo phân phối CloudFront chỉ định nguồn gốc trỏ về bộ cân bằng tải hướng ngoài. | 18/5 |
| Thứ Ba | Cấp phát bộ cân bằng tải Application Load Balancer hướng ngoài (External ALB) tại public subnets. | 19/5 |
| Thứ Tư | Cấu hình Target Groups và các quy tắc điều hướng giao thức HTTP/HTTPS cho tầng máy chủ Web. | 20/5 |
| Thứ Năm | Triển khai cài đặt hệ thống bộ cân bằng tải nội bộ riêng tư (Internal ALB). | 21/5 |
| Thứ Sáu (Lên văn phòng) | Liên kết liên thông để tầng máy chủ Web trỏ đích đến bộ Internal ALB khi thực hiện gọi API nghiệp vụ. | 22/5 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Phân phối mạng lưới CloudFront được kích hoạt với các cơ chế lưu bộ nhớ đệm (cache) mặc định.
  - Bài học: Tận dụng mạng lưới CDN giúp giảm đáng kể tải xử lý cho máy chủ gốc nhờ việc phản hồi các tệp tĩnh ngay tại các trạm biên gần người dùng.
- **Thứ Ba:**
  - Kết quả đạt được: External ALB hoạt động tốt tại vùng public subnet, sẵn sàng tiếp nhận điều phối luồng request từ internet.
  - Bài học: Bộ cân bằng tải hướng ngoại đóng vai trò làm lá chắn trung gian tiếp nhận và phân phối thông minh luồng traffic vào mạng nội bộ.
- **Thứ Tư:**
  - Kết quả đạt được: Hệ thống Target Groups vượt qua các bài kiểm tra trạng thái sức khỏe (health checks) trên cổng 80/443.
  - Bài học: Xác định chính xác đường dẫn kiểm tra sức khỏe giúp ngăn chặn việc ALB chuyển hướng traffic vào các máy chủ đang gặp sự cố gián đoạn.
- **Thứ Năm:**
  - Kết quả đạt được: Internal ALB vận hành ổn định trong phân vùng mạng kín, che giấu hoàn hảo cụm máy chủ API phía sau.
  - Bài học: Sử dụng bộ cân bằng tải nội bộ giúp tầng frontend giao tiếp dễ dàng thông qua một domain tĩnh thay vì phải quản lý danh sách IP máy chủ API.
- **Thứ Sáu (Lên văn phòng):**
  - Kết quả đạt được: Hành trình luồng dữ liệu đi từ internet bên ngoài xuyên suốt xuống đến tầng xử lý API cuối được xác thực hoàn chỉnh.
  - Bài học: Mô hình thiết kế Dual-ALB (kết hợp hai bộ cân bằng tải) cung cấp một giải pháp cô lập an toàn tuyệt đối cho các hệ thống doanh nghiệp.
