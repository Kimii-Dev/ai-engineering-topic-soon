# Project Scope: AI Scholarship Information Assistant

**Project Name:** AI-Finder-Scholarship
**Domain:** Higher Education / Student Financial Services

## Problem Statement
The rules for accessing higher education scholarships and financial aid are determined through complex processes of eligibility conditions, income level, CGPA cutoffs and strict deadlines found within several PDF manuals. It is common for students to either miss application deadlines or apply for inappropriate scholarships because of lack of information. With AI engineering, an assistance program can be built to extract eligible opportunities based on a natural language query by users.

## Evidence of the Problem
- Evidence 1: The public higher education bodies run huge scholarship and bursary guidelines in different administrative portals which lead to high query load and navigation problems.
- Source / Citation: Financial Aid Guidelines & Student Services Directory from Ministry of Higher Education Malaysia
- Evidence 2: 

## Initial Related Work
- Study / Solution 1: Manual consultation with university financial aid officers -> Limitation: Limited by office hours and slow response time during the application season.
- Study / Solution 2: Printed PDFs for scholarships and noticeboards on website -> Limitation: Spread out over multiple platforms, cumbersome to search manually and difficult to overlook subtle qualifications for the applicants.
- Study / Solution 3: Generic web/LLM search -> Limitation: Lack of verifiable basis from official guidelines and the risk of hallucinations for income ceilings and qualifications.

## Engineering Gap / Limitation
The available systems are either manually curated by filtering out documents or use generic AI models that are not grounded in any way and do not have citation capabilities.

## Initial Project Objectives
- O1: Develop a document-based AI solution based on policies of the university and foundation for academic scholarship.
- O2: Develop a retrieval system with clear guardrails that ensures all responses are grounded in the policies of acceptable documents.
- O3: Assess the system based on measures of accuracy, eligibility grounding, latency and resistance to fraudulent financial claims.

## Target Users
Undergraduate and prospective university students searching for scholarships, bursaries and financial aid options.

## Data Sources
- Source 1: University Undergraduate Scholarships and Financial Assistance Guide PDF
- Source 2: Guidelines for the Institutional Foundation Endowment Bursary PDF

## Differences from EduAdvisor
- Similar to EduAdvisor: Has a document-based RAG framework which includes vector-based retrieval, metrics and safety guardrails.
- Not similar to EduAdvisor: Is concerned with eligibility criteria related to finances, income limits of family members, CGPA criteria and deadline for awards.

## Responsible AI Risks
- Risk 1 (Hallucination): The model generates imaginary scholarships awards, false income limits or false application deadlines, leading to the generation of invalid applications by the students.
- Risk 2 (Fairness): Inadequate representation of certain niche bursary documents results in unequal distribution of retrieval effectiveness among diverse student populations.
- Risk 3 (Safety Risk): Users enter personal financial information within their queries which the system must not record or reveal any identifiable financial data of users.