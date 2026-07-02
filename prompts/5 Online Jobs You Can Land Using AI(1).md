# 5 Online Jobs You Can Land Using AI

Status: Living reference document — source material for `prompts/scriptwriting_engine_v1.md`
Source: DeepSeek-organized guide from GitHub course, condensed and reformatted for AIOS
Primary extraction target: YouTube Ghostwriting (highest-leverage first job, matches existing Upwork profile + Day One Output writing skill)

---

## 1. The 5 Jobs (Ranked by Entry Speed)

| Job | Starting Pay | Ceiling | Entry Move |
|---|---|---|---|
| YouTube Ghostwriter | $200–$2,000/script | $3K–$10K+/mo as creative director | DM 5 YouTubers, free sample |
| Sales Page Copywriter | $1K–$10K+/page | Revenue share | 3 sample pages, free audits |
| Local AI Plumber (Consultant) | $100–$300/hr | $1K–$5K/setup + retainers | Local FB groups, free audits |
| Caption Cannon (Social Media Manager) | $500–$3K/mo/client | ~$10K/mo at 3–5 clients | Niche portfolio, free trial week |
| Grant Hunter | $1K–$5K/application | 5-figure % on wins | Local nonprofits, contingency model |

**Selected first job: YouTube Ghostwriter.** Reasons — lowest entry friction, directly reuses the Day One Output writing skill and voice-extraction pattern already built, and the Upwork profile is already live in this niche.

---

## 2. Upwork Profile — Current State

- Title: YouTube Ghost Writer, Rate: $15/hr, ID unverified
- **Fix priority:** verify ID first (unlocks free Invite-to-Job responses, 0 Connects), raise rate to $35/hr, publish 2 portfolio pieces, add skill tags (Sales Page Copywriting, YouTube Scriptwriting, Audience Engagement, Ghostwriting, Creative Direction)

Full optimized overview text lives in `artifacts/upwork-profile.md` (already generated — reconcile the two before republishing).

---

## 3. The Voice Cloning System (Core Mechanism)

Two-step chain: **Analyze** a creator's transcripts into a Voice DNA Blueprint → **Generate** a script that is forced to comply with that blueprint. This is the same mechanism as Stage 1 (Voice DNA Extraction) in the SOVEREIGN production OS — same pattern, applied to a client's voice instead of my own.

The full executable version of this chain is now built out as `prompts/scriptwriting_engine_v1.md`. Use that file, not this summary, when actually running the workflow.

**Non-negotiable mechanism note:** the audit step (self-flagging banned/negative vocabulary before delivering) is what separates cloned voice from generic AI output. Skipping it is the #1 quality failure identified in the source material.

---

## 4. Target Creator List (Outreach Priority)

| Rank | Channel | Subs | Videos | Why |
|---|---|---|---|---|
| 1 | AI Injection | 196 | 228 | Most extreme effort-to-growth ratio — highly motivated, clearly mis-scripting |
| 2 | JimCircuit | 212 | 132 | Same pattern, likely burning out |
| 3 | Sunny Israni | 1.68K | 251 | 251 videos for 1.68K subs — serious effort disconnect |
| 4 | Claude Unlocked | 124 | 44 | Newer, stuck — good voice-cloning test case |
| 5 | Tokscript | 99 | 22 | Small sample but clear struggle |

Free-pitch outreach template and tracking sheet columns are in Section 6 below.

---

## 5. Discovery Interview Question Bank

**Background/Motivation:** Why start the channel? Pivotal experience that shaped content style? What keeps you going despite low views?

**Audience/Pain:** Who is the ideal viewer? What misconceptions do you want to address? What feedback surprised or frustrated you?

**Process/Pain:** Walk through the current script process. What's hardest or slowest? Describe a recent underperforming video — what went wrong?

**Goals:** Top 3 goals for next 3–6 months? Magic-wand growth outcome?

**Voice:** How would you describe your on-camera tone? What makes content feel "you" vs. generic AI output?

**Follow-up technique — Peel the Onion:** What → Why → How → Impact → Example. Never accept a one-line answer as final; always ask "tell me more about that" or "walk me through exactly where that happened."

---

## 6. Outreach Template

```
Hi [Name],

I saw your [specific video] and love your focus on practical AI. As a
ghostwriter specializing in AI content, I rewrote a sample script
improving hooks/storytelling while matching your voice — would love
to send it free as a test. No strings attached.

[Attach sample]
```

Track: Channel | Contact Date | Platform Used | Response | Follow-up

---

## 7. Differentiation — The "Why Not Just Train Claude Myself" Objection

One-sentence counter:

> "You can train Claude on my sample script's structure, but you can't replicate the strategic judgment, interview-driven insights, and performance optimization that turns a script into consistent growth — that's what you're paying me for."

Five reasons this holds: human insight from interviews AI can't extract, YouTube-specific structural optimization (hooks, retention, analytics-informed tweaks), ongoing iteration (a process isn't replicable from one sample), full creative direction (thumbnails, titles, calendar, repurposing), and ethical/technical guardrails (watermarking, light contracts, transparent AI disclosure).

---

## 8. Connects Strategy (Upwork-Specific)

- **Free path:** verified ID + published portfolio → clients Invite directly → 0 Connects required to respond
- **Off-platform flip:** pitch on X/LinkedIn/cold email → convert interest into an Upwork Direct Contract → 0 Connects
- **Paid fallback:** small bundle ($5–10 for 30–60 Connects) only if the free paths stall

Target jobs with under 20 proposals, client online now, personalized proposals only — never templated.

---

## 9. Pricing Ladder

| Stage | Rate |
|---|---|
| Jobs 1–3 | $35–$50/hr or $200–$300/script (build reviews + JSS) |
| Jobs 4–6 | +50% (social proof exists) |
| Job 7+ | Premium pricing |

---

## 10. 30-Day Calendar (Reference Only)

Week 1: ID verification, profile optimization, portfolio upload, first Voice DNA run.
Week 2: Analyze 3 scripts from target creator, write 2 samples (voice-matched + free-pitch improvement).
Week 3: Outreach to all 5 target creators, follow-ups, discovery interviews with responders.
Week 4: Deliver samples, follow up, send paid proposals, start paid work, build case study, plan month 2.

---

## Update Log

- 2026-07-02: Archived from DeepSeek-organized guide. Voice cloning system extracted and rebuilt as standalone chainable prompt file: `prompts/scriptwriting_engine_v1.md`. Cross-reference `artifacts/upwork-profile.md` for existing live profile copy before republishing an updated version.
