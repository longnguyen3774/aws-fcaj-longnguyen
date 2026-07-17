---
title: "Event 1"
date: 2026-06-06
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài Thu Hoạch: AWS FIRST CLOUD AI JOURNEY MEET UP

### Thông Tin Sự Kiện

| Thông tin | Chi tiết |
|-----------|----------|
| **Tên sự kiện** | AWS FIRST CLOUD AI JOURNEY MEET UP |
| **Thời gian** | 09:00, ngày 06/06/2026 |
| **Địa điểm** | Tầng 26, tòa nhà Bitexco, số 02 đường Hải Triều, phường Sài Gòn, TP. Hồ Chí Minh |
| **Vai trò** | Người tham dự |

---

## 1. Tọa Đàm Cùng Slavik Dimitrovich (AWS Principal Evangelist & Chuyên gia AI của FCJ)
*Người hỏi: Anh Long*

Anh Long đã đặt ra **3 câu hỏi lớn** mang tính thực tế cao về tương lai ngành lập trình, khoảng cách kỳ vọng công nghệ và lộ trình phát triển cho kỹ sư trẻ.

### 3 Câu Hỏi Lớn & Phân Tích Từ Chuyên Gia

#### Câu hỏi 1: Kỹ năng (skill) nào AI có thể thay thế, kỹ năng nào vẫn còn hữu ích (relevant) trong 5 năm tới?
*   **AI tối ưu hóa mức trung bình (leveraging the average):** AI đang thiết lập một tiêu chuẩn mới cho mức hiệu suất tối thiểu có thể chấp nhận được. Những người làm việc ở mức trung bình sẽ dễ dàng bị thay thế.
*   **Đừng làm việc chỉ vì lương (paycheck):** Những ai đang làm các công việc rập khuôn, chỉ để nhận lương tháng nên chủ động tìm kiếm những công việc phù hợp và mang lại nhiều giá trị hơn.
*   **Không ngừng xuất sắc (Continuously excellent):** Cách duy nhất để luôn đi trước AI là liên tục nâng cao năng lực để đạt đến sự xuất sắc.
*   **Chủ động đón đầu:** Hãy tự hỏi bản thân mỗi ngày: *"Làm thế nào tôi có thể sử dụng AI như một công cụ hỗ trợ để tối ưu hiệu suất?"*
*   **Cảnh giác với sự phụ thuộc:** Quá phụ thuộc vào AI sẽ dần làm cùn mòn tư duy phản biện và năng lực kỹ thuật tự thân của bạn.

#### Câu hỏi 2: Khoảng cách giữa kỳ vọng của doanh nghiệp và khả năng thực tế của AI là gì?
*   **Kỳ vọng của chủ doanh nghiệp:** Muốn tự động hóa hoàn toàn các quy trình vận hành (completely autonomous business processes).
*   **Thực tế:** Hiện tại vẫn chưa có một **khung đánh giá chuẩn chỉnh (evaluation framework)** để đo lường và bảo chứng cho độ tin cậy của các hệ thống tự vận hành hoàn toàn này.
*   **Giải pháp:**
    1.  **Áp dụng AI cho đội ngũ kỹ thuật trước:** Vì ở đây đã có sẵn các bộ chỉ số đo lường (evaluation metrics) rõ ràng.
    2.  **Chuẩn hóa hệ thống trước:** Hãy dọn dẹp và tối ưu hóa hạ tầng công nghệ (tech stack) trước khi tích hợp AI vào hệ thống (AI-infused).
*   **2 hướng phát triển dự án:**
    *   *Hướng 1:* Đi từ đam mê cá nhân.
    *   *Hướng 2:* Đi từ thực tế của khách hàng (những nỗi đau, bài toán lặp đi lặp lại mà bạn liên tục nhìn thấy từ khách hàng).

#### Câu hỏi 3: Nếu là một kỹ sư 25 tuổi ở thời điểm hiện tại, bác sẽ làm gì?
*   **Nhìn lại quá khứ:** 15 năm trước, Điện toán đám mây (Cloud) xuất hiện đã hạ thấp rào cản gia nhập thị trường phần mềm.
*   **Hiện tại:** AI xuất hiện và tiếp tục hạ thấp rào cản đó xuống sâu hơn nữa.
*   **Lời khuyên hành động:** Hãy bắt tay vào xây dựng ngay một vài quy trình kinh doanh nhỏ để thử nghiệm, tự vận hành và bắt đầu khởi nghiệp.

---

## 2. Phần Trình Bày Của Học Viên & Kỹ Sư Trẻ

### A. Sử dụng Agent trong Game Multiplayer
*Diễn giả: Quốc Bảo (Sinh viên Swinburne - Thuyết trình solo)*

Bạn Quốc Bảo đã trình bày phương pháp sử dụng kiến trúc **agents** (không phải AI Agents) để xử lý trạng thái trong trò chơi nhiều người chơi.

#### Phía Client (3 chức năng cốt lõi):
1.  Tạo kết nối bền vững với API.
2.  Liên tục kiểm tra (check) xem server có gửi dữ liệu gì về hay không.
3.  Gửi và nhận tín hiệu trực tiếp từ AWS Lambda.

#### Các thông điệp từ Server & Phản hồi của Client:
*   `Wait_for_opponent` (Chờ đối thủ)
*   `Match_found` (Đã tìm thấy trận)
*   `Wait_for_opponent_choice` (Chờ đối thủ lựa chọn)
*   `Result` (Kết quả)
*   `Opponent_disconnected` (Đối thủ mất kết nối)

---

### B. Đi sâu vào Docker: Bảo mật, Cổng kết nối và Tối ưu hóa
*Diễn giả: Bảo Huỳnh (Junior Cloud Native Developer tại Envada Vietnam - Gen Z 2k3, tốt nghiệp năm 2025, cựu thành viên NAB Innovation Center)*

> **Disclaimer:** Đây không phải là buổi hướng dẫn Docker cơ bản (Docker 101). Nội dung tập trung vào bảo mật, quản lý port, và tối ưu hóa image.

*   **Ảo hóa:** Tạo máy ảo Linux trên hệ điều hành Windows. Tất cả các tiến trình (processes) chạy bên trong máy ảo đều hoàn toàn độc lập.
*   **Hao phí tài nguyên:** Hệ điều hành (OS) tiêu tốn rất nhiều tài nguyên. Việc sử dụng toàn bộ một máy ảo chỉ để chạy các API chatbot là quá lãng phí (overkill).
*   **Tham số `--rm`:** Rất hữu ích khi test nhanh dưới local, nhưng **KHÔNG** được sử dụng trên môi trường production.
*   **Thực tế doanh nghiệp:** Khi vào công ty, hệ thống/sản phẩm thường đã có sẵn, công việc chính của bạn sẽ là bảo trì (maintenance).
*   **Hai vai trò của Docker:** Vừa dùng để đóng gói ứng dụng (build app), vừa làm môi trường cô lập an toàn (sandbox) để chạy thử nghiệm (ví dụ: phân tích mã độc/virus).
*   **Lĩnh vực Security:** Nếu định hướng làm về bảo mật, bạn sẽ phải làm việc với Docker Container rất nhiều.
*   **Lưu ý về dữ liệu:** Dữ liệu trong container nếu không được gắn (mount) ra thư mục local thông qua **Volume** thì khi tắt/xóa container, toàn bộ dữ liệu đó sẽ bị mất sạch.

---

### C. Giải quyết hạn chế của RAG bằng GraphRAG
*Diễn giả: Phát (Sinh viên Swinburne - Thực tập sinh tại NAB)*

*   **Hạn chế của RAG truyền thống:** Chỉ tìm kiếm dựa trên ngữ nghĩa (semantic similarity) mà thiếu đi mối quan hệ (relationship) giữa các thực thể, đồng thời các phân đoạn dữ liệu (chunks) dễ bị phân mảnh.
*   **Giải pháp:** Sử dụng GraphRAG để mô hình hóa dữ liệu dạng đồ thị, giúp kết nối thông tin logic và chặt chẽ hơn.

---

### D. Đối mặt với Overfitting trong Machine Learning
*Diễn giả: Đại*

*   Bạn Đại đặt ra 2 câu hỏi chuyên sâu và **thẳng thắn thừa nhận** bản thân hiện tại chưa có đủ kiến thức và kỹ năng chuyên môn để giải quyết triệt để vấn đề Overfitting (quá khớp) trong mô hình ML. Điều này thể hiện tinh thần cầu tiến rất tốt.

---

## 3. Kinh Nghiệm Vận Hành Hệ Thống & Chiến Thuật Phỏng Vấn
*Chia sẻ bởi: Anh Vinh (SysAdmin - Central Retail Group, 5 năm kinh nghiệm IT Helpdesk)*

### Các sự cố thực tế (Áp lực Vận hành & Trực On-call)
Anh Vinh chia sẻ những sự cố "xương máu" mang đậm tính chất vận hành (khá tương đồng với trải nghiệm của Duy):

*   **Sự cố 1: Nghẽn kết nối tại FE Credit**
    *   *Tình huống:* Toàn bộ lượng người dùng đồng thời (concurrent users) cùng thực hiện đăng nhập vào hệ thống tại một thời điểm.
    *   *Hậu quả:* Hệ thống quá tải dẫn đến Timeout và downtime toàn diện.
    *   *Áp lực:* Doanh nghiệp thất thoát doanh thu nghiêm trọng do nhân viên không thể truy cập hệ thống để làm việc.
*   **Sự cố 2: Cảnh báo phần cứng ảo (Phantom Hardware Alert)**
    *   *Tình huống:* Hệ thống liên tục gửi cảnh báo (alert), nhưng khi vào kiểm tra thủ công (troubleshoot) thì không phát hiện lỗi vật lý nào.
    *   *Nguyên nhân:* Chỉ số hàng đợi đọc/ghi ổ cứng (disk queue waiting status) vượt ngưỡng 100% – vượt quá khả năng xử lý của phần cứng hiện tại.
    *   *Thách thức:* Để thay thế ổ cứng bị nghẽn này, hệ thống buộc phải dừng hoạt động (downtime) trong 2 ngày – điều mà ban giám đốc hoàn toàn không chấp nhận vì thiệt hại quá lớn.

---

### Kinh nghiệm Phỏng vấn & Phát triển Sự nghiệp

*   **Ôn tập trọng tâm:** Tập trung ôn luyện kỹ các kiến thức liên quan trực tiếp đến vị trí ứng tuyển.
*   **Tìm hiểu Tech Stack thực tế:** Tìm hiểu các công nghệ thực tế doanh nghiệp đang dùng. Nếu bảng mô tả công việc (JD) không ghi rõ, hãy tìm kiếm chức danh tương tự của công ty đó trên LinkedIn để xem các kỹ sư hiện tại đang làm việc với những công cụ nào.
*   **Tỷ lệ 30/70:** Quá trình phỏng vấn thường gồm **30% kỹ thuật chuyên môn** và **70% là tư duy hệ thống & Mindset** (ví dụ: *Khi hệ thống AI gặp sự cố, bạn sẽ tiếp cận và xử lý nó như thế nào?*).
*   **Mô tả chi tiết cách sửa lỗi:** Hãy trình bày thật chi tiết và logic quá trình bạn tư duy, cô lập vùng lỗi và troubleshoot một sự cố trong quá khứ.
*   **Làm các dự án End-to-End:** Để triển khai một sản phẩm thương mại điện tử thực tế cần rất nhiều cấu phần: FE, BE, Database clustering, Monitoring,... Bạn nên tự làm nhiều bài lab và các dự án hoàn chỉnh (end-to-end) để bù đắp cho việc thiếu hụt kinh nghiệm làm việc thực tế.
*   **Đừng sợ phỏng vấn:** Nếu có cơ hội, hãy cứ mạnh dạn đi phỏng vấn ở nhiều nơi. Điều này giúp bạn tích lũy kinh nghiệm cọ xát và nắm bắt được nhu cầu thực tế của thị trường tuyển dụng.

---

### Hình Ảnh Sự Kiện

![AWS First Cloud AI Journey Workshop](/images/event1.jpg)