# BUILD → SHIP → SCALE: The Full Course

**How to turn Claude into a product factory, and turn that factory into income.**
Built for: zero budget, Trinidad location, solo operator, ForgeOS/FreedomCalc/Proposal Forge/Prediction Engine as live test cases.

---

## HOW THIS COURSE WORKS

Three parts, each with modules. Each module: **mechanism** (why it works) → **exact steps** → **copy-paste prompt** → **mistake that kills beginners** → **apply it to one of your existing apps**. No fluff, no "it depends" without a number attached.

The core loop you're being trained on:

```
IDEA → BUILD (artifact/code) → SHIP (deployed, real URL, real data) → SCALE (paying users, automated ops) → repeat
```

Every app you already have (ForgeOS, FreedomCalc, Proposal Forge, Prediction Engine, All Fours) is stuck at a different stage of this loop. By the end you'll know exactly which stage each one is in and the next unlock for it.

---

# PART 1 — BUILD

## Module 1.1 — Webpages & Websites (single-file artifacts)

**Mechanism:** Claude's artifact system renders one self-contained HTML/CSS/JS file live, no server needed. This is the fastest possible iteration loop — you describe, you see it render, you refine in the same breath. The single-file constraint is a feature, not a limitation: it forces you to think in terms of shippable units instead of sprawling codebases you'll never finish.

**Steps:**
1. Describe the page's *job*, not its layout: "landing page that converts cold Trinidad freelancers into FreedomCalc trial users" beats "make a nice landing page."
2. Ask Claude to build it as one HTML file with inline CSS/JS.
3. Iterate 3-5 times max on one artifact before starting a new one — past that, the diffs get messy and Claude starts contradicting earlier structure.
4. Test on mobile explicitly — CSS that's fine on desktop preview wraps badly on phones, and most of your traffic will be mobile.

**Copy-paste prompt:**
> "Build a single-file HTML landing page for [product]. Audience: [who]. One core action: [signup/buy/etc]. Explicitly test and describe how it will look on a 375px-wide mobile screen before finalizing."

**Mistake that kills beginners:** Asking for a "multi-page site" in one artifact. Artifacts are single-file — a real multi-page site needs Module 2.4 (deployment), not more prompting.

**Apply it:** Your Proposal Forge and FreedomCalc both need a landing page separate from the tool itself — the tool sells the feature, the landing page sells the outcome (time saved, debt paid off). Build that landing page as its own artifact this week.

---

## Module 1.2 — Web Apps (React artifacts, state, persistence)

**Mechanism:** React artifacts give you `useState`/`useReducer` for in-session memory, plus a genuine **persistent storage API** (`window.storage.get/set/delete/list`) that survives across sessions — this is what turns a toy calculator into an actual product people can return to. Storage is scoped personal (private to the user) or shared (visible to everyone using that artifact) — you choose per key.

**Steps:**
1. Pick ONE user action the app must nail (for FreedomCalc: "enter debts, see payoff order"). Everything else is v2.
2. Use `useState` for anything that resets on refresh (form inputs mid-entry). Use `window.storage` for anything that must survive (saved debt list, entry history).
3. Design your storage keys before writing code: `hierarchical:id` pattern, e.g. `debts:user_entry_1`. Combine data updated together into one key — don't make 5 separate storage calls for one save action.
4. Always wrap storage calls in try/catch; a missing key throws, it doesn't return null quietly.

**Copy-paste prompt:**
> "Build this as a React artifact with persistent storage using window.storage. Core loop: [action]. Data that must persist: [list]. Combine related fields into single storage keys. Add a loading state and a way to reset data."

**Mistake that kills beginners:** Storing 10 small keys instead of 1 combined key — this hits rate limits and makes the app feel laggy. One object, one key, per logical unit.

**Apply it:** FreedomCalc's debt list and Proposal Forge's saved proposal templates should both move to `window.storage` if they aren't already — that's the difference between "tool I used once" and "tool I keep coming back to."

---

## Module 1.3 — Working With Real Data

**Mechanism:** A demo with fake numbers proves nothing to a buyer. Real data proves the tool works on *their* mess. Claude artifacts can parse CSV (papaparse), Excel (SheetJS/xlsx), and call live APIs — this is what separates "prototype" from "thing I'd trust with my actual finances."

**Steps:**
1. For CSV/Excel import: use `Papa.parse()` or `XLSX.read()` inside the artifact — never ask the user to reformat their file first, that's friction that kills adoption.
2. For live external data (crypto prices for Prediction Engine, exchange rates), artifacts can't freely call arbitrary external APIs from client-side JS due to CORS — route through a documented public API that allows browser calls, or build the fetch step in Claude Code / a small backend instead.
3. Validate and show errors inline ("row 14 missing amount") rather than silently failing — trust is your entire product at this stage.

**Copy-paste prompt:**
> "Add CSV import to this artifact using papaparse. Expected columns: [list]. Show a clear inline error for any malformed row instead of failing silently. Show a preview of parsed data before the user confirms import."

**Mistake that kills beginners:** Building the prettiest UI first, testing with real data last. Reverse it — real data first, UI polish in Module 2.2.

**Apply it:** Run your actual last 3 months of expenses through FreedomCalc this week. Whatever breaks is your real Module 1.3 homework, not a hypothetical one.

---

# PART 2 — SHIP

## Module 2.1 — Design That Doesn't Look AI-Generated

**Mechanism:** Buyers pattern-match "looks templated" to "not trustworthy" in under a second. Distinctive typography, intentional color (not default blue-and-gray), and real spacing decisions signal a product someone cared about — which is a conversion factor, not vanity.

**Steps:**
1. Pick ONE typeface pairing and ONE accent color before building anything — decide this first, not last.
2. Avoid centered-everything, default border-radius, and generic gradient backgrounds — these are the tells of an unedited AI output.
3. Ask Claude explicitly to avoid "templated" defaults and justify spacing/color choices — this changes the output measurably.

**Copy-paste prompt:**
> "Redesign this artifact's visual style. Avoid generic AI-template look — no default blue gradients, no centered-everything. Pick a distinctive but appropriate typeface pairing and one accent color, and tell me why they fit [product]'s audience."

**Mistake that kills beginners:** Polishing visuals before the core loop (Module 1.2) works. Function first, face second.

---

## Module 2.2 — Plugins & Integrations (MCP, connectors)

**Mechanism:** MCP (Model Context Protocol) lets an AI-powered artifact or Claude session call external tools/services directly — Google Drive, Gmail, Slack, or a custom server you define. This is what turns "static calculator" into "tool that pulls your real bank CSV automatically" — the integration IS the product moat, because it removes a manual step your competitor's tool still requires.

**Steps:**
1. Identify the one manual step your users hate most (re-entering data, copy-pasting between apps). That's your integration target.
2. For AI-powered artifacts, you can call the Claude API directly from inside the artifact and, where relevant, attach MCP servers the user has connected (e.g., Google Drive) — but note: this requires the viewer to be signed in to Claude, so it can't be a fully public no-login tool.
3. Don't over-scope — one integration shipped beats three half-built ones.

**Mistake that kills beginners:** Trying to build a "platform" with 5 integrations before one person has used the tool with zero integrations. Ship the manual version first, automate the proven bottleneck second.

**Apply it:** Proposal Forge's highest-leverage integration is pulling client info from an existing doc/sheet instead of manual entry — that's your Module 2.2 target, not a nice-to-have.

---

## Module 2.3 — Workflows & Automation Pipelines

**Mechanism:** Every hour you spend manually running a task is an hour that doesn't scale past you. ForgeOS on PythonAnywhere is already your automation backbone — the skill here is knowing what belongs in a scheduled script (cron-style, no human needed) versus what belongs in an interactive tool (a human makes a decision each time).

**Steps:**
1. List every recurring task across your apps (content posting, data refresh, report generation).
2. For each: does a human need to make a judgment call, or is it purely mechanical? Mechanical → automate in ForgeOS. Judgment → keep it interactive, but pre-fill everything possible so the human only decides, never types.
3. Log every automated run somewhere you can check later (even a simple text log) — silent automation that fails silently is worse than doing it manually.

**Mistake that kills beginners:** Automating a task before it's been done manually and correctly at least 5 times. You can't automate a process you don't understand yet.

---

## Module 2.4 — The Deployment Pipeline (going from artifact to real product)

**Mechanism:** An artifact is a single conversation's output. A **published** artifact gets a permanent shareable link with zero hosting cost to you (compute is billed to the end user's own usage, not to you) — this is the fastest, truest zero-budget deployment path available. For anything needing a real backend, multi-page routing, or a custom domain, you graduate to free-tier hosting.

**The three tiers, in order of effort:**

| Tier | What it is | When to use | Cost |
|---|---|---|---|
| Publish artifact | One click, permanent public link | Calculators, single-purpose tools, MVPs to validate demand | $0 |
| Static hosting (GitHub Pages / Vercel free tier / Netlify free tier) | Real domain, multi-page, faster load | Once you need a custom domain or multiple pages | $0 |
| PythonAnywhere (already running ForgeOS) | Real backend, database, scheduled jobs | Once the tool needs server-side logic, auth, or cron jobs | $0 on free tier |

**Steps:**
1. Validate on Tier 1 first — publish the artifact, get 10 real people to use it, before spending a single hour on real hosting.
2. Only move to Tier 2/3 once Tier 1 proves people want it — don't build infrastructure for a product with zero users.
3. Note the hard limit: AI-powered artifacts (ones that call Claude's API at runtime) require the viewer to be logged into Claude — they can't be made fully public/no-login. If your product needs to work for someone with zero Claude account, it needs to move off artifacts entirely into Tier 2/3.

**Mistake that kills beginners:** Building a full backend on PythonAnywhere before validating anyone wants the product on Tier 1. That's weeks of unpaid infrastructure work for an unproven idea.

**Apply it:** Prediction Engine and All Fours are both good Tier-1 candidates right now — publish them as-is this week and see if anyone actually uses them before investing more build time.

---

# PART 3 — SCALE (turning the skillset into a business)

## Module 3.1 — Productization: Tool → Business

**Mechanism:** A tool becomes a business at the exact moment someone would rather pay than lose access. That threshold isn't about features — it's about the tool being load-bearing in their life/work. Your job in this module is to find which of your 5 apps has crossed, or is closest to, that threshold.

**Steps:**
1. Rank your apps by "how much would it hurt someone to lose this" — not by how much code you've written.
2. For your top candidate, add the minimum viable business layer: a way to know who's using it (even just an email capture in storage), and a way to charge (Gumroad or Stripe payment links need zero backend to start).
3. Resist adding features. Add distribution and a payment link instead — most zero-revenue tools have a feature problem's opposite: a discovery problem.

**Mistake that kills beginners:** Building more features to "make it worth paying for" instead of just asking 10 current users if they'd pay, and for what.

---

## Module 3.2 — Distribution on Zero Budget

**Mechanism:** You already have a built-in distribution channel — the AI Sovereignty Movement audience. The highest-leverage move is routing every piece of that content toward one of your tools as a concrete demonstration, not talking about AI in the abstract.

**Steps:**
1. Every AI Sovereignty Movement post should end with "I built this in an afternoon with Claude — try it: [link]" pointing at a published artifact.
2. Use your own build process as the content — "how I built FreedomCalc's debt payoff logic in 20 minutes" is both proof and marketing in one piece.
3. Track which specific piece of content drove which specific signup — without this you're guessing, not scaling.

**Mistake that kills beginners:** Separating "content business" and "tools business" into two unrelated efforts instead of making each tool the proof for the content and each piece of content the funnel for the tool.

---

## Module 3.3 — Pricing & Monetization Mechanics

**Mechanism:** At your current numbers, every dollar of monthly recurring revenue matters more than a single big one-time sale — MRR compounds, one-time doesn't. Price for retention, not for maximum extraction on day one.

**Steps:**
1. Start with a single price point, not three tiers — tiers are a later optimization once you have 20+ paying users to segment.
2. Use Gumroad (free to start, takes a cut only on sale) or a Stripe Payment Link (no code) — both are zero upfront cost.
3. Price anchored to the outcome (debt paid off faster, proposals sent faster) not to your build time — buyers don't care how long it took you.

**Mistake that kills beginners:** Underpricing out of guilt about a simple tool. If it solves a real problem, price it like it does — you can always discount, you can't easily raise price on existing users.

---

## Module 3.4 — The Reusable Pipeline

This is the template to run on every future app idea, so you're never starting from zero process again:

1. **Build** — single-file artifact, one core loop, real data by day 3.
2. **Ship** — publish the artifact (Tier 1), get 10 real users before writing any backend.
3. **Validate** — would they pay? Ask directly, don't infer.
4. **Scale** — payment link + one integration that removes their biggest manual step + route AI Sovereignty content at it.

Every app that doesn't survive step 3 gets killed or shelved — that's a feature of the pipeline, not a failure of the app.

---

## REMEMBER THIS:

Q: Why publish an artifact instead of building a backend first?
A: Compute cost is billed to the end user, not you — free validation before any infrastructure spend.

Q: Why does storage key design matter?
A: Combined keys avoid rate limits and lag; one object per logical unit beats five small calls.

Q: What's the real threshold where a tool becomes a business?
A: When someone would rather pay than lose access — not feature count.

Q: What's the #1 beginner mistake across Build, Ship, and Scale?
A: Doing more of the current stage (more features, more polish, more infrastructure) instead of moving to the next one.

**NEXT ACTION:** Pick your single highest "would hurt to lose" app (Module 3.1, step 1) and publish its artifact link (Module 2.4, Tier 1) in the next 30 minutes — no new features first.
