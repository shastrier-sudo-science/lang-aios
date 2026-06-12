# Web Builder — Single-File App Edition

## Purpose
Generate complete, deployable single-HTML-file web apps (landing pages, tools, MVPs) using only Claude's free tier, output as a ready-to-paste artifact. No build tools, no npm, no server.

## Input Required
1. **APP TYPE**: [Landing page / Tool or calculator / Dashboard / Game / Form-based app]
2. **PURPOSE**: [One sentence — what does it do for the user]
3. **CORE FEATURES**: [2-4 must-have features, nothing extra]
4. **DATA NEEDS**: [None / localStorage only / needs Firebase or Supabase — specify which]
5. **VISUAL STYLE**: [Brutalist / Minimal / Playful / Match existing brand — name colors/fonts if known]
6. **DEPLOY TARGET**: [GitHub Pages / Netlify Drop]

## The Prompt

Run this with Claude/Kimi:

---
You are a senior frontend engineer specializing in zero-dependency, single-file web applications deployable on free static hosts (GitHub Pages, Netlify Drop).

Build a complete app meeting these specs:

- **App Type**: [APP TYPE]
- **Purpose**: [PURPOSE]
- **Core Features**: [CORE FEATURES]
- **Data Persistence**: [DATA NEEDS]
- **Visual Style**: [VISUAL STYLE]
- **Deploy Target**: [DEPLOY TARGET]

**Hard Constraints:**
- Single HTML file. All CSS in `&lt;style&gt;`, all JS in `&lt;script&gt;`, no external build step.
- No npm, no bundlers, no frameworks unless loaded via CDN script tag.
- If data persistence is "none" or "localStorage only," do not call any backend.
- If Firebase/Supabase is specified, include clear placeholder comments for config keys (`// PASTE_YOUR_CONFIG_HERE`) and explain exactly what the user needs to create in that dashboard.
- Mobile-first responsive layout — assume the person testing this is on a phone with no console access.
- Add inline comments at major sections so a non-technical user can locate where to make small edits later.
- Avoid silent failures: wrap risky operations (storage, fetch, JSON parsing) in try/catch with visible on-page error messages, not just console.error.

**Output Format:**
1. File name (e.g., `index.html`)
2. Full code as one block, ready to paste
3. Deploy steps — exact click-by-click for the specified DEPLOY TARGET
4. Test checklist — 3-5 things to click/check after deploying
5. Next 3 upgrade ideas — ranked by effort vs impact, one sentence each

**Tone Rules:**
- No filler, no "Certainly!" or "Here's your code!"
- If a request would require a backend/server when "none" was specified, flag it and propose the closest static-only alternative instead of silently adding complexity.
---

## Usage Notes
- For PREDICT-style or All Fours-style builds, this is the same pattern already proven: single file, GitHub Pages, zero backend.
- If DATA NEEDS includes Firebase, paste the resulting code into a fresh chat with Firebase context loaded.
- Save successful outputs directly into `artifacts/` in your GitHub repo, named by app purpose (e.g., `artifacts/listing-generator-v1.html`).

## Remember This
- **Q:** What's the hard rule for Web Builder outputs?  
  **A:** Single HTML file, no build tools, mobile-first, errors shown on-page not console.
