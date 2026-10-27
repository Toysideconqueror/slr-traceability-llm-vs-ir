# GAP Analysis — G1: Fine-tuning LLM hiện đại cho Traceability Link Recovery

> _Note: the merged team evidence table cited below (`team-synthesis/evidence-table-merged.md`, 54 papers) is a team-level working document and is not part of this repository._

**Thành viên:** Ý
**GAP type:** GAP-T (Technology)
**Ngày:** 2026-07-13
**Evidence table nguồn:** team-synthesis/evidence-table-merged.md (N = 54 paper)

---

## 1. Mô tả GAP

Chưa có paper nào trong tập included fine-tune một LLM hiện đại (GPT-4o, Claude, Llama 3.1...) riêng cho bài toán Traceability Link Recovery (TLR). Tất cả các paper dùng LLM hiện đại đều tiếp cận qua zero-shot/few-shot prompting hoặc RAG (Retrieval-Augmented Generation), không có paper nào cập nhật trọng số (weights) của model cho task này.

**Bằng chứng từ evidence table:**
- Cột Tool/LLM: 5/54 paper dùng LLM hiện đại (GPT-4o, GPT-4o mini, GPT-4 Turbo, GPT-3.5, Claude Sonnet, Llama 3.1, Codellama) — toàn bộ đều mô tả cách dùng qua **prompting/retrieval**, không có mô tả fine-tuning.
- Ví dụ cụ thể: "Requirements Traceability Link Recovery via Retrieval-Augmented Generation" (Hey et al., REFSQ 2025) so sánh 2 kiểu prompt (KISS vs Chain-of-Thought) trên GPT-4o/GPT-4o mini/Codellama/Llama 3.1, nhưng không fine-tune model nào.
- Paper "Who's Who? LLM-assisted Software Traceability" (Fuchss et al., 2026) thử 7 LLM khác nhau (kể cả open-source Llama 3.1 70b) nhưng đều qua prompting (ExArch/ArTEMiS), không fine-tune.
- Việc fine-tune chỉ xuất hiện ở model cũ hơn: T-BERT (Lin et al., 2021) fine-tune MS-CodeBERT — không phải LLM hiện đại theo định nghĩa GAP.

---

## 2. Kiểm tra phản chứng

GAP tuyên bố: *"Chưa có paper nào fine-tune một LLM hiện đại (GPT-4o, Claude, Llama 3.1...) riêng cho bài toán TLR — tất cả đều dùng zero-shot/few-shot prompting hoặc RAG."*

| Paper | Đã làm GAP này chưa? | Chi tiết |
|-------|----------------------|----------|
| Hey, Fuchß, Keim, Koziolek — RAG (REFSQ 2025) | Không | Chỉ prompting (KISS/CoT) trên GPT-4o, GPT-4o mini, Codellama 13b, Llama 3.1 8b; temperature=0, không fine-tune |
| Fuchss et al. — Who's Who? (2026) | Không | 7 LLM (GPT-4o/mini/Turbo/3.5, Codellama, Llama 3.1 8b/70b) đều qua prompting (ExArch/ArTEMiS) |
| Alor et al. — Claude Sonnet/GPT-4o/o3-mini (2026, TOSEM) | Không | Inference trực tiếp để đánh giá, không fine-tune |
| Hassine — GPT-3.5 cho security requirements (2024) | Không | Prompting; ngoài ra GPT-3.5 không phải "LLM hiện đại" theo phạm vi GAP |
| Peng et al. — Prompts Matter (2023) | Không (củng cố GAP) | Bài này nghiên cứu riêng về prompt engineering, không đề cập fine-tuning |
| Lin et al. — T-BERT (2021) | Có fine-tune, nhưng không phải LLM hiện đại | Fine-tune MS-CodeBERT, ra đời trước GPT-4o/Claude/Llama 3.1 |
| North et al. — Code Gradients (2024) | Không tính | WizardCoder/CodeLlama đã được fine-tune sẵn bởi nhà sản xuất gốc, không phải bởi paper này; mục tiêu là explainability cho code generation, không phải TLR |

**Kết luận:** GAP xác nhận ✅ — Rà soát toàn bộ 54 paper trong evidence table, không tìm thấy paper nào fine-tune một LLM hiện đại (GPT-4o/Claude/Llama 3.1 trở lên) riêng cho task TLR. Mọi ứng dụng LLM hiện đại đều dừng ở prompting/RAG.

*(N_included = 54 ≥ 10 nên không bắt buộc chạy Supplementary Validation L1-L3. Có thể chạy L1 nhanh — search "fine-tune GPT-4o" AND "traceability link recovery" trên Scholar/IEEE — để tăng độ chắc chắn trước khi họp nhóm, nếu muốn.)*

---

## 3. Feasibility Check

| Tiêu chí | Mức | Ghi chú |
|---------|-----|---------|
| Dataset | ✅ | SEOSS (18 dự án Java, Rath et al., dùng trong RCT/T-BERT) hoặc CoEST benchmark (eTour, iTrust, SMOS, eAnci) — public, đã gán nhãn sẵn |
| API/Tool | ❌ (nếu chọn GPT-4o) / ✅ (nếu chọn Llama 3.1 8B) | OpenAI không có free tier cho fine-tuning GPT-4o, tốn phí theo token; Llama 3.1 8B mã nguồn mở, tải free từ HuggingFace |
| Tính toán | ⚠️ | Fine-tune full GPT-4o cần hạ tầng lớn; fine-tune Llama 3.1 8B bằng QLoRA (4-bit) chạy được trên Colab/Kaggle T4 free, nhưng chậm |
| Ground truth | ✅ | Có sẵn trace link đã gán nhãn từ SEOSS/CoEST |
| Code base | ⚠️ | Chưa có repo fine-tune LLM cho TLR cụ thể; HuggingFace PEFT/LoRA có template sẵn nhưng cần adapt cho task link-prediction |
| Kỹ năng | ⚠️ | Cần học LoRA/QLoRA + thư viện PEFT — có docs rõ ràng, học được trong khoảng 1 tuần |
| Thời gian | — | |

**Kết quả:** 1 ❌ (nếu giữ GPT-4o) + 3 ⚠️ → Rủi ro cao nếu giữ nguyên phạm vi GPT-4o. **Khuyến nghị downscope trước khi commit** (xem mục 5).

---

## 4. Phát biểu GAP chính thức

Chưa có nghiên cứu nào đánh giá hiệu quả của việc fine-tune một LLM mã nguồn mở hiện đại (Llama 3.1) cho task Requirements-to-Code Traceability Link Recovery bằng kỹ thuật parameter-efficient fine-tuning (LoRA/QLoRA), so với cách tiếp cận zero-shot/few-shot prompting đang chiếm ưu thế trong các nghiên cứu hiện tại.

---

## 5. Đề xuất sơ bộ cho nhóm (chuẩn bị họp RBL-3)

**Dataset khả thi:** SEOSS 18-project Java dataset (Rath et al., dùng lại trong T-BERT/RCT) — 13.721 requirement, 55.196 file, 231.323 trace link, public, đã có sẵn train/test split từ các paper trước, dễ so sánh trực tiếp.

**Metric đề xuất:** F1, MAP@3 — theo cột Metric phổ biến nhất trong evidence table (dùng lại chuẩn của T-BERT/RAG-REFSQ để so sánh công bằng).

**LLM/Tool đề xuất:** Llama 3.1 8B + QLoRA (4-bit, qua thư viện HuggingFace PEFT) — đây là công nghệ chưa xuất hiện trong cột Tool/LLM của evidence table (hiện chỉ có GPT-4o/Claude/Llama qua prompting).

**Baseline đề xuất:** So với (1) GPT-4o + CoT prompting (F1=45.1% theo Hey et al. REFSQ 2025) và (2) T-BERT fine-tuned BERT (F1=0.884-0.972 theo Lin et al. 2021, tuy đo trên dataset khác nên chỉ so sánh tương đối).

**Rủi ro cần bàn với nhóm:** Nếu QLoRA trên Colab/Kaggle free vẫn quá chậm/không đủ VRAM, có thể downscope thêm sang Llama 3.1 8B → giảm xuống model nhỏ hơn (vd. Llama 3.2 3B) hoặc giảm N mẫu dataset.
