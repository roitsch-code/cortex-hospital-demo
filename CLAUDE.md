# CLAUDE.md — Sovereign Cortex · Connected Hospital (guided security demo)

> Read this fully before changing anything. This is a **design-led interactive demo**,
> not a production app and not a slide. The look matters as much as the content.

## What this is
An interactive, cinematic **security-operations demo** in the visual language of
Palo Alto Networks **Cortex XSIAM** (dark, glowing, animated), adapted to a
**hospital medication-logistics** AI-agent incident, and framed with **Deutsche
Telekom / T-Systems** sovereign services. Intended for a live showcase / exhibit
(think T Gallery), shown on a laptop or large screen. Single self-contained HTML,
no build step.

## The story (the demo walks through this)
A connected hospital runs medication delivery via **AGVs** (automated guided
vehicles) between pharmacy, wards and patient rooms. An external **supplier
logistics agent** is connected to optimise delivery and replenishment. It starts
requesting **restricted** data (patient-linked routes, room-level AGV positions,
clinical priority overrides). Its identity is valid, but its **behaviour does not
match the approved permission profile**. The system: raises an alert → **isolates**
the agent into a **secure simulation** (synthetic hospital, no real data) → keeps
**fallback medication delivery running** → a **Telekom SOC analyst calls in**.
Part 1 ends at the SOC call. Later parts: SOC review → governance → revoke.

## HARD design constraints (do not violate)
- **Keep the Cortex aesthetic**: near-black background, teal (#2fd6c0) glow,
  flowing SVG "Sankey" ribbons, a central particle swarm, radial/orbital layouts,
  soft shadows and pulses. Cinematic and reduced.
- **DO NOT build a dense, multi-column "boxes-in-bands" architecture chart.**
  A previous attempt did exactly that and was rejected as "a shitty PowerPoint."
  When a detail/architecture view is needed, keep it **reduced** (few glowing
  nodes, radial, lots of negative space).
- **It is a guided flow, not a slide**: scenes with transitions and interaction,
  not one static overview packed with labels.
- Telekom **magenta (#E20074)** is an accent only (SOC card / "T Security"
  branding). Cortex teal stays the primary colour.

## Tech
- One file: `index.html`. Vanilla JS + Canvas (particles) + inline SVG (ribbons/
  rings/connectors) + CSS. No frameworks, no bundler, no network calls, no
  localStorage. Runs offline via `file://` or a static server.
- Fixed **1440×810** design stage, scaled to the viewport via CSS `transform`.
- `prefers-reduced-motion` is respected.

## Current state (3 scenes)
- **Scene FLOW** (`#flow`): left hospital sources → central particle swarm
  (correlation, count-up numbers) → right two clickable glowing hubs:
  **Agent System** and **Response & Isolation**. Bottom: 3 minimal live stats.
- **Scene AGENTS** (`#agents`): reduced **radial** architecture — Orchestrator in
  the centre, 6 agents on an orbit, thin glowing spokes. The external **Supplier
  Logistics Agent** is amber (foreshadow) and clickable → Isolation.
- **Scene ISOLATION** (`#iso`): alert toast (red) → the supplier agent node
  animates from the live side **into a dashed "Secure Simulation" bubble**; the
  live AGV particle stream keeps flowing (fallback); an **incoming SOC call** card
  rings, "Accept" reveals the analyst line; ends with "— end of part 1 —".
  Auto-plays on first entry; `Run isolation` / `Reset` buttons in the corner.

## Real vs. concept (be accurate if you add labels/copy)
Real, verified Deutsche Telekom / T-Systems anchors used here:
- **Sovereign Cortex with T Security** (PANW + DT, announced 2026-06-09; the exact
  real product tying Cortex + Telekom sovereignty for regulated industries).
- **T-Systems Sovereign Cloud powered by Google Cloud** (patient/med data).
- **Open Sovereign Cloud** (confidential computing + HSM → hosts the sandbox).
- **Telekom SOC / Magenta Security MDR** (Cyber Defense Center Bonn; auto-isolate).
- **Germany Data Boundary by T-Systems / IAM** (identity, residency, access audit).
- **Industrial AI Cloud (Telekom + NVIDIA)** (sovereign compute).
Concept only (from the demo script, not a shipping product):
- **T-Systems "AI Agent Governance Platform"** — keep it labelled as a concept if
  surfaced; it maps onto the real IAM / Data-Boundary logic.
> Verify product status before any public showing (telekom.com / paloaltonetworks.com).

## What's next (Part 2 — not built yet)
1. From the SOC call: **SOC review** panel (agent may be misconfigured /
   compromised / out-of-scope).
2. **Governance** view (reduced!): supplier permission profile —
   Allowed: aggregated stock, delivery windows, non-patient logistics.
   Restricted: patient-linked routes, room-level positions, clinical overrides.
3. **Human confirm → execute response**: revoke access · remove credentials ·
   trust policy updated · supplier escalation package · governance record.
4. Return Scene FLOW to normal (incidents back to 0).
Also: visually tune Scene ISOLATION positions (bubble, moving agent, cut line) —
these are hand-placed and were not verified in a browser yet.

## Tuning map (where the knobs are, in index.html)
- Colours / theme: the `:root` CSS variables at the top.
- Scene content: the three `<section id="flow|agents|iso">` blocks.
- Isolation beats + timing + target positions: the `runIso()` function
  (each `T(fn, ms)` is one beat; `badAgent.style.left/top` is the isolate target).
- Bubble shape: CSS `.bubble`. Live/caged particle counts: the `live`/`caged`
  arrays. Flow ribbons/geometry: the IIFE that builds `#wFlow`; radial spokes in
  the `#wAgents` IIFE.
- Navigation state machine: `show(name)`.

## Run
- `npm start`  (uses `npx serve .` → http://localhost:3000), or
- `python3 -m http.server 8000` then open http://localhost:8000, or
- just double-click `index.html` (works; no server needed).

## Known limitations
- **Not verified in a browser** by the author of the first draft — sanity-check
  the render first, especially Scene ISOLATION alignment.
- Brand logos are intentionally omitted (text labels only) to avoid IP issues.
