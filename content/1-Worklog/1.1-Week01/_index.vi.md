---
title: "Tuần 1"
date: 2026-04-20
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

**Mục tiêu tuần:**
- Thiết kế kiến trúc mạng có tính sẵn sàng cao (High-Availability) trên môi trường cloud.
- Cấu hình Amazon VPC với các subnet công khai (public) và riêng tư (private) trên nhiều Availability Zones khác nhau.
- Thiết lập kết nối internet và các bảng định tuyến an toàn cho các tầng xử lý dữ liệu bên ngoài.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Khởi tạo thành công hạ tầng mạng core Amazon VPC với dải địa hình CIDR block tùy chỉnh. | 20/4 |
| Thứ Ba | Phân bổ cấu hình các subnet public và private đồng đều qua nhiều vùng Availability Zones. | 21/4 |
| Thứ Tư | Triển khai cấu hình cổng Internet Gateway và gắn kết trực tiếp vào hệ thống VPC. | 22/4 |
| Thứ Năm | Cấu hình bảng Public Route Tables để định tuyến lưu lượng truy cập từ Internet ra bên ngoài. | 23/4 |
| Thứ Sáu | Thiết lập các cổng kết nối NAT Gateways tại public subnet để cấp internet một chiều cho private subnet. | 24/4 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Hệ thống VPC được thiết lập thành công, cô lập toàn bộ hạ tầng mạng của ứng dụng.
  - Bài học: Phân tách phân đoạn mạng đúng chuẩn là yếu tố cốt lõi để bảo vệ dữ liệu nội bộ khỏi lưu lượng web công cộng.
- **Thứ Ba:**
  - Kết quả đạt được: Các subnet được phân bổ đồng đều qua các vùng AZ nhằm chuẩn bị sẵn sàng cho tính năng chịu lỗi.
  - Bài học: Phân tán tài nguyên trên nhiều vùng AZ ngăn ngừa rủi ro gián đoạn hệ thống khi một vùng địa lý gặp sự cố.
- **Thứ Tư:**
  - Kết quả đạt được: Cổng kết nối Internet Gateway hoạt động ổn định và chính xác.
  - Bài học: Chỉ liên kết Internet Gateway với các public subnet để duy trì tính khép kín và an toàn cho vùng private.
- **Thứ Năm:**
  - Kết quả đạt được: Các tuyến đường định tuyến cho vùng public được xác thực và kích hoạt hoàn chỉnh.
  - Bài học: Khai báo rõ ràng các bảng định tuyến giúp loại bỏ hoàn toàn nguy cơ vô tình lộ lọt tài nguyên nội bộ ra internet.
- **Thứ Sáu:**
  - Kết quả đạt được: NAT Gateways triển khai thành công, cho phép các instance trong vùng riêng tư tải cập nhật.
  - Bài học: NAT Gateways cho phép máy chủ nội bộ kết nối ra ngoài an toàn mà không cần phải chấp nhận các kết nối không mong muốn từ bên ngoài vào.
