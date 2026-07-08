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
  as subordinate third-party sources, **never** in the main flow and **never** above /
  replacing T Cloud Public. `docs/Aws_logo.svg.webp` is present but **unused** (AWS is a
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
**85** Resolved / **11** Open). The **18 Manual are all handled by CDC Bonn**: **7**
analyst-closed (fold into the 85 Resolved = 78 auto + 7 manual) + **11** still Open in
queue — so the CDC-handled count is **18** everywhere (Cases-Overview bars split it
7 resolved / 11 in queue; the funnel draws the 7 rising from Manual up into Resolved).
Tiles (order): Events ingestion 2.4 B/24H · Data ingestion 9 TB/24H · Prevented events
54 K · **Total open cases 11** (the last tile is the jump-off into the Open-cases live
queue — see below). Open breakdown 3/3/5/0. SOC tag: "assisted by T Security · Cyber
Defense Center Bonn".
> **Open-cases live queue** (`#dvOpen`, `buildOpenView`/`openOpenView`/`closeOpenView`,
> data `OC_SEV`/`OC_LIST`/`OC_NEW`): the *Total open cases* tile is an Absprungpunkt to a
> `.dv` detail page. It opens showing **11**, then after ~1.1 s a **12th case arrives
> live — a High**, `C-4490 "Supplier agent · out-of-profile data request"` (clicking it opens the Part 2 case): the count pulses 11→12, the
> new row slides in at the top with a NEW badge + glow, and High bumps 3→4
> (so 3/4/5/0 = 12). This "+1 live" is intentional narrative — the snapshot tiles / the
> `nOpen` funnel popover stay at **11**; do NOT reconcile them to 12.
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
- Header brand: a small green **Cortex "C"** logo (`.cxlogo`, a single evenodd path
  traced from `docs/Cortex_logo.png`, brand green `#74c86c`) sitting **inline inside the
  title**, sized to the title's cap-height (~21px), immediately left of a **per-view title**
  (`#brandTitle`, set in `showView`): **"Cortex Command Center"** on the radar/assets view,
  **"Cortex XSIAM"** on the flow view — both over "AI-driven Security Operations · powered
  by [inline T Security logo]".
- **Flow sources**: `SRC24` / `SRC30` arrays (name, `s` asset count, `icon`, `w` ribbon
  weight, `ep` endpoint-highlight, `t` Telekom-magenta, `rate`, `res`). Icons via
  `ICONS` + `iconSVG()`; the magenta "tmark" uses `TSVG`.
- **Flow numbers**: `MODES` (`h24`/`d30` → `left`/`center`/`right` spine cfg); the DOM
  in `#right24`/`#right30`/`#tiles24`/`#tiles30`; the prioritization `#prio` block +
  `BREAK` array. Spine values come from `MODES` via `setSpine`, **overriding** the
  static `data-count` placeholders in the HTML.
- **Flow canvas** (particles, streams, magenta strand, core): the `frame()` render loop
  + `newInflow`/`newOut`/`rebuildParticles`.
- **Detail popovers**: the `D` object in `detailHTML(key)`; wired by `wire()` /
  `wireSources()`.
- **Assets**: `A_BUCKETS` (buckets), `A_LOC` (sites: cats + status; `imedone:1` on the
  clinical-care sites Main Campus + Outpatient renders the magenta iMedOne® system chip
  in `selectLocation`), `PMARK` (site marks), `buildAssetsUI` / `selectBucket` /
  `selectLocation` / `drawAssets` (radar + magenta sweep). Radar center
  `AC={x:800,y:440,R:264}`, `ACX0=800`.
- **Shared asset vocabulary (KEEP CONSISTENT)**: the same category/source strings —
  **Medical devices (IoMT)** · **Clinical endpoints** · **Imaging / PACS** ·
  **Laboratory (LIS)** · **Identities & access** · **Servers & VMs** · **Network & OT** —
  are reused verbatim across `SRC24`, `A_LOC` cats (both clinical sites), `INV`, and
  `DYN_MARKS`. Never re-spell one of them in only one list. **Casing**: category /
  descriptor names are sentence case (only the first word capitalised; acronyms like
  IoMT/PACS/LIS/OT/VMs stay upper); brand/product/site names (iMedOne · HIS, T Cloud
  Public, Azure, GitHub, Main Campus …) and view titles keep Title Case.
- **Two case-flows share one grammar (KEEP IN SYNC)**: the main-flow funnel (`buildWires`
  24H block) and the Cases-Overview lifecycle (`buildCases`) draw the *same* ribbon set —
  Cases→Automated (teal) / Cases→Manual (grey); Automated→Resolved (teal, 78);
  Manual→Resolved (teal, the 7 rising bottom→top); Manual→Open (amber, 11). There is **no
  Automated→Open** ribbon (it would be 0). Both use the same circle nodes: Automated /
  Manual are 52px `.disc2` icon circles (`.co-fun` reuses the funnode styles on the
  overview). Edit both together.
- **Connection rule (EVERY flow line, all views)**: lines attach at a node's **edge at
  mid-height** (horizontal tangents; vertical drops leave the bottom edge → top edge) and
  **stop exactly on the rim** — never float, never enter a shape. Numbers are the anchors:
  `.cap`/`.co-node>span`/`.outcome>span` labels hang absolutely BELOW the number so the
  number's midline sits exactly on the wire height. Wires start/stop at the number's
  left/right edge (e.g. `buildWires`: waist 440 → "2,412" → 562→core-rim; Cases +30/−32;
  funnel discs ±26). Same rule in `buildCases` and the agent scene (`agLinkH`/`agLinkV`).
- **24H detail overlays** (`.dv` pattern, opened by overriding the spine clicks):
  `buildInventory`/`openInventory` (Data Inventory, `INV`), `buildDynamic`/`openDynamic`
  (Dynamic View, `DYN_MARKS`/`DYN_FEED`), `buildCases`/`openCases` (Cases Overview,
  handling bars + MITRE list). Wired at the end of the script; each has a `‹ Flow` back
  button and Esc-closes. NB: scope label rules as `.dvnode>span` / `.co-node>span` so the
  count-up number spans keep the big font.
- **Animated overlay flows**: all three overlays run **particles along their ribbons/lines**
  via `dvFlow(svg,geom,n,col,opts)` (spawns SVG dots) + `dvTick()` (advances them with
  `getPointAtLength`, hooked into the main `frame()` loop). `ribbon()` returns its path so
  callers can animate it. Data Inventory flows **source→centre** (+ centre→Issues/Prevented),
  Dynamic View flows **outer marks→centre** (`rev:true`), Cases Overview flows **along the
  lifecycle**. Each `buildX` calls `dvClear()` first; each `closeX` calls `dvClear()` so the
  loop idles when closed. `prefers-reduced-motion` → `dvTick` no-ops (no particles).
- **Vendor logos**: `LOGO` = 4 inlined webp data-URIs (Microsoft 365, Azure, Google
  Cloud, GitHub), tinted mono via `filter:brightness(0) invert(.72)`. Used ONLY in the
  Data Inventory + Dynamic View as subordinate third-party sources — **never** in the
  main flow, and **never** above/replacing T Cloud Public. All four are **icon-only marks
  + a normal text label** (no baked-in wordmark) so the third-party rows read uniformly;
  the Office/Google wordmark logos were cropped to their icon (`docs/o365-icon.webp`,
  `docs/gcp-icon.webp`; the `wide` row variant is retired). Sources live in `docs/*.webp`.
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
- Active branch: `claude/issues-cases-flow-refine-hlxipr` (based on the earlier
  `claude/cortex-xsiam-research-drgysn` line, now ahead of it). Push with
  `-u origin <branch>` and retry with backoff on network errors. Do **not** open a PR
  unless asked.
- Commit-message footer:
  `Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>` and
  `Claude-Session: <the current claude.ai/code session URL>`.
- Never put a model identifier in commits, PRs, code, or any pushed artifact.

## Part 2 · Supplier agent case (`#dvAgent`)
A `.dv` scene styled like a **Cortex case interface**, reached by clicking the incoming
new case in the Open-cases live queue (the 12th row `C-4490 "Supplier agent · out-of-profile
data request"` → `openAgent`). **No score badge, no voice banner, no auto-play.** Layout:
- **top** = case header (crumb · title · High/status/Agentic-governance chips) + the
  **alert** ("Unusual agent behavior detected…") + a two-bullet **Summarized by AI** list.
- **middle = two distinct layers** (the whole point — digital ≠ physical):
  1. **AI orchestration agents** (`.ag-dagent`, glowing concentric-ring orbs `.orb>i.r1/.r2/.r3`,
     per-node `--ac` accent): the external **Supplier logistics agent** (`.ag-sup`, pink,
     dashed pulsing ring, `external` badge) → **API gateway · scoped** (`.ag-gate`, shield) →
     **Delivery scheduling** + **Stock replenishment** → **Route & traffic control** (fleet
     dispatch). Its **approved scope** is drawn as **teal solid ribbons** (`.ag-gatelink`
     supplier→gateway, plus the internal mesh) with `dvFlow` particles that never stop.
  2. **Physical · medication AGVs** (`.ag-corridor` lane + `.ag-loc` location tiles
     Pharmacy → Ward med room → Patient room → **Restricted ward** `.lock`; `.ag-cart`
     robots CSS-animated along the corridor via `@keyframes agvrun` on `--x0/--x1`). The
     dispatcher drives the fleet (Route → corridor) and carts run Pharmacy→Ward→Patient.
  The **attempted (denied) access** is the contrast: **red dashed `.ag-suplink` edges** from
  the supplier reach past its gateway scope to three **`.ag-blk` chips** (Live AGV location ·
  Patient-linked routes · Restricted ward). Allowed = teal to gateway; denied = red dashed to
  the blocked chips.
- **right** = a **Resolution Center** driving a **3-step** flow (`agState` 1→3, `s1…s3`
  classes, `agBuild`/`agRender`):
  1 **Alert** → click *Isolate agent* → 2 **Isolation** (the `.ag-sandbox` dashed *Secure
  simulation* container fades in around the supplier, which turns magenta; its red
  attempted-access `.ag-suplink` edges are cut; blocked chips fade; **internal agents + AGVs
  keep operating**) → click *Revoke supplier access* → 3 **Revoke** (supplier greyed, the
  `.ag-gatelink` severed, status Resolved, audit `.ag-donenote` lit).
Reduced/glowing, real Cortex/AGV naming, `prefers-reduced-motion` safe (carts + particles
snap off). `‹ Open cases` / Esc returns to the queue (instant, no re-anim).

## What's next / open ideas (not built)
- If real vendor logo SVGs are provided, swap them into the source list + site marks.
- Optional voice-over / TTS for the agent-scene beats (the scene itself is already wired to
  the C-4490 open case).

## Known limitations
- Positions in all views are hand-placed for 1440×810; re-screenshot after edits.
