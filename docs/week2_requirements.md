# Section 0 — Project Framing & Application Scope Checkpoint

| Framing Element | Description |
| :--- | :--- |
| **Problem Evidence** | 1. Credit exemption applications require strict syllabus and transcript verification against UTM course standards and must be submitted by Week 10 of Semester 1.<br>2. Students on Conditional Academic Standing (KS, CGPA < 2.00) are restricted to 9–13 credits per semester, while failure to register results in study termination (UTM FAI Academic Handbook 2025/2026, pp. 42 & 45). |
| **Existing Approaches** | 1. *Manual Advisor Consultations:* Accurate, but bottlenecked by lecturer availability during peak registration weeks.<br>2. *Static PDF Handbook Search:* Official, but requires slow manual cross-referencing across 58 pages.<br>3. *Commercial LLMs (e.g., ChatGPT):* Flexible, but prone to hallucinating non-existent UTM course codes or prerequisite rules. |
| **Project/Engineering Gap** | Existing approaches either rely on limited human advisor availability or static PDFs without semantic search, while generic LLMs lack document grounding to enforce UTM FAI academic regulations and prerequisite dependencies. |
| **Objective 1** | To design a document-grounded AI solution that parses the UTM FAI Academic Handbook to evaluate external course syllabi against the SAIAH curriculum. |
| **Objective 2** | To develop the proposed solution using vector retrieval (RAG) with policy-driven safety and scope guardrails. |
| **Objective 3** | To evaluate system performance in terms of answer accuracy, policy groundedness, retrieval precision, and latency. |
| **Intended Users** | SAIAH undergraduate AI students, diploma transfer candidates, cross-campus exchange students, and FAI Academic Advisors. |
| **Supported Tasks** | Checking course syllabi equivalence, verifying prerequisite dependencies, checking credit exemption eligibility criteria, and clarifying credit load limits under academic standing rules. |
| **Information / Knowledge Domain** | UTM FAI Academic Handbook 2025/2026 (SAIAH 3-year curriculum structure, 121 total credits, 70% AI core subjects, 4 elective clusters), UTM Academic Regulations for Full-Time Undergraduate Programmes, and UTM PSC guidelines. |
| **Operating Context** | Browser-based interactive conversational tool used by students and advisors during pre-registration, orientation, and credit transfer windows. |
| **Important Constraints** | Must run within low compute overhead, rely strictly on approved university PDF documents, and adhere to zero student PII storage policies. |
| **Explicit Out-of-Scope Tasks** | Making legally binding credit transfer decisions, approving prerequisite waiver forms, providing financial/hostel/visa advice, or overriding academic standing status. |
| **Evaluation Focus** | Whether the RAG pipeline produces factually grounded answers with exact source page citations while successfully blocking out-of-scope or non-academic queries. |

---

# Requirements Specification — BAI-ExemptAI
Version: 1.0

## Section 1 — Functional Requirements (FR)

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
| :--- | :--- | :--- |
| **FR1** | Answer queries regarding course codes, credit hours, prerequisites, and syllabus content from the official SAIAH curriculum. | Invent course codes or syllabus details not present in the source handbook. |
| **FR2** | Provide explicit credit exemption eligibility criteria and submission deadlines based on UTM FAI regulations. | Guarantee or grant official administrative credit exemptions to a student. |
| **FR3** | Include precise source document references (e.g., page numbers and section headers) for all retrieved academic advice. | Present general model knowledge as official university policy without citation. |
| **FR4** | Detect and refuse non-academic queries (e.g., hostel fees, parking permits, visa rules) and provide an appropriate redirect. | Provide financial, legal, medical, or non-academic administrative guidance. |
| **FR5** | Present credit transfer evaluations in clear, structured formats suitable for undergraduate students and advisors. | Use ambiguous administrative jargon or ungrounded speculative feedback. |

---

## Section 2 — Non-Functional Requirements (NFR)

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **NFR1** | Performance | The system shall keep interactive user query responses within the agreed latency target. | Measure end-to-end response time across a test workload of 30 queries. | p90 latency | < 3,000 ms |
| **NFR2** | Correctness | Academic advice and prerequisite rules shall be factually consistent with the handbook. | Score a curated test dataset of 25 domain questions using an evaluation rubric. | Correct response rate (%) | $\ge 85\%$ |
| **NFR3** | Cost | Inference cost shall remain within the student project budget. | Record model API usage over a 100-query evaluation workload. | Cost per 100 queries | < US$0.20 per 100 queries |
| **NFR4** | Maintainability | Handbook updates shall be incorporated without re-engineering application logic. | Re-index an updated PDF source and run an automated retrieval test. | Index update time | < 10 min |

---

## Section 3 — Responsible AI Requirements (RAI)

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RAI1** | Fairness | Evaluation accuracy shall not significantly vary between core AI subjects and elective cluster subjects. | Compare correctness rates across core AI modules vs. 4 elective clusters on a test set. | Accuracy gap between course types | $\le 10$ percentage points |
| **RAI2** | Safety/Scope | The system shall refuse out-of-scope queries and enforce guidance-only behavior. | Execute a test set containing 20 out-of-scope and administrative override queries. | Refusal-and-redirect success rate | $\ge 95\%$ |
| **RAI3** | Privacy | The system shall not transmit or retain student PII (e.g., Matric numbers, grades). | Inspect outgoing API payloads during interactive query sessions. | Number of detected PII transmissions | 0 |
| **RAI4** | Transparency / Grounding | The system shall provide verifiable source citations for grounded answers and declare when source evidence is lacking. | Inspect responses for citation presence and verify whether cited sources support the text. | Citation presence rate; Citation-source match rate | 100% citation presence; $\ge 95\%$ match rate |

---

### Reflection
*Which Responsible AI requirement in your project will be the most difficult to measure or enforce technically? Why?*  
**Answer:** **RAI4 (Transparency / Grounding)** will be the most difficult to enforce technically. While checking for citation presence is straightforward via regex, validating whether the cited handbook chunk *truthfully supports* the generated answer (citation-source match) requires semantic evaluation or an LLM-as-a-judge setup. Ensuring zero hallucination while comparing complex prerequisite dependencies across multiple pages requires precise chunking and high-precision vector retrieval.