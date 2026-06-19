# Courses — Daily Learning System

**Purpose:** Store all AI-generated courses. Pull daily questions for consistent learning without re-reading entire modules.

**How It Works:**
1. Save each course as a folder with numbered modules
2. Run `daily-question-generator.md` skill each morning
3. Answer 1-3 questions in `logs/` or verbally to AI
4. Track streak and completion in `course-index.md`

**Folder Structure:**
courses/ 
├── README.md 
├── course-index.md 
├── daily-question-generator.md 
├── ai-business-claude/ 
│ ├── module-01.md │ 
├── module-02.md │ └── ... 
├── mindset-systems/ │ 
├── module-01.md │ └── ... └── ...

**Rules:**
- One course per folder
- Modules numbered sequentially
- Each module must have a "Key Concepts" section at the bottom (used by the question generator)
- No course longer than 10 modules (split if needed)

## 📚 Courses Folder (`/courses`)

This folder contains plain-text learning resources covering **Coding, Math, Algorithms, Business, and Finances**. Since all files are `.txt` or `.md`, they can be fed directly into your AI with zero preprocessing—maximizing your limited 3-hour daily window.

### Recommended Folder Structure
Organize your text files by domain for easier retrieval:

/courses/
├── coding/          # Language syntax, frameworks, best practices
├── math/            # Linear algebra, calculus, statistics for AI/Dev
├── algorithms/      # Data structures, sorting, dynamic programming
├── business/        # Sales, marketing, operations, systems thinking
├── finances/        # Accounting, valuation, cash flow management
└── daily-question-generator.md  # YOUR CORE TOOL (see below)

---

## 🚀 The "Sovereign" Playbook: How to Get the HIGHEST Value

Since you have **3 hours/day** and a **$419 TTD** constraint, passive reading is a waste of time. Here is the exact system to turn every text file into applied, profit-generating knowledge.

### 1. The Daily Question Generator (Your Primary Engine)
Your `daily-question-generator.md` is the most important file in this folder. Before you read *any* new course text, run this prompt with your AI:

> *"Using the `daily-question-generator.md` framework, take this course text and generate 3 specific questions. They must force me to: (1) Recall the core rule, (2) Apply it to my current active project (e.g., PropBot or Proposal-Forge), and (3) Adapt it to my Trinidad & Tobago market context."*

**Why this gives max value**: It turns passive text into an active, high-stakes quiz. You don't read to "know"; you read to *answer*. This drastically reduces study time and increases retention.

### 2. The "Build or Compute" Rule (Coding, Math, Algorithms)
For technical texts, **never read code or formulas without executing them**.
- Copy the code/algo from the text file and paste it into your AI.
- Prompt: *"Rewrite this [algorithm/formula] to solve my specific problem in [Project Name]. Then, explain it to me like I'm building an MVP, not a PhD thesis."*
- Immediately save the AI's working implementation into `/artifacts/code-snippets/`. 
- **Value**: You now own a working piece of code, not just a textbook concept.

### 3. The "Framework Extraction" Rule (Business & Finances)
For business and finance texts, your goal is to extract **calculators and checklists**.
- Take a chapter on, say, "Cash Flow Management" or "Value-Based Pricing."
- Prompt: *"Extract the exact mathematical formula or step-by-step checklist from this text. Turn it into a reusable prompt I can add to my `/prompts` folder for future proposal generation."*
- Save the resulting prompt in `/prompts/finance-pricing-expert.md`.
- **Value**: Next time you write a client proposal, your AI will automatically apply that financial framework without you re-reading the book.

### 4. The "Synthesize Across Domains" Hack (The Superpower)
This is where you get **exponential** value. Since you have Coding, Math, *and* Business texts, merge them:
- Take an algorithm from `/algorithms` and a business constraint from `/business`.
- Prompt: *"Combine the efficiency principle from this algorithm with the customer acquisition framework from this business text. Design a lean workflow for my daily 3-hour block."*
- **Value**: You create interdisciplinary insights that most founders miss. This makes your `AIOS` system truly unique.

### 5. The 24-Hour Log Rule (Close the Loop)
After using the Daily Question Generator and applying the lesson, you **must** log it within 24 hours.
Create a log entry in `/logs/course-applications.md` with this exact format:
- **Date**: [Today]
- **Source**: [Course file name]
- **Question Asked** (from the generator): [The question]
- **My Action**: [What I coded, built, or priced]
- **Result**: [Did it save time? Make money? Fix a bug?]
- **Tweak**: [What I changed to fit my local context]

**Why this gives max value**: This log becomes your *custom* playbook. After 10 logs, you stop needing the original courses altogether—you just read your own battle-tested adaptations.
