# Daily Briefing Generator

## Purpose
Generate a single morning briefing that compresses your Mind/Body/Wealth priorities, active project status, and the one highest-leverage action for your 3-hour window — without re-explaining your whole context each time.

## Input Required
1. **TODAY'S CONSTRAINTS**: [Energy level — high/medium/low; any time already lost]
2. **ACTIVE PROJECT FOCUS**: [Which project(s) you're touching today — or "unsure, tell me"]
3. **YESTERDAY'S UNFINISHED ITEM**: [If any — paste it, or "none"]
4. **FINANCIAL SNAPSHOT** (optional): [Current surplus/debt numbers if you have them handy — otherwise Claude notes "pull from Supabase"]

## The Prompt

Run this with Claude/Kimi:

---
You are my daily briefing generator. Compress the following into ONE scannable briefing for a 3-hour focused work window (Trinidad & Tobago, zero-budget, AI-execution model).

**Today's Energy:** [TODAY'S CONSTRAINTS]
**Project Focus:** [ACTIVE PROJECT FOCUS]
**Yesterday's Unfinished Item:** [YESTERDAY'S UNFINISHED ITEM]
**Financial Snapshot:** [FINANCIAL SNAPSHOT or "pull from Supabase system_state"]

**Output Format (strict):**
TODAY'S BRIEFING — [DATE]
Hour 1 (Creation/Trust): [single specific task, time-boxed]
Hour 2 (System Engineering): [single specific task, time-boxed]
Hour 3 (Testing/Learning): [single specific task, time-boxed]
Carry-Over Risk: [is yesterday's unfinished item blocking today? yes/no + 1-line fix]
Mind/Body/Wealth Check: [one line each — what moves today, even slightly]
Kill Date Watch: [any project approaching kill_date — flag or "none active"]
If Low Energy: [fallback: the ONE thing to do if the 3-hour window collapses to 30 minutes]

**Rules:**
- No padding, no motivational filler.
- Every task must be specific enough to start without further thinking.
- If energy is "low," automatically shrink Hours 2-3 into optional/skip and expand the Hour 1 task as the sole priority.
---

## Usage Notes
- Run this first thing, before opening any project files — it's meant to decide what before you context-switch into how.
- For SOVEREIGN sessions, this briefing slots in before the BOOT SEQUENCE — use its output to pick which sub-prompt to load.
- Store each day's briefing output in `logs/YYYY-MM-DD-briefing.md` for a searchable history of what you actually worked on vs planned.

## Remember This
- **Q:** What does the Daily Briefing do with low energy input?  
  **A:** Shrinks to one Hour 1 task, marks Hours 2-3 optional.
- **Q:** Where do briefing outputs get archived?  
  **A:** GitHub repo, `logs/` folder, one file per day.
