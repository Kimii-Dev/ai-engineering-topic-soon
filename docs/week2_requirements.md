# Section 0 — Project Framing & Application Scope Checkpoint

| Framing Element | Description |
| :--- | :--- |
| **Problem Evidence** | The public higher education authorities have a wide range of scholarship regulations in different administrative portals, resulting in a large number of inquiries and difficulty navigating through those portals (MOHE Malaysia Guidelines: https://www.mohe.gov.my/). Unguided LLMs are subject to risks of hallucinations when accessing unindexed policy areas (Gao et al., 2023, arXiv:2312.10997). |
| **Existing Approaches** | 1. Consultation with financial aid officers manually (subject to office hours).<br>2. Static PDF manuals (disjointed, difficult to search manually).<br>3. General LLMs (hallucinates income cap eligibility). |
| **Project/Engineering Gap** | There is a need for a natural language query matching to actual policy clauses with references instead of forcing students to filter information from complex financial PDFs manually. |
| **Objective 01** | To create an AI system for document-grounded queries using official guidelines for university and foundation scholarships. |
| **Objective 02** | To create a retrieval system with well-defined guardrails ensuring that all answers are grounded in official policy documents. |
| **Objective 03** | To test the system by such metrics as accuracy, grounding in eligibility, latency, and rejection of ungrounded financial assertions. |
| **Target Audience** | Undergraduates and prospective university students seeking scholarships, bursaries, and financial aid. |
| **Tasks** | Responding to inquiries regarding scholarship eligibility criteria, CGPA minimums, family income cutoffs, supporting documents, and application deadline dates. |
| **Domain of Information/Knowledge** | Institutional scholarship guides, endowed bursary guidelines, and public financial aid policies. |
| **Operational Context** | Web-based portal for academic advising running as an interactive Q&A agent. |
| **Key Constraints** | Needs to be able to function within the API rate limits, perform at a reasonable speed (<3000ms), and access publicly available PDF documents only. |
| **Explicitly Out-of-Scope Tasks** | Shall NOT approve scholarships, review bank account statements, calculate tax returns, and offer personal financial advice. |
| **Focus of Evaluation** | Retrieval-augmented generation’s effect on citation accuracy and removal of invented eligibility criteria in comparison to base LLMs. |

---

# Section 1 — Functional Requirements Specification

Version: 1.0

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
| :--- | :--- | :--- |
| **FR1** | Answer queries regarding scholarship eligibility criteria, CGPA cutoffs, and income thresholds using official policy documents. | Invent scholarship names, CGPA requirements, or eligibility rules not present in the source documents. |
| **FR2** | Provide direct verifiable source citations (document title and page/section) for all policy claims. | Present unverified general financial advice as an approved university policy. |
| **FR3** | Retrieve and summarize application submission deadlines and required supporting document lists. | Automatically submit scholarship applications on behalf of the student. |
| **FR4** | Decline out-of-scope queries (e.g., career advice, course enrollment, personal loans) and provide an appropriate redirect. | Offer legal, tax, personal financial planning, or mental health counselling advice. |
| **FR5** | Present eligibility summaries in clear, concise language accessible to undergraduate students. | Make final binding decisions on scholarship award approvals or rejections. |

---

# Section 2 — Non-Functional Requirements Specification

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **NFR1** | Performance | The system shall keep interactive responses within the agreed latency target. | Measure end-to-end latency from query submission to final response generation across a 30-query test set. | p90 latency | < 3,000 ms |
| **NFR2** | Correctness | Answers shall be factually consistent with approved source documents. | Score a curated test dataset of 30 standard financial aid questions using an expert evaluation rubric. | Correct response rate (%) | ≥ 85% |
| **NFR3** | Cost | Inference and embedding API costs shall remain within project budget constraints. | Record API token consumption across the evaluation workload. | Cost per 100 queries | < US$0.50 per 100 queries |
| **NFR4** | Maintainability | Updated scholarship PDF documents shall be indexed without rebuilding unrelated pipeline components. | Measure the execution time required to parse, chunk, embed, and re-index a newly published policy PDF. | Index update time | < 10 minutes |

---

# Section 3 — Responsible AI Requirements Specification

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RAI1** | Fairness | System answer correctness shall not vary significantly across different student income categories or study faculties. | Evaluate a stratified test set of queries across STEM, Arts, and B40/M40 income categories. | Absolute correctness rate gap between groups | ≤ 10 percentage points |
| **RAI2** | Safety / Scope | The system shall refuse out-of-scope or malicious queries (e.g., tax evasion, loan fraud) and redirect users appropriately. | Run a safety evaluation dataset containing at least 20 out-of-scope and prompt-injection queries. | Refusal-and-redirect success rate | ≥ 95% |
| **RAI3** | Privacy | The system shall not store or transmit student personally identifiable information (PII) to external model APIs. | Inspect outgoing API payloads for IC/Passport numbers, bank accounts, or phone numbers. | Number of detected PII transmissions | 0 |
| **RAI4** | Transparency / Grounding | The system shall provide verifiable source citations for all claims and indicate when sufficient context is missing. | Inspect generated responses for citation presence and verify citation-to-source grounding match. | Citation presence rate; citation-source match rate | 100% citation presence; ≥ 95% source match |