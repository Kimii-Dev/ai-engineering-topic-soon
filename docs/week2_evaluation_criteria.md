# Evaluation Criteria — Scholarship Information Assistant

Version: 1.0

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Evaluation Method | Metric | Threshold | User / Business Outcome |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **O3 / NFR2** | Policy Answer Correctness | Domain-specific capability | Assess a test set of 30 common eligibility query cases against ground-truth PDF rules. | Accuracy of responses (%) | ≥ 85% | Students get reliable advice about financial aid policies. |
| **O1 / FR2 / RAI4** | Source Citation & Grounding Check | Instruction-following capability | Check outputs for citation tags, match with source document chunks. | Citation inclusion rate which matching rate | 100% inclusion which ≥ 95% match | Students will be able to check the correctness of the policy rules against official PDF of the university. |
| **O2 / RAI2** | Out-of-Scope Queries Refusal | Instruction-following capability | Test the system with 20 out-of-scope queries (e.g. loan scam, registration). | Refusal rate (%) | ≥ 95% | Protection against making mistakes in financial matterswhich prevents abuse of the system. |
| **O3 / NFR1** | Response latency | Cost and latency | Calculate the total processing time through the entire evaluation workload. | p90 latency | < 3,000 ms | Assures that the system provides a good user experience for students portals. |
| **O1 / FR5** | Response clarity | Generation capability | Rate response clarity and formatting based on a specific rubric (scale of 1-5). | Average clarity score | ≥ 4.0 / 5.0 | The students understand income criteria and application process. |

---

### Reflection
**Reflection: Which evaluation criterion is most important for determining whether your AI application will be useful to its intended users? Why?**

*The **Source Citation & Grounding Match (RAI4)** criterion is the most important. As applications for financial assistance are tied to certain deadline constraints and the cutoff date for eligibility, a fictitious criterion will definitely put a student at risk of losing his or her scholarship or filling out an application that won't be counted. Full 100% citation presence with valid sources matches makes everything transparent and credible for students.*