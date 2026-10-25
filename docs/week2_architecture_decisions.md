# Architecture Requirements Mapping & Decisions — BAI-ExemptAI

## Section 1 — Architecture Needs Identification

| Requirement ID | What does the requirement need? | Architecture Response |
| :--- | :--- | :--- |
| **FR1 / NFR2** | Access to up-to-date SAIAH 3-year curriculum, core course syllabi, and prerequisite rules. | Grounded Document Store & Retrieval Engine (Vector DB containing parsed handbook chunks). |
| **FR3 / RAI4** | Answers must cite exact handbook source page numbers and sections. | Metadata Tracking Module attached to document loader and retriever pipeline. |
| **RAI2 / FR4** | Non-academic queries (hostel, fees, visa) must be intercepted and refused. | Input Scope & Safety Guardrail filter placed before retriever execution. |
| **NFR1** | End-to-end interactive response time must remain under 3 seconds. | Efficient vector indexing (FAISS) and lightweight embedding/LLM orchestration. |
| **RAI3** | Zero student PII transmission to external model endpoints. | In-memory query sanitization layer prior to LLM invocation. |

---

## Section 2 — Architecture Decision Records (ADR)

### Decision 1: Retrieval-Augmented Generation (RAG) vs. Model Fine-Tuning
* **Requirement / Constraint:** FR1, FR3, NFR4, RAI4 (Must provide grounded answers with exact source citations and support rapid handbook updates).
* **Alternatives Considered:** 
  1. Base LLM prompt engineering only
  2. Fine-tuning a domain LLM on handbook text
  3. Retrieval-Augmented Generation (RAG) over vector embeddings
* **Selected Option:** RAG over vector embeddings (FAISS / MiniLM embeddings).
* **Trade-off Accepted:** Increased architectural complexity (vector storage and chunking pipeline), but guarantees factual grounding, exact page citations, and zero cost when updating handbooks.

### Decision 2: Explicit Pre-Retrieval Guardrail vs. System Prompt Instruction Only
* **Requirement / Constraint:** RAI2, FR4 (Out-of-scope queries must be reliably refused with $\ge 95\%$ success).
* **Alternatives Considered:** 
  1. Relying solely on system prompt refusal rules in the LLM
  2. Dedicated pre-retrieval input guardrail component
* **Selected Option:** Dedicated pre-retrieval input guardrail component (keyword/intent classifier).
* **Trade-off Accepted:** Slight additional execution latency overhead (~50ms), but prevents unnecessary vector search / LLM API calls on out-of-scope queries while ensuring high safety reliability.

---

## Section 3 — Initial Requirements Traceability Matrix

| Objective | Requirement ID | Evaluation Criterion | Architecture Element | Later Evidence |
| :--- | :--- | :--- | :--- | :--- |
| **O1** | FR1 / FR3 | Source Citation & Grounding | Document Loader, Vector Store (FAISS), Metadata Retriever | Automated test evaluating citation presence and page accuracy rate on 25 sample queries. |
| **O2** | RAI2 / FR4 | Out-of-Scope Refusal | Input Scope & Safety Guardrail Filter | Execution of 20 out-of-scope test cases verifying refusal message and HTTP response code. |
| **O3** | NFR1 / NFR2 | Response Latency & Correctness | RAG Engine, LLM Service, Evaluation Logger | Benchmarking script recording p90 end-to-end latency and rubric correctness scores across 30 queries. |

---

### Reflection
*Which architecture decision involved the most important trade-off? Which requirement drove the decision, and what trade-off did you accept?*  
**Answer:** **Decision 1 (RAG vs. Fine-Tuning)** involved the most important trade-off. It was driven by **RAI4 (Transparency/Grounding)** and **NFR4 (Maintainability)**. We accepted the trade-off of higher system architectural complexity (managing chunking strategies, embeddings, and vector stores) rather than simply calling a model API, because RAG is the only architecture that provides exact, verifiable page citations and allows instant handbook updates without expensive retraining.