---
title: "Tuần 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Mục tiêu tuần:**
- Khởi chạy các máy chủ ảo Amazon EC2 nền tảng để chạy ứng dụng giao diện storefront.
- Triển khai các instance chạy dịch vụ vi mô RESTful API nội bộ.
- Cấu hình môi trường runtime ứng dụng cục bộ và cài đặt trình điều khiển (drivers) kết nối database.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Khởi chạy các máy chủ ảo EC2 chạy hệ điều hành Ubuntu trong vùng private subnets dành riêng cho tầng Web Frontend. | 11/5 |
| Thứ Ba | Khởi chạy các máy chủ ảo EC2 tương ứng để chạy mã nguồn dịch vụ cho tầng RESTful API nội bộ. | 12/5 |
| Thứ Tư | Cài đặt các gói thư viện phụ thuộc, môi trường Node.js và Python runtimes trên cả hai loại máy chủ. | 13/5 |
| Thứ Năm | Cấu hình trình điều khiển client kết nối cơ sở dữ liệu PostgreSQL cùng các bộ tham số môi trường liên quan. | 14/5 |
| Thứ Sáu (Lên văn phòng) | Thực hiện các bài kiểm tra kết nối mạng cục bộ lặp và kết nối bắc cầu xuyên suốt giữa hai tầng ứng dụng. | 15/5 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Các máy chủ tính toán giao diện web được phân bổ thành công trên nhiều vùng sẵn sàng (AZs).
  - Bài học: Đặt cấu hình máy chủ Web trong private subnet đảm bảo ngăn chặn triệt để mọi hành vi xâm nhập trái phép từ bên ngoài mạng.
- **Thứ Ba:**
  - Kết quả đạt được: Tầng máy chủ API nội bộ được cô lập sâu thành công trong các phân vùng private subnets tách biệt.
  - Bài học: Tầng xử lý logic nghiệp vụ API cần được giữ kín, chỉ cho phép tiếp nhận yêu cầu điều phối thông qua bộ cân bằng tải.
- **Thứ Tư:**
  - Kết quả đạt được: Môi trường runtime của ứng dụng và các biến môi trường cấu hình được đồng bộ hoàn tất.
  - Bài học: Chuẩn hóa cấu hình runtime đồng bộ giúp loại bỏ lỗi không tương thích phiên bản khi ứng dụng thực thi thực tế.
- **Thứ Năm:**
  - Kết quả đạt được: Cấu hình tài khoản kết nối database được ánh xạ an toàn thông qua các bộ quản lý tham số.
  - Bài học: Tuyệt đối không lưu cứng (hardcode) mật khẩu database trong mã nguồn; thay vào đó dữ liệu được nạp động qua cấu hình hệ thống.
- **Thứ Sáu (Lên văn phòng):**
  - Kết quả đạt được: Các lệnh ping và kiểm tra telnet giữa tầng máy chủ Web và API trả về kết quả phản hồi thông suốt.
  - Bài học: Xác thực kết nối nội bộ thành công chứng minh hệ thống quy tắc Security Groups đang hoạt động chuẩn xác theo thiết kế kiến trúc phân tầng.
