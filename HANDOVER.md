# Handover — Cyber Security Command Center (T Gallery hospital demo)

_Last updated: 2026-07-07 · branch `claude/cortex-xsiam-research-drgysn`_

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

## What changed most recently
- **Adapted the issue-cases flow to the hospital Command Center.** Sources are now
  hospital systems with clinical icons; iMedOne · HIS and T Cloud Public render in
  magenta with the **real Telekom "T"**. Added a subtle magenta particle strand +
  second magenta sonar pulse into the core.
- **Reconciled all flow numbers** to the asset model (24H: 2,412 → 96 → 78/18 → 85/11;
  30D: 148K → 34K → 312, Active 168, Resolved 144; Vulnerable Assets tile = 5,840).
- **Updated every flow detail popover** (`detailHTML` `D` object) + the MTTR mini-legend
  to match those numbers.
- **Fixed two consistency bugs:** widened source rows so "Medical Devices · 18.6K" no
  longer clips; set the Assets "Data Ingestion" tile to **9 TB/24H** (was a stale
  65 TB) so it matches the flow; refreshed the static asset sub-caption placeholder.

## Verified
`node --check` on the extracted script (OK) + Playwright screenshots at 1440×810 ×2:
assets view, 24H flow, 30D flow, cases/manual popovers, and the source-label fix.
All render correctly, numbers reconcile, no invented product names, no JS errors.

## Open items / next steps
- **Logos:** the only real logo asset in the repo is `docs/tsec-logo-white.svg`. The
  user has said source/vendor logos are "in the folder," but none besides that have ever
  actually been present. Current build uses clean line icons + the recreated iMedOne
  wordmark + the real Telekom "T". If real vendor SVGs get added, wire them into the
  source list (`iconSVG`) and site marks (`PMARK`).
- **Possible Part 2** (not requested/built): SOC review → governance (supplier
  permission profile) → human-confirmed response. Keep any such view reduced, real
  names only.
- Re-verify Telekom/PANW product statuses before any public showing.

## How to work on it
- Edit `index.html` only. Verify per the checklist in `CLAUDE.md` before committing.
- Commit footer + branch/push rules are in `CLAUDE.md` (Git section). Don't open a PR
  unless asked.
