# CashPilot v0 — Runway-First Finance Cockpit

Zero-sync finance cockpit for solo freelancers (T&T edition): manual entry, runway-first
forecast, bucket envelopes, ClientPay scoring, dunning ladder, Pipeline (5-stage kanban)
and a ProposalForge Outcome Bridge. **No bank connections, no data leaves your browser**
(all operational data lives in `localStorage` on your machine — key `cashpilot_v1`).

Stack: **Next.js 16 (App Router) · React 19 · TypeScript 5 · Tailwind 4 · shadcn/ui ·
recharts · zustand (persist)**. One API route (`/api/dunning`) for AI-redrafted payment
reminder emails, with static-templates fallback if the AI call fails.

---

## 1. Quick start (local)

```bash
# unpack the zip, then from inside cashpilot-v0/:
bun install          # or: npm install / pnpm install
bun run dev          # or: npm run dev
# open http://localhost:3000
```

- First visit auto-loads a **demo dataset** (with an amber banner you can dismiss) so the
  Dashboard is populated instantly — no clicks needed.
- To start with **your own numbers**: `Settings → Reset all`, then add entries in the
  **Money** tab.
- Everything you enter persists in your browser (`localStorage`). Nothing is uploaded.

## 2. The 8 tabs

| Tab | What it does |
|---|---|
| Dashboard | Cash on hand, monthly burn, runway (color-toned), Freedom %, 90-day forecast area chart, income-vs-expense bars, bucket donut, alerts |
| Money | Add income/expense entries; newest-first ledger + monthly totals |
| Buckets | Tax / Runway / Profit / Operating envelopes, simulate-next-income slider, Freedom tracker |
| Clients | ClientPay score (avg days-to-pay, on-time %, tiers), effective hourly rate, revenue per client |
| Invoices | Status chips, overdue detection, **Mark paid**, AI dunning modal (Gentle / Firm / Final / Late-fee) with Copy + Redraft |
| Pipeline | 5-stage kanban (Lead → Sent → Verbal → Won → Lost/Ghosted), weighted totals, per-deal win-probability override |
| PF Bridge | Paste-import outcomes from ProposalForge (7-field JSON), duplicate/outcome guards, sample export |
| Settings | Bucket % validation (sum ≤ 100), Freedom target, default payment terms, Load demo / Reset all |

## 3. Where the logic lives (for extending)

```
src/
├── lib/
│   ├── types.ts     # all TS types (Entry, Client, Invoice, PipelineDeal, PF records…)
│   ├── calc.ts      # PURE calc engine: burn, runway, buckets, freedomStats,
│   │                # effectiveHourly, ClientPay score, dunning ladder,
│   │                # 90-day forecast, alerts, PF mapping  ← change numbers here
│   ├── store.ts     # zustand persist store ("cashpilot_v1") + demo auto-seed logic
│   ├── demo.ts      # the demo dataset (edit to change first-run experience)
│   ├── format.ts    # TT$ currency + date formatting (incl. en-TT ICU quirk guard)
│   └── db.ts        # Prisma client (UNUSED by v0 — scaffold only; safe to delete
│                    #   together with prisma/ + db/ if you never plan server DB)
├── components/cashpilot/
│   ├── cockpit.tsx      # tab shell + demo banner
│   ├── top-bar.tsx      # runway chip + trust badge
│   ├── tab-bar.tsx, bits.tsx
│   └── tabs/*.tsx       # one file per tab (dashboard, money, buckets, clients,
│                        #   invoices, pipeline, bridge, settings)
└── app/
    ├── page.tsx             # single route → renders <CashPilotCockpit/>
    ├── layout.tsx, globals.css
    └── api/dunning/route.ts # the only API route (AI email redraft)
```

**Data model note:** v0 is deliberately zero-sync. If you later want a server DB, the
Prisma+SQLite scaffold is already wired (`DATABASE_URL=file:./db/custom.db` in `.env`;
`bun run db:push` to sync schema) — but nothing in the UI reads/writes it today.

## 4. AI dunning route (`/api/dunning`)

- Uses `z-ai-web-dev-sdk` (server-side only). In the original environment it calls the
  platform LLM. **On your own machine without platform credentials the call will fail —
  this is handled**: the route falls back to 4 static ladder templates, so the Dunning
  modal always works. To use a different provider, edit
  `src/app/api/dunning/route.ts` and swap the SDK call for your own (e.g. OpenAI-
  compatible) endpoint, keeping the same request/response shape:
  `{ tone, client, amount, daysLate, invoiceRef }` → `{ subject, body }`.

## 5. Deploying (e.g. Vercel)

```bash
bun run build   # next build (standalone output configured in next.config.ts)
```

- Push to a Git repo → import into Vercel → deploy (framework auto-detected).
- The app is client-side; no env vars are required at runtime. `.env` here only points
  Prisma at a local SQLite file (unused).
- Remember: data is per-browser. If you later move state server-side, start from
  `src/lib/store.ts`.

## 6. Known v0 boundaries (by design)

- Manual entry only — no bank sync, no Plaid (trust/regulatory decision, see the
  ZeroSync pivot materials).
- Single user, single browser; no auth.
- Demo "today" anchor: overdue day-counts in the demo dataset can drift ±1 day from the
  2026-09-11 seed date.
- Next.js 16.1.x (environment-mandated) instead of the originally specced 15 — no
  behavioral impact for v0.

## 7. Handy scripts

```bash
bun run lint        # eslint (currently zero errors/warnings)
bunx tsc --noEmit   # typecheck (clean)
bun run build       # production build
bun run db:push     # only if you opt into the Prisma scaffold
```
