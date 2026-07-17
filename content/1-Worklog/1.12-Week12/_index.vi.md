---
title: "Tuần 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

**Mục tiêu tuần:**
- Tự động hóa hoàn toàn chuỗi quy trình xử lý dữ liệu đầu cuối sử dụng công cụ điều phối Amazon EventBridge Scheduler.
- Xây dựng hệ thống bảng điều khiển trung tâm Amazon CloudWatch Dashboards cùng các cơ chế cảnh báo tự động khi có sự cố.
- Tiến hành kiểm thử nghiệm thu toàn diện hệ thống và thực hiện quy trình dọn dẹp, tối ưu hóa các tài nguyên cloud dư thừa.

**Các công việc cần triển khai trong tuần này:**

| Thứ | Công việc | Ngày |
|---|---|---|
| Thứ Hai | Thiết lập cấu hình các quy tắc lịch trình trong Amazon EventBridge Scheduler để kích hoạt tự động chuỗi quy trình vào khung giờ thấp điểm. | 06/7 |
| Thứ Ba | Liên kết các luồng sự kiện để EventBridge tự động gọi tuần tự từ tiến trình Glue sang máy chủ huấn luyện `ML-Forecast-Server`. | 07/7 |
| Thứ Tư | Xây dựng bảng điều khiển trung tâm Amazon CloudWatch Dashboard trực quan hóa tổng thể trạng thái Web, hiệu năng ETL và ML. | 08/7 |
| Thứ Năm | Cấu hình dịch vụ Amazon SNS gửi thông báo khẩn cấp trực tiếp về email của quản trị viên khi có bất kỳ sự cố dừng chạy ở tầng API hay ETL. | 09/7 |
| Thứ Sáu | Thực hiện bài kiểm thử nghiệm thu tổng thể chạy mượt mà từ đầu đến cuối và tiến hành thu hồi các tài nguyên lưu trữ tạm thời. | 10/7 |

**Kết quả đạt được trong tuần là gì:**
- **Thứ Hai:**
  - Kết quả đạt được: Lịch trình tự động chạy hàng ngày được thiết lập kích hoạt thành công trên nền tảng EventBridge.
  - Bài học: Cơ chế điều phối tự động dựa trên sự kiện loại bỏ hoàn toàn các thao tác thủ công, đảm bảo các dự báo kinh doanh luôn được cập nhật mới liên tục mỗi ngày.
- **Thứ Ba:**
  - Kết quả đạt được: Chuỗi quy trình liên kết tuần tự hoạt động chuẩn xác: dữ liệu làm sạch xong mới kích hoạt tiến trình học máy chạy huấn luyện.
  - Bài học: Ràng buộc các bước chạy theo chuỗi logic giúp ngăn chặn triệt để tình trạng mô hình học máy học sai kiến thức do nạp phải các tập dữ liệu rỗng hoặc lỗi.
- **Thứ Tư:**
  - Kết quả đạt được: Bảng giám sát trực quan hóa trực tuyến hoạt động ổn định, cung cấp cái nhìn toàn cảnh về tình trạng sức khỏe của hệ thống hạ tầng cloud.
  - Bài học: Tập trung hóa các chỉ số đo đạc trên một màn hình duy nhất giúp các kỹ sư vận hành hệ thống nhanh chóng phát hiện điểm nghẽn và gỡ lỗi khi có sự cố.
- **Thứ Năm:**
  - Kết quả đạt được: Hệ thống cảnh báo SNS hoạt động chính xác, gửi email thông báo phản hồi tức thì khi có kịch bản giả lập lỗi xảy ra.
  - Bài học: Cơ chế chủ động đưa ra cảnh báo lỗi giúp đội ngũ kỹ thuật có thể can thiệp xử lý kịp thời trước khi sự cố gây ảnh hưởng đến hoạt động vận hành của doanh nghiệp.
- **Thứ Sáu:**
  - Kết quả đạt được: Toàn bộ hệ thống vượt qua bài kiểm tra nghiệm thu tổng thể, các tệp dữ liệu rác được dọn dẹp sạch sẽ để tối ưu hóa hóa đơn chi phí.
  - Bài học: Hoạt động dọn dẹp định kỳ các tài nguyên lưu trữ tạm thời trên cloud là một quy trình bắt buộc giúp duy trì hệ thống luôn gọn nhẹ và tiết kiệm ngân sách dài hạn.
