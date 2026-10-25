# Evaluation Criteria — BAI-ExemptAI

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold | User / Business Outcome |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **3 / NFR2** | Answer Correctness | Domain-specific capability | Evaluate a test set of 25 SAIAH course and prerequisite queries against the handbook using a factual correctness rubric. | Correct response rate (%) | $\ge 85\%$ | Students receive accurate, trustworthy academic guidance for subject registration. |
| **1 / FR3 / RAI4** | Source Citation & Grounding | Instruction-following capability | Inspect document-grounded responses for page citations and verify whether cited chunks support the generated statements. | Citation presence rate; Citation-source match rate | 100% citation presence; $\ge 95\%$ match rate | Students and advisors can independently verify every advice item directly against the PDF handbook. |
| **2 / RAI2** | Out-of-Scope Refusal | Instruction-following capability | Test the system with a dataset of 20 out-of-scope (e.g., hostel fees, visa rules, grade overrides) queries. | Refusal-and-redirect success rate | $\ge 95\%$ | Prevents inappropriate advice and restricts tool usage strictly to academic syllabus scope. |
| **3 / NFR1** | Response Latency | Cost and latency | Measure end-to-end response time from user query submission to complete output rendering across 30 queries. | p90 latency | < 3,000 ms | Ensures a fast, smooth interactive experience during peak course registration periods. |
| **1 / FR5** | Guidance Clarity | Generation capability | Score response structure and readability on a 1–5 scale using a student usability rubric. | Average clarity rubric score | $\ge 4.0 / 5.0$ | Students can easily understand credit rules and syllabus comparisons without confusion. |

---

### Reflection
*Which evaluation criterion is most important for determining whether your AI application will be useful to its intended users? Why?*  
**Answer:** **Source Citation & Grounding (O1 / FR3 / RAI4)** is the most critical evaluation criterion. Academic credit transfer and prerequisite planning carry official administrative weight. If the assistant provides an accurate summary but cannot prove its source with precise handbook page references, advisors and students will not trust or adopt the tool. Verifiable citations bridge the gap between AI generation and official university policy enforcement.