# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | VinFast | Repetitive | Tự động so khớp hóa đơn, giấy tờ bảo trì và chi phí phụ tùng giữa hệ thống sản xuất và kho vận hàng ngày. |
| 2 | Xanh SM | Time-consuming | Điều phối lại lộ trình tài xế khi có kẹt xe hoặc hủy chuyến, cần xử lý thủ công với nhiều cuộc gọi và cập nhật. |
| 3 | Vinhomes | AI-upgrade | Soạn thảo và phân loại phản hồi cho đánh giá 1-star của cư dân, hiện tại vẫn do nhân viên CSKH làm thủ công. |
| 4 | Vinmec | Stakeholder Pain | Quản lý lại lịch hẹn khám và nhắc bệnh nhân đến khám, giảm tình trạng hủy/không đến và quá tải phòng khám. |
| 5 | Khác (Vinpearl) | AI-upgrade | Dự đoán lưu lượng khách và phân bổ nhân sự/phòng chờ nhằm giảm thời gian xếp hàng và tăng trải nghiệm du lịch. |
---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #___                                     │
│                                                             │
│ Bài toán (1 câu): ________________________________________  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? ______________________________________ │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. ___ ──> 2. ___ ──> 3. ___ ──> 4. ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? ___ (⏱ ___ phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? _____________________ │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? ______________________ │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #1
Bài toán (1 câu): Tự động so khớp hoá đơn bảo trì, phiếu xuất kho và chứng từ phụ tùng giữa nhà máy VinFast và kho vận mỗi ngày.
Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác (Ghi rõ)________
Ai đang đau (Actor)? Nhân viên kế toán và quản lý kho phụ tùng.
Workflow thủ công hiện tại (3-5 bước):
  1. Thu thập hoá đơn, phiếu xuất kho, và đề nghị bảo trì.
  2. So sánh thủ công từng mục phụ tùng với dữ liệu ERP.
  3. Xác nhận chênh lệch và yêu cầu làm rõ từ nhà máy/kho.
  4. Cập nhật lại hệ thống và phát hành lệnh thanh toán.
Bước nào tốn thời gian/lỗi nhất? So sánh dữ liệu thủ công và phát hiện chênh lệch (⏱ 15-25 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Bước so sánh và xác định chênh lệch giữa hoá đơn, phiếu xuất kho và dép dụng cụ.
Đo thành công bằng gì (Metric có số)? Giảm thời gian kiểm tra từ ~20 phút/lượt xuống dưới 5 phút; giảm sai sót đối chiếu xuống dưới 5%.
Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent

### Quick Problem Card #2
Bài toán (1 câu): Điều chỉnh lộ trình và ưu tiên phân bổ tài xế Xanh SM khi có kẹt xe, hủy chuyến hoặc yêu cầu đặc biệt của khách.
Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác (Ghi rõ)________
Ai đang đau (Actor)? Điều phối viên trung tâm điều vận và tài xế.
Workflow thủ công hiện tại (3-5 bước):
  1. Nhận báo cáo kẹt xe/hủy chuyến từ tài xế hoặc khách.
  2. Gọi điện hoặc nhắn tin cho tài xế khác để điều chuyển.
  3. Chỉnh sửa lộ trình thủ công trong hệ thống điều độ.
  4. Thông báo lại cho khách và tài xế về lịch trình mới.
Bước nào tốn thời gian/lỗi nhất? Điều chỉnh lộ trình và tìm tài xế thay thế (⏱ 10-15 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Phân tích tình huống, đề xuất lộ trình thay thế và tài xế phù hợp tự động.
Đo thành công bằng gì (Metric có số)? Giảm thời gian điều phối xuống dưới 5 phút; tăng tỷ lệ chấp nhận điều phối mới lên 80%.
Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent

### Quick Problem Card #3
Bài toán (1 câu): Soạn thảo và phân loại phản hồi cho đánh giá 1-star của cư dân Vinhomes để giảm thời gian xử lý và tăng chuẩn xác.
Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  [ ] Vinmec  [ ] Khác (Ghi rõ)________
Ai đang đau (Actor)? Nhân viên chăm sóc khách hàng Vinhomes.
Workflow thủ công hiện tại (3-5 bước):
  1. Nhận đánh giá 1-star từ nền tảng quản lý cư dân.
  2. Đọc nội dung đánh giá và phân loại vấn đề.
  3. Viết phản hồi thủ công hoặc chuyển sang bộ phận liên quan.
  4. Gửi phản hồi và theo dõi hành động khắc phục.
Bước nào tốn thời gian/lỗi nhất? Đọc, phân loại và soạn thảo phản hồi phù hợp (⏱ 12-18 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Phân tích nội dung đánh giá, phân loại nguyên nhân và sinh phản hồi mẫu theo chính sách.
Đo thành công bằng gì (Metric có số)? Giảm thời gian soạn trả lời từ 15 phút xuống còn 3 phút; đạt 90% phản hồi phù hợp với kịch bản CSKH.
Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---