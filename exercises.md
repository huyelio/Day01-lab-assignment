# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi tăng temperature từ 0.0 lên 1.5, câu trả lời có xu hướng đa dạng chủ đề hơn (bờ biển/Vịnh Hạ Long, cà phê trứng, Sơn Đoòng) thay vì lặp cùng một khuôn. Ở mức thấp (0.0), văn phong ổn định và "an toàn", còn mức cao (1.0–1.5) linh hoạt và sáng tạo hơn nhưng đôi khi dễ lan man hoặc ít nhất quán hơn. Với prompt này, 0.5–1.0 cho cảm giác cân bằng tốt giữa độ tự nhiên và độ kiểm soát.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi chọn khoảng **0.2–0.4** (mặc định 0.3) để câu trả lời nhất quán, hạn chế "bịa" thông tin và giữ giọng điệu ổn định. Chatbot CSKH cần độ chính xác và khả năng lặp lại cao hơn là sáng tạo.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Tổng output token/ngày = 10.000 người * 3 lần gọi * 350 token = **10.500.000 token/ngày** = 10.500 đơn vị "1K token".  
> - GPT-4o: 10.500 * $0.010 = **$105.00/ngày**  
> - GPT-4o-mini: 10.500 * $0.0006 = **$6.30/ngày**  
> => GPT-4o đắt hơn khoảng **16.7 lần** (chênh **$98.70/ngày**).

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi xử lý tác vụ độ quan trọng cao như tư vấn tài chính/pháp lý nội bộ, nơi cần lập luận chắc chắn và chất lượng đầu ra cao vì sai sót gây thiệt hại lớn.  
> GPT-4o-mini phù hợp cho workload lớn, lặp lại và độ rủi ro thấp như FAQ, phân loại ticket cơ bản, tóm tắt nội dung ngắn — nơi tốc độ và chi phí là ưu tiên.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi phản hồi dài hoặc người dùng cần cảm giác "hệ thống đang trả lời ngay" (chatbot hỗ trợ trực tiếp, trợ lý viết nội dung, phiên dịch/tương tác thời gian thực), vì nó giảm thời gian chờ cảm nhận và tăng trải nghiệm mượt. Ngược lại, non-streaming phù hợp khi cần xử lý trọn vẹn trước khi hiển thị (ví dụ: trả về JSON chuẩn, kết quả cần hậu kiểm/kiểm duyệt, hoặc tác vụ backend không có UI thời gian thực), giúp đơn giản hóa logic hiển thị và xử lý lỗi.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
