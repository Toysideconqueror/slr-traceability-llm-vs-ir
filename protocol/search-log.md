# Nhật ký tìm kiếm (Search Log)

**Thành viên:** nguyeny (Trưởng nhóm)
**Database phụ trách:** IEEE Xplore
**Cập nhật:** 05/07/2026 — thay thế bộ 4 query cũ (quá hẹp, tổng 22 kết quả) bằng bộ 4 query mới, mở rộng phạm vi để tránh bỏ sót tài liệu liên quan ở vòng sàng lọc đầu tiên (Round 1).

## 1. Lịch sử tìm kiếm (Search History)

* **Query 1 (Cốt lõi — LLM & Traceability Link Recovery):**
  * **Ngày search:** 05/07/2026
  * **Query nguyên văn:** `("All Metadata":"traceability link recovery" OR "All Metadata":"requirements traceability" OR "All Metadata":"traceability links") AND ("All Metadata":"large language model" OR "All Metadata":"LLM" OR "All Metadata":"GPT" OR "All Metadata":"ChatGPT")`
  * **Số kết quả trả về:** 14
  * **Ghi chú:** Bắt các bài trực tiếp về TLR dùng LLM/GPT — nhóm liên quan nhất đến RQ chính.

* **Query 2 (Kỹ thuật Prompting cho SE nói chung):**
  * **Ngày search:** 05/07/2026
  * **Query nguyên văn:** `("All Metadata":"zero-shot" OR "All Metadata":"few-shot" OR "All Metadata":"in-context learning" OR "All Metadata":"prompt engineering") AND ("All Metadata":"software requirements" OR "All Metadata":"source code" OR "All Metadata":"requirements engineering")`
  * **Số kết quả trả về:** 550
  * **Ghi chú:** Không ép buộc từ "traceability" nên phạm vi rất rộng (bao gồm nhiều bài về code generation, test generation không liên quan trực tiếp — cần lọc kỹ ở Round 2 theo IC-P/EC-O).

* **Query 3 (Phương pháp Baseline — IR cho Traceability):**
  * **Ngày search:** 05/07/2026
  * **Query nguyên văn:** `("All Metadata":"traceability" OR "All Metadata":"traceability recovery") AND ("All Metadata":"information retrieval" OR "All Metadata":"vector space model" OR "All Metadata":"latent semantic indexing" OR "All Metadata":"BM25")`
  * **Số kết quả trả về:** 362
  * **Ghi chú:** Bỏ ràng buộc "class-level" so với bộ query cũ để không loại nhầm các bài baseline quan trọng — sẽ lọc "class-level" bằng tay ở Round 2/3 theo IC-P.

* **Query 4 (Hallucination trong LLM cho code/liên kết kỹ thuật):**
  * **Ngày search:** 05/07/2026
  * **Query nguyên văn:** `("All Metadata":"hallucination") AND ("All Metadata":"large language model" OR "All Metadata":"LLM" OR "All Metadata":"GPT" OR "All Metadata":"code generation")`
  * **Số kết quả trả về:** 671
  * **Ghi chú:** Phục vụ RQ3 (tỷ lệ hallucination). Mở rộng ra ngoài traceability nên phần lớn kết quả sẽ bị loại ở Round 2 do không liên quan đến traceability (EC-O).

## 2. Tổng hợp kết quả

| Bước | Số lượng Paper | Ghi chú |
| :--- | :--- | :--- |
| **Tổng tìm được (Raw)** | **1597** | Tổng số từ 4 query: 14 + 550 + 362 + 671. |
| **Trùng lặp chéo giữa các query** | **20** | 18 bài xuất hiện ở ≥2 query (ví dụ 8 bài trùng giữa Query 1 & Query 3, 2 bài trùng cả 3 query 1/2/3). |
| **Sau khi bỏ trùng (Dedup)** | **1577** | Số dòng trong `01_all_records.csv`. Cột `Source_Queries` trong file ghi rõ bài đến từ (các) query nào. |

## 3. Lưu ý cho vòng sàng lọc tiếp theo

Do Query 2 và Query 4 có phạm vi rất rộng (550 và 671 kết quả), phần lớn `1577` bản ghi trong `01_all_records.csv` **chưa qua sàng lọc theo tiêu chí IC/EC** (xem `ie_criteria.md`). Bước tiếp theo cần:

1. Áp dụng lọc nhanh theo tiêu đề/từ khóa để loại các bài rõ ràng ngoài phạm vi (EC-O: Code Summarization, Bug Localization, Fault Prediction; các bài về unit test generation, de-obfuscation không liên quan đến traceability).
2. Áp dụng IC-Y (>= 2020) và IC-T (peer-reviewed, không phải short paper/EC-S) để loại tiếp.
3. Chỉ giữ lại các bài liên quan đến **requirement-to-source-code traceability** (IC-P) cho vòng đọc abstract đầy đủ (Round 2).
