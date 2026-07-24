# 02 — Deep-Dive Report

## Nhóm và thành viên
- Tên Nhóm: Vin Smart Future AI Product Team
- Thành viên:
  - [Trần Đoàn Quang Vũ - 2A202601999]

---

## 1. Quyết định lựa chọn bài toán
**Bài toán được chọn:** Điều chỉnh lộ trình và phân bổ tài xế Xanh SM khi có kẹt xe, hủy chuyến hoặc yêu cầu đặc biệt của khách.

Lý do chọn:
- Đây là quy trình vận hành thực tế của Xanh SM với tần suất cao và nhiều biến cố thời tiết/tắc đường.
- Bài toán có rõ ràng điểm đau cho điều phối viên và tài xế, có thể đo được bằng thời gian xử lý và tỷ lệ chuyến hoàn thành.
- Một giải pháp AI có thể tăng tốc độ quyết định, giảm thiểu call/nhắn tin thủ công và giữ an toàn thông qua Human-in-the-loop.

---

## 2. Problem Statement (6-field)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Điều phối viên trung tâm điều vận Xanh SM và đội ngũ vận hành lộ trình. |
| **2. Current Workflow** | 1) Nhận báo cáo kẹt xe/hủy chuyến từ tài xế/khách qua hệ thống nội bộ. 2) Cập nhật tình hình đường đi bằng cách kiểm tra bản đồ và thông tin xe. 3) Tìm tài xế thay thế hoặc điều chỉnh lộ trình thủ công trong hệ thống điều độ. 4) Gọi/nội dung SMS thông báo khách và tài xế về lịch trình mới. 5) Theo dõi trạng thái chuyến tiếp theo. |
| **3. Bottleneck** | Bước 2 và 3: Phân tích tình huống và chọn lộ trình/tài xế thay thế phù hợp. Quy trình hiện tại yêu cầu nhiều thao tác thủ công, tra cứu bản đồ, chọn tài xế, và viết thông báo. Điều này tốn 10-15 phút mỗi sự cố và dễ sai sót khi thông tin thay đổi nhanh. |
| **4. Business Impact** | Mỗi sự cố chậm trễ khiến chuyến bị hoãn, gây gián đoạn dịch vụ, làm khách hàng không hài lòng, tăng chi phí điều phối và giảm doanh thu. Ước tính nếu mỗi ngày có 15-20 sự cố tương tự, đội điều vận mất 3-5 giờ làm việc và có thể mất 8-12% công suất phục vụ trong giờ cao điểm. |
| **5. Success Metric** | 1) Giảm thời gian xử lý sự cố từ 10-15 phút xuống dưới 5 phút. 2) Tăng tỷ lệ đề xuất lộ trình/tài xế phù hợp được chấp nhận lên ≥80%. 3) Giảm số lần chỉnh sửa lại kế hoạch số lần từ 3 xuống dưới 1 lần mỗi sự cố. |
| **6. Operational Boundary** | AI chỉ được phép phân tích dữ liệu hiện có và đề xuất phương án, không được tự động điều chuyển tài xế trước khi có phê duyệt điều phối viên. AI không được đề xuất lộ trình vượt quá khu vực hoạt động, không được đặt tài xế vô tình quá tải, và không được bỏ qua quy tắc an toàn như thời gian nghỉ phép. Nếu AI không đủ tự tin, phải trả về yêu cầu hồi cứu người điều phối. |

---

## 3. Future-State Flow & AI Fit

**AI Fit:** [x] LLM Feature  [ ] Rule / State-Machine  [ ] Agentic Loop

**Lý do:** Bài toán yêu cầu tổng hợp ngôn ngữ và ngữ cảnh vận hành, nhưng quy trình vẫn cần người điều phối phê duyệt ở cuối. Một LLM feature có thể đóng vai trò gợi ý thông minh, trong khi con người vẫn giữ quyền quyết định cuối cùng.

**Future-State Flow:**

```text
Nhận báo cáo sự cố ──> 🔵 AI phân tích tình huống ──> 🔵 AI đề xuất lộ trình/tài xế ──> 🟢 Điều phối viên duyệt ──> 🟢 Gửi thông báo
                             │
                             ▼
                       ↩️ Fallback:
         Nếu AI không tự tin hoặc dữ liệu thiếu,
         chuyển về quy trình thủ công và gọi nhóm hỗ trợ.
```

**Mô tả bước:**
1. **Nhận báo cáo sự cố:** Hệ thống tiếp nhận thông tin kẹt xe, hủy chuyến, hoặc yêu cầu đặc biệt từ tài xế/khách.
2. **🔵 AI phân tích tình huống:** LLM đọc dữ liệu lịch sử chuyến, trạng thái tài xế, điều kiện giao thông và loại xe; xác định các phương án hợp lý.
3. **🔵 AI đề xuất lộ trình/tài xế:** AI trả về một tập hợp giải pháp được xếp hạng, kèm lý do ưu tiên và các cảnh báo an toàn.
4. **🟢 Điều phối viên duyệt:** Điều phối viên kiểm tra, chỉnh sửa nếu cần, duyệt đề xuất và xuất lệnh điều chuyển.
5. **🟢 Gửi thông báo:** Thông báo được gửi tới tài xế và khách dưới dạng draft nội dung, không được gửi tự động nếu chưa được duyệt.

**Điểm HITL:** Điều phối viên phải phê duyệt mọi đề xuất trước khi hệ thống thực hiện điều chuyển tài xế hoặc thay đổi lộ trình. Điều này kiểm soát rủi ro khi AI tạo sai lệnh trong tình huống đặc thù.

**Fallback:**
- Nếu AI phát hiện thiếu dữ liệu, không tìm được tài xế phù hợp, hoặc độ tự tin thấp, nó trả về trạng thái `request_human_review`.
- Hệ thống chuyển nhanh về quy trình thủ công hiện tại và điều phối viên sử dụng công cụ chuẩn để xử lý.

---

## 4. Evaluate

### AI Readiness Checklist
- [x] Có dữ liệu vận hành ban đầu để mô phỏng sự cố và lộ trình điều phối.
- [x] Rủi ro AI sai được kiểm soát bằng bước Human-in-the-loop (điều phối viên duyệt trước khi gửi).
- [x] Stakeholders sẵn sàng thử nghiệm pilot trong một vùng hạn chế trước khi mở rộng.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future
- [x] GO (Bắt đầu xây dựng Prototype)
- [ ] NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline)
- [ ] NO-GO (Không khả thi / Rule-based tốt hơn)

**Justification:**
- Bài toán có ranh giới rõ ràng, hoạt động trong một hệ thống điều vận chuyên biệt của Xanh SM.
- AI được dùng làm trợ lý gợi ý, không thay thế con người; đây là mô hình an toàn với HITL và fallback rõ ràng.
- Mục tiêu đo được bằng thời gian xử lý và tỷ lệ chấp nhận đề xuất, phù hợp để xây pilot.
- Mô hình LLM feature có thể giảm áp lực cho đội điều phối và tăng khả năng phản ứng nhanh khi có sự cố.

---

## 5. Ghi chú bổ sung
- Trước khi phát triển tiếp, nhóm cần thu thập thêm log sự cố thực tế trong 2 tuần để định nghĩa chuẩn xác dữ liệu đầu vào và độ tin cậy của đề xuất.
- Nếu pilot thành công, bước tiếp theo là tích hợp API bản đồ/điều độ và tự động sinh nội dung thông báo draft cho tài xế.
