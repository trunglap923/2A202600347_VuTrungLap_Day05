# UX Exercise — Vietnam Airlines Chatbot NEO

**Học viên:** Vũ Trung Lập

**Sản phẩm phân tích:** Vietnam Airlines — Chatbot NEO

**Truy cập:** [vietnamairlines.com](https://www.vietnamairlines.com/vn/vi/home)

---

## Phần 1 — Khám phá

### Marketing hứa gì?

Vietnam Airlines quảng bá NEO là **"trợ lý ảo thông minh 24/7"**, hỗ trợ khách hàng:

- Tra cứu chuyến bay, lịch trình, giá vé
- Hỗ trợ check-in online
- Giải đáp thắc mắc về hành lý, quy định
- Hỗ trợ đặt vé, thay đổi chuyến bay
- Hoạt động đa nền tảng: website + Zalo OA

**Kỳ vọng từ marketing:** NEO là chatbot AI có khả năng hiểu ngôn ngữ tự nhiên, trả lời linh hoạt, thay thế tổng đài truyền thống.

### Thực tế khi dùng thử

Khi truy cập website, NEO hiện dưới dạng **widget chat góc trái dưới** với nội dung "Chat với NEO". Trước khi sử dụng, user phải đồng ý điều khoản bảo mật và bấm "BẮT ĐẦU".

**Quan sát chính:**

| Đặc điểm         | Mô tả                                                                      |
| ---------------- | -------------------------------------------------------------------------- |
| Kiểu chatbot     | **Task-based + Rule-based**, không phải AI generative                      |
| Giao diện        | Có nút gợi ý nhanh (quick replies): Đặt vé, Check-in, Hành lý, FAQ         |
| Ngôn ngữ         | Hỗ trợ Tiếng Việt + Tiếng Anh                                              |
| Nhận diện intent | Dựa trên **keyword matching**, không phải NLU sâu                          |
| Response style   | Trả lời bằng template cố định, kèm link điều hướng đến trang web tương ứng |
| Cá nhân hóa      | **Không có** — không nhớ lịch sử, không đề xuất theo ngữ cảnh              |

---

## Phần 2 — Phân tích 4 Paths

### Path 1: Khi AI đúng ✅

**Tình huống:** Hỏi "Tôi muốn check-in online" hoặc "Quy định hành lý xách tay"

- NEO nhận đúng intent → trả về **link trực tiếp** đến trang check-in / trang quy định hành lý
- Response nhanh (< 2 giây), các bước rõ ràng
- User click link → được chuyển đến trang đúng trên website VNA

**Nhận xét:** Path này NEO xử lý **tốt nhất**. Với các câu hỏi FAQ phổ biến (check-in, hành lý, giá vé nội địa), NEO hoạt động như một **bảng điều hướng thông minh** — tìm nhanh hơn tự tìm trên menu website. Đây là value chính của NEO ở thời điểm hiện tại.

---

### Path 2: Khi AI không chắc ⚠️

**Tình huống:** Hỏi mơ hồ như "Tôi muốn đi Đà Nẵng" (thiếu ngày, thiếu điểm khởi hành) hoặc dùng ngôn ngữ tự nhiên phức tạp

- NEO **không hỏi lại** để clarify thông tin thiếu
- Thay vào đó, trả về **câu trả lời chung chung** hoặc gợi ý một danh sách topic mặc định
- Không hiển thị confidence score hay alternatives cho user chọn
- Trong một số trường hợp, NEO **im lặng hoàn toàn** — không phản hồi gì

**Nhận xét:** Đây là **path yếu nhất** của NEO. Một chatbot AI tốt khi không chắc chắn nên chủ động hỏi lại: _"Bạn muốn đi ngày nào?"_, _"Khởi hành từ đâu?"_. NEO thiếu hoàn toàn cơ chế **clarification loop** — khi không hiểu thì bế tắc, user phải tự đoán cách hỏi lại cho đúng format.

---

### Path 3: Khi AI sai ❌

**Tình huống:** Hỏi "Chuyến bay HN đi HCM giá rẻ nhất tuần sau" → NEO trả lời thông tin không liên quan hoặc sai context

- NEO **không có cơ chế báo lỗi** — không nói "Tôi không chắc" hay "Kết quả có thể không chính xác"
- User phải **tự nhận ra** câu trả lời sai bằng kinh nghiệm
- **Không có nút "Sai rồi"** hay "Report" để user phản hồi
- **Không có nút thumbs up/down** sau mỗi câu trả lời
- Để sửa, user phải **hỏi lại từ đầu** bằng cách diễn đạt khác → mất thời gian, gây frustration

**Nhận xét:** NEO thiếu hoàn toàn **error recovery flow**. Khi sai, user không có cách nào thông báo cho hệ thống. So sánh với ChatGPT hay Google Bard đều có nút 👍👎 sau mỗi response — NEO không có bất kỳ feedback mechanism nào.

---

### Path 4: Khi user mất niềm tin 😤

**Tình huống:** Sau 2-3 lần NEO trả lời sai hoặc không hiểu, user muốn gặp nhân viên thật

- NEO **có hiển thị** option chuyển sang tổng đài / nhân viên, nhưng:
  - Không phải lúc nào cũng hiện rõ
  - Phải hỏi đúng từ khóa ("gặp nhân viên", "tổng đài") mới kích hoạt
  - Không có nút **"Gặp nhân viên"** luôn hiện trên giao diện
- Không có option **"Tắt chatbot, dùng tìm kiếm thường"**
- Fallback duy nhất: user **tự thoát chatbot** và gọi hotline 1900 1100

**Nhận xét:** NEO thiếu **graceful degradation**. Theo framework từ bài giảng, khi user mất tin, product phải có exit rõ ràng và fallback dễ tìm (Google PAIR Guidebook). NEO buộc user phải tự tìm cách thoát — tạo trải nghiệm tiêu cực.

---

### Tổng hợp 4 Paths

| Path              | Chất lượng | Ghi chú                                               |
| ----------------- | ---------- | ----------------------------------------------------- |
| 1 — AI đúng       | ⭐⭐⭐⭐   | Tốt với FAQ & điều hướng cơ bản                       |
| 2 — AI không chắc | ⭐         | **Yếu nhất** — không hỏi lại, không show alternatives |
| 3 — AI sai        | ⭐⭐       | Không có error recovery, không có feedback mechanism  |
| 4 — User mất tin  | ⭐⭐       | Fallback tồn tại nhưng khó tìm, không proactive       |

**Path yếu nhất: Path 2 (AI không chắc)**

- NEO là rule-based nên khi intent nằm ngoài rule set → không có output nào
- Không có mechanism để hỏi lại, gợi ý alternatives, hay show confidence
- User bế tắc hoàn toàn, không biết phải làm gì tiếp

---

## Gap: Marketing vs Thực tế

|                   | Marketing                                                                 | Thực tế                                                                                  |
| ----------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Định vị**       | "Trợ lý ảo thông minh" — gợi ý NEO có khả năng AI, hiểu ngôn ngữ tự nhiên | **Rule-based chatbot** — hoạt động dựa trên keyword matching và decision tree cố định    |
| **Phạm vi**       | Hứa hỗ trợ "mọi nhu cầu" từ đặt vé đến thay đổi chuyến bay                | Chỉ **điều hướng** đến trang web tương ứng, không thực sự thực hiện giao dịch trong chat |
| **Trải nghiệm**   | "24/7, nhanh chóng, tiện lợi"                                             | Nhanh với FAQ đơn giản, **bế tắc** với câu hỏi phức tạp hoặc mơ hồ                       |
| **AI capability** | Gợi ý "trí tuệ nhân tạo"                                                  | Không có NLU sâu, không có learning từ user interaction, không cá nhân hóa               |

**Gap lớn nhất:** Marketing dùng từ "AI" và "trợ lý ảo thông minh" tạo kỳ vọng user rằng NEO hiểu ngôn ngữ tự nhiên như ChatGPT. Thực tế, NEO là **keyword-based routing tool** — hoạt động tốt khi user biết cách hỏi đúng format, nhưng thất bại khi user nói tự nhiên. Khoảng cách giữa kỳ vọng (100% hiểu mọi câu) và thực tế (~60-70% intent đơn giản) tạo frustration cho user.

---

## Sketch

_(Xem file đính kèm: sketch.jpg)_
