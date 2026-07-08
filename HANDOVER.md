# Handover — Cyber Security Command Center (T Gallery hospital demo)

_Last updated: 2026-07-08 · branch `claude/issues-cases-flow-refine-hlxipr`_

> Read `CLAUDE.md` first — it is the full design brief, the number model, and the tuning
> map. This file is just the current state + how to run, view, and continue.

## Where things stand
A single self-contained `index.html` — a cinematic Cortex-XSIAM-style security demo for a
generic ~1,300-bed university hospital, branded **T Security**. Vanilla JS + Canvas +
inline SVG/CSS. No build, no network calls, runs offline. Fixed 1440×810 stage scaled to
the viewport. `prefers-reduced-motion` respected. **No JS errors.**

Two views (`showView('assets' | 'flow')`):

1. **Assets Command Center** (entry) — centered radar organised **by site** (Main Campus
   dominant + 5 satellites), iMedOne® anchor, magenta radar sweep, 4 nested buckets,
   per-site drill-in. `Show Issues ›` → flow.
2. **Issue-Cases Flow** — sources → correlation core → cases → outcome funnel, with a
   **24H ⇄ 30D** toggle. In **24H** the three spine anchors open full **reduced
   drill-down overlays** (`.dv` pattern, each with a `‹ Flow` back button + Esc):
   - **Issues → Data Inventory** — grouped sources (Clinical & Medical / Network &
     Identity / Sovereign Cloud / Third-party) with volume + sparkline, ribbons into
     Issues + Prevented Events.
   - **Correlation core → Dynamic View** — radial automation donut (81% = 78/96),
     sources as orbital marks, scattered severity flags, live SOC feed.
   - **Cases → Cases Overview** — lifecycle funnel + case-handling bars + Automation
     Headroom + MITRE ATT&CK "cases by tactic".
   In **30D** the center opens the **Prioritization** overlay and Cases keeps a popover;
   all other elements open small detail popovers (`detailHTML(key)`).

**Branding note (settled + researched):** on-screen SOC tag is **"assisted by T Security ·
Cyber Defense Center Bonn"**. T Security = DT's sovereign SOC arm (*Sovereign Cortex with
T Security*, PANW + DT); CDC Bonn = DT's real Master SOC. *Magenta Security* is the
consumer MDR brand and is deliberately kept off-screen. See CLAUDE.md "Real vs. concept".

**Sovereignty rule:** hospital/clinical systems are the primary sources; **T Cloud Public
stays magenta/sovereign and is never replaced or out-ranked** by a hyperscaler. The
vendor logos (M365 / Azure / Google Cloud / GitHub·Research) appear ONLY as subordinate
grey third-party sources inside Data Inventory + Dynamic View.

## Numbers (see CLAUDE.md for the full reconciled model)
24H: **2,412** Issues → **96** Cases (**78** Automated / **18** Manual → **85** Resolved /
**11** Open); 9 TB/24H · 2.4 B/24H · 54 K prevented. Dynamic donut 78/96 = **81%**. Cases
Overview handling (78+7+11) and MITRE tactics both sum to **96**. 30D: 148K → 34K → 312.

## How to view / run
- **Offline (best):** open the branch and double-click `index.html` — no server needed.
  `git fetch origin && git checkout claude/issues-cases-flow-refine-hlxipr && open index.html`
- **In-browser, zero install:** htmlpreview (works because everything is inlined):
  `https://htmlpreview.github.io/?https://raw.githubusercontent.com/roitsch-code/cortex-hospital-demo/claude/issues-cases-flow-refine-hlxipr/index.html`
- **Local server:** `python3 -m http.server 8000` → http://localhost:8000
- Not yet published to GitHub Pages (would be a public URL) — offer only if asked.

## Verified
`node --check` on the extracted `<script>` (clean) + Playwright at 1440×810 ×2: the assets
view, 24H flow, and all three drill-downs screenshotted, plus a full click-through sweep
(assets → flow → each overlay open/close → 24H⇄30D → 30D Prioritization via the centre
label). Numbers reconcile everywhere; **no JS errors**; real names only.

## Open items / next steps
- **Logos:** 4 vendor webp are inlined mono in `LOGO`; `docs/Aws_logo.svg.webp` is present
  but **unused** (weak fit). webp is raster — for vector-perfect marks, drop real `.svg`
  into `docs/` and re-point `LOGO`. `docs/imedone.png` (real wordmark) is available to
  swap for the CSS iMedOne wordmark if wanted.
- **Possible Part 2** (not built): SOC review → governance (supplier permission profile)
  → human-confirmed response. Keep reduced, real names only.
- Re-verify Telekom/PANW product statuses before any public showing.

## How to work on it
- Edit `index.html` only. Verify per the checklist in `CLAUDE.md` before committing
  (`node --check` + Playwright screenshots + numbers reconcile + no invented names).
- Positions are hand-placed for 1440×810 — re-screenshot after any layout edit.
- Commit footer + branch/push rules are in `CLAUDE.md` (Git section). Don't open a PR
  unless asked.
