Complete handoff — copy the whole block below and paste it as your first message in the new chat:

````markdown
# StarWanderer — Project Handoff (paste this into a fresh session)

## 1. What this is
- **StarWanderer**: a 2D browser space sandbox game (trade / mine / haul / fight pirates / jump between systems). Solo dev: Shastrie.
- Live on **Vercel** (git-connected to a GitHub repo; repo moved off GitHub Pages). No backend, no build step.
- **Zero-build multi-file workflow**: plain vanilla JS files loaded via `<script>` tags — NO bundler, NO npm, NO framework. All paths relative (works on subpaths and file://).
- Save: **localStorage key `starwanderer_save_v1`** (must never change — players have saves).
- Language of the codebase: ES5-style classic scripts, `"use strict"`, `var`, prototype methods, `var self = this` aliasing. Keep that style for new game code.

## 2. File tree (game root = `public/` in the dev sandbox; = repo root on GitHub)
```
index.html          (deploy shell: canvas + station overlay + 11 script tags + deploy-guard IIFE)
style.css           (266 lines, dark theme, touch pads, letterbox, safe-area insets)
js/boot-error.js    (15)   load order 1  — red banner if js/ or style.css missing on the host
js/content.js       (511)  2  — static data: SHIP_STATS, commodities, systems, factions, news strings, missions
js/assets.js        (73)   3  — asset manifest (Assets.get/ok), graceful procedural fallback if a PNG is missing
js/engine.js        (1029) 4  — sim: GameEngine, fixed tick SIM_STEP=1000/60 accumulator loop (deterministic, "for a future authoritative server")
js/render.js        (1024) 5  — fixed 1920x1080 coords; drawShipSprite(); SHIP_IMG_H; SHIP_FLAME_REAR; SHIP_ART_ROT; swHudScale; decor
js/input.js         (422)  6  — keyboard/mouse + TouchSys (touch stick, FIRE/MINE/MED pads, boot gated on maxTouchPoints>0)
js/fitting.js       (218)  7  — ship fitting math (module slots, insurance premiums)
js/persistence.js   (183)  8  — save/load starwanderer_save_v1 (autosave on state change + beforeunload; never persists title/death screens)
js/audio.js         (86)   9  — AudioSys (laser/explosion/notify...), init on first user gesture
js/station-ui.js    (497)  10 — docked station DOM UI: Trade / Fitting / Shipyard tabs, news ticker, toasts
js/main.js          (92)   11 — boot: fitCanvas (letterbox 16:9 + DPR cap), key/mouse wiring, screen switcher
assets/             32 files: bg/ (3 jpg), celestial/ (6 png), props/ (8 png), ships/ (11 png), stations/ (4 png)
starwanderer-dist.zip  full deploy package, 46 files, 2,009,282 B, zip -r -X -D, all entries byte-verified
DEPLOY.txt          upload instructions incl. GitHub drag-the-folder gotcha + Vercel section
```

## 3. Critical engine conventions (do not break)
- **Angles**: engine math uses standard atan2 convention (0 = +X/right). Player stores `p.angle = atan2(dy,dx) + PI/2` (nose-up draw convention). NPC pirates/haulers store pure travel bearing; render adds +PI/2.
- **Sprite art**: all 9 player hull PNGs are painted nose-UP in image space. `assets/ships/pirate.png` and `hauler.png` are painted NOSE-LEFT, corrected by `SHIP_ART_ROT = { pirate: PI/2, hauler: PI/2 }` in render.js (image branch only; the procedural fallback vectors are already nose-up and must not be rotated).
- **Render is pure presentation** — never touches sim state; randomness allowed only in fx (flames/particles). Deterministic sim uses `this.rand()`.
- **State shape**: `engine.state.{player, systems, bullets, particles, keys, screen, tick, combatLog, notification, deathReport}`; `engine.camera.{x,y,z,hs}` (z = world zoom on small screens, hs = HUD scale). Screen values: title / space / starmap / station / help / gameover.
- **Player hulls (SHIP_STATS keys)**: scout, freighter, fighter, mule, pathfinder, wasp, atlas, rampart (L6 gate, 75k), sovereign (L9 gate, 160k). NPCs: pirate, hauler.
- **Mobile (P6-MOBILE)**: letterboxed 16:9 canvas at display res; HUD auto-scales physically (~2.1x on phones); fullscreen button #fsBtn; portrait rotate hint #rotateHint; 44px touch targets; `body.touch` class.
- World: multiple systems (Sol...), stations, jump gates, asteroids (hold E to mine), pirate spawns per-system security, NPC haulers flying station→gate routes, faction standing, GNN news ticker, mission system ("DATA WING DIRECTIVE"), clone-death insurance ladder (10 levels, 70%→97% payout), modules upgrade to LV10 (~1.85x compounding prices), currency CR, fuel burned per jump.

## 4. Build history (version markers)
- **P1–P4**: core loop — flight/shooting, world bigger than viewport, mining, trading, docking, economy tick, hints, pirate spawning off camera edge, save/load.
- **P5**: file split into the 11-script zero-build bundle + deploy guard; touch controls P5.
- **P6**: modules LV10, clone insurance ladder, apex hulls Rampart/Sovereign, js/assets.js (11th script) + assets/ art pack with procedural fallback, per-system decor.
- **P6-MOBILE**: letterbox canvas, DPR backing store, auto-scaling HUD, camera zoom, big touch UI, fullscreen, rotate hint. Changed exactly: index.html, style.css, js/main.js, js/render.js, js/engine.js, js/input.js.
- **P7-SHIPART**: painted ship sprites extracted from the user's two JPG sprite sheets (Python/PIL pipeline with flood-fill bg removal + sheet-grid-line removal). All 11 ships mapped to art; missing PNG falls back to procedural vectors. Changed: js/assets.js, js/render.js + 6 new / 5 replaced ship PNGs.
- **P7-FIX NOSE-FORWARD** (latest): pirate/hauler art is nose-LEFT -> flew sideways. Fixed via SHIP_ART_ROT (render.js) + patrol pirates now face their motion (engine.js). Player hulls untouched. Upload to the repo = just those 2 files.

## 5. Deployment workflow
- User (non-git) uploads changed files via GitHub web UI -> Vercel auto-deploys (~1 min) -> hard refresh (Ctrl+Shift+R).
- **Gotcha**: when uploading folders via the web UI, drag the `js/` and `assets/` FOLDERS themselves (loose files upload without the folder and break the game). Single files upload fine individually.
- Sanity check after deploy: `https://<url>/js/main.js` and `https://<url>/style.css` must return code, not 404.
- Sandbox delivery pattern: "game files" download panel (bottom-right button on the preview page, `src/app/page.tsx`) lists the current zip + the individual files changed by the latest update + DEPLOY.txt.

## 6. Roadmap options (the brainstorm — nothing decided yet)

### Distribution / traffic (agreed: do first, monetization needs players)
- [ ] **itch.io page**: upload zip as HTML5 game, pay-what-you-want or fixed price. Zero code changes needed. ~1 hour.
- [ ] **PWA install**: manifest.json + service worker + icons -> installable on phones/desktop, offline play, fullscreen. Fits the existing P6-MOBILE work. Can be built in the sandbox now.
- [ ] **Share/screenshot button**: photo mode + share -> players market the game organically.
- [ ] **Web portals**: CrazyGames / Poki ad revenue share, they bring traffic, need submission + approval.
- [ ] **Devlogs** (YouTube/TikTok): solo space games do well; the sprite-extraction story is good content.

### Multiplayer ladder (climb, don't jump — engine is already deterministic tick-based)
- **Stage 1 — Living universe (async, no netcode, free-tier friendly)**: global shared economy + events via 2-3 Vercel serverless functions + free DB (Turso/Supabase). Player actions nudge market prices, post to the existing GNN news ticker, spawn named wrecks, feed a bounty board + leaderboard. Feels multiplayer, zero lag/cheat surface.
- **Stage 2 — Shared co-op flight**: real WebSockets, authoritative server. Vercel functions can't hold sockets -> small always-on server (fly.io, PartyKit, or a $5 VPS). Co-op trading/convoys is more forgiving than PvP.
- **Stage 3 — PvP netcode**: lag compensation, anti-cheat, matchmaking. Only if Stage 1 proves retention.

### Monetization menu
| Model | Ceiling | Needs |
|---|---|---|
| itch PWYW | Low | an afternoon |
| Portal ad rev-share | Low–med | approval; they bring players |
| Ko-fi/Patreon | Low–med | devlog cadence |
| "Captain's License" DLC | Med | payments (Lemon Squeezy) + key-check endpoint + premium content (extra systems/hulls/story) |
| Steam premium $5–8 | Highest for solo | $100 fee, Tauri wrapper, achievements/cloud saves, 2–4 more months of content |

### Recommended sequence
1. PWA + share button + itch.io page (traffic)
2. Stage 1 living universe (wow-per-dollar; reuses GNN ticker + economyTick)
3. Content depth: faction storyline (standing system exists), bounty hunting, hardcore permadeath leaderboard mode
4. Decision point: if numbers pull, Steam premium via Tauri; flesh out story campaign first

## 7. If this session runs in the same dev sandbox
- Project at `/home/z/my-project`; game root `public/`; wrapper page `src/app/page.tsx` (full-screen iframe of `/game.html` + download panel).
- Dev server: `bun run dev` on port 3000 (already running; logs in `dev.log`). Lint: `bun run lint` (public/** is eslint-ignored — intentional, game code keeps its classic style).
- E2E: `agent-browser` CLI; game iframe is reached via parent eval + `document.querySelector('iframe').contentWindow`; engine instance at `window.engine`; headless has no touch points.
- `worklog.md` in project root logs every task (Task IDs 11–15 so far); append a section per task.
- Packaging: stage to /tmp, `zip -r -X -D`, then byte-verify every entry with `cmp`, keep 46-file structure (shell + style.css + DEPLOY.txt at zip root + js/ + assets/).
- Never run `bun run build`; never change the save key; keep zero-build (no bundler) for game code.
````

One tip: when you start the new chat, tell it which option to tackle first (e.g., "start with the PWA + share button, then Stage 1 living universe") — the doc gives it everything it needs to skip re-discovery and go straight to building. It's been a genuinely fun build, Shastrie — the game is in great shape to grow.
