I want to build a game Here's the complete brief 

```markdown
# PROJECT BRIEF — StarWanderer (design brainstorm concluded, ready to build)

## Context
I'm a solo dev building StarWanderer, a 2D browser space sandbox:
- Live: https://shastrier-sudo-science.github.io/StarWanderer/
- Repo: github.com/shastrier-sudo-science/StarWanderer
- Tech: deliberately ZERO-BUILD — the entire game is one file (index.html, ~1,360 lines,
  vanilla JS + Canvas 2D + DOM overlay for station UI). No npm, no build step, hosted
  on GitHub Pages, edited in a plain text editor. Protect this workflow where possible.
- Long-term vision: an Eve Online-inspired MMO with our own spin, but strictly
  SINGLE-PLAYER until every mechanic, system, structure, rule, and sprite is functional.
- This brief is the output of a completed code review + design brainstorm. Do NOT
  re-analyze from scratch — the roadmap below is agreed. If the code contradicts
  this brief, the code is the source of truth; flag discrepancies and continue.

## 1. What exists in the game today
- 6 hand-crafted systems (Sol, Alpha Centauri, Vega, Sirius, Tau Ceti, Proxima) linked
  by jump gates; each system is ONE 1920x1080 room (player clamped to screen, no
  camera, no scrolling)
- 7 stations; docking opens a DOM overlay with 4 tabs: Trade (6 commodities),
  Missions (delivery/combat/exploration, max 4 active, rerolled on every dock),
  Upgrades (6 flat stat mods), Shipyard (Scout/Freighter/Fighter)
- Pirates: 3 tiers, patrol/chase AI, per-system spawn rate 0.003–0.009/frame, cap 6
- XP levels 1–10 (XP_TABLE caps at 22,000), credits, totalKills
- Supply/demand per station per commodity (random walk ±10 every 600 ticks)
- Death = full game reset. No persistence anywhere. No audio, no touch, no delta-time.

## 2. Known bugs from code review (all P0 fixes)
1. PRICE DESYNC: UI displays calcPrice = base x (1+(demand-supply)/100), but engine
   buyItem/sellItem charges flat station.prices x amount. Sell displayed as 88% of
   dynamic price but paid at base. All price math must move into the engine.
2. PRICES NEVER CHANGE: updateStationPrices() only drifts supply/demand; the prices
   object is static forever. "Prices fluctuate over time" tip is currently false.
3. Delivery missions don't occupy cargo — cargoItem is flavor text; mission completes
   merely by docking at the target station. Trade loop and mission loop never touch.
4. No persistence (refresh = total loss) and no delta-time (rAF frame-based loop, so
   144Hz monitors play ~2.4x faster than 60Hz).
5. Dock/undock rerolls station missions (exploit).
6. Exploration missions complete on arrival though description says "return with
   survey data".
7. Combat missions count kills in ANY system though description says "in this system".
8. Fuel is a tradeable commodity but ships never consume it. skills:{} is vestigial.

## 3. LOCKED design decisions (agreed — do not relitigate)
- DEATH MODEL: Eve-style asset loss. On destruction: lose ship + cargo + installed
  modules; KEEP credits/skills/reputation; respawn in a clone at last docked station.
  Hull insurance pays a % of ship value, funded by a premium (main credit sink).
- SCOPE: single-player until ALL gameplay mechanics, systems, structures, rules, and
  sprites are functional. Multiplayer is deferred but must never be designed out.
- CORE FANTASY: THE TRADER. Combat and exploration exist as inputs to the trading
  game, not parallel games.

## 4. Design pillars (trader-first)
Four loops that feed each other:
- LEGIBLE SIGNALS: price history sparklines, system security rating, market news feed
- MARKET IMPACT: the player's own trades move prices; regional spreads create routes
- RISK PREMIUM: formalize pirateSpawnRate as a sec-status rating (Eve-style 0.0–1.0);
  safe core = thin margins, frontier = fat margins + real loss risk + insurance math
- CARGO IS CAPITAL: capacity/speed tradeoff across ships, fuel burn, insured value
Cheap synergy hiding in existing data: survey missions + the existing "Data Crystals"
commodity → surveys should produce a sellable SURVEY DATA commodity (exploration
feeds the market). Later: asteroids → ore → refining → existing commodity table.
Differentiation ("our spin"): browser-native "Eve in a tab" (zero install, 15-minute
sessions, async market that moves while offline); legible 2D tactics where terrain
has TRADE meaning (nebulae conceal haulers but slow them, gravity lanes cut fuel but
are predictable ambush zones, migrating pirate hot zones); first-finder naming of
discovered anomalies/derelicts; player-authored frontier law (much later).

## 5. Build ladder (phases with exit criteria — build in this order)
- P0 — HONEST FOUNDATIONS: unify price math in engine; make prices respond to
  supply/demand AND to player trades; delta-time loop; localStorage autosave
  (position, credits, cargo, ship, missions, visited systems); deliveries physically
  occupy cargo; death → clone + insurance policy; seeded RNG in all sim logic.
  EXIT: a session survives refresh, and the trading tip is no longer a lie.
- P1 — LIVING MARKET: sec-status per system; margin-vs-risk spreads; price history
  UI; fuel consumption; news ticker (events move prices, e.g. war in Sirius →
  weapons spike).
  EXIT: a player can run a profitable route and explain WHY it worked.
- P2 — WORLD DENSITY: camera + scrolling systems (4x+ screen size, parallax stars);
  asteroid mining → ore → refining pipeline; NPC haulers whose prices/losses ripple;
  derelict scanning; WebAudio (engine hum, lasers, dock chime).
  EXIT: three viable playstyles (hauler / miner / bounty hunter) all paid by ONE economy.
- P3 — DEPTH: slot-based ship fitting (weapon/utility/defense + power budget)
  replacing flat stat stacking; courier contracts with collateral; faction standing
  (prices, mission access, gate permissions); regional market view.
  EXIT: ship builds and trade routes are theorycraftable.
- P4 — CONTENT & POLISH: sprites, audio polish, more systems, events.
  EXIT: "all mechanics, systems, structures, rules, sprites functional" — the agreed
  gate before any multiplayer discussion.

## 6. Technical guardrails (so nothing gets thrown away)
1. Seeded RNG everywhere in sim logic — no bare Math.random() in economy/AI paths.
2. State is plain serializable data; render/UI is a pure function of state. Fold
   stray module globals (stationTabState, stationAmounts) into state/UI-state.
3. Data-driven content: systems/stations/commodities/ships as JSON, not code literals.
4. Formalize an economy tick (extend the existing 600-tick price refresh).
5. Stay single-file through P2; split into sim/render/ui/data modules only when file
   size forces it. The split must be mechanical, not architectural.
6. The sim must remain deterministic and tick-based so a future authoritative server
   can run it unchanged.

## 7. First action in this thread
Start P0 against the real repo code. Read index.html fully first, then implement P0
items as small, individually verifiable increments, preserving the zero-build
single-file approach. Ask me before making any decision that contradicts this brief.
```

Start P0
