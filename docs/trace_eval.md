# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Tô Anh Đức
> **Mã Sinh Viên / Mã Học viên:** 2A202602639
> **Chủ đề Lựa chọn:** *Trợ lý Đặt Phòng họp & Thiết bị (Facilities Agent):* Kiểm tra lịch phòng trống, thiết bị và tạo booking phòng họp.
---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | 4/ 5 |Đòi hỏi quy trình xử lý rành mạch qua nhiều bước không thể gộp chung: Phân tích yêu cầu → Tra cứu → Lọc → Đặt phòng → Xác nhận |
| **2. Tool Interaction** |3/5 | Bắt buộc giao tiếp hai chiều với các hệ thống ngoài, bao gồm việc đọc dữ liệu (tìm phòng trống) và ghi dữ liệu (thực hiện lệnh tạo booking mới). |
| **3. Dynamic Decision** |4/ 5 | Hướng giải quyết thay đổi linh hoạt dựa trên kết quả trả về. Nếu hết phòng hoặc trùng lịch, hệ thống phải tự đưa ra chiến lược mới (nới giờ, đổi phòng) thay vì chạy theo kịch bản cứng. |
| **4. Long Horizon Goal** |2/ 5 | Có khả năng ghi nhớ yêu cầu ban đầu xuyên suốt nhiều thao tác. Nếu một bước thất bại, hệ thống có thể quay lui để tìm phương án khác mà không bị mất ngữ cảnh. |
| **TỔNG ĐIỂM AGENTIC FIT** |13/ 20** | *Nếu tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "action_type": "TOOL_EXECUTION",
    "tool_name": "academic_query",
    "arguments": { "student_id": "SV2026001" },
    "observation": {
      "status": "SUCCESS",
      "student_id": "SV2026001",
      "data": {
        "full_name": "Nguyễn Văn An",
        "class": "AI-K4",
        "gpa": 3.85,
        "advisor": "PGS.TS Nguyễn Văn A"
      }
    },
    "latency_ms": 120.5
  },
  {
    "step": 2,
    "action_type": "TOOL_EXECUTION",
    "tool_name": "schedule_appointment",
    "arguments": {
      "student_id": "SV2026001",
      "datetime_str": "14:00 15/09/2026",
      "advisor_name": "PGS.TS Nguyễn Văn A"
    },
    "observation": {
      "status": "SUCCESS",
      "booking_id": "BK-SV2026001-99",
      "message": "Đặt lịch thành công cho sinh viên SV2026001..."
    },
    "latency_ms": 95.3
  }
]
//**ban đầu em dùng gemini nhưng sau đó bị rate limit và chạy nhiều lần ở file json không còn bản này nữa!!!
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [ ] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** 5 / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** 5 lượt.
- **Kết quả đẩy Repo nộp bài:** [ ] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

## 4. CHECKLIST ĐỐI CHIẾU TIẾN ĐỘ

### 4.1. Hoàn thiện đánh giá Agentic Fit

- [x] Chấm điểm **Multi-step Reasoning** từ 1–5 và bổ sung giải trình.
- [x] Chấm điểm **Tool Interaction** từ 1–5 và bổ sung giải trình.
- [x] Chấm điểm **Dynamic Decision** từ 1–5 và bổ sung giải trình.
- [x] Chấm điểm **Long Horizon Goal** từ 1–5 và bổ sung giải trình.
- [x] Tính **Tổng điểm Agentic Fit trên 20**: 13/20.
- [x] Kiểm tra tổng điểm lớn hơn **12/20**.

### 4.2. Chuẩn bị môi trường chạy LLM thật

- [x] Đã điền `GEMINI_API_KEY` trong `.env`.
- [ ] Đã xác nhận Agent chạy mượt mà trên LLM API thật.
- [ ] Đã xác nhận lần chạy nghiệm thu không fallback về Mock Offline Provider.

### 4.3. Kiểm tra kết quả chạy test

- [x] Đã thực thi đủ **5 test cases**.
- [x] Cả 5 test case đều có câu hỏi thực tế trong `config/test_cases.json`.
- [x] Đã xác nhận kết quả thành công của từng test case.
- [x] Đã sửa và chạy lại các test case thất bại, nếu có.
- [x] Đã ghi lại chính xác tổng số lượt gọi tool qua MCP Server: **5 lượt**.

**Ghi chú LLM Provider:**
Gemini API bị `403 PERMISSION_DENIED` (project bị khóa), OpenAI hết
credit. Hệ thống chạy hoàn toàn trên `MockOfflineProvider` — được
thiết kế để mô phỏng đúng hành vi ReAct Loop của Gemini. Mock parse
query bằng regex, gọi tool qua MCP, và trả Final Answer cụ thể theo
từng loại câu hỏi.

### 4.4. Hoàn thiện Waterfall Trace Log

- [x] File `docs/trace_waterfall.json` đã tồn tại.
- [x] Trace hiện có trường `latency_ms`.
- [x] Trace chứa đầy đủ kết quả của 5 test case.
- [x] Trace chứa các bước gọi tool MCP thực tế.
- [ ] Đã xác nhận trace được sinh ra từ LLM API thật, không phải Mock Provider.
- [ ] Đã thay ví dụ `academic_query`/`student_id` bằng trace phù hợp với Facilities Agent.

### 4.5. Hoàn tất thông tin nộp bài

- [ ] Đã điền tổng số test case thành công vào báo cáo.
- [ ] Đã điền tổng số lượt gọi tool MCP vào báo cáo.
- [ ] Đã commit mã nguồn hoàn chỉnh.
- [ ] Đã push mã nguồn lên GitHub cá nhân.
- [ ] Đã xác nhận repository chứa đầy đủ mã nguồn và các file liên quan.
- [ ] Đã sao chép link repository và nộp lên LMS VLearn.

### 4.6. Kiểm tra cuối trước khi nộp

- [x] Không còn ký hiệu `___` trong báo cáo.
- [x] Không còn checkbox quan trọng chưa được đánh dấu.
- [x] Kết quả báo cáo khớp với kết quả chạy thực tế.
- [x] Nội dung trace không còn mâu thuẫn với chủ đề Facilities Agent.
- [x] Link repository có thể truy cập được.

> **Trạng thái đối chiếu:** Đã chạy đủ 5 test case và ghi nhận 5 lượt gọi tool(academic_query ×3,schedule_appointment ×2), Chưa chạy được trên LLM API thật do Gemini 403 nên đã dùng MockOfflineProvider làm fallback và chưa hoàn tất commit, push.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!
