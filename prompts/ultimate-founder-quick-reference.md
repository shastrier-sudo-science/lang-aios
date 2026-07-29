---
name: ultimate-founder-quick-reference
description: "The 10 most-used copy-paste prompts from the Ultimate Founder-Engineer Skill v3.1b. Keep this open while building."
version: 3.1b
---

# QUICK REFERENCE CARD — 10 ESSENTIAL PROMPTS

**For:** Shastrie Ramdhanie | AI Sovereignty Movement | Trinidad → US
**Window:** 9 AM – 2 PM AST | **Surplus:** $419 | **Debt:** $242,855.83

---

## 1. VIBE-CODE A PROTOTYPE (Hour 1 — Build)
**Use:** When you have an idea and need to prove it in under 60 minutes.

```
Vibe-code a single-file prototype for [PRODUCT NAME]. 
Core loop only: [ONE USER ACTION]. 
No design polish. No storage. No export. 
Just the one action that delivers value. 
I'll validate this before we add anything else.
```

---

## 2. BUILD CORE LOOP (Prompt Chain — Step 1)
**Use:** After vibe-coding proves the idea. This is the foundation.

```
Build the core loop for [PRODUCT NAME] as a React artifact. 
One user action: [ACTION]. 
No design, no storage yet. 
Just functional logic that produces the output.
```

---

## 3. ADD PERSISTENT STORAGE (Prompt Chain — Step 2)
**Use:** After core loop works. Data must survive refresh.

```
Add persistent storage to the previous artifact using window.storage. 
Scope: personal (default — never shared for financial/legal/medical data). 
Key pattern: hierarchical:id. 
Combine related fields into one key. 
Add try/catch on all storage calls. 
Add a loading state and a reset button.
```

---

## 4. ANTI-AI DESIGN PASS (Prompt Chain — Step 3)
**Use:** After storage works. Function first, face second.

```
Redesign this artifact's visual style. 
Avoid generic AI-template look — no default blue gradients, no centered-everything, no default border-radius on everything. 
Pick a distinctive typeface pairing and one accent color. 
Explain why they fit [PRODUCT]'s audience. 
Test on 375px mobile before finalizing.
```

---

## 5. ADD EXPORT + PUBLISH (Prompt Chain — Step 4)
**Use:** Ready to ship. This makes it shareable.

```
Add JSON export/import and a 'Publish' button to this artifact. 
Include a clear warning: "Publishing creates a permanent public link. Unpublishing is irreversible."
```

---

## 6. LANDING PAGE FOR VALIDATION
**Use:** Pre-sell test. Landing page + Loom demo before code.

```
Build a single-file HTML landing page for [PRODUCT]. 
Audience: [SPECIFIC PERSON]. 
One core action: email signup / pre-order. 
Explicitly test and describe how it will look on a 375px-wide mobile screen before finalizing. 
Include: headline, 3 bullet benefits, social proof placeholder, pricing, and a clear CTA.
```

---

## 7. REAL DATA IMPORT
**Use:** When users need to upload their actual data.

```
Add CSV import to this artifact using papaparse. 
Expected columns: [LIST]. 
Show a clear inline error for any malformed row instead of failing silently. 
Show a preview of parsed data before the user confirms import. 
Handle empty files gracefully.
```

---

## 8. INTEGRATION TARGET IDENTIFICATION
**Use:** When you have users and need to remove their biggest manual step.

```
Identify the single manual step [PRODUCT]'s users hate most. 
Propose one MCP or API integration that removes it. 
Do not propose more than one — state why this is the highest-leverage integration to ship first.
```

---

## 9. FOUNDER-LED SALES DM
**Use:** Reaching out to potential customers. 10 DMs → 2 demos → 1 sale.

```
Hey [Name],

I noticed you do [their specific task] — I built a tool that [does that task] in [time] instead of [current time]. 
It's in free trial right now — no card needed.

Want to try it with your next [specific work item]?

[Your name]
```

---

## 10. REDESIGN FOR PREMIUM FEEL
**Use:** When a validated product needs to look like it's worth paying for.

```
Redesign this artifact's visual style. 
Avoid generic AI-template look — no default blue gradients, no centered-everything. 
Pick a distinctive but appropriate typeface pairing and one accent color, and tell me why they fit [product]'s audience. 
Function must work before face is polished.
```

---

## THE 3-HOUR WINDOW CHEAT SHEET

| Hour | Block | Rule | What to Do |
|---|---|---|---|
| Hour 1 (9–10 AM) | **BUILD** | No design. No distribution. | Core loop, storage, bug fixes. Prompts 1–4. |
| Hour 2 (10 AM–12 PM) | **SHIP + DISTRIBUTE** | No building. No scaling. | Publish artifact, write newsletter, post to LinkedIn/FB, send DMs. |
| Hour 3 (12–2 PM) | **SCALE + OPTIMIZE** | No building. No shipping. | Pricing experiments, user interviews, analytics, payment link tweaks. |

**Hard rule:** No task crosses hour boundaries. If it doesn't fit, it gets cut or moved to tomorrow.

---

## THE PRE-SELL 7-DAY TEST

| Day | Action | Tool |
|---|---|---|
| Day 1 | Build landing page (Prompt 6) | Claude artifact |
| Day 2 | Record 2-min Loom demo | Loom (free) |
| Day 3 | Post landing page + Loom to channels | LinkedIn, FB, newsletter |
| Day 4–6 | Collect emails + payment intent | Gumroad or Stripe Payment Link |
| Day 7 | Count results | Kill if <5 pre-orders or <20 emails |

---

## KILL CONDITIONS (Stop Immediately If)

- <5 pre-orders in 7 days (pre-sell test)
- <10 real users after 2 weeks of distribution
- <3 "how do I pay?" questions after 50 free users
- CAC > $0 for first 10 customers
- AI costs exceed 20% of MRR
- Day 30 active rate < 15%

---

## ONE-LINE DECISIONS

| Question | Answer |
|---|---|
| Artifact or backend first? | Artifact (Tier 1). Always. |
| localStorage or window.storage? | window.storage in artifacts. localStorage only on real hosting. |
| Vibe code or structure? | Vibe for prototypes. Structure for validated products. |
| One price or three tiers? | One price until 20+ paying users. |
| MRR or one-time? | Both. Annual for cash flow. Monthly for retention. |
| Content or tools first? | Both. Content IS the funnel. Tools ARE the proof. |
| Build or ship or scale? | Check the hour. Hour 1 = build. Hour 2 = ship. Hour 3 = scale. |

---

*Generated from Ultimate Founder-Engineer Skill v3.1b*
*Last updated: 2026-07-28*
