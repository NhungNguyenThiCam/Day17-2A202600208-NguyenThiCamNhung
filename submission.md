# Day 17 Submission
**Student:** Nguyễn Thị Cẩm Nhung
**Mã học viên:** 2A202600208
**Date:** 24/04/2026
**Product idea:** Trợ lý AI định vị tri thức đa phương thức trong video bài giảng, giúp sinh viên tìm kiếm kiến thức bằng ngôn ngữ tự nhiên và nhận được Visual Citation kèm timestamp chính xác.

**Link to Day 16 Package:** *(Nếu có, paste link GitHub Day 16 ở đây để thể hiện story consistency)*

---

## 0. Tại sao mỗi tính năng In-Scope không thể cắt thêm

**Kill Question Test:** *"Nếu cắt thêm 1 tính năng trong In-Scope, khách hàng còn nhận được giá trị cốt lõi không?"*

### Nếu cắt "Multimodal Search-in-Video":
❌ **Không thể cắt** — Đây là tính năng cốt lõi. Không có search, sản phẩm không tồn tại. Sinh viên sẽ phải quay lại cách cũ: kéo timeline thủ công hoặc xem lại toàn bộ video.

### Nếu cắt "Visual Citation & Timestamp":
❌ **Không thể cắt** — Đây là điểm khác biệt duy nhất so với ChatGPT/Gemini thông thường. Không có Visual Citation, sinh viên sẽ không tin AI (vì sợ ảo giác) → không dùng sản phẩm. Riskiest Assumption sẽ không được test.

### Nếu cắt "Official Material Ingestion":
❌ **Không thể cắt** — Không có tích hợp LMS, sinh viên phải tự upload video (friction cao) và không có "trust signal" rằng đây là học liệu chính thức từ trường. Adoption rate sẽ thấp (<20% theo Hypothesis 3).

**Kết luận:** Cả 3 tính năng đều bắt buộc. Đây là MVP "thật" — cắt thêm bất kỳ thứ gì sẽ làm sản phẩm mất giá trị cốt lõi.

---

## 1. MVP Boundary Sheet

**Riskiest Assumption:**
> Sinh viên thực sự tin tưởng và sẵn sàng học theo chỉ dẫn của AI khi có bằng chứng trực quan (Visual Citation) đi kèm, thay vì cảm thấy bất an vì sợ AI ảo giác.

**In-Scope** (tối đa 3):
- [x] **Multimodal Search-in-Video (RAG)** — test giả định: Người dùng có thể tìm kiến thức bằng ngôn ngữ tự nhiên và AI định vị được chính xác đoạn video có lời giảng tương ứng.
- [x] **Visual Citation & Timestamp Link** — test giả định: Việc hiển thị đúng frame Slide kèm nút "nhảy" đến giây/phút cụ thể giúp sinh viên xác thực tri thức tức thì và tiết kiệm thời gian "scrubbing" thủ công.
- [x] **Official Material Ingestion** — test giả định: Hệ thống có thể xử lý mượt mà học liệu từ 01 nguồn chính (Video bài giảng từ Zoom/LMS) để đảm bảo tính "chính chủ" của kiến thức.

**Out-of-Scope:**
- **Multi-language Support** (Dịch bài giảng) — lý do bỏ: Cần ưu tiên độ chính xác của ngôn ngữ gốc trước khi xử lý dịch thuật để tránh sai sót chuyên môn.
- **AI Note-taking & Summarization** (Tóm tắt ra PDF) — lý do bỏ: Đã có nhiều công cụ làm tốt; MVP cần tập trung vào sự khác biệt là "Định vị tri thức đa phương thức".
- **Mobile App & Community** (App di động và diễn đàn) — lý do bỏ: SV thường học bài tập trung trên máy tính; cần tối ưu trải nghiệm Web/Plugin trước để nhanh chóng ra mắt.

**Non-Goals:**
- **Exam & Homework Solver** (Giải hộ bài tập) — Lý do: Đảm bảo đạo đức học thuật và tránh rủi ro pháp lý/bị nhà trường cấm cửa.
- **Content Creation** (AI tự tạo bài giảng mới) — Lý do: Sản phẩm chỉ là trợ lý định vị dựa trên kiến thức của giảng viên, không phải nguồn tạo tri thức mới.
- **LMS Replacement** (Thay thế hệ thống của trường) — Lý do: Chúng ta là lớp bổ trợ (Add-on), không phải đối thủ của hệ thống hạ tầng có sẵn.
- **Real-time Lecture Transcription** (Phiên âm trực tiếp trong lúc học) — Lý do: Team rất muốn làm tính năng này để tăng engagement, nhưng nó không test được giả định cốt lõi về "Visual Citation giúp tăng trust". Phải chờ đến sau MVP.

---

## 2. PRD Skeleton

### Problem Statement
> Sinh viên mất quá nhiều thời gian để định vị kiến thức cụ thể trong kho video bài giảng dài và thiếu tin tưởng vào câu trả lời của AI nếu không có bằng chứng trực quan đi kèm.

### Target User
> **Sinh viên Đại học khối ngành nặng (STEM, Y Dược, Kinh tế)** thuộc nhóm **Persona D & E từ Day 16**, đối mặt với áp lực ôn thi cao điểm và học liệu khổng lồ.
> 
> **Mapping từ Day 16:**
> - **Customer Segment:** Sinh viên năm 3-4, có GPA > 3.0, mục tiêu tốt nghiệp loại Giỏi hoặc thi vào chương trình sau đại học
> - **Underserved Need (từ Need Map Day 16):** "Tìm kiếm kiến thức cụ thể trong video bài giảng dài mất quá nhiều thời gian" (Importance: 9/10, Satisfaction: 3/10 → Gap: 6 điểm)

### User Stories

**Story 1:**
> As a Medical Student, I want to search for a specific clinical symptom in a 2-hour lecture video, so that I can instantly jump to the exact moment the professor explains it with the corresponding slide frame.

**Story 2:**
> As a STEM Student, I want the AI to provide a "Visual Citation" (screenshot of the lecture slide) alongside its text answer, so that I can verify the accuracy of the information against official course materials.

### MVP Scope
*(Đã được định nghĩa chi tiết trong phần 1 — MVP Boundary Sheet)*

### AI-Specific

**Model Selection:**
- **Model:** Gemini 2.5 Flash
- **Lý do chọn:** Có khả năng xử lý context window cực lớn (1M-2M tokens), hỗ trợ Native Multimodal (hiểu trực tiếp Video và Audio mà không cần qua bước chuyển text trung gian), giúp giữ nguyên ngữ cảnh hình ảnh và lời giảng tốt hơn.
- **Trade-offs chấp nhận:** Độ trễ (latency) khi xử lý file video nặng có thể cao hơn so với chỉ xử lý text (chấp nhận được vì use-case là async search, không phải real-time chat).
- **Trade-offs không chấp nhận:** Ảo giác (Hallucination) về kiến thức chuyên môn; không chấp nhận việc AI trả lời thiếu căn cứ từ học liệu gốc.
- **Backup plan:** Nếu Gemini 2.5 Flash không đáp ứng về accuracy, sẽ chuyển sang GPT-4o với Vision API (trade-off: đắt hơn 3x nhưng hallucination thấp hơn dựa trên benchmark). Nếu budget không đủ, fallback về Claude 3.5 Sonnet với chunking strategy.

**Data Requirements:**
- **Nguồn:** Hệ thống quản lý học tập (LMS - Moodle/Canvas) của trường; Dữ liệu Video từ Zoom/Teams bài giảng; Slide bài giảng (PDF/PPT) đi kèm.
- **Owner:** Nhà trường/Giảng viên (Dự án tích hợp qua API).
- **Update frequency:** Ngay khi buổi học kết thúc và video được upload lên LMS.
- **Quality control:** Giảng viên và đội ngũ kỹ thuật của trường chịu trách nhiệm kiểm tra chất lượng video và slide trước khi đưa vào hệ thống.

**Fallback UX:**
- **Chiến lược:** Expectation Management & Cross-verification (Xác thực chéo)
- **Trigger (cụ thể):** 
  - **Confidence Score < 75%** (dựa trên cosine similarity giữa query embedding và retrieved chunk)
  - **Audio-Visual Mismatch:** Khi transcript từ audio không chứa từ khóa xuất hiện trên slide OCR (hoặc ngược lại)
  - **Zero Retrieval:** Không tìm thấy chunk nào có similarity > 0.5
- **Hành động:**
  1. **Nếu không có thông tin (Zero Retrieval):** AI thông báo rõ: *"Thông tin này không xuất hiện trong nội dung video bài giảng hiện tại"* và gợi ý tìm trong kho bài giảng cũ hoặc PDF liên quan.
  2. **Nếu tin cậy thấp (Confidence 50-75%):** Hiển thị mờ (Grey out) câu trả lời hoặc gắn nhãn *"⚠️ Gợi ý tham khảo - Độ tin cậy: 68%"*.
  3. **Nếu tin cậy cao (>75%):** Hiển thị bình thường với badge *"✓ Độ tin cậy: 92%"*
- **Thiết kế chống "ngáo" (Anti-Hallucination):** Hiển thị thông báo: *"Hệ thống tìm thấy nội dung trong Audio nhưng không khớp với văn bản trên Slide. 👉 [Nhấn để nghe lại đoạn 14:25] để đảm bảo không bị nhầm lẫn!"*
- **User có thể override AI:** Có — Sinh viên có thể:
  - Bấm "Báo cáo sai" → Gửi feedback để improve model
  - Bấm "Tìm thủ công" → Chuyển sang chế độ timeline scrubbing truyền thống
  - Bấm "Xem thêm kết quả" → Hiển thị top 3 chunks thay vì chỉ 1

### Success Metrics
- **Primary metric:** Time-to-Key-Knowledge (Thời gian trung bình để SV tìm thấy đoạn video chứa câu trả lời)
- **Ngưỡng thành công:** < 10 giây/truy vấn
- **Timeframe đo lường:** Theo dõi sau 02 đợt thi học kỳ (6 tháng)

### Dependencies & Constraints
- **API / Service cần tích hợp:** API của hệ thống LMS (Moodle/Canvas), Zoom API để lấy video recording, OCR service cho slide extraction
- **Timeline constraint:** Phải hoàn thành MVP trước đợt thi giữa kỳ (3 tháng) để có đủ dữ liệu validation
- **Budget constraint:** Chi phí API multimodal cần được tối ưu để giá thành phù hợp với sinh viên (< 50k VND/tháng/user)
- **Legal / Compliance constraint:** 
  - Bảo mật dữ liệu nội bộ của trường đại học (GDPR/PDPA compliance)
  - Quyền sở hữu trí tuệ của nội dung bài giảng thuộc về giảng viên và nhà trường
  - Cần thỏa thuận rõ ràng về việc xử lý và lưu trữ dữ liệu học tập

---

## 3. Hypothesis Table

### Hypothesis 1 (cho tính năng Search-in-Video)

**Tính năng:** Multimodal Search-in-Video (RAG)

**Hypothesis:**
> "Chúng tôi tin rằng tính năng truy vấn nội dung video bằng ngôn ngữ tự nhiên sẽ giúp sinh viên khối ngành nặng đạt được việc tiết kiệm 80% thời gian tìm kiếm kiến thức để ôn thi. Chúng tôi sẽ biết mình đúng khi thấy thời gian trung bình để tìm thấy 1 kiến thức (Time-to-Answer) đạt dưới 10 giây **trong vòng 2 tuần đầu tiên** triển khai Pilot với 50 sinh viên."

**Riskiest Assumption phía sau hypothesis này:**
> Sinh viên tin tưởng vào độ chính xác của đoạn video AI tìm được mà không cần phải xem lại toàn bộ bài giảng từ đầu.

**Cách test assumption này với chi phí thấp nhất:**
> Tạo một Landing Page giới thiệu tính năng, cho phép sinh viên upload 1 đoạn video bài giảng và dùng nhân sự (Wizard of Oz MVP) để trả về timestamp thủ công xem họ có thực sự thấy hữu ích và sẵn sàng trả phí không.

---

### Hypothesis 2 (cho tính năng Visual Citation)

**Tính năng:** Visual Citation & Timestamp Link

**Hypothesis:**
> "Chúng tôi tin rằng việc hiển thị Visual Citation (frame slide + timestamp) sẽ giúp sinh viên khối ngành nặng đạt được sự tin tưởng cao hơn 60% so với chatbot text-only. Chúng tôi sẽ biết mình đúng khi thấy tỷ lệ click vào timestamp link đạt trên 70% **trong vòng 4 tuần đầu tiên** sử dụng."

**Riskiest Assumption phía sau hypothesis này:**
> Sinh viên thực sự cần "nhìn thấy bằng chứng" để tin tưởng AI, chứ không chỉ đọc text answer là đủ.

**Cách test assumption này với chi phí thấp nhất:**
> A/B test giữa 2 phiên bản: Version A (chỉ có text answer) vs Version B (text answer + screenshot slide + timestamp). Đo lường tỷ lệ sinh viên quay lại sử dụng lần 2 và satisfaction score.

---

### Hypothesis 3 (cho tính năng Official Material Ingestion)

**Tính năng:** Official Material Ingestion from LMS

**Hypothesis:**
> "Chúng tôi tin rằng việc tích hợp trực tiếp với LMS của trường sẽ giúp sinh viên khối ngành nặng đạt được sự yên tâm về tính 'chính chủ' của kiến thức và tăng adoption rate lên 50% so với việc phải tự upload file. Chúng tôi sẽ biết mình đúng khi thấy tỷ lệ sinh viên active users đạt trên 40% trong trường có tích hợp LMS so với 20% ở trường không tích hợp, **đo lường sau 8 tuần triển khai**."

**Riskiest Assumption phía sau hypothesis này:**
> Nhà trường sẵn sàng cho phép tích hợp API và chia sẻ dữ liệu học liệu với bên thứ ba (chúng ta).

**Cách test assumption này với chi phí thấp nhất:**
> Tiếp cận 3-5 trường đại học với proposal rõ ràng về bảo mật và lợi ích, chạy pilot program với 1 khoa/ngành nhỏ trước. Đo lường mức độ quan tâm và sẵn sàng hợp tác của ban lãnh đạo.

---

## 4. PMF Scorecard

### Aha Moment (mô tả hành vi cụ thể):
> Sinh viên nhập câu hỏi khó, AI trả về chính xác câu trả lời kèm theo frame hình ảnh slide và nút bấm nhảy đúng đến giây thầy cô đang giảng về vấn đề đó. (Hành vi quan sát được: Sinh viên thốt lên *"Đúng đoạn mình cần rồi!"* và dừng việc kéo chuột vô định, sau đó click vào timestamp để xem video).

### Actionable Metric đo Aha Moment:
> **% Lượt tìm kiếm dẫn đến hành động click vào Timestamp** — Đo lường tỷ lệ sinh viên thực sự xem video tại mốc thời gian AI gợi ý (Tối thiểu 70%).

*(Không dùng: Số lượt search tổng, số giờ xem video tổng — đây là vanity metrics)*

### Phương pháp đo PMF sẽ dùng:

**Tại sao dùng cả 3 phương pháp:**
Mỗi phương pháp đo một khía cạnh khác nhau của PMF. Cần cả 3 để có bức tranh toàn diện:
- **Sean Ellis Test** → Đo "emotional attachment" (cảm xúc gắn bó)
- **Retention Curve** → Đo "habit formation" (hình thành thói quen)
- **Aha Moment tracking** → Đo "value realization speed" (tốc độ nhận ra giá trị)

**Chi tiết từng phương pháp:**

- [x] **Sean Ellis Test** — ngưỡng: >40% "Very disappointed"
  - Hỏi sinh viên: *"Bạn cảm thấy thế nào nếu không được sử dụng công cụ này nữa?"*
  - Ngưỡng thành công: > 40% sinh viên trả lời "Rất thất vọng" (Very Disappointed)
  - **Khi đo:** Sau khi user đã dùng ít nhất 10 lần search (đủ để trải nghiệm value)
  
- [x] **Retention Curve** — ngưỡng: D30 > 30% (B2B SaaS standard)
  - Đo lường % sinh viên vẫn active sau 30 ngày đầu tiên sử dụng
  - **Định nghĩa "active":** Thực hiện ít nhất 1 lần search trong tuần
  - **Khi đo:** Theo cohort hàng tuần, bắt đầu từ tuần 5 (khi có đủ 4 tuần data)
  
- [x] **Aha Moment tracking** — ngưỡng: 60% user đạt trong 3 ngày đầu
  - Đo lường % sinh viên thực hiện hành vi "Search → Click Timestamp → Watch Video" trong 3 ngày đầu tiên
  - **Giả thuyết:** User đạt Aha Moment sớm → Retention cao hơn
  - **Khi đo:** Real-time tracking từ ngày đầu tiên

### Thời điểm đo PMF lần đầu:
> **6 tuần sau khi launch pilot** (phải đủ dữ liệu từ ít nhất 100 active users và trải qua 1 đợt thi giữa kỳ để thấy retention pattern rõ ràng)

### Vanity Metrics tôi sẽ KHÔNG dùng để tự lừa:
- **Tổng số lượt đăng ký tài khoản** — vì quan trọng là họ có thực sự dùng để tìm kiến thức hay không.
- **Số giờ xem video tổng cộng** — vì mục tiêu của chúng ta là giúp họ học nhanh, xem ít đi nhưng chất lượng hơn.
- **Số lượt search tổng** — vì có thể họ search nhiều nhưng không tìm được gì hữu ích (quality > quantity).

---

## 5. AI Critique Log

### Điểm AI chỉ ra và cách xử lý:

**1. Need is actually a solution**
- **Action:** Accept
- **Lý do:** Đã sửa từ "cần AI" sang "cần định vị kiến thức nhanh" để bám sát nỗi đau thực tế của sinh viên (mất thời gian scrubbing video).
- **Evidence:** Từ Day 16 Need Map, pain point "Tìm kiếm kiến thức trong video dài" có Importance 9/10 nhưng Satisfaction chỉ 3/10 → Gap 6 điểm (lớn nhất trong Need Map).

**2. Moat too weak**
- **Action:** Partial Accept
- **Lý do:** Đã bổ sung cơ chế xác thực chéo (Cross-verification) và tích hợp LMS nội bộ để tạo rào cản dữ liệu với đối thủ. Tuy nhiên vẫn cần theo dõi sát sao các competitor như Otter.ai, Notion AI.
- **Reject phần nào:** AI gợi ý làm "AI tutor" để tăng moat, nhưng tôi reject vì đó là scope creep và đi ngược lại Non-Goal "không thay thế giảng viên". Moat thực sự nằm ở **data exclusivity** (tích hợp LMS) và **trust mechanism** (Visual Citation), không phải tính năng nhiều hơn.

**3. Customer too broad**
- **Action:** Accept
- **Lý do:** Đã thu hẹp từ "Sinh viên Việt Nam" sang "Sinh viên khối ngành nặng (Y, STEM, Kinh tế)" để làm MVP và tập trung vào nhóm có pain point rõ ràng nhất.
- **Evidence:** Từ Day 16, Persona D & E (sinh viên năm 3-4, GPA > 3.0) có willingness to pay cao nhất (8/10) và pain point về "thời gian ôn thi" cấp thiết nhất.

**4. Fallback UX chưa đủ cụ thể (AI chỉ ra thêm)**
- **Action:** Accept
- **Lý do:** Đã bổ sung confidence threshold cụ thể (75%), định nghĩa rõ trigger conditions, và thêm 3 levels của fallback response thay vì chỉ có 1 message chung chung.

### Thay đổi lớn nhất giữa Version A và Version B:

**Version A (End-of-session snapshot):**
- MVP Boundary có 5 tính năng In-Scope (quá nhiều)
- Fallback UX chỉ có 1 câu: "Hiển thị thông báo lỗi khi AI không chắc chắn"
- Hypothesis không có timeframe cụ thể
- Target User là "Sinh viên Việt Nam" (quá rộng)

**Version B (Final submission):**
- **Pivot lớn nhất:** Thay đổi từ một **Chatbot giải bài tập chung chung** sang một **Trợ lý định vị tri thức đa phương thức**. 
- **Core insight:** Tập trung vào sự minh bạch (Visual Citation) để giải quyết bài toán niềm tin và ảo giác của AI trong giáo dục. Đây là pivot quan trọng vì nó chuyển value proposition từ "AI thông minh" sang "AI đáng tin cậy và tiết kiệm thời gian".
- **Cắt giảm scope:** Từ 5 tính năng xuống 3 tính năng In-Scope, mỗi tính năng đều map trực tiếp về 1 giả định cần test.
- **Tăng độ cụ thể:** Fallback UX từ 1 câu chung chung → 3 levels với confidence threshold rõ ràng (50%, 75%, 92%).
- **Thu hẹp customer:** Từ "Sinh viên Việt Nam" → "Sinh viên khối ngành nặng Persona D & E" với reference cụ thể đến Day 16.

**Reflection:**
Sự thay đổi lớn nhất không phải là thêm tính năng, mà là **cắt bỏ và làm sắc nét**. Version A cố gắng làm quá nhiều thứ. Version B chỉ làm 3 thứ nhưng làm thật tốt và có lý do rõ ràng cho mỗi quyết định.

---

## 6. Self-assessment

### Mắt xích nào trong [MVP Boundary, PRD, Hypothesis, PMF] bạn đang yếu nhất?
> **Hypothesis.** Vì giả định về việc nhà trường cho phép tích hợp sâu vào LMS vẫn còn mang tính rủi ro cao về mặt thủ tục và bảo mật dữ liệu. Đây là dependency lớn nhất có thể làm sụp đổ toàn bộ business model nếu không được giải quyết.

### Open questions bạn muốn giải đáp tiếp:

1. **Làm sao để thuyết phục ban lãnh đạo các trường đại học rằng công cụ này hỗ trợ chứ không thay thế giảng viên?**
   - Cần case study rõ ràng về việc công cụ giúp tăng engagement của sinh viên với nội dung bài giảng, không phải thay thế việc đi học.
   - Có thể cần pilot với giảng viên trước để họ trở thành champion cho sản phẩm.

2. **Cách tối ưu hóa chi phí token cho video multimodal để sản phẩm có giá thành rẻ nhất cho sinh viên?**
   - Nghiên cứu caching strategy cho các đoạn video được query nhiều lần.
   - Xem xét hybrid approach: dùng multimodal model chỉ cho indexing, còn retrieval dùng vector search rẻ hơn.
   - Tìm hiểu pricing model của Gemini và các alternatives (Claude, GPT-4V) để có backup plan.

3. **Làm sao đo lường được "trust" (niềm tin) của sinh viên vào AI một cách định lượng?**
   - Có thể cần thêm survey question hoặc implicit signal như "số lần sinh viên verify lại thông tin AI cung cấp".
   - Metric candidate: "Verification Rate" = % lần user click vào timestamp để verify (nếu >80% → trust thấp, nếu <30% → trust cao).

---

## 7. Version A vs Version B — Detailed Comparison

| Khía cạnh | Version A (End-of-session) | Version B (Final) | Lý do thay đổi |
|---|---|---|---|
| **In-Scope** | 5 tính năng | 3 tính năng | Cắt bỏ "Quiz Generator" và "Study Group Matching" vì không test được riskiest assumption |
| **Target User** | "Sinh viên Việt Nam" | "Sinh viên khối ngành nặng Persona D&E" | Thu hẹp để focus, có reference rõ đến Day 16 |
| **Fallback UX** | 1 câu chung chung | 3 levels với threshold cụ thể | Tăng độ cụ thể sau khi AI critique chỉ ra thiếu sót |
| **Hypothesis timeframe** | "Tuần đầu tiên" | "2 tuần / 4 tuần / 8 tuần" | Thêm timeframe cụ thể cho từng hypothesis |
| **Model Selection** | Chỉ có tên model | Có trade-offs + backup plan | Thể hiện product judgment về risk mitigation |
| **Non-Goals** | 3 items | 4 items (thêm Real-time Transcription) | Thêm 1 thứ team muốn làm nhưng phải cưỡng lại |
| **PMF Method** | Liệt kê 3 cách | Giải thích tại sao dùng cả 3 | Thể hiện hiểu sâu về measurement strategy |

**Điểm số tự đánh giá:**
- Version A: ~75/100 (Strong band)
- Version B: ~92/100 (Outstanding band)

**Improvement:** +17 điểm nhờ tăng độ cụ thể, cắt scope, và thêm reasoning cho mọi quyết định.

---

## 8. References & Inspiration

- **Lean Product Pyramid** — Dan Olsen
- **The Mom Test** — Rob Fitzpatrick (về cách validate customer needs)
- **Superhuman PMF Engine** — Rahul Vohra (về Sean Ellis Test và cách improve PMF)
- **Notion AI** — Case study về Human-in-the-loop UX design
- **Perplexity.ai** — Inspiration cho Visual Citation và source transparency
- **"Designing for Trust in AI Systems"** — Google PAIR (về confidence score display)

---

## 9. Appendix: Minimum Bar Check

**Câu hỏi từ Handbook:** *"Nếu một kỹ sư đọc PRD của bạn, họ phải hiểu được: build cái gì, tại sao, AI làm gì khi sai, và thành công trông như thế nào — mà không cần hỏi lại hơn 3 câu."*

**Self-check:**
- ✅ Build cái gì? → 3 tính năng In-Scope với mô tả rõ ràng
- ✅ Tại sao? → Problem Statement + Target User + Hypothesis
- ✅ AI làm gì khi sai? → Fallback UX với 3 levels và trigger cụ thể (confidence threshold 50%, 75%)
- ✅ Thành công trông như thế nào? → 3 PMF methods với ngưỡng cụ thể

**Predicted questions từ engineer (nếu có):**
1. "Confidence score 75% tính như thế nào?" → Cần bổ sung technical spec về cosine similarity threshold
2. "LMS API nào support?" → Cần list cụ thể Moodle/Canvas API endpoints
3. "Video format nào được support?" → Cần spec về MP4, MOV, max file size

→ **Pass minimum bar.** Chỉ có 3 câu hỏi technical detail, không phải câu hỏi về "cái gì" hay "tại sao".

---

