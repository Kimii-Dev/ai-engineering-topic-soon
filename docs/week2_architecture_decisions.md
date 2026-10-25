# Section 1 — Requirements to Architecture Mapping

| Requirement ID | What is needed in the requirement? | Architecture Response |
| :--- | :--- | :--- |
| **FR2 / RAI4** | Answers should provide verifiable citations and factual answers. | Vector Index & Retrieval Component for providing official document pieces as context. |
| **RAI2** | Queries which do not fall within the scope or are not authorized should not be allowed. | Input Scope / Safety Control filter at the application entry point. |
| **NFR2** | High accuracy in answering questions through the institutional PDF. | Document Data Pipeline (Loader, Cleaner, Chunker, Embedder) and Knowledge Store. |
| **NFR1** | Response latency time should be less than 3,000 ms end-to-end. | Streamlined RAG pipeline with efficient vector retrieval and fast LLM inference service. |

---

# Section 2 — Architecture Decision Records (ADR)

### Decision 1: Include Retrieval-Augmented Generation (RAG) Data Pipeline
* **Requirement/Constraint:** FR1, FR2, RAI4 (All answers must be strictly based on official documents with citations).
* **Options Considered:** 
  1. Base LLM without retrieval (Uses only pre-trained knowledge).
  2. Keyword Search for static keyword search providing PDF links.
  3. Dynamic Knowledge Access (RAG) with Vector Store.
* **Option Selected:** Dynamic Knowledge Access (RAG Pipeline).
* **Compromise Made:** Increased architectural complexity and retrieval latency for no-hallucinations policy and verifiable citations.

### Decision 2: Implement Explicit Input/Output Scope Control
* **Requirement/Constraint:** RAI2, FR4 (Queries which fall out-of-scope or are inappropriate have to be rejected).
* **Options Discussed:**
  1. Instructions through system prompt alone.
  2. Scope/Safety Control module dedicated for this purpose.
* **Option Selected:** Scope/Safety Control module at the application level.
* **Trade-Off Agreed:** False positives in query rejection along with some latency overhead in favor of robust safety barriers for non-financial/non-harmful queries.

---

# Section 3 — Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
| :--- | :--- | :--- | :--- | :--- |
| **[01]** | FR2 / RAI4 | Source Citation and Grounding Match | Knowledge Source and Vector Index | Automatic detection of citation on 30 queries. |
| **[02]** | RAI2 / FR4 | Out-of-Scope Refusal Ratio | Input Scope and Safety Control | Ratio of successful refusals on 20 safety tests. |
| **[03]** | NFR1 / NFR2 | Response Latency and Correctness | Language Model Service and Evaluation Point | Logs of latency and correctness evaluation by experts. |

---

### Reflection
**Which architecture decision involved the most important trade-off? Which requirement drove the decision, and what trade-off did you accept?**

*The implementation of a **dynamic knowledge access (RAG) pipeline** came at the cost of the most critical compromise. In accordance with **RAI4 (Transparency/Grounding)** and **FR2 (Source Citations)**, I made peace with a complex pipeline (including chunking, embeddings, vector database), along with increased retrieval time, in order to ensure the grounding of all financial statements in a reliable university PDF.*