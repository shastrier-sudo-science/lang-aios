# Build Safety & Debugging Doc — All Future Client Builds

Status: Living reference document, update after every client build
Sources: vibe-security skill, All Fours debugging history (Firebase desync), SOVEREIGN RLS pattern, CODE sub-prompt fallback matrix

---

## 1. Pre-Code Checklist (run before writing any line of code)

- [ ] Spec doc signed off (feature list, data model, out-of-scope list)
- [ ] Hosting account created (Vercel/Netlify, real account, not Drop)
- [ ] Supabase project created, RLS enabled on every table from day one
- [ ] AI API spending cap set in provider dashboard (OpenAI/Anthropic) BEFORE first API call
- [ ] `.env` / `.env.local` added to `.gitignore` before first commit

## 2. AI Integration Security (every build that calls an AI API)

**API keys never touch the client.** No `NEXT_PUBLIC_*` or `VITE_*` prefix on any AI key. All AI calls route through a backend (Supabase Edge Function or Next.js Route Handler).

**Two-layer spending protection:**
1. Hard cap in the AI provider's dashboard (catches total runaway cost)
2. Per-user usage quota in your database, enforced server-side via RPC (catches single-user abuse)

**Prompt injection**: user input goes in the `user` message role, never concatenated into the `system` prompt. Reference the `buildPrompt()` pattern from PropBot — user data is interpolated into a template, not used to construct instructions.

**LLM output is untrusted**: if displaying AI-generated text, sanitize before rendering as HTML. Never `eval()` or execute AI output as code.

## 3. Authentication & Authorization

- Use Supabase Auth (or equivalent) — never hand-roll password hashing
- Every Server Action / API route validates: (1) input shape with Zod, (2) user is logged in, (3) user owns the resource being accessed/modified
- Middleware-level auth checks are a convenience, not the only wall — re-verify in the actual route handler or database query
- Never pass full database row objects to client components; select only needed fields

## 4. Database Safety (Supabase/Postgres)

**RLS is mandatory, not optional**, on every table containing user data. Pattern from SOVEREIGN:
```sql
-- Separate owner_config table (no RLS) read by is_owner() SECURITY DEFINER function
-- This avoids infinite recursion when policies need to check ownership
```

**Idempotent migrations always**: `CREATE TABLE IF NOT EXISTS`, `DROP POLICY IF EXISTS` before `CREATE POLICY`. Drop and recreate constraints rather than altering them when expanding allowed values.

**Inspect before writing**: run an `information_schema` query to confirm actual column names before any INSERT into an existing table. Check constraints via `pg_get_constraintdef`.

**Rate limit counters**: never store in a publicly-writable table — users can reset their own counters via the REST API. Use a Supabase RPC function (`SECURITY DEFINER`) or a private schema table not exposed via PostgREST.

## 5. Payments (Stripe) — for any build with subscriptions

- **Never trust client-submitted prices.** Use Stripe Price IDs created in the dashboard; look up the product server-side.
- **Webhook signature verification requires the raw body** — in Next.js, use `request.text()` not `request.json()` before verifying.
- **Subscription status checked server-side on every protected request** from your database (synced via webhook), never from a cached session value or stale JWT claim.
- **Checkout session metadata** (user ID, plan) set server-side when creating the session — never accept from client.

## 6. Real-Time / Multiplayer (lessons from All Fours)

All Fours debugging surfaced two recurring failure modes:

**Duplicate listeners**: Firebase Realtime Database listeners attached multiple times (e.g., on re-render) cause duplicate event handling and state corruption. Always clean up listeners on unmount/dependency change.

**State desync**: client-side optimistic updates that aren't reconciled with server state cause divergence between players. Pattern: batch state changes, treat server state as source of truth, reconcile on every update rather than trusting local state.

For Supabase real-time equivalents: same rules apply — unsubscribe channels on cleanup, treat Postgres as source of truth, throttle/batch updates to stay within free-tier WebSocket message quotas.

## 7. Rate Limiting (apply to every endpoint that needs it)

Required on: auth endpoints, AI API calls, email/SMS sending, file processing, any webhook-like endpoint.

Combine per-IP and per-user limiting — either alone is defeated (IP rotation or new account creation).

For free-tier stacks: Upstash Redis (serverless, has rate-limit primitives) or a private Supabase schema table not exposed via PostgREST.

## 8. Secrets Management

| What | Client-safe? |
|---|---|
| Supabase anon key | Yes |
| Stripe publishable key (`pk_*`) | Yes |
| Firebase client config | Yes |
| Supabase `service_role` key | **NEVER** |
| Stripe secret key (`sk_*`) | **NEVER** |
| AI provider API keys | **NEVER** |
| Database connection strings | **NEVER** |

If a secret was ever committed to git, it's compromised — rotate it, don't just delete the file.

## 9. Tool Failure Fallback Matrix (from CODE sub-prompt, applies to client builds too)

- PythonAnywhere CPU limit hit → Google Apps Script
- Supabase connection pool exhausted → retry with 2s backoff, fallback to Google Sheets temporarily
- Vercel build fails → check for Node.js native imports in edge routes; fallback to Netlify
- AI provider rate limit → switch providers temporarily (Claude ↔ Gemini ↔ OpenAI)

## 10. Pre-Launch Test Checklist (per build, before handing to client)

- [ ] Test with `gitleaks detect` for leaked secrets in git history
- [ ] Confirm `.env` is not tracked: `git ls-files | grep .env` returns nothing
- [ ] Verify RLS by attempting to query another user's data with a test account
- [ ] Confirm AI API spending cap is active
- [ ] Test rate limiting on auth and AI endpoints (rapid requests should 429)
- [ ] Confirm Stripe webhook signature verification works (test mode event)
- [ ] Full user flow test: signup → core feature → usage limit reached → upgrade prompt

---

## Update Log

- 2026-06-13: Initial version, compiled from vibe-security skill + All Fours debugging history + SOVEREIGN RLS pattern + CODE sub-prompt fallback matrix. Created alongside PropBot spec as first reference application.
