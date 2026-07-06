# Sovereign Cortex — Connected Hospital (guided security demo)

Interactive Cortex-style security demo for a hospital medication-logistics
AI-agent incident, framed with Deutsche Telekom / T-Systems sovereign services.
Single self-contained HTML, no build step.

See **CLAUDE.md** for full context, design constraints, current state and roadmap.

## Files
- `index.html` — the guided flow (3 scenes: flow → agents → isolation).
- `reference/command-center-cortex.html` — the original Cortex command-center
  aesthetic (turn-1 reference for the look; hospital data not applied here).

## Run
Any of these:
```bash
npm start                     # -> http://localhost:3000  (uses npx serve)
# or
python3 -m http.server 8000   # -> http://localhost:8000
# or just double-click index.html
```

## Continue in Claude Code — paste this as your first message
```
Read CLAUDE.md first, then start a static server (npm start) and open the demo.
Do NOT redesign it as a dense chart — keep the Cortex aesthetic and the guided-
flow structure (see the HARD design constraints in CLAUDE.md).

First task: sanity-check the render of Scene ISOLATION (#iso) and fix the hand-
placed positions of the bubble, the moving supplier-agent node, and the cut line
so the "isolate into secure simulation" beat reads cleanly. Then let's plan
Part 2 (SOC review → governance → revoke) as new reduced scenes.
```
