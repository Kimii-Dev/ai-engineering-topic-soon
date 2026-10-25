# Project Scoping Document

**Project Name:** BAI-ExemptAI - UTM AI Credit Transfer & Prerequisite Assistant  
**Domain:** Higher Education / Academic Administration

## Problem Statement
Students entering or transferring into the Bachelor in Artificial Intelligence with Honours (SAIAH) at the UTM Faculty of Artificial Intelligence (FAI)—including diploma holders, direct-entry candidates, and cross-campus students—face delays evaluating credit exemptions, elective cluster alignment, and prerequisite dependencies. The 3-year degree structure (121 total credits) features 70% core AI content across complex courses (e.g., Python Programming, Mathematics for ML, Deep Learning, AI Engineering) and 4 elective clusters, making manual syllabus cross-referencing tedious and prone to registration errors. An AI engineering approach enables a document-grounded assistant that performs semantic syllabus matching and verifies credit exemption eligibility against official FAI regulations.

## Evidence of the Problem
1. **Evidence 1:** According to the FAI Academic Handbook, credit exemption applications must be submitted within strict timeframes (by Week 10 of the first semester) and require detailed syllabus and transcript verification against UTM course standards.
   * *Source/Citation:* UTM Faculty of Artificial Intelligence Academic Handbook 2025/2026, Page 42 (Credit Exemption & Credit Transfer).
2. **Evidence 2:** Students who fail to manage their course registrations properly or fall into Conditional Status (KS, CGPA < 2.00) are strictly restricted to 9–13 credits per semester, while failure to register results in termination of study.
   * *Source/Citation:* FAI Academic Handbook 2025/2026, Pages 42 & 45 (Credit Load Per Semester & Academic Standing).

## Initial Related Work / Existing Approaches
1. **Study / Solution 1:** Manual Academic Advisor Consultations
   * *Source / Citation:* UTM FAI Academic Advisory System.
   * *Key Limitation:* Constrained by lecturer availability during peak course registration and add/drop windows.
2. **Study / Solution 2:** Static PDF Academic Handbook Lookup
   * *Source / Citation:* FAI Bachelor in Artificial Intelligence Academic Handbook 2025/2026.
   * *Key Limitation:* Static PDF document requiring manual cross-referencing across 58 pages of course codes, prerequisites, and cluster lists.
3. **Study / Solution 3:** Ungrounded Commercial LLMs (e.g., ChatGPT)
   * *Source / Citation:* Standard commercial conversational AI tools.
   * *Key Limitation:* High risk of hallucinating non-existent course codes, incorrect prerequisite chains, or unapproved credit transfer limits.

## Engineering Gap / Limitation
Existing approaches either depend on limited human advisor office hours or static PDF guides that lack semantic search, while generic LLMs lack document grounding to enforce UTM FAI academic regulations and course prerequisite rules.

## Initial Project Objectives
* **O1:** To design a document-grounded AI solution that parses the UTM FAI Academic Handbook to evaluate external course syllabi against the SAIAH curriculum.
* **O2:** To develop the proposed solution using vector retrieval (RAG) with policy-driven safety and scope guardrails.
* **O3:** To evaluate system performance in terms of answer accuracy, policy groundedness, retrieval precision, and latency.

## Target Users
Undergraduate AI students (SAIAH), diploma transfer candidates, international/exchange students, and FAI Academic Advisors.

## Data Sources
1. **Source 1:** UTM Faculty of Artificial Intelligence Academic Handbook 2025/2026 (Bachelor in Artificial Intelligence with Honours - SAIAH) PDF
   * *URL:* `https://fai.utm.my/`
2. **Source 2:** UTM Academic Regulations for Full-Time Undergraduate Programmes PDF
   * *URL:* `https://ugs.utm.my/academic-rules/`
3. **Source 3:** UTM Professional Skill Certificate (UTM PSC) Guidelines PDF
   * *URL:* `https://ugs.utm.my/utm-professional-skills-certificate-utm-psc/`

## Relation to EduAdvisor Benchmark
* **Similar to EduAdvisor:** Employs Retrieval-Augmented Generation (RAG) over official academic PDF documents to eliminate hallucinated answers.
* **Different from EduAdvisor:** Tailored specifically to the 3-year Bachelor in Artificial Intelligence (SAIAH) curriculum at UTM FAI, including 70% AI core subjects (SAIA 1113 to SAIA 3146), 4 specialized elective clusters (AI Advanced Algorithm, Robotic & Automation, AI in Business, Applied AI), and UTM GPA/CPA academic standing rules.

## Responsible AI Risks
* **Risk 1 (Hallucination):** Model invents an invalid credit transfer for a core AI subject (e.g., SAIA 2113 Machine Learning), leading a student to miss essential prerequisite knowledge.
* **Risk 2 (Fairness):** Non-standard course titles from external polytechnics or international universities receive lower semantic matching scores.
* **Risk 3 (Safety/Scope):** Student misinterprets system guidance as a binding administrative exemption; requires a guardrail enforcing pre-evaluation scope only.