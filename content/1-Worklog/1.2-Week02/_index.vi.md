---
title: "Tuần 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Mục tiêu tuần:**
- Áp dụng nguyên tắc đặc quyền tối thiểu (least-privilege) cho các chính sách bảo mật AWS IAM và các execution roles.
- Cấu hình các nhóm bảo mật (Security Groups) cơ sở để cô lập kiến trúc đa tầng (multi-tier).
- Thiết lập cơ chế VPC Flow Logs phục vụ cho công tác kiểm toán lưu lượng mạng ứng dụng.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Soạn thảo các chính sách AWS IAM phân quyền tối thiểu dành riêng cho dịch vụ EC2, Glue, và Lambda. | 27/4 |
| Thứ Ba | Khởi tạo các IAM Execution Roles chuyên dụng và gắn kèm các định nghĩa chính sách tương ứng. | 28/4 |
| Thứ Tư | Cấu hình các nhóm bảo mật Security Groups nền tảng độc lập cho các tầng Web, API, và Database. | 29/4 |
| Thứ Năm | Triển khai quy tắc lồng ghép Security Group lẫn nhau (nesting) để kiểm soát chặt chẽ luồng traffic giữa các tầng. | 30/4 |
| Thứ Sáu | Kích hoạt tính năng VPC Flow Logs để theo dõi luồng mạng và đẩy trực tiếp về Amazon CloudWatch. | 01/5 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Bản dự thảo chính sách IAM được phê duyệt, giới hạn nghiêm ngặt các hành động trên tài nguyên cụ thể.
  - Bài học: Áp dụng quyền hạn tối thiểu giúp thu hẹp tối đa phạm vi ảnh hưởng nếu thông tin xác thực vô tình bị lộ lọt.
- **Thứ Ba:**
  - Kết quả đạt được: Cấp phát thành công các vai trò hệ thống cho từng dịch vụ AWS và hoàn tất xác thực.
  - Bài học: Sử dụng IAM Role loại bỏ hoàn toàn nhu cầu lưu trữ khóa truy cập (Access Keys) dài hạn bên trong mã nguồn ứng dụng.
- **Thứ Tư:**
  - Kết quả đạt được: Các nhóm bảo mật phân tầng được khởi tạo thành công.
  - Bài học: Đặt các tầng ứng dụng phía sau các nhóm bảo mật riêng biệt tạo nên một bức tường phòng thủ chuyên sâu vững chắc.
- **Thứ Năm:**
  - Kết quả đạt được: Quy tắc lồng nhóm bảo mật hoạt động tốt (Tầng API chỉ chấp nhận dữ liệu đến từ tầng Web).
  - Bài học: Sử dụng Security Group ID làm điều kiện chặn lọc giúp hệ thống tự động giữ vững an ninh ngay cả khi tự động mở rộng instance (Auto Scaling).
- **Thứ Sáu:**
  - Kết quả đạt được: Hệ thống Flow Logs hoạt động ổn định, truyền dữ liệu thời gian thực về CloudWatch Logs.
  - Bài học: Ghi nhật ký mạng liên tục là điều kiện bắt buộc để phục vụ công tác giám sát an ninh và điều tra sự cố luồng đi.
