# BAI-ExemptAI - UTM AI Credit Transfer & Prerequisite Assistant

> Evaluates external course syllabi against the official UTM Faculty of Artificial Intelligence (FAI) handbook to provide document-grounded credit exemption and prerequisite guidance.

## Problem Statement
Students in the Bachelor in Artificial Intelligence (SAIAH) program at UTM FAI face multi-week delays evaluating credit exemptions and prerequisite dependencies because course details, cluster electives, and credit rules are scattered across a 58-page handbook. BAI-ExemptAI provides instant, document-grounded guidance to streamline credit evaluation and reduce academic advisor workload.

## Evidence of the Problem
- Credit exemption applications require strict syllabus comparison against UTM core AI subjects and must be filed by Week 10 of Semester 1.
- Incorrect course registration or unapproved prerequisite skipping risks Conditional Academic Standing (KS) or course termination.

## Initial Related Work / Existing Approaches
- **Manual Academic Advising:** Accurate, but constrained by advisor availability during busy registration windows.
- **Static Handbook Search:** Official, but slow to cross-reference manually across core modules and 4 elective clusters.
- **General Commercial LLMs:** Flexible, but prone to hallucinating UTM course codes, credit loads, or grade boundaries.

## Engineering Gap / Limitation
Existing approaches lack a semantic, document-grounded RAG pipeline capable of accurately comparing external syllabus outcomes against UTM FAI core AI requirements and academic rules.

## Project Objectives
- **O1:** Design a document-grounded AI credit exemption assistant for UTM FAI.
- **O2:** Develop the system using vector retrieval (RAG) with policy safety guardrails.
- **O3:** Evaluate answer groundedness, retrieval accuracy, latency, and safety.

## Target Users
Undergraduate AI students (SAIAH), diploma transfer candidates, and FAI Academic Advisors.

## Data Sources
- UTM Faculty of Artificial Intelligence Academic Handbook 2025/2026 (SAIAH) PDF (`https://fai.utm.my/`)
- UTM Academic Regulations for Full-Time Undergraduate Programmes PDF (`https://ugs.utm.my/academic-rules/`)
- UTM Professional Skill Certificate (UTM PSC) Guidelines PDF (`https://ugs.utm.my/utm-professional-skills-certificate-utm-psc/`)

## Weekly Progress
| Week | Focus | Deliverable | Status |
| :--- | :--- | :--- | :---: |
| Week1 | System map + project scope | README + docs | / |