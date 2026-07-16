# CRIT Validator — Objection-to-Copy Pipeline

## Purpose
Two-phase prompt chain that simulates target-customer objections, then writes landing page copy engineered to defeat those exact objections. No API key, no code execution — run both phases in Claude.ai or ChatGPT free tier.

## Input Required
1. **PAIN POINT**: [One sentence — the specific problem your product solves]
2. **TARGET CUSTOMER**: [Specific role, e.g. "freelance web designer," not "small business owner"]
3. **PRICE POINT**: [e.g. "$29/mo"]

## Phase 1 — Role + Interview (Extract the Friction)

Run this first, in a fresh chat:

---
Context: You are a [TARGET CUSTOMER] who experiences this pain point: "[PAIN POINT]".

Role: You are highly skeptical, busy, and protective of your budget. You are actively looking for reasons not to buy new software.

Interview task: I am pitching you a SaaS solution that solves this for [PRICE POINT]. Give me your top 5 objections to paying for it. Focus on: trust, ROI, workflow friction, and free alternatives you'd try first.

Output ONLY a numbered list of 5 objections. Be specific to my exact pain point, not generic SaaS objections. Be ruthless.
---

Copy the 5 objections out of the response.

## Phase 2 — Context + Task (Engineer the Conversion)

Paste this into a new message (same chat or a fresh one — doesn't matter, no API state to manage):

---
Context: I am building a landing page for a SaaS that solves this pain point: "[PAIN POINT]" for [PRICE POINT].

Role: You are an elite direct-response B2B copywriter specializing in high-conversion SaaS pages.

Task: Below are the 5 real objections my target customer has. Write landing page copy that acknowledges and destroys each one.

Objections:
[PASTE THE 5 OBJECTIONS FROM PHASE 1]

Required structure:
1. Hero headline — name the pain and the outcome
2. Sub-headline — the mechanism and time-to-value
3. "We know what you're thinking" section — name their objections directly
4. Objection-crushers — 3-4 bullets, each defeating one objection with logic or a specific workflow detail
5. Risk-reversal CTA

Write the actual copy, not placeholder text.
---

## Output
Full landing page copy, ready to paste into your `web-builder.md` HTML template or directly into a Bubble/static page.

## Usage Notes
- **Model choice**: Phase 1 works fine on any free model since it's roleplay, not reasoning-heavy — use Grok or ChatGPT free tier per your multi-AI routing rule (Claude reserved for security-sensitive code). Phase 2 benefits from Claude's reasoning for copy quality.
- **Iterate**: run Phase 1 with 3-5 different target customer phrasings for the same pain point. The version where the objections are easiest to defeat with tech you already have is your validated angle.
- **No local execution needed**: this replaces `crit_validator.py` entirely. Delete the Python dependency — nothing here touches your zero-budget constraint.
- Save each output pair (objections + copy) to `artifacts/crit-validation/[product-name].md` for reuse.

## Remember This
Q: Why two phases instead of one prompt?
A: Objections must exist before copy can defeat them — sequencing forces specificity over generic pitch language.

Q: Why not the Anthropic API script?
A: Pay-per-token cost and local Python execution both violate the zero-budget, mobile-only constraint.

Q: Which AI for Phase 1 vs Phase 2?
A: Grok/ChatGPT free tier for roleplay, Claude for the higher-reasoning copywriting task.
