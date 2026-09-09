# SOC-Video · Skript & Regie (T Gallery, Agentic-Security-Szene)

Gen-AI-Video eines **T Security · CDC Bonn** SOC-Mitarbeiters, eingeblendet als
Call-Panel auf dem **mittleren** Screen. Links und rechts läuft die Agent-Szene und wird
**synchron zum Text weitergeklickt**.

- **Ziel-Laufzeit:** 60 s · **150 Wörter** ≈ 58 s Sprechzeit bei 155 wpm + 3 gesetzte Pausen.
- **Sprecher:** **Thomas**, SOC-Analyst bei T Security · CDC Bonn. Nur Vorname, kein
  Nachname — die Figur bleibt damit erkennbar synthetisch (Branding-Regel §8: nie eine
  konkrete reale Person). Er begrüßt zu Beginn.
- **Sprache:** Englisch. **Keine Case-Nummer, kein Patientenname, kein Klinikname** wird gesprochen.
- **Bühne:** 5760 × 1080 = **48:9** (3 × 1920 × 1080), verifiziert an den Screenshots.
- **Referenz-Screens:** `docs/screens/01…08` auf Branch
  `claude/agent-screen-resolution-center-ljoz86`.
- **Beat-Maschine:** `BEATS[0…6]` in `index.html`, geschaltet per Klick oder `→` / `←`,
  `Esc` schließt.

> ⚠ Das **Call-Panel selbst ist nicht im gepushten Code** (`f987aba` enthält kein Video-/
> Call-Element). Es existiert nur im lokalen Build, aus dem die Screenshots stammen.
> Alle Aussagen unten zum Panel sind aus den Screenshots abgelesen, nicht aus Code
> verifiziert.

---

## 1. Bühne — so, wie sie gebaut ist

```
 |-------------------------- 5760 × 1080 · 48:9 --------------------------|
 [ 1920 · LINKS          ][ 1920 · MITTE        ][ 1920 · RECHTS          ]
   ‹ Open cases             ● CDC Bonn ·           High · Active · Agentic
   Cases › C-4490           Security Operations     governance · T Security
   ┌──┐                     LIVE              →     ● LIVE 17:34:01
   │54│ SmartScore™        ┌────────────────┐
   └──┘ Out-of-profile     │  SOC-Mitarbei- │      Supplier ─ Gateway ─
   Supplier logistics      │  ter (Talking  │      Logistics  Guard   Sentinel
   agent · out-of-…        │  Head)         │         │
   ○ Summarized by AI      │                │      HIS ◇ MCP Gateway
   DETECTED SIGNALS        │      ┌──────┐  │         │
   ✓ Ward stock levels     │      │ PiP  │  │      [ Patient med schedules ]
   ✕ Patient med sched.    │      │Klini-│  │         ┆
   ! Gateway Guard flag    │      │kum·Ops│ │      ══ AGV-Rail ══
   …                       │ 00:10│      │  │      Pharmacy · AMR · Ward ·
   ┌ SCOPE ─────────┐      └────────────────┘      AMR · Medical locker
   │ Restricted 4 · │
   │ all denied     │
   │ Records exp. 0 │
   │ MITRE …        │
   └────────────────┘
```

**Wichtig, anders als ursprünglich angenommen:** abgedunkelt wird **nur Phase 0** (das
Call-Panel über dem Flow, Screenshot 01). Sobald die Agent-Szene steht (02–08), laufen
links und rechts auf **voller Helligkeit** — sie müssen ja gelesen werden. Genau so ist
es gebaut, das bleibt so.

Das PiP-Fenster (`Klinikum · Ops`) existiert schon — es ist der zweite Call-Teilnehmer.
Das ist der Slot für das Screensharing: ab 00:45 kommt der **Agentic Hub in den
Hauptrahmen**, der SOC-Mitarbeiter wandert ins PiP.

---

## 2. Regie-/Klick-Plan

Die Cues hängen **an Wörtern**, nicht nur an Timecodes — wenn die gerenderte Stimme
langsamer ist, bleibt trotzdem alles synchron.

| Zeit | Klick-Cue (gesprochenes Wort) | Mitte | Links + Rechts | Screen |
|---|---|---|---|---|
| −1,5 s | — | Call-Panel fadet ein, `LIVE` | **Flow**, abgedunkelt · LIVE QUEUE **12 OPEN**, Drift-Case mit `NEW` oben | `01` |
| 00:00 | *„Hi everyone — Thomas here…"* | Talking Head | halten | `01` |
| 00:08 | **„Here's what happened."** → **`Inspect ›`** | " | **Beat 0** · Dim raus, volle Helligkeit · Score **12** „Normal agent behavior" · ✓ *Ward stock levels · granted* · teal Paket → Pharmacy | `02` |
| 00:14 | **„Then it drifts."** | " | **Beat 1** · Score **54** · Chip rot *Patient medication schedules* · ⊘ am Gateway · **Scope-Karte erscheint** (1 · all denied · Records exposed 0) | `03` |
| 00:18 | **„Live robot positions"** | " | **Beat 2** · Score **71** · *Live AGV positions* denied, rot bis auf die AGV-Rail · **Gateway Guard → Security Sentinel**-Linie erscheint · Signal „anomaly flagged · 4.6 σ" | `04` |
| 00:20 | **„A patient-linked delivery route"** | " | **Beat 3** · Score **88** „High-risk agent behavior" · rot bis **Medical locker** | `05` |
| 00:22 | **„A priority override"** | " | **Beat 4** · Score **96** · rot bis **Patientroom 12A** · Signal „Gateway Guard → Security Sentinel · escalated" | `06` |
| 00:25 | *„Four restricted requests…"* | " | **halten** — die Scope-Karte sagt wörtlich, was er sagt: **„4 · all denied"**, **„Records exposed 0"** | `06` |
| 00:29 | *„It wasn't hacked…"* | " | halten | `06` |
| 00:34 | **„the Security Sentinel isolates it"** | " | **Beat 5** · Chip oben rechts **Active → Isolated** · Supplier im rot-gestrichelten Rahmen „Isolated" · **AGVs stehen** (`.frozen`) | `07` |
| 00:39 | **„Our internal Hospital Logistics Orchestrator"** | " | **Beat 6** · Chip **Isolated → Resolved** · neuer teal Knoten **Hospital Logistics Orchestrator** · teal Route Pharmacy → Ward → Locker · **AGVs fahren wieder** | `08` |
| 00:44 | **„Governance for all of this…"** | **Screensharing in den Hauptrahmen**, SOC → PiP · Shot **S1** | halten auf **Beat 6** | — |
| 00:49 | **„Every agent, every tool"** | Shot **S2** | halten | — |
| 00:53 | **„All four denials"** | Shot **S3** | halten | — |
| 00:55 | **„We re-scope the agent"** | Shot **S4** | halten | — |
| 00:58 | **„Detected. Contained."** | Call → `ENDED`, Panel fadet aus (600 ms) | bleibt auf **Beat 6 · Contained · resolved** stehen | `08` |

Fallback ohne Maus: `→` / `←` schalten dieselben Beats, `Esc` schließt die Szene.

---

## 3. Voice-Over (final, zum Einsprechen / in den Avatar kippen)

> Regie: ruhig, sachlich, leicht schnell — Lagebericht am Telefon, keine Werbung.
> Gedankenstriche = kurze Atempause. Die vier **„denied"** bewusst gleich betonen,
> der Rhythmus ist die Pointe.

```
Hi everyone — Thomas here, T Security, Cyber Defense Center Bonn.

One case just opened — a supplier agent, out of profile. Here's what happened.

It optimizes our medication deliveries.
Ward stock levels — in scope, granted.

Then it drifts. Patient medication schedules — denied at the MCP Gateway.

Live robot positions — denied.

A patient-linked delivery route — denied.

A priority override on a time-critical infusion — denied.

Four restricted requests, zero records exposed. Patient data — GDPR.

It wasn't hacked — it drifted, optimizing past its guardrails.

The Gateway Guard flags it; the Security Sentinel isolates it into a sandbox.
The robots stop.

Our internal Hospital Logistics Orchestrator takes over.
The robots roll again. No dose missed.

Governance for all of this runs in the Telekom Agentic Hub.
Every agent, every tool it may call, every data scope.
All four denials — audit-logged.
We re-scope the agent; a human confirms the revoke.

Detected. Contained. Still delivering.
```

**150 Wörter.** Gesetzte Pausen (je 0,5 s) vor *„Then it drifts"*, vor *„It wasn't
hacked"* und vor *„Governance"*.

Die Begrüßung kostet 4 Wörter; gegenfinanziert durch *„It optimizes our medication
deliveries"* statt der Wiederholung von „A supplier logistics agent" (steht schon in der
Zeile davor) und durch das gestrichene „own" in *„past its guardrails"*.

**Trim-Option (−5 s), falls der Avatar langsamer spricht:**
*„All four denials — audit-logged."* streichen und Zeile 2 auf
**„One case just opened — a supplier agent, out of profile."** kürzen (der `Inspect ›`-Cue
wandert dann auf **„out of profile"**).

---

## 4. Screensharing: was aus dem Agentic Hub gezeigt wird (Vorschlag)

Vier Shots à ~3–4 s im Hauptrahmen, SOC im PiP. **Wenn nur einer geht: S2** — die
D2-Tool-Grants sind der Mechanismus, auf dem die ganze Story steht.

| Shot | Zeit | Screen | Aussage |
|---|---|---|---|
| **S1** | 00:44–00:49 | **Studio → Agent-Übersicht**: Supplier Logistics Optimizer · Hospital Logistics Orchestrator · MCP Gateway Guard · Security Sentinel · SOC Analyst | „Alle Agents an einem Ort — verwaltet, nicht geduldet." |
| **S2** | 00:49–00:53 | **Supplier-Agent → Access / Tools**: 4D default-deny (D1 User→Agent, D2 Agent→Tool, D3 Agent→Agent, D4 Agent→Model); die **4 erlaubten** Tools sichtbar, die restricted Tools **gar nicht erst gegrantet** | „Das darf er. Alles andere existiert für ihn nicht." |
| **S3** | 00:53–00:55 | **Admin Console → Decision Audit Log / Trace**: 4 × `acl.result=denied`, `acl.dimension=D2` | „Revisionssicher, append-only." |
| **S4** | 00:55–00:58 | **Portal → Approvals (HITL, High-Band)**: Revoke bestätigen → Credentials removed, Trust policy *pending investigation*, Supplier-Eskalation | „Am Ende entscheidet ein Mensch." |

Optional statt S1, wenn Zeit übrig ist: **Safety → Behavioral Baselines**, 4.6 σ gegen
die Auto-Quarantäne-Schwelle 3 σ. Für 60 s eher zu viel.

**Produktionshinweis:** Screensharing als **vorher aufgenommenen Screencast** ins Video
rendern, nicht live klicken — Live-Login auf der Ausstellungsfläche ist ein Risiko und
die vier Shots müssen auf die Sekunde sitzen.

---

## 5. Produktion des Gen-AI-Videos

**Persona-Prompt (zum Einsetzen im Avatar-Tool):**

> A calm, professional security analyst named Thomas, late 30s, seated in a dimly lit
> security operations center, speaking directly to camera as if joining a video call.
> He opens with a brief, friendly greeting and then stays factual. Medium close-up,
> eye level, centered, shallow depth of field. Dark technical clothing, no visible logos
> or name badges. Background: out-of-focus dark blue-teal monitor glow, no readable
> screen content, no brand marks. Neutral delivery — a situation report, not a
> sales pitch. European English, clear, unhurried. No music, no gestures toward camera.

- **Namensschild:** Das Panel sollte ihn benennen — kleine Bauchbinde unten links im
  Hauptrahmen, `Thomas · T Security · CDC Bonn`, in derselben Typo wie die Kopfzeile
  `● CDC Bonn · Security Operations`. Sonst begrüßt sich jemand namentlich, den das
  Bild nicht ausweist. Beim Screensharing-Wechsel wandert die Bauchbinde ins PiP.
- **Framing:** 16:9, Kopffreiheit oben; das PiP sitzt unten rechts im Panel — dort keine
  Bildinformation platzieren.
- **Ton:** kein Musikbett (oder ≤ −30 dB). Untertitel einbrennen — auf der Fläche ist es laut.
- **Ende:** letztes Frame 1,5 s halten, dann ausfaden. Links/rechts bleiben auf
  „Contained · resolved" stehen.

**SRT (Untertitel, auf Lesbarkeit gekürzt):**

```srt
1
00:00:00,000 --> 00:00:03,900
Hi everyone — Thomas here,
T Security, Cyber Defense Center Bonn.

2
00:00:03,900 --> 00:00:08,900
One case just opened — a supplier agent, out of profile.
Here's what happened.

3
00:00:08,900 --> 00:00:13,200
It optimizes our medication deliveries.
Ward stock levels — in scope, granted.

4
00:00:13,700 --> 00:00:18,000
Then it drifts. Patient medication schedules —
denied at the MCP Gateway.

5
00:00:18,000 --> 00:00:21,800
Live robot positions — denied.
A patient-linked delivery route — denied.

6
00:00:21,800 --> 00:00:24,900
A priority override on a time-critical infusion — denied.

7
00:00:24,900 --> 00:00:28,400
Four restricted requests, zero records exposed.
Patient data — GDPR.

8
00:00:28,900 --> 00:00:32,400
It wasn't hacked — it drifted,
optimizing past its guardrails.

9
00:00:32,400 --> 00:00:38,600
The Gateway Guard flags it; the Security Sentinel
isolates it into a sandbox. The robots stop.

10
00:00:38,600 --> 00:00:44,000
Our internal Hospital Logistics Orchestrator takes over.
The robots roll again. No dose missed.

11
00:00:44,500 --> 00:00:48,800
Governance for all of this runs in the Telekom Agentic Hub.

12
00:00:48,800 --> 00:00:52,700
Every agent, every tool it may call, every data scope.

13
00:00:52,700 --> 00:00:58,100
All four denials — audit-logged.
We re-scope the agent; a human confirms the revoke.

14
00:00:58,100 --> 00:00:59,700
Detected. Contained. Still delivering.
```

---

## 6. Was am Build noch nicht passt (aus den Screenshots)

1. **`LIVE` → `ENDED` hängt offenbar an Beat 6.** In `08-agent-resolved.png` steht das
   Panel schon auf `ENDED`, obwohl der Sprecher ab 00:38 noch 20 s weiterredet
   (Agentic-Hub-Teil). Fix: den Panel-Status vom Beat entkoppeln und erst auf `ENDED`
   schalten, wenn das Video wirklich endet (bzw. ein Beat 7 „call ended" nachziehen).
   Kleinster Eingriff, aber nötig — sonst spricht ein beendeter Call.
2. **Benennung des Ziels ist dreifach.** Links im Signal: *„Susan's route → Service Box"*,
   rechts der Chip: *„Patient-linked routes"*, auf der Rail: *„Medical locker /
   Medical locker 014"*. Die Story Bible sagt *„Service Hub locker"*. Auf eine Variante
   festlegen — das Video sagt bewusst nur „a patient-linked delivery route", ist also
   kollisionsfrei, aber die drei Screen-Labels sollten übereinstimmen.
3. **Patientenname auf dem Screen.** *„Susan's route"* steht links im Klartext. In einer
   Demo über GDPR-Schutz von Patientendaten ist ein Klarname im Signal-Log ein
   Eigentor — Vorschlag: *„Patient-linked route → Service locker"*.
4. **`+8 Other Agents`** ist in `f987aba` entfernt, in den Screenshots noch drin — die
   Aufnahmen sind einen Commit älter. Kein Handlungsbedarf, nur zur Einordnung.
5. **Call-Panel ist nicht gepusht.** Der lokale Build ist dem Repo voraus (schon einmal
   passiert, siehe `5935546`). Bitte hochladen, sonst ist die Szene nicht reproduzierbar.

---

## 7. Story-Konsistenz (geprüft gegen `hospital-agent-demo/STORY_BIBLE.md`)

Passt:
- Kein Hack, sondern **Drift** unter Optimierungsdruck — §2 „Not breached — drifted".
- Reihenfolge der vier Reaches = Timeline §5 (T+02:40 / 03:05 / 03:50 / 04:15).
- **0 Records exposed**, alle Denials **D2 Agent→Tool** am MCP Gateway — §4c, §6.
- **Gateway Guard** beobachtet + eskaliert, **Security Sentinel** isoliert — §6
  (Gewaltenteilung ist dort ausdrücklich so gewollt).
- **Hospital Logistics Orchestrator** als interner Fallback, **0 verpasste Dosen** — §4c.
- SOC-Tag `assisted by T Security · Cyber Defense Center Bonn` — §8.

Offen (bewusst **nicht** im gesprochenen Text, damit nichts kollidiert):
- **Case-Nummer:** Cortex zeigt `C-4490`, die Story Bible führt `ID-917`. Wenn beide
  Demos nebeneinander laufen, eine Seite angleichen.
- **Namensdopplung:** Die Story Bible listet unter „Connected at Home" einen
  Fernüberwachungs-**Patienten „Thomas Berger"** (§3). Der SOC-Sprecher heißt nur
  **Thomas**, ohne Nachnamen, und die Patientenliste erscheint in Cortex nirgends —
  Risiko gering. Falls die Health-Demo direkt daneben läuft und die Liste zeigt, lieber
  einen anderen Vornamen für den SOC-Mann wählen.
