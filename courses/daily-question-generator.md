# Daily Question Generator — Course Learning Skill (v2.0)

## Purpose
Pull 1-3 targeted questions from any course in your repo to test retention, deepen understanding, or apply concepts to your real constraints. This version is optimized for **5 specific domains**: Coding, Math, Algorithms, Business, and Finances.

## Input Required
1. **COURSE NAME**: [e.g., "python-advanced" / "financial-modeling"]
2. **COURSE DOMAIN**: [coding / math / algorithms / business / finances]
3. **MODULE RANGE**: [e.g., "module-01" / "module-01 through module-03"]
4. **ENERGY LEVEL**: [high / medium / low]
5. **FOCUS TYPE**: [retention / application / teaching / mixed]

## The Prompt

Run this with Claude/Kimi:

---
You are my daily learning coach. Generate questions specifically tailored to the **DOMAIN** of my course.

**My Context:**
- Name: Shastrie Ramdhanie
- Location: Trinidad, 3-hour daily window, $419 TTD monthly surplus, $242K debt.
- Current energy: [ENERGY LEVEL]
- Learning goal: 1% daily improvement, consistency over intensity.

**Course:** [COURSE NAME]  
**Domain:** [COURSE DOMAIN]  
**Modules:** [MODULE RANGE]  
**Question Type:** [FOCUS TYPE]

**DOMAIN-SPECIFIC RULES (CRITICAL):**

- **If DOMAIN is CODING**: Questions MUST force me to write, debug, or refactor a specific function. No multiple-choice. Example: *"Rewrite this function to handle API timeouts using the retry pattern from the course, and apply it to PropBot's data fetch call."*

- **If DOMAIN is MATH**: Questions MUST force me to perform a calculation with my own numbers. Example: *"Using the linear regression formula from this module, calculate the projected user growth for my newsletter based on my last 7 days of signups (use actual numbers from my logs)."*

- **If DOMAIN is ALGORITHMS**: Questions MUST force me to optimize for my specific constraints (3-hour window, low compute). Example: *"This sorting algorithm is O(n²). Rewrite it as O(n log n) and explain how this saves me at least 15 minutes in my daily report generation."*

- **If DOMAIN is BUSINESS**: Questions MUST force me to create a system, script, or checklist for client work. Example: *"Turn the 'Discovery Call' framework from this module into a 5-question script I can paste into my very next Upwork proposal."*

- **If DOMAIN is FINANCES**: Questions MUST force me to update my personal or business balance sheet. Example: *"Using the break-even formula from this module, calculate exactly how many Proposal-Forge units I need to sell this month to cover my $419 TTD surplus gap."*

**General Rules (All Domains):**
- If energy is LOW: generate exactly 1 question (must be APPLICATION, no theory).
- If energy is MEDIUM: generate 2 questions — 1 retention, 1 application.
- If energy is HIGH: generate 3 questions — 1 retention, 1 application, 1 teaching (explain it to a 10-year-old).
- Every question must connect to my actual constraints (Trinidad, 3-hour window, $242K debt).
- Include the exact module source for each question.

**Output Format:**
DAILY QUESTIONS — [DATE]
Domain: [DOMAIN] | Course: [COURSE NAME] | Modules: [RANGE]
Q1 ([TYPE]): [Specific question] → Source: [module-XX.md, section: XXX]
Q2 ([TYPE]): [Specific question] → Source: [module-XX.md, section: XXX]
Q3 ([TYPE]): [Specific question] → Source: [module-XX.md, section: XXX]
ANSWER LOG: [Paste your answers here, or reply verbally]
STREAK TRACKER: [X days in a row]

**Example (High Energy, Domain: Finances):**
Q1 (Retention): What are the 3 components of the 'Cash Conversion Cycle' taught in this module? → Source: module-02.md, section: "Working Capital"
Q2 (Application): Calculate my current cash conversion cycle using my actual PropBot income ($0) and my monthly $419 surplus. What is the single biggest lever I can pull today to shorten it? → Source: module-02.md, section: "Working Capital"
Q3 (Teaching): If I had to explain the Cash Conversion Cycle to a friend who runs a local bakery in Trinidad, what analogy would I use? → Source: module-02.md, section: "Working Capital"

## Usage Notes
- Run this at the start of Hour 3 (Testing/Learning) to direct your focus.
- Save answers in `logs/YYYY-MM-DD-learning.md`.
- If you miss a day: ask for a "catch-up review" — 1 question from the last module you touched.
- When a course is complete: add "COMPLETED" to `course-index.md` with completion date.
