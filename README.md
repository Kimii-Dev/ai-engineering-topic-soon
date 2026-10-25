# Scholarship Information Assistant ('AI-Finder-Scholarship')

> Answers student questions about scholarship eligibility, CGPA criteria, income thresholds and application deadlines, strictly grounded in official financial aid PDF documents.

## Problem Statement
Students struggle to navigate complex, fragmented scholarship handbooks to find financial aid they qualify for. 'AI-Finder-Scholarship' provides instant, document-grounded eligibility answers and application guidance 24/7.

## Evidence of the Problem
- Financial aid guidelines and eligibility terms are distributed across multiple official PDFs and government portals (Ministry of Higher Education Malaysia).
- 

## Initial Related Work / Existing Approaches
- Human assistance with financial aid – context-aware, but constrained by limited operating times and overload of staff during busy times.
- Website FAQ pages and PDF guides – accurate and reliable, but piecemeal and hard to find using personal criteria.
- Generic AI assistants – versatile and context-aware, but unconnected to the official financial documents and prone to hallucinating.

## Engineering Gap / Limitation
Existing solutions lack natural-language query matching against exact policy clauses with verifiable citations, forcing students to manually filter dense financial PDFs.

## Project Objectives
- O1: Develop an AI-based scholarship advising solution based on document knowledge.
- O2: Implement the retrieval pipeline with safety guardrails and source citation techniques.
- O3: Assess answer quality, eligibility correctness, latency and safety from hallucinations of policies.

## Target Users
Undergraduate and prospective university students searching for scholarships, bursaries and financial aid options.

## Data Sources
- University Undergraduate Scholarships and Financial Assistance Guide PDF
- Guidelines for the Institutional Foundation Endowment Bursary PDF

## Weekly Progress
| Week | Focus | Deliverable | Status |
| :--- | :--- | :--- | :---: |
| W1 | System map + project scope | README + docs | / |