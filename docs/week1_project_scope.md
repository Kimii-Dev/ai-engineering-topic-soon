# Project Scoping Document

**Project Name:** BAI-ExemptAI - UTM AI Credit Transfer & Prerequisite Assistant  
**Domain:** Higher Education / Academic Administration

## Problem Statement
The evaluation process is slow for students joining the Bachelor in Artificial Intelligence with Honours (SAIAH) program at UTM Faculty of Artificial Intelligence (FAI), who include diploma entry students, direct entry students and transfer students. The SAIAH program runs for three years and entails 121 credits, which is 70% AI-related content in complicated subjects such as Python Programming, Mathematics for ML, Deep Learning and AI Engineering with four elective clusters. This makes the syllabi comparison process difficult and can lead to enrollment problems. Through AI engineering, one is able to develop an assistant that does semantic syllabus matching and confirms exemption credit eligibility from the FAI regulations.

## Evidence of the Problem
1. **Evidence 1:** The FAI Academic Handbook states that applications for credit exemptions should be made within tight deadlines (within Week 10 of the first semester) and that they have to go through verification of the syllabi and transcripts against UTM courses.
   * *Source/Citation:* UTM Faculty of Artificial Intelligence Academic Handbook 2025/2026, p. 42 (Credit Exemption & Credit Transfer).
2. **Evidence 2:** Those who do not control their course registration well or find themselves in Conditional Status (KS, CGPA < 2.00) are restricted to taking 9 to 13 units per semester, failing which can lead to termination of studies.
   * *Source/Citation:* FAI Academic Handbook 2025/2026, pp. 42 & 45 (Credit Load Per Semester & Academic Standing).

## Initial Related Work / Existing Approaches
1. **Study/Solution 1:** Manual Advisor Sessions
   * *Source/Citation:* UTM FAI Academic Advisory System
   * *Major Drawback:* Restricted by the availability of lecturers during high registration periods.
2. **Study/Solution 2:** Static PDF of FAI Academic Handbook Search
   * *Source/Citation:* FAI Bachelor in Artificial Intelligence Academic Handbook 2025/2026
   * *Major Drawback:* Static PDF document that needs manual referencing across 58 pages containing course codes, prerequisites and clusters.
3. **Study/Solution 3:** Untrained Commercial LLMs (ChatGPT)
   * *Source/Citation:* Standard commercial conversational AI applications
   * *Major Drawback:* Likelihood to hallucinate non-existing course codes, prerequisite chains and wrong credit transfer limits.

## Engineering Gap / Limitation
Current methods rely on restricted access to human advisors office hours or static PDF manuals that do not offer semantic search capabilities, whereas generic LLMs fail to have document grounding to ensure UTM FAI academic and prerequisite rules.

## Initial Project Objectives
* **O1:** Design a document-based AI solution to analyze the UTM FAI Academic Handbook and compare external courses syllabuses against the SAIAH curriculum.
* **O2:** Develop the proposed solution using vector retrieval (RAG) with policy-oriented safety guardrails.
* **O3:** Assess the performance of the developed system based on answer accuracy, policy grounding, retrieval precision and latency.

## Target Users
AI undergraduates (SAIAH), candidates for diploma transfers, exchange students and FAI Academic Advisors.

## Data Sources
1. **Source 1:** UTM Faculty of Artificial Intelligence Academic Handbook 2025/2026 (Bachelor in Artificial Intelligence with Honours - SAIAH) PDF
   * *URL:* `https://fai.utm.my/undergraduate-registration-kit/`
2. **Source 2:** UTM Academic Regulations for Full-Time Undergraduate Programmes PDF
   * *URL:* `https://ugs.utm.my/academic-rules/`
3. **Source 3:** UTM Professional Skill Certificate (UTM PSC) Guidelines PDF
   * *URL:* `https://ugs.utm.my/utm-professional-skills-certificate-utm-psc/`

## Relation to EduAdvisor Benchmark
**Similar to EduAdvisor:** Utilizes Retrieval-Augmented Generation (RAG) via the official academic PDF files to prevent any kind of hallucinations.
**Difference from EduAdvisor:** Customized for the 3-year Bachelor of Artificial Intelligence program at UTM FAI, comprising 70% AI core subjects (SAIA 1113-SAIA 3146), 4 specialized elective groupings (AI Advanced Algorithms, Robotics & Automation, AI Business, AI Application) and UTM GPA/CPA system academic requirements.

## Responsible AI Risks
* **Risk 1 (Hallucination):** Model generates an invalid transfer of credit for a key AI subject (e.g., SAIA 2113 Machine Learning), causing a student to lack important prerequisite information.
* **Risk 2 (Bias/Fairness):** Unusual names of courses from other polytechnics or international universities get low semantic match scores.
* **Risk 3 (Safety/Scope):** Student misunderstands guidance from the system as an official exemption from evaluation which needs a guardrail to limit scope to pre-evaluation only.