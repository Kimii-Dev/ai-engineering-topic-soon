# BAI-ExemptAI - UTM AI Credit Transfer & Prerequisite Assistant

> Evaluates external course syllabi against the official UTM Faculty of Artificial Intelligence (FAI) handbook to provide document-grounded credit exemption and prerequisite guidance.

## Problem Statement
SAIAH students at UTM FAI experience weeks of delay while getting their credits evaluated for exemption and dependency on prerequisites due to information on course specifications, cluster options and credit requirements being dispersed over a 58-page booklet. This is where BAI-ExemptAI comes into play to provide prompt documentation-based assistance.

## Evidence of the Problem
- Syllabi must be compared strictly to UTM core AI courses for the purpose of credit exemptions, which are submitted at Week 10 of Semester 1.
- Errors in course selection or unauthorized bypassing of prerequisites may lead to Conditional Academic Standing (KS).

## Initial Related Work / Existing Approaches
- **Manual Academic Advising:** Reliable but dependent on advisor availability during peak enrollment periods.
- **Static Handbook Search:** Authoritative but inefficient for manual cross-referencing through all core classes and 4 electives.
- **General Commercial LLMs:** Adaptable but liable to generating fictional UTM course codes, credit loads or grades ranges.

## Engineering Gap / Limitation
Current methods fail to provide a semantic and document-based RAG pipeline for comparing external syllabus results with UTM FAI Core AI requirements and regulations.

## Project Objectives
- **O1:** Create an AI credit exemption assistant using documents for UTM FAI.
- **O2:** Implement the system using RAG (retrieval-augmented generation) with safety policies.
- **O3:** Test groundedness of answers, retrieval quality, latency and safety.

## Target Users
Undergraduate AI students (SAIAH), diploma transfer candidates and FAI Academic Advisors.

## Data Sources
- UTM Faculty of Artificial Intelligence Academic Handbook 2025/2026 (SAIAH) PDF (`https://fai.utm.my/undergraduate-registration-kit/`)
- UTM Academic Regulations for Full-Time Undergraduate Programmes PDF (`https://ugs.utm.my/academic-rules/`)
- UTM Professional Skill Certificate (UTM PSC) Guidelines PDF (`https://ugs.utm.my/utm-professional-skills-certificate-utm-psc/`)

## Weekly Progress
| Week | Focus | Deliverable | Status |
| :--- | :--- | :--- | :---: |
| Week1 | System map + project scope | README + docs | / |