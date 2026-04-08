# UX exercise — Vietnam Airlines Chatbot NEO

## Sản phẩm: Vietnam Airlines — Chatbot NEO (tra cứu chuyến bay, hỗ trợ khách hàng)

## 4 paths

### 1. AI đúng

- User hỏi "Tôi muốn check-in online" hoặc "Quy định hành lý xách tay"
- NEO nhận đúng intent → trả về link trực tiếp đến trang tương ứng trên website VNA
- UI: response nhanh (<2 giây), hiện quick reply buttons + link điều hướng, không cần confirm thêm
- Hoạt động như **bảng điều hướng thông minh** — tìm nhanh hơn tự lục menu website

### 2. AI không chắc

- User hỏi mơ hồ: "Tôi muốn đi Đà Nẵng" (thiếu ngày, thiếu điểm khởi hành) hoặc ngôn ngữ tự nhiên phức tạp
- NEO **không hỏi lại** để clarify — trả về câu trả lời chung chung hoặc gợi ý danh sách topic mặc định
- Trong một số trường hợp, NEO **im lặng hoàn toàn** — không phản hồi gì
- Vấn đề: thiếu hoàn toàn **clarification loop** — không có cơ chế "Bạn muốn đi ngày nào?", "Khởi hành từ đâu?"
- User phải tự đoán cách hỏi lại cho đúng format

### 3. AI sai

- User hỏi "Chuyến bay HN đi HCM giá rẻ nhất tuần sau" → NEO trả thông tin sai context hoặc không liên quan
- User phải **tự nhận ra** câu trả lời sai bằng kinh nghiệm — NEO không nói "Tôi không chắc"
- Sửa: phải **hỏi lại từ đầu** bằng cách diễn đạt khác → mất thời gian, gây frustration
- Vấn đề: không có nút 👍👎 sau response, không có "Sai rồi" hay "Report" → không feedback mechanism nào
- So sánh: ChatGPT, Google Bard đều có feedback buttons — NEO không có

### 4. User mất niềm tin

- Sau 2-3 lần NEO trả sai, user muốn gặp nhân viên thật
- NEO có option chuyển tổng đài nhưng: phải hỏi đúng keyword ("gặp nhân viên"), không có nút luôn hiện trên giao diện
- Không có option "Tắt chatbot, dùng tìm kiếm thường"
- Fallback duy nhất: user tự thoát chatbot → gọi hotline 1900 1100
- Vấn đề: thiếu **graceful degradation** — khi user mất tin, product phải có exit rõ ràng và fallback dễ tìm

## Path yếu nhất: Path 2 + 3

- NEO là rule-based/keyword matching → khi intent nằm ngoài rule set, bế tắc hoàn toàn
- Không có mechanism hỏi lại, show alternatives, hay show confidence
- Khi AI sai, error recovery mất quá nhiều bước — phải hỏi lại từ đầu
- Không có feedback loop rõ — user sửa nhưng NEO không ghi nhận, không học

## Gap marketing vs thực tế

- Marketing: "Trợ lý ảo **thông minh** 24/7" — gợi ý NEO hiểu ngôn ngữ tự nhiên như AI thật
- Thực tế: **keyword-based routing tool** — hoạt động dựa trên keyword matching + decision tree cố định,
  không có NLU sâu, không learning từ user interaction, không cá nhân hóa
- Gap lớn nhất: marketing dùng từ "AI" tạo kỳ vọng user rằng NEO hiểu mọi câu hỏi tự nhiên.
  Thực tế chỉ đúng ~60-70% intent đơn giản, FAQ phổ biến → frustration khi user nói tự nhiên

## Sketch

(Ảnh đính kèm: sketch.pdf)

- As-is: user hỏi → NEO nhận keyword → trả link/template → nếu không hiểu: im lặng hoặc trả generic → user bế tắc
- To-be: user hỏi → NEO nhận keyword → nếu confidence thấp: hiện "Bạn có thể nói rõ hơn?" + gợi ý 3 intent gần nhất
  → user chọn/clarify → NEO trả lời đúng hơn → cuối response hiện 👍👎 → AI ghi nhận để cải thiện
