# Handover — Cyber Security Command Center (T Gallery hospital demo)

_Last updated: 2026-07-07 · branch `claude/issues-cases-flow-refine-hlxipr`_

## Where things stand
The demo is a single self-contained `index.html` with **two working views**, both
tuned for a generic ~1,300-bed university hospital and branded with T Security. It runs
offline (double-click) or via `python3 -m http.server 8000`. **No JS errors**;
`prefers-reduced-motion` respected. See `CLAUDE.md` for the full design brief, the
number model, and the tuning map.

1. **Assets Command Center** (entry) — centered radar organised **by site**
   (Main Campus dominant + 5 satellites), iMedOne® left anchor, magenta radar sweep,
   4 nested buckets, per-site drill-in. `Show Issues ›` → flow.
2. **Issue-Cases Flow** — sources → correlation core → cases → outcome funnel, with a
   **24H ⇄ 30D** toggle and clickable detail popovers + a Prioritization overlay.
   In 24H the three spine anchors now open **full drill-down overlays** (below).

## What changed most recently (flow-refine session)
- **24H funnel polish:** lifted "78 Automated" clear of the disc/stream, pushed
  "18 Manual" off its circle.
- **Renamed the SOC tag** to **"assisted by T Security · Cyber Defense Center Bonn"**
  (magenta glow) + a new magenta connector Manual → SOC; matched the `manual` popover.
  Naming was researched — see CLAUDE.md "Real vs. concept" (T Security = the sovereign
  SOC arm; Magenta Security is the consumer MDR brand, kept off-screen).
- **Three new reduced drill-down overlays** (24H, `.dv` pattern, each with `‹ Flow`
  back + Esc):
  - **Issues → Data Inventory:** grouped sources (Clinical & Medical / Network & Identity
    / Sovereign Cloud / Third-party) with volume + sparkline, ribbons into Issues +
    Prevented Events. T Cloud Public + iMedOne stay magenta/sovereign **above** the
    third-party sources.
  - **Core → Dynamic View:** radial automation donut (81% = 78/96), sources as orbital
    marks, scattered severity flags, live SOC feed. (30D core still = Prioritization.)
  - **Cases → Cases Overview:** lifecycle funnel + case-handling bars + Automation
    Headroom + MITRE ATT&CK "cases by tactic" (sums to 96). (30D cases still = popover.)
- **Inlined 4 vendor logos** (Microsoft 365, Azure, Google Cloud, GitHub·Research) as
  mono-tinted webp data-URIs in `LOGO`; used ONLY in Data Inventory + Dynamic View as
  subordinate third-party sources. **T Cloud Public is never replaced by a hyperscaler.**

## Verified
`node --check` clean + Playwright screenshots at 1440×810 ×2 of: 24H flow, Data
Inventory, Dynamic View, Cases Overview, plus a full click-through sweep (assets → flow →
each overlay open/close → 24H⇄30D → 30D Prioritization via the centre label). Numbers
reconcile everywhere; **no JS errors**; real names only.

## Open items / next steps
- **Logos on disk:** `docs/` now holds the provided assets — 4 used (M365/Azure/GCP/
  GitHub, inlined), plus `Aws_logo.svg.webp` (**unused** — AWS judged a weak fit for a
  sovereign German hospital), `imedone.png` + `imgt2.jpeg`/`T_logo_rgb_p.svg` (real
  iMedOne wordmark + coloured Telekom "T"; the demo currently uses the CSS wordmark +
  white vector "T"). Swap in if desired.
- webp is raster — logos are inlined as-is (mono-tinted), not traced to vector. Drop real
  `.svg` versions into `docs/` and re-point `LOGO` for vector-perfect marks.
- **Possible Part 2** (not built): SOC review → governance → human-confirmed response.
  Keep reduced, real names only.
- Re-verify Telekom/PANW product statuses before any public showing.

## How to work on it
- Edit `index.html` only. Verify per the checklist in `CLAUDE.md` before committing.
- Commit footer + branch/push rules are in `CLAUDE.md` (Git section). Don't open a PR
  unless asked.
