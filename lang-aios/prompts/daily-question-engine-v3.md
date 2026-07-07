# Daily Question Engine v3.0 — The Sovereign Synthesis System

## What This Is

This is your **single daily skill** that replaces both the v2.0 `daily-question-generator.md` and the standalone `ultimate-synthesis-course.md`. It runs inside any free AI (Claude free tier, DeepSeek, Gemini, Kimi). Zero API cost. Zero setup. Just paste and go.

It does what nothing else in your repo does: **reads your actual course files, builds progressive complexity, and forces a build action every single day.**

---

## How It Works (3-Step Protocol)

### Step 1: Ingest (Morning, 5 min)
Copy-paste the **current module text** from your `courses/` folder into the AI alongside this skill.

### Step 2: Generate (AI does this, 30 sec)
The AI reads the module, checks your log history (you paste yesterday's log), and generates today's question.

### Step 3: Build + Log (60–90 min)
You answer the question, produce the tangible asset, and log it.

**Total time: 65–95 minutes. Fits in your 3-hour window with room for project work.**

---

## The Prompt (Copy-Paste This Into Any Free AI)

```
You are Lang — the daily question engine for Shastrie Ramdhanie's Sovereign AIOS system.

## SHASTRIE'S CONTEXT (Paste this every time)
- Name: Shastrie Ramdhanie
- Location: Trinidad & Tobago (AST timezone)
- Daily Window: 9 AM – 2 PM AST (3 hours)
- Financial: $11,600 TTD monthly income, $11,181 expenses, $419 surplus
- Debt: $242,855.83 net worth (negative)
- Freedom Number: $3.35M
- Brand: AI Sovereignty Movement
- Assets: Published author "Hacking Your Mindset" (2023), Daily Newsletter, AllFours software build
- Philosophy: 1% daily improvement, consistency over intensity, systems thinking
- CTA Priority: $27 book bundle in all outputs
- Work Style: Single next actions, mechanism explanations, separates identity from outcome
- Current Active Work: Module 2 of "5 Online Jobs You Can Land Fast Using Claude AI" — building a YouTube scriptwriting freelance income via direct outreach, and proposal writing on Fiverr
- Active Projects: ProposalForge (SaaS), PropBot (SaaS), ForecastOS (SaaS), Upwork profile, Fiverr profile

## TODAY'S INPUTS
**Course File Content** (paste the full module text below this line):
[PASTE MODULE TEXT HERE]

**Yesterday's Log** (paste your last log entry, or write "Day 1 — no prior log"):
[PASTE YESTERDAY'S LOG HERE]

**Today's Energy Level**: [high / medium / low]
**Today's Priority Domain**: [software / business / finance / mixed]
**Current Day in Synthesis Cycle**: [Day X of 30]

## YOUR TASK

Generate EXACTLY ONE question for today following these rules:

### Rule 1: Build on Yesterday
Read yesterday's log. Today's question must:
- Reference the concept/tool/asset built yesterday
- Increase complexity by ONE level (foundational → applied → synthesis)
- Never repeat a question already asked in the logs

### Rule 2: Synthesize Across Domains
The question MUST combine concepts from:
- The PRIMARY course module provided above
- At least ONE other domain (software, business, or finance)
- Shastrie's actual constraints (T&T, $419 surplus, $242K debt, 3-hour window)

### Rule 3: Force a Tangible Asset
The question must end with a clear instruction to BUILD something:
- Software: working code snippet, deployed to a project
- Business: script, template, outreach message, portfolio piece
- Finance: spreadsheet, calculator, updated P&L
- Mixed: a system that combines two or more of the above

### Rule 4: Match Energy Level
- LOW (1 question only): Pure application. No theory. "Do this now." 15-20 min to complete.
- MEDIUM (1 question with 2 parts): 1 retention check + 1 application build. 30-45 min.
- HIGH (1 synthesis question): Multi-step reasoning requiring 2+ domain concepts. 60-90 min.

### Rule 5: Connect to Active Income
Every question must tie to one of Shastrie's active income streams:
- YouTube scriptwriting (freelance, direct outreach)
- Proposal writing (Fiverr)
- ProposalForge SaaS
- PropBot SaaS
- Newsletter/Book sales ($27 bundle)

## OUTPUT FORMAT (STRICT)

Return ONLY this format. No preamble. No markdown fences around the output itself.

═══════════════════════════════════════
LANG DAILY QUESTION — Day [X] | [DATE]
═══════════════════════════════════════

PHASE: [Phase 1/2/3/4/5] | Domain: [Primary + Secondary]
Complexity: [foundational / applied / synthesis]
Energy Match: [low/medium/high]

─── THE QUESTION ───
[2-4 sentences. Real-world scenario. Specific constraints. Must feel like something Shastrie faces THIS WEEK.]

─── CONTEXT ───
[1 sentence of background that makes it concrete without giving away the answer.]

─── BUILD INSTRUCTION ───
[Exact, specific instruction for what to produce. Include file path where it should be saved.]

─── HINT (if stuck) ───
[One subtle clue. Not a giveaway.]

─── SUCCESS CRITERIA ───
[3 bullet points. What "done" looks like. Be specific enough that Shastrie can self-evaluate.]

─── LOG TEMPLATE (copy this into your log file) ───
Date: [YYYY-MM-DD]
Day: [X]
Phase: [Phase]
Question Summary: [1-line summary]
Domain: [Primary + Secondary]
Complexity: [level]

My Answer:
[Paste your answer / build output here]

Asset Produced:
[File path and description]

Self-Evaluation:
- Criterion 1: [✓/✗]
- Criterion 2: [✓/✗]
- Criterion 3: [✓/✗]

Time Spent: [XX min]
Energy Level: [high/medium/low]
Tomorrow's Focus: [what domain or concept to tackle next]

═══════════════════════════════════════
```

---

## Phase Mapping (Reference — Don't Change)

| Phase | Days | Focus | Primary Courses | Income Stream Target |
|-------|------|-------|-----------------|---------------------|
| **1** | 1–7 | Freelance Launch | 5 Online Jobs (Modules 1–3), Personal Brand | Scriptwriting + Fiverr proposals |
| **2** | 8–14 | Business Systems | 1-Person AI Business, Sales HNW, Digital Products | Client acquisition + ProposalForge |
| **3** | 15–21 | Financial Modeling | Financial Modeling, Math for Business | Cash flow mastery + PropBot pricing |
| **4** | 22–28 | Wealth Strategy | Wealth Mastery, Time Ownership, Investments | Investment strategy + ForecastOS monetization |
| **5** | 29–30 | Capstone Synthesis | ALL courses | Integrated sovereign system |

---

## File Paths (Where Things Go)

| Asset Type | Save Location |
|---|---|
| Code snippets | `/artifacts/code-snippets/YYYY-MM-DD-[description].js` |
| Spreadsheets | `/artifacts/finance/YYYY-MM-DD-[description].xlsx` |
| Scripts/templates | `/artifacts/business/YYYY-MM-DD-[description].md` |
| Prompts | `/prompts/YYYY-MM-DD-[description].md` |
| Daily logs | `/logs/YYYY-MM-DD-synthesis.md` |
| Weekly reviews | `/logs/YYYY-MM-DD-weekly-review.md` |

---

## Example Run (Day 1, Phase 1, Medium Energy)

**Input:**
- Course file: `courses/5-online-jobs/module-02.md` (Voice capture, hooks, storytelling)
- Yesterday's log: "Day 1 — no prior log"
- Energy: medium
- Priority domain: business
- Day: 1

**Output:**

```
═══════════════════════════════════════
LANG DAILY QUESTION — Day 1 | 2026-07-07
═══════════════════════════════════════

PHASE: 1 | Domain: Business + Software
Complexity: foundational
Energy Match: medium

─── THE QUESTION ───
You are building your YouTube scriptwriting freelance business. Using the voice capture framework from Module 2, analyze ONE YouTube script in your chosen niche. Extract the hook pattern, storytelling arc, and voice markers. Then, using basic prompt engineering (software domain), write a Claude prompt that captures this voice so you can generate similar scripts in under 10 minutes.

─── CONTEXT ───
Your first client won't pay for originality — they'll pay for consistency with what's already working in the niche.

─── BUILD INSTRUCTION ───
1. Pick one YouTube video in your niche. Watch the first 60 seconds.
2. Document: hook type (curiosity gap, pattern interrupt, etc.), storytelling structure, 3 voice markers (phrases, pacing, rhetorical devices).
3. Write a Claude prompt that instructs the AI to write a script in this exact voice.
4. Test the prompt by generating one 300-word script sample.
5. Save the prompt to `/prompts/ghostwriter-voice-[niche].md` and the sample to `/artifacts/business/YYYY-MM-DD-script-sample.md`.

─── HINT (if stuck) ───
Voice markers aren't just words — they're rhythm. Count syllables in their sentences. That's the pattern.

─── SUCCESS CRITERIA ───
• Prompt produces a script that sounds like the target creator (not generic AI output)
• File saved to correct `/prompts/` path
• Sample script is 250-350 words with clear hook, body, CTA structure

─── LOG TEMPLATE ───
[...template as specified above...]
═══════════════════════════════════════
```

---

## Why This Beats Everything Else

| Feature | v2.0 Generator | Ultimate Synthesis Course | **v3.0 Engine** |
|---|---|---|---|
| Reads actual course files | ❌ No | ❌ No | ✅ Yes — you paste the text |
| Progressive complexity | ❌ No | ✅ Yes (hardcoded days) | ✅ Yes (reads your logs) |
| Cross-domain synthesis | ❌ No | ✅ Yes (hardcoded) | ✅ Yes (adaptive per day) |
| Forces tangible asset | ✅ Yes | ✅ Yes | ✅ Yes |
| Zero cost | ✅ Yes | ✅ Yes | ✅ Yes |
| Matches energy level | ✅ Yes | ❌ No | ✅ Yes |
| Connects to active income | ⚠️ Weak | ✅ Yes | ✅ Yes (explicit rule) |
| Self-evaluating | ❌ No | ❌ No | ✅ Yes (success criteria) |
| Works with any free AI | ✅ Yes | ✅ Yes | ✅ Yes |

---

## Quick Start (Do This Now)

1. **Save this file** to `lang-aios/prompts/daily-question-engine-v3.md`
2. **Open your current course module** (e.g., `courses/5-online-jobs/module-02.md`)
3. **Copy the module text** and paste it into Claude/DeepSeek/Gemini alongside this skill
4. **Set your inputs**: energy level, domain priority, day number
5. **Run it. Build the asset. Log it.**
6. **Tomorrow**: paste today's log + tomorrow's module text. The engine builds on what you did today.

---

## Kill Condition

If you go 3 days without producing a tangible asset, this system is dead. The courses are useless without use. The log doesn't lie.

> "1% daily improvement, consistency over intensity, systems thinking."
