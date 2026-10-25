# Section 0 — Project Framing & Application Scope Checkpoint

| Framing Element | Description |
| :--- | :--- |
| **Problem Evidence** | Public higher education bodies manage extensive scholarship guidelines across separate administrative portals, creating high inquiry volume and user navigation friction (MOHE Malaysia Guidelines: https://www.mohe.gov.my/). Unassisted LLMs suffer from hallucination risks when querying unindexed policy domains (Gao et al., 2023, arXiv:2312.10997). |
| **Existing Approaches** | 1. Manual consultation with financial aid officers (limited by office hours).<br>2. Static PDF handbooks (fragmented, hard to search manually).<br>3. Generic LLMs (prone to hallucinating eligibility income caps). |
| **Project/Engineering Gap** | Existing solutions lack natural-language query matching against exact policy clauses with verifiable citations, forcing students to manually filter dense financial PDFs. |
| **Objective O1** | To design a document-grounded AI solution based on official university and foundation scholarship guidelines. |
| **Objective O2** | To develop a retrieval system with clear guardrails that ensures all responses are grounded in official policy documents. |
| **Objective O3** | To evaluate the system based on accuracy, eligibility grounding, latency, and resistance to ungrounded financial claims. |
| **Intended Users** | Undergraduate and prospective university students searching for scholarships, bursaries, and financial aid options. |
| **Supported Tasks** | Answering questions on scholarship eligibility, CGPA cutoffs, household income thresholds, required supporting documents, and application deadlines. |
| **Information / Knowledge Domain** | Official institutional scholarship handbooks, endowed bursary guidelines, and public financial aid policy documents. |
| **Operating Context** | Web-based student portal interface operating as an interactive Q&A assistant for academic advising. |
| **Important Constraints** | Must run within standard API rate limits, support fast response times (<3000ms), and utilize publicly accessible PDF documents only. |
| **Explicit Out-of-Scope Tasks** | Shall NOT grant final scholarship approvals, evaluate bank account statements, compute tax returns, or provide personal financial planning advice. |
| **Evaluation Focus** | Determining whether retrieval-augmented generation improves citation accuracy and eliminates hallucinated eligibility criteria compared to base LLMs. |

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