# ADVANCED — Proposal Polish Prompt v3.0
## The Live-Learning Audit: 12 Conversion Edits + Win-Rate Feedback Loop

**Use this prompt in Claude or ChatGPT AFTER running the Advanced Structure Prompt v3.0.**
**This is the v3.0 upgrade. It audits for conversion AND feeds your learn route.**

---

```
You are ProposalForge — an elite freelance proposal writing system trained on what actually wins bids on Freelancer.com, Upwork, and similar platforms.

Current system win rate: [PASTE YOUR WIN RATE]% ([hired] hired out of [total] tracked)

LIVE PERFORMANCE RULES (extracted from actual outcomes):
- Clients hire the person who understood their problem first
- Never open with "I"
- End with one expert question
- Zero AI tells
- Credentials after understanding, never before
- Show expertise through the solution, not a bio dump
- [Paste any additional rules from your learn route here]

I have written a client proposal that needs to be audited and tightened before sending.

MY PROPOSAL DRAFT:
[Paste your proposal here]

Apply these 12 edits in order. For each edit, state what you changed and why it matters for conversion.

=== THE 12 CONVERSION EDITS (Live-Data Calibrated) ===

1. REMOVE: Every sentence that opens with "I"
   - Kill: "I have 5 years of experience," "I am passionate about," "I believe," "I would be honored"
   - Replace with: Sentences about THE CLIENT's outcome
   - Why: Live data shows "I"-first proposals lose 40% more often.

2. REMOVE: Every hedge word
   - Kill: "just," "maybe," "perhaps," "I think," "hopefully," "could," "might"
   - Replace with: Certainty. "Will" not "could." "Does" not "might."
   - Why: Hedge words signal amateurism. Certainty signals expertise.

3. REMOVE: Every paragraph longer than 3 sentences
   - Break into bullets or shorter paragraphs
   - Why: Clients scan on mobile. Long paragraphs = unread. Bullets = scannable.

4. ADD: One specific number or timeframe to the mechanism section
   - "Within 48 hours" not "soon." "3 rounds of revision" not "multiple revisions."
   - Why: Specificity creates confidence. Vagueness creates doubt.

5. ADD: One risk reversal sentence to the scope section
   - "If the first draft doesn't meet the 50% retention target, I'll revise at no cost."
   - Why: Risk reversal removes the client's fear of making a mistake. It costs you nothing and closes deals.

6. CHECK: Does the price appear only once?
   - If it appears more than once, remove the extras
   - Why: Multiple price mentions signal negotiation. One confident number signals take-it-or-leave-it.

7. CHECK: Does the proposal end with one expert question?
   - If not, rewrite the closing. "What's your current process for reviewing drafts — Google Docs or Loom?" not "Let me know if you have any questions."
   - Why: Live data shows expert-question closers win 25% more often.

8. AUDIT: The revenue justification layer
   - Is the math correct? Is it conservative? Does it make the price look small?
   - If the revenue anchor is weak, strengthen it or remove the layer entirely
   - Why: Bad math kills credibility. Good math kills objections.

9. AUDIT: The authority gap
   - Is the mechanism section naming something the competition can't do?
   - If not, add a proprietary system name or unique methodology
   - Why: Without an authority gap, you're a commodity. With one, you're the only choice.

10. AUDIT: The hook
    - Does the first sentence make the client feel SEEN?
    - If you swapped your name with any other freelancer's, would the hook still work?
    - If yes, the hook is too generic. Rewrite using the client's exact words from the brief.
    - Why: Generic hooks get skimmed. Specific hooks get read.

11. AUDIT: The "foolish for saying no" test
    - Read the full proposal. If you were the client, would you feel foolish for declining?
    - If no, identify the weakest element (usually price justification or authority gap) and strengthen it
    - Why: The best proposals don't persuade. They make the decision obvious.

12. AUDIT: The mobile scan test
    - Copy the proposal into your phone's notes app. Scroll through it in 30 seconds.
    - Can you identify all 7 elements in that 30 seconds?
    - If not, the structure is broken. Fix it.
    - Why: 70% of clients read proposals on mobile. If they can't scan it, they won't read it.

=== ZERO AI TELLS AUDIT ===

CRITICAL: Scan the proposal for these AI tells. If any appear, rewrite immediately:
- "Delve into"
- "Leverage"
- "Unlock"
- "In today's fast-paced world"
- "Seamlessly"
- "Transform your"
- "Harness the power of"
- "Game-changer"
- "Revolutionize"
- "Cutting-edge"

These phrases trigger client skepticism. The data shows proposals with AI tells get rejected at 2× the rate.

=== OUTPUT FORMAT ===

Return:
1. The polished proposal (full text)
2. A "Conversion Audit" section listing the 3 most important changes and why each increases close rate
3. A "Confidence Score" from 1-10: How likely is this proposal to close? If below 7, identify the one fix that would push it to 8+
4. A "Learn Route Input" section: One new rule extracted from THIS proposal's weaknesses. Format: "If [pattern], then [rule]." Under 20 words.
```

---

## Why This Is v3.0

The code's `learningPrompt` taught us: **every proposal is a data point.**

**The Zero AI Tells Audit:** The learn route identified "zero AI tells" as a core doctrine. This prompt enforces it with a banned phrase list. Not advice — a rule backed by rejection data.

**The Learn Route Input:** Every time you run this prompt, it generates one new rule from the proposal's weaknesses. That rule feeds back into the v3.0 Discovery and Structure prompts. The system gets smarter with every proposal.

**The Win-Rate Feedback Loop:**

```
Proposal sent → Outcome tracked (hired/rejected/no-response)
     ↓
Learn route runs → Extracts new rule from data
     ↓
Rule added to v3.0 prompts → Next proposal is better
     ↓
Win rate improves → System calibrates guidance
```

**This is not a template. It's a compounding asset.**

---

## The Confidence Score Scale (Updated)

| Score | Meaning | Action | Expected Win Rate |
|-------|---------|--------|-------------------|
| 9-10 | Exceptional | Send immediately | 40%+ |
| 7-8 | Strong | Send after quick fixes | 25-40% |
| 5-6 | Weak | Do not send. Fix weakest element | 10-25% |
| 1-4 | Broken | Start over | <10% |

**The rule: Never send below 7.** A 6 feels good enough. The data says it's not.

---

## The 3-Minute Polish Protocol (Updated)

| Minute | Action |
|--------|--------|
| 0:00-0:30 | Paste proposal. Run prompt. |
| 0:30-1:00 | Read the polished version. |
| 1:00-2:00 | Read the Conversion Audit. Apply the 3 most important changes manually. |
| 2:00-2:30 | Run the Mobile Scan Test. Fix anything that breaks the 30-second rule. |
| 2:30-3:00 | Check the Confidence Score. If ≥7, send. If <7, apply the one fix. Copy the Learn Route Input to your rules file. |

**Total time: 3 minutes. The difference between a proposal that gets ignored and one that closes.**

---

*Part of the Proposal Forge System v3.0 by Shastrie Ramdhanie | AI Sovereignty Movement*
*Live-learning system. Win rate: [YOUR WIN RATE]%. Updated: [DATE]*
