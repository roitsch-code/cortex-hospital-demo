# CLAUDE.md — Cyber Security Command Center (T Gallery hospital demo)

> Read this fully before changing anything. This is a **design-led interactive demo**
> for the **T Gallery** (a Deutsche Telekom exhibit), not a production app and not a
> slide. The look matters as much as the content. **Fake data, but internally
> consistent and correct.**

## What this is
A cinematic **security-operations demo** in the visual language of Palo Alto Networks
**Cortex XSIAM 3.0** (dark, glowing, animated), adapted to a **generic large university
hospital** (~1,300 beds; research + global collaborations) and framed with Deutsche
Telekom **T Security** branding. Single self-contained `index.html`, no build step,
runs offline. Shown on a laptop or large screen at a live exhibit.

## The demo (two views, one file)
Navigation is a small state machine: `showView('assets' | 'flow')`.

1. **Assets Command Center** (`#assetsView`) — the **entry screen**. A centered radar
   organised **by site** (not department, not geography): **Main Campus** dominant at
   top, plus satellites (Outpatient Centers, T Cloud Public, Telemedicine & Home,
   Reference Labs, Research Institute) as orbital callouts with a faint connector each.
   Left anchor = the **iMedOne®** wordmark (real Telekom HIS). Four nested **buckets**
   (All ⊃ At Risk ⊃ Active Threats ⊃ At Risk+Threats) re-tint the radar glow and count
   up the center. A **magenta radar sweep** scans the static asset dot-field. Click a
   site → slide-in detail (category donut + status). `Show Issues ›` → the flow.

2. **Issue-Cases Flow** (`#flowView`) — the main pipeline, left→right:
   **Sources** (hospital systems, left) → particle streams through curved ribbons →
   central **correlation core** (concentric rings, some CW some CCW, count-up numbers) →
   **Cases** → right-hand outcome funnel. A **24H ⇄ 30D** toggle (top-right) swaps the
   whole flow. The 30D center opens a **Prioritization** overlay. Everything is
   clickable → detail popovers (`detailHTML(key)`).
   In **24H**, the three spine anchors open full reduced drill-down overlays instead of
   popovers: **Issues → Data Inventory** (grouped sources + volumes/sparklines →
   Issues/Prevented), **correlation core → Dynamic View** (radial automation donut +
   orbital source marks + live feed), **Cases → Cases Overview** (lifecycle funnel +
   handling bars + MITRE ATT&CK by tactic). All share the `.dv` overlay pattern.

## Ultrawide flow (aspect)
Target screen is a **32:9** ultrawide (iiyama ProLite XCB4594DQSU, **5120×1440**). The
**assets entry view stays 16:9** (fixed 1440×810). The **flow view runs at 32:9**
(**2880×810** — same height, wider only; "Höhe lassen, nur Breite"; 2880×810 scales 1:1 to
5120×1440). Layout is driven by `WIDE`/`applyGeo()` + the `LAYOUT.narrow`/`LAYOUT.wide`
tables (only X coords change; every Y stays put). `showView('flow')` sets `WIDE=true`;
`showView('assets')` sets it false and resizes stage/canvas back to 1440. The core is
centred at x=1440; 2,412 and 96 sit mirror-symmetric about it (1440±360).
- **The bottom stat tiles (`#tiles24`/`#tiles30`) are removed** from the flow (hidden in
  `renderMode`) — the ingestion/prevented cards looked cluttered on the wide screen.
- ⚠ **Canvas clear must use `STAGE.w`**, not a hard-coded width. `frame()` does
  `ctx.clearRect(0,0,STAGE.w,810)`; clearing only 1440 leaves the right half of the wide
  canvas un-cleared, so particles + core dots accumulate into bright "sonar" shells/streaks.
- In wide mode the **left step becomes the Data-Inventory breakdown** promoted into the
  flow (`buildSourcesWide()` → grouped rows from `INV`, with volumes + sparklines), exactly
  like the user's 3rd screenshot. Core + Cases stay the cinematic flow (kept **reduced** —
  no dense boxes). Narrow (16:9) keeps the simple `SRC24`/`SRC30` list.
- **Open cases = a `LIVE QUEUE` list** on the far right (`#liveQueue`, built from `QUEUE`
  by `buildQueue()`), one row per open case (severity badge · title · case-id · tag). It
  fills the right and balances the source list on the left. The 18-Manual node feeds it.
  (Replaces the old chevron/`#nOpen` display; 30D still uses the 5 status `.pcard`s.)
- **Agent-drift scenario** (24H only): the flow just runs; a click on the **empty flow
  backdrop** (`e.target===#stage`) toggles `fireDrift()`/`resetDrift()`. `fireDrift()`
  prepends the `DRIFT_CASE` row to the queue — *"Supplier agent · out-of-profile data
  request"* (High, `C-4490`, **NEW** badge, highlighted) with a sub-line *"Out-of-profile
  request to iMedOne · auto-contained by policy · queued for T Security · CDC Bonn"* — and
  bumps the header `11 → 12 OPEN`. Ties into the Telekom Agentic-Hub governance story.
  Real names only.

## HARD design constraints (do not violate)
- **Keep the Cortex aesthetic**: near-black background, teal (`#2fd6c0`) glow, flowing
  SVG ribbons, particle swarm, radial/orbital layouts, soft shadows and pulses.
  Cinematic and reduced.
- **DO NOT build a dense "boxes-in-bands" architecture chart.** A previous attempt did
  and was rejected as "a shitty PowerPoint." Detail views stay **reduced** (few glowing
  nodes, negative space).
- **It is a guided flow, not a slide** — scenes with transitions and interaction.
- **Telekom magenta (`#E20074`) is an accent only** — T Security branding, the iMedOne +
  T Cloud sources/marks, the radar sweep, and a subtle magenta particle strand in the
  flow. Cortex **teal stays primary**.
- **Animation is SLOW** with clear left→right choreography. `prefers-reduced-motion`
  is respected (all count-ups/particles snap to final state).

## Real vs. concept — ONLY use real, verifiable names
The user was emphatic: **"dont invent shit."** Do NOT invent product names.
Real names used here (keep them):
- **iMedOne®** — real Telekom Hospital Information System (HIS).
- **T Cloud Public** — hosting for iMedOne + a cloud site/source.
- **T Security** — the DT security arm branded in *Sovereign Cortex with T Security*
  (PANW + DT, announced 2026-06-09; provides the SOC + IAM). Header brand **and** the
  assisting SOC on the flow.
- **Cyber Defense Center (CDC) Bonn** — DT's real integrated Cyber Defense & Security
  Operations Center in Bonn (largest in Europe). This is the SOC that assists.
- **Magenta Security** — DT's *customer MDR product line* (MDR Start/Pro); a different
  brand layer, **not** used in this sovereign framing. Kept off-screen.
  > Naming was researched (telekom.com / t-systems.com / PANW press). On-screen SOC tag:
  > **"assisted by T Security · Cyber Defense Center Bonn"** — verified correct here.
Generic on screen (no hospital name): the campus is just **"Main Campus"** — no
"Venusberg"/UKB/Bonn hospital naming anywhere in the UI.
> Before any public showing, re-verify product status (telekom.com / paloaltonetworks.com).

## Logos / marks
- **`docs/tsec-logo-white.svg`** — the official Telekom **"T"** glyph, inlined as `TSVG`
  and reused for the T Cloud source + cloud site mark. **viewBox MUST be `0 0 231 275`**
  — a smaller height (e.g. 237) crops the bottom bar. **Never hand-draw / hallucinate a
  Telekom "T".**
- **iMedOne®** is a recreated CSS wordmark (white on magenta). The real raster wordmark
  `docs/imedone.png` is also in the repo (unused) if you ever want to swap it in.
- **Vendor logos** (`docs/*.webp`, provided by the user): **Microsoft 365, Azure, Google
  Cloud, GitHub** are inlined as base64 in `LOGO` and rendered mono-grey
  (`filter:brightness(0) invert(.72)`) — used ONLY in the Data Inventory + Dynamic View
  as subordinate third-party sources, **never** above / replacing T Cloud Public. In the
  **16:9** flow they must **never** appear in the main flow. In the **21:9 wide flow**
  (see below) the left column *is* the promoted Data-Inventory breakdown, so the
  third-party rows (incl. logos) legitimately appear there — grouped under a distinct
  "THIRD-PARTY SOURCES" header, still mono-grey and subordinate, never above the T-Systems
  sources. (This matches the user's own 21:9 mock-up.) `docs/Aws_logo.svg.webp` is present but **unused** (AWS is a
  weak fit for a sovereign German hospital). webp is raster; drop real `.svg` versions in
  `docs/` and re-point `LOGO` if you want vector-perfect marks.
- All flow-source + site icons are clean line-drawn category glyphs (`ICONS`, `PMARK`) —
  **not** vendor logos. Keep it that way for the hospital sources.

## The number model (single source of truth — keep everything reconciled)
**Assets** (nested subsets): All **35,600** ⊃ At Risk **5,840** ⊃ Active Threats **84** ⊃
At Risk+Threats **29**. All split = 24.9K Medical/Clinical · 10.7K IT & Cloud. Sites sum
to 35,600 (Campus 30,200 · Outpatient 2,100 · T Cloud 1,760 · Telemedicine 640 · Labs 520
· Research 380); each site's categories sum to its total and its statuses sum to the
buckets (risk 5,840 / threat 84 / both 29). Data Ingestion = **9 TB/24H**.
**Flow 24H**: **2,412** Issues → **96** Cases (**78** Automated / **18** Manual →
**85** Resolved / **11** Open). Tiles: 2.4 B/24H · 9 TB/24H · 11 Open · 54 K prevented.
Open breakdown 3/3/5/0. SOC tag: "assisted by T Security · Cyber Defense Center Bonn".
*Drift scenario (24H, on click):* the LIVE QUEUE gains a new High case at the top
(11→**12** open) — a transient demo state, `resetDrift()` restores the base list.
**Flow 30D**: **148K** → **34K** unique → **312** Cases (Active **168** = 9 Require
Attention + 121 In Progress + 38 Mitigated; Resolved **144** = 61 Resolved + 83 Accepted
Risk). Tiles: Vulnerable Assets **5,840** (ties to assets At Risk) · Active Cases 168
(sev 44/71/48/5) · MTTR **26 days** (sev 21/21/34/35). Prioritization overlay:
148K → 34K → 4.8K open issues → 312 (99.8% reduction).
> When you change any number, update its detail popover in `detailHTML()` **and** any
> mini-legend so the two never disagree.

## Tech
- One file: `index.html`. Vanilla JS + Canvas (particles/radar) + inline SVG
  (ribbons/rings/marks) + CSS. No frameworks, no bundler, no network calls, no storage.
- Fixed **1440×810** design stage, scaled to the viewport via CSS `transform`.

## Tuning map (where the knobs are, in index.html)
- Colours / theme: the `:root` CSS variables at the top.
- Header brand: title "Cyber Security Command Center" + "AI-driven Security Operations ·
  powered by [inline T Security logo]".
- **Flow sources**: `SRC24` / `SRC30` arrays (name, `s` asset count, `icon`, `w` ribbon
  weight, `ep` endpoint-highlight, `t` Telekom-magenta, `rate`, `res`). Icons via
  `ICONS` + `iconSVG()`; the magenta "tmark" uses `TSVG`.
- **Flow numbers**: `MODES` (`h24`/`d30` → `left`/`center`/`right` spine cfg); the DOM
  in `#right24`/`#right30`/`#tiles24`/`#tiles30`; the prioritization `#prio` block +
  `BREAK` array. Spine values come from `MODES` via `setSpine`, **overriding** the
  static `data-count` placeholders in the HTML.
- **Flow canvas** (particles, streams, magenta strand, core): the `frame()` render loop
  + `newInflow`/`newOut`/`rebuildParticles`. Particles + wires now read the live geometry
  (`CENTER`/`WAIST`/`CASES`/… are `let`, reassigned by `applyGeo()`) and the current source
  list `CURSRC` (set by `buildSources`), so both aspects work off one code path.
- **21:9 layout knobs**: `LAYOUT.narrow`/`LAYOUT.wide` (X coords + `dom` element lefts),
  `applyGeo()`, `WIDE`, `buildSourcesWide()`/`wireSourcesWide()` (24H uses `INV`, 30D uses
  `INV30`). The two spine numbers are mirror-symmetric about the core centre (2,412 and 96
  sit at `CENTER±223`). **No bridge ribbon** touches either number — the particle swarm
  converges onto it and re-diverges (left: sources→2,412→core; right: core→96→funnel). The
  funnel diverges from `CASES+48` (clear of the "96") and each outcome ribbon ends just
  **before** its number so it never crosses the label. 24H funnel: 78 automated → resolved,
  18 manual splits **7 → resolved** + **11 → open**.
- **Agent-drift scenario**: `fireDrift()`/`resetDrift()`, `#driftW` callout, `#flowHint`,
  `#critCount`/`#critNew`, `#openTileNum`; toggled by the `#stage` empty-backdrop click.
- **Detail popovers**: the `D` object in `detailHTML(key)`; wired by `wire()` /
  `wireSources()`.
- **Assets**: `A_BUCKETS` (buckets), `A_LOC` (sites: cats + status), `PMARK` (site
  marks), `buildAssetsUI` / `selectBucket` / `selectLocation` / `drawAssets` (radar +
  magenta sweep). Radar center `AC={x:800,y:440,R:264}`, `ACX0=800`.
- **24H detail overlays** (`.dv` pattern, opened by overriding the spine clicks):
  `buildInventory`/`openInventory` (Data Inventory, `INV`), `buildDynamic`/`openDynamic`
  (Dynamic View, `DYN_MARKS`/`DYN_FEED`), `buildCases`/`openCases` (Cases Overview,
  handling bars + MITRE list). Wired at the end of the script; each has a `‹ Flow` back
  button and Esc-closes. NB: scope label rules as `.dvnode>span` / `.co-node>span` so the
  count-up number spans keep the big font.
- **Vendor logos**: `LOGO` = 4 inlined webp data-URIs (Microsoft 365, Azure, Google
  Cloud, GitHub), tinted mono via `filter:brightness(0) invert(.72)`. Used ONLY in the
  Data Inventory + Dynamic View as subordinate third-party sources — **never** in the
  main flow, and **never** above/replacing T Cloud Public. Sources live in `docs/*.webp`.
- Navigation: `showView(name)`; mode switch: `renderMode(m)`.

## Run
- `npm start` (`npx serve .` → http://localhost:3000), or
- `python3 -m http.server 8000` → http://localhost:8000, or
- just double-click `index.html` (works offline; no server needed).

## Verifying a change (do this before committing)
1. Syntax: extract the `<script>` and `node --check` it.
2. Serve (`python3 -m http.server 8000`) and screenshot with Playwright — Chromium at
   `/opt/pw-browsers/chromium-1194/chrome-linux/chrome`, `NODE_PATH=$(npm root -g)`,
   viewport 1440×810, deviceScaleFactor 2. Capture the assets view, the 24H flow, the
   30D flow, and any popover you touched. Listen for `pageerror` — must be **NO JS
   ERRORS**. (The favicon 404 in the console is harmless.)
3. Check numbers reconcile (see the number model) and no invented product names crept in.

## Git
- Active branch: `claude/flow-layout-21-9-ivhesc` (21:9 wide flow + drift scenario, based on
  the earlier `claude/issues-cases-flow-refine-hlxipr` line). Push with `-u origin <branch>`
  and retry with backoff on network errors. Do **not** open a PR unless asked.
- Commit-message footer:
  `Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>` and
  `Claude-Session: <the current claude.ai/code session URL>`.
- Never put a model identifier in commits, PRs, code, or any pushed artifact.

## What's next / open ideas (not built)
- If real vendor logo SVGs are provided, swap them into the source list + site marks.
- Possible Part 2 (from the original concept, not required): SOC review → governance
  (supplier permission profile) → human-confirmed response (revoke / audit record).
  Keep any such view **reduced**, real names only.

## Known limitations
- Isolation/agent-architecture scenes from the original draft were **removed** — the
  demo is now the two views above. Ignore older references to Scene AGENTS / ISOLATION.
- Positions in both views are hand-placed for 1440×810; re-screenshot after edits.
