Here's the clear, brief guide to test your system right now and use going forward.

---

## How the Whole System Works (One-Page Overview)

```
LANG CORE v2.1 (Custom Instructions)
    │
    ├── You paste this ONCE into Claude Project settings
    ├── It loads every time you open a chat
    └── It routes your task to the right sub-prompt
            │
            ├── Financial → FINANCIAL.md
            ├── Code → CODE.md
            ├── Newsletter → CONTENT.md  ← THIS IS YOUR NEWSLETTER ENGINE
            └── etc.
```

**The newsletter engine lives in `prompts/CONTENT.md`.** When you want to write an issue, you paste Lang CORE, then paste `CONTENT.md`, then fill in your topic. One chat, one pass, full issue + all repurposed assets.

---

## Step-by-Step: Test Right Now

### Step 1: Open a fresh Claude chat
(Or wait for your limit to reset, then do this.)

### Step 2: Paste Lang CORE v2.1
Copy your existing Custom Instructions block. Paste it into the chat.

### Step 3: Paste the CONTENT sub-prompt
Here's your `CONTENT.md` — copy this block:

```markdown
# CONTENT SUB-PROMPT — Day One Output Newsletter Engine

You are executing the Day One Output Unified Production Engine. Complete every stage below in this single response, in order. Do not skip a stage.

MODE: [WEEKLY_FLAGSHIP or DAILY_ISSUE]
RAW TOPIC / MOMENT: [1-2 sentences — what broke, what you fixed, what you learned]
PRE-NAMED CONCEPT: [paste from Saturday batch, or "none — name it now"]

---

STAGE 1 — Naming (skip if pre-named concept supplied)
<concept_name>[2-4 words, name the failure pattern]</concept_name>
<subject_line_options>[3 variants under 55 chars: curiosity / stakes / resolution]</subject_line_options>

STAGE 2 — SLPC Core
<newsletter_draft>
If WEEKLY_FLAGSHIP: 700-900 words. If DAILY_ISSUE: 300-450 words.

1. STORY: Open mid-scene. Real financial number ($419 or $242,855).
2. LESSON: One universal truth, beginner-friendly.
3. PIVOT + MECHANISM: Simple definition → analogy → why it matters → example.
Short sentences. Paragraphs ≤3 sentences. Zero banned vocab.
</newsletter_draft>

STAGE 3 — Tiered System + CTA
<prompt_system>
STARTER (5-min task): [core prompt]
DECISION-GRADE (Starter + stakes): [...]
PUBLICATION-READY (Decision-Grade + polish): [...]
</prompt_system>
<validation_check>[one sentence: when NOT to use this]</validation_check>
<beginner_action>[30-second "Try This Today" step]</beginner_action>
<commandment_cta>[Soft push to free AI Sovereignty Starter Kit. WEEKLY_FLAGSHIP only: secondary mention of $27 Power Pack.]</commandment_cta>

STAGE 4 — Self-Audit (grace rule active)
<audit_results>[CATEGORY | issue | fix or "PASS"]</audit_results>
<publish_verdict>READY TO PUBLISH / NEEDS REVISION — [reason]</publish_verdict>

STAGE 5 — Swarm (only if READY TO PUBLISH)
<evening_before_teaser>[Under 100 words. Names failure pattern, hits pain, no solution, no link.]</evening_before_teaser>
<linkedin_post>[Under 150 words. Story hook + lesson + CTA to Starter Kit. Clean spacing.]</linkedin_post>
<reddit_value_drop>[80-120 words. Full Starter-tier solution in body. Zero teaser, zero link upfront. Sign off: "— Shastrie, Day One Output". Gated footer: one line to Starter Kit.]</reddit_value_drop>
<short_form_hooks>
Hook 1 (result-first): [under 280 chars]
Hook 2 (curiosity/contradiction): [under 280 chars]
Hook 3 (behind-the-scenes): [under 280 chars]
</short_form_hooks>
<same_day_cta_post>[Under 100 words. Punchy question on failure pattern. Link in first comment only.]</same_day_cta_post>

Output only tagged sections, in order. No preamble, no summary.
```

### Step 4: Fill in your brackets
Replace the bracketed fields with a real topic from your week. Example test:

```
MODE: DAILY_ISSUE
RAW TOPIC / MOMENT: I spent 45 minutes debugging why Claude kept hallucinating a fake Supabase function name in my AllFours game code.
PRE-NAMED CONCEPT: none — name it now
```

### Step 5: Hit enter
Claude runs all 5 stages in one pass. You get back:
- Concept name
- Subject lines
- Full newsletter draft
- Tiered prompt system
- Audit results
- All 4 repurposed assets (if audit passes)

---

## Going Forward: Your Weekly Rhythm

| Day | What You Do | Time |
|---|---|---|
| **Saturday** | Paste Lang CORE → `//LOAD CONTENT.md` → Run Stage 1 five times (name flagship + Mon–Thu issues) → Run full prompt in WEEKLY_FLAGSHIP mode | 60–90 min |
| **Sunday** | Post the 3 short-form hooks + Monday's evening teaser | 15 min |
| **Monday–Thursday** | Paste Lang CORE → `//LOAD CONTENT.md` → Fill in that day's pre-named concept → Run in DAILY_ISSUE mode | 30–45 min |
| **Thursday evening** | Post Friday's teaser (batched Saturday) | 5 min |

---

## What Success Looks Like

After one test run, you should have:
- [ ] One newsletter draft that sounds like you (not generic AI)
- [ ] One proprietary failure pattern name
- [ ] Three subject line options
- [ ] Four repurposed assets ready to copy-paste
- [ ] A READY TO PUBLISH verdict (or clear flags on what to fix)

If the voice feels off, the issue is usually in the Lang CORE Custom Instructions — not the CONTENT sub-prompt. The Core sets your identity; the sub-prompt sets the structure.

---

## Single Next Action

Right now, while your Claude limit resets: pick one real thing that broke or frustrated you this week. Write it as 1–2 sentences. That's your `RAW TOPIC / MOMENT`. Save it in a text file. When Claude is back, paste Lang CORE → CONTENT.md → your topic → hit enter. Test once. Ship or flag what drifts.
