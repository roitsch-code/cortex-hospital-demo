# Cortex Hospital Demo — Cyber Security Command Center (T Gallery)

Cinematische, interaktive Security-Operations-Demo in der visuellen Sprache von
**Cortex XSIAM 3.0**, adaptiert auf ein generisches großes Uniklinikum und mit
Deutsche-Telekom-**T-Security**-Branding gerahmt. Gebaut für die **T Gallery**
(Ausstellung der Deutschen Telekom). Eine einzige, in sich geschlossene `index.html` —
kein Build, keine Netzwerkaufrufe, **läuft offline**. Daten sind fiktiv, aber in sich
stimmig.

## Zuerst lesen
- **[`HANDOVER.md`](./HANDOVER.md)** — Übergabe/Onboarding auf **Deutsch**: was das ist,
  wie man es ansieht, welcher Branch gilt, Design-Regeln, Zahlenmodell, Repo-Zugang.
- **[`CLAUDE.md`](./CLAUDE.md)** — vollständige technische Design-Spezifikation
  (Englisch): Zahlenmodell, harte Design-Constraints, „Tuning Map".

## Was drin ist
Zwei Views (`showView('assets' | 'flow')`):
1. **Assets Command Center** (Einstieg, 16:9) — Radar nach Standort, iMedOne®-Anker,
   Buckets, Radar-Sweep.
2. **Issue-Cases Flow** (32:9) — Sources → Correlation Core → Cases → Live Queue, mit
   **24H ⇄ 30D**-Umschalter, vier 24H-Drill-down-Overlays und dem **Agent Resolution
   Center** (Agent-Drift-Szenario).

## Ansehen / starten
```bash
# 1) offline – am einfachsten:
open index.html            # Datei einfach doppelklicken

# 2) lokaler Server:
python3 -m http.server 8000    # -> http://localhost:8000
# oder
npm start                      # -> http://localhost:3000
```

## Aktueller Stand
Der vollständige, verifizierte Build liegt auf Branch
**`claude/cortex-demo-handover-0tpnha`** (identisch zum Entwicklungs-Branch
`claude/flow-layout-21-9-ivhesc`) — inkl. dieser Doku. Ältere `claude/*`-Branches sind
eine frühere Parallel-Linie; Details in [`HANDOVER.md`](./HANDOVER.md).
