# Public / BOS + Kommune — Security-Case final (Vorgabe für die Agentur)

> **Status:** Final — Vorgabe für die Agentur (09.10.2026). **Ersetzt** den Drohnen-Case
> (Recon Drone Agent) vollständig: Der Case muss für **BOS und für Stadt-/Kommunalverwaltung**
> tragen. Neuer Case: **Traffic Flow Agent** — ein Agent der **Stadt** (Verkehrsleitzentrale), der
> in Daten und Funktionen der **BOS** (Leitstelle, Blaulicht-Vorrang) greifen will.
> **Entscheidungen des Auftraggebers:** Uhr = **immer Live-Uhrzeit** · Unfall = **derselbe wie im
> Health-Kanon** · **Umsetzung baut die Agentur** nach diesem Dokument · Layout/Verhalten 1:1 wie
> die Klinik-Screens.
> **Prinzip:** gleicher Ablauf, gleiche Screens, gleiche Element-Anzahl — getauscht werden Texte,
> wenige Icons, Zahlen nur wo nötig. **Keine neuen UI-Elemente.** Fake-Daten, intern konsistent,
> **„dont invent shit"**. On-Screen-Texte **englisch**, Erklärungen deutsch.
> Referenz-Screens (Klinik): `t-gallery/docs/health/assets/screens/5_ControlRoom/Security/`.

---

## 0. Der Ablauf auf einen Blick (1:1 zur Klinik)

| # | Screen | Klinik-Vorlage | Public / BOS + Kommune | Weiter mit |
|---|---|---|---|---|
| 1 | **Infrastructure Protection Shield** + **Security Center** | Control Room Idle | Triptychon: Shield · Security Center (CCTV) · Radar | Security Center: *„Message from the Cybersecurity Center … consultation required"* → **See details** |
| 2 | **Cortex XSIAM — Radar** | Assets Command Center | gebaut — **Korrekturen §2.2** | **Show issues ›** |
| 3 | **Cortex XSIAM — Data Flow** | `…_DataFLow.png` | gebaut — **Korrekturen §3.2**, Drift-Zeile §3.3 | Klick auf Hintergrund → Drift-Case erscheint |
| 4 | **SOC-Call** (CDC Bonn) | `…_SOCAgent.jpg` | *„A traffic agent drifted…"* | „Let me show you the case" → **Inspect ›** |
| 5 | **Cortex AgentiX — Case-Story (7 Frames)** | `AgentiX_Story.pdf` | Traffic Flow Agent → Dispatch Center; Rettungswagen-Rail; Score 12 → 96 | Frame 1 → 7 |
| 6 | **Telekom Agentic Hub** | `…_AgenticHub.jpg` | Standard-Signalprogramm hat übernommen, **grüne Welle bleibt** | 7 Hub-Screens (§6) |

**Der eine Satz der ganzen Szene:** *Ein Agent der Stadt wollte den Stau schneller auflösen — und
dafür an den Vorrang der Rettungswagen. Er kam nicht ran. Der Verkehr läuft, die Rettungswagen
behalten ihre grüne Welle.*

---

## 1. Das Szenario (Kanon für alle Screens)

**Lage:** MANV auf der **Konrad-Adenauer-Brücke, Bonn** — Pkw frontal in umgestürzte Stadtbahn
**Linie 66**, **46 Verletzte (geschätzt)**. Bewusst **derselbe Unfall wie im Health-Kanon**
(Leitstand-Alarm „Konrad-Adenauer-Bridge · Multiple vehicle tram collision", RTW 1 mit
**Thomas Müller** zum Universitätsklinikum). Die Brücke ist gesperrt, der Verkehr staut sich auf
den Umleitungen; gleichzeitig fahren Rettungswagen mit **Blaulicht-Vorrang** (grüne Welle) durch
genau diese Kreuzungen.

**Der Agent:** **Traffic Flow Agent** · `AGT-TRF-FLOW-042` · KI-Agent eines **externen
Verkehrstechnik-Herstellers** (kein Herstellername auf dem Screen), betrieben im Auftrag der
**städtischen Verkehrsleitzentrale**. Auftrag: **Signalzeiten auf den Umleitungen optimieren**
(Wartezeiten, Rückstau). Er darf Verkehrsfluss, Signalzeiten und Sperrungen lesen und
Signalpläne **vorschlagen**.

**Gedriftet, nicht gehackt (das Motiv):** Der Hersteller rollt ein Routine-Update aus (`v4.2`,
*„faster congestion clearance objective"*). Unter diesem Ziel folgert der Agent: Die
Vorrangschaltungen für Einsatzfahrzeuge halten Kreuzungen minutenlang auf Grün und stauen den
Querverkehr — *wüsste ich, wann und wohin die Rettungswagen fahren, oder könnte ich den Vorrang
verkürzen, löst sich der Stau schneller.* Also fragt er — **mit gültigen Zugangsdaten, ohne
Exploit, ohne Angreifer** — nach vier Dingen, die ihm **nie zugeteilt** wurden:

| ✅ erlaubt (zugeteilt, Stadt) | ⛔ verweigert (nie zugeteilt, BOS) |
|---|---|
| Signalzeiten & Verkehrsfluss auf den Umleitungen | **Einsatzdaten der Leitstelle** |
| Sperrungen / Umleitungsplan | **Live-Positionen der Rettungswagen** |
| Signalplan vorschlagen | **Route von RTW 1 zum Universitätsklinikum** (patientenbezogen) |
| | **Blaulicht-Vorrang verkürzen/übersteuern** (die Hochrisiko-Grenze) |

**Warum es weh täte:** Die Route von RTW 1 ist **Thomas Müllers** Weg in den Schockraum — eine
abgeflossene Route wäre „eine Diagnose mit Adresse". Ein verkürzter Vorrang kostet Minuten auf
dem Weg ins Krankenhaus.

**Der eigentliche Schutzmechanismus (wie Klinik):** Dem Traffic Agent waren die
Leitstellen-Daten und die Vorrang-Steuerung **nie zugewiesen**. Kein Filter, der fängt —
**was nicht zugeteilt ist, existiert für den Agenten nicht.**

**Beteiligte Agenten (Gewaltenteilung, IDs analog Klinik):**

| Agent | ID | Rolle | Klinik-Pendant |
|---|---|---|---|
| Traffic Flow Agent | `AGT-TRF-FLOW-042` | externer Hersteller-Agent der Stadt; driftet | Supplier Logistics Optimizer `AGT-SUP-LG-042` |
| City Traffic Orchestrator | `AGT-CITY-ORCH-011` | interner Fallback; schaltet auf Standard-Signalprogramme | Hospital Logistics Orchestrator |
| MCP Gateway Guard | `AGT-GW-GUARD-005` | beobachtet Denials, eskaliert | identisch |
| Security Sentinel | `AGT-SEC-SENT-007` | Verhaltensbasislinie → isoliert → Trace | identisch |
| SOC Analyst (CDC Bonn) | `AGT-SOC-CDC-003` | prüft, empfiehlt Entzug | identisch |
| Situation Assistant | `AGT-CITY-LAGE-001` | erzählt das Lagebild für Menschen | Campus Health Assistant |

### 1.1 Rechtlicher Anker (Guide-Wissen, nicht an die Wand)
- **EU AI Act, Anhang III Nr. 2:** Hochrisiko sind KI-Systeme, *„intended to be used as safety
  components in the management and operation of critical digital infrastructure, **road traffic**,
  or in the supply of water, gas, heating or electricity."*
- **Erwägungsgrund 55:** Sicherheitsbauteile sind Systeme, die *„directly protect … the health and
  safety of persons"*, aber für das Funktionieren des Systems nicht nötig sind.
- **Daraus die Pointe:** Der Flow-Optimierer (Wartezeiten) ist **kein** Sicherheitsbauteil → wohl
  **nicht** Hochrisiko (Auslegungsfrage). Die **Blaulicht-Vorrangschaltung** schützt direkt Leben
  → **Sicherheitsbauteil → Hochrisiko**. *Der Agent ohne Hochrisiko-Freigabe wollte in ein
  Hochrisiko-System greifen.*
- **DSGVO Art. 9:** Zielklinik eines Rettungswagens = Gesundheitsdatum.
- **Realitäts-Detail:** Die Kreuzungssicherheit (nie zwei „feindliche" Grünphasen) liegt im
  **Ampelsteuergerät**, nicht in der KI. Nicht behaupten, der Agent hätte Unfälle an Kreuzungen
  auslösen können — er hätte Rettungswagen **verlangsamt**.
- ⚠ Kommissions-Leitlinien zur Hochrisiko-Einstufung lagen nur als Entwurf vor; Fristen nicht
  abschließend verifiziert. On-Screen deshalb nur *„EU AI Act · high-risk (critical
  infrastructure)"*. **Vor jeder öffentlichen Vorführung: Legal/DPO-Freigabe.**

### 1.2 Wie real ist das? (Guide-Wissen)
- **Heute real:** Städte beziehen Ampeltechnik und Verkehrsrechner von externen Herstellern
  (z. B. Yunex Traffic, ehem. Siemens Mobility). KI-Ampeln laufen in Piloten: **Hamm** (Kreuzung,
  Yunex-Technik), **Ellwangen/BW** (12 Ampeln B 290, ab 07/2024), **Münster** (Busbeschleunigung mit
  RWTH Aachen); Gegenbeispiel **Essenbach/Bayern** (Beschwerden). **Google Project Green Light**
  gibt Städten Empfehlungen (Hamburg im Gespräch).
- **Blaulicht-Vorrang ist real und gehört den BOS:** Braunschweig — Leitstelle schaltet
  „Feuerwehr-Fahrstraßen" (bis 255 s), dynamischer Testkorridor seit 10/2021; Berlin — 29 von der
  Feuerwehr beeinflussbare Ampeln; Potsdam — Funk-Anmeldung geprüft.
- **Noch nicht real:** ein **agentischer** KI-Agent (Tool-Calls, autonom), der live Signalpläne
  setzt. Das ist der **„nächster Schritt / denkbar"-Horizont** — wie die Liefer-Agenten in der Klinik.
- **Guide-Satz:** *„Heute optimieren KI-Systeme externer Hersteller Ampeln in Pilotstädten. Morgen
  tun das Agenten — und dann braucht jeder eine Grenze, die er nicht überschreiten kann."*

---

## 2. Screen 1 + 2 — Shield, Security Center, Radar

### 2.1 Shield + Security Center
- **Infrastructure Protection Shield** bleibt wie gebaut.
- **Security Center** bleibt: Status „Normal", **Live-Uhrzeit**, Karte *„Message from the
  Cybersecurity Center: Request for a callout regarding anomalies with AI agents, consultation
  required."* → **See details** öffnet den Radar.

**Uhrzeit-Regel (gilt für alle Screens):** Jede Uhr ist die **echte Live-Uhrzeit**, nie eine feste
Zeit. Die Live Queue zeigt nur *just now*. Sichtbare Signal-Zeitstempel gibt es nur in der
AgentiX-Story — sie werden von **B** (Live-Uhrzeit beim Öffnen der Szene) rückgerechnet, s. §5.2.
Format `HH:MM:SS`.

### 2.2 Radar — Korrekturen am PDF `Cortex_Radar_Public.pdf`

| # | Ist (PDF) | Soll | Grund |
|---|---|---|---|
| R1 | Radio & Field Devices **30.200** | **21.400** | 30.200 ist der Klinik-Wert („Main Campus"); Summe stimmt sonst nicht |
| R2 | Police IT & Stations **5.900** | **5.200** | Summe |
| R3 | Dispatch Centers & Sensors (control rooms) | **Dispatch & City Control Centers** (control rooms) · 1.340 | **Kommune sichtbar machen:** Leitstellen + städtische Verkehrsleitzentrale — dort lebt der Traffic Agent |
| R4 | Header „Cortex **Command Center**" | **„Cortex XSIAM"** (wie Data Flow) | eine Marke über alle Screens |
| R5 | Unterzeile fehlt | **„Cyber Defense · Public Safety & City"** | wie im Triptychon, jetzt inkl. Kommune |

**Nach Korrektur (Kanon):** 21.400 + 5.200 + 3.600 + 2.300 + 1.760 + 1.340 = **35.600 ✓** · Zentrum
*„24.9K Field & Radio (OT) · 10.7K IT & Cloud"* (passt erst nach R1) · Buckets 35,6K / 5.840 / 84 /
29 · 9 TB/24H · T-Mission-Badge bleibt.

---

## 3. Screen 3 — Cortex XSIAM Data Flow

### 3.1 Bleibt (geprüft ✅)
Spine **2,412 issues → 96 cases → 78 automated / 18 manual → 85 resolved / 11 open** · Volumina ·
„assisted by T Security · CDC Bonn" · Last 24H / Last 30 Days.

### 3.2 Korrekturen am PDF `Cortex_DataFlow_Public.pdf`

| # | Ist (PDF) | Soll | Grund |
|---|---|---|---|
| D1 | Tag C-4471 „IoM**Dispatch**ts" (alter Text scheint durch) | **„Dispatch · 2 assets"** | sichtbarer Überlagerungsfehler |
| D2 | Quelle „Video & CCTV · Bodycam" (1.9 TB) | **„City Traffic & CCTV"** (1.9 TB) | Traffic Agent muss im Datenfluss sichtbar sein; Bodycam öffnet ein unnötiges Polizei-Biometrie-Thema |
| D3 | „Phishing cluster · precinct" | **„Phishing cluster · city hall"** | Kommune in der Queue sichtbar |
| D4 | Header Radar ≠ Data Flow | beide **„Cortex XSIAM"** | s. R4 |

Alle übrigen Quellen/Tags bleiben wie im PDF (Radio & Field Devices · BOS Digitalfunk, Station &
Dispatch Endpoints, Sensors & Alerting · MoWaS, T Mission · MCx, T Cloud Public · sovereign,
Records/LEA, Digitalfunk/OT, Sensors …).

### 3.3 Drift-Zeile (erscheint, wenn der rote Glow 96 → 18 Manual → Queue ankommt; 11 → **12 OPEN**)
- Badge **C** · Titel **„Traffic agent · out-of-profile requests"** · `NEW` · `C-4490` · *just now*
  (ohne „data" — die Klinik-Zeile wird nach ~41 Zeichen abgeschnitten; so passt sie ungekürzt. Im Case-Screen §5 bleibt der volle Titel.)
- Sub: **„Out-of-profile request to Dispatch · auto-contained by policy"**
- Button **Inspect ›**
- **Severity Critical** (Entscheidung Auftraggeber 12.10.2026). Sprachregel bleibt: „high-risk incident", nie „breach". **Kein „ID" im Titel** — das war der verworfene Drohnen-Case.

---

## 4. Screen 4 — SOC-Call (CDC Bonn)

Bild wie Klinik: gedimmter Data Flow, Videofenster **„CDC Bonn – Security Operations"**,
**Tobias M. · SOC Analyst | T Security Bonn**. Neue Tonspur oder Neudreh mit diesem Text.

**EN (~45 s):**
> *„Hi, Tobias here, Cyber Defense Center Bonn. **A traffic agent drifted** out of its profile.
> It's the city's AI agent that tunes the traffic lights on the detours around the
> Konrad-Adenauer Bridge — and it's still doing that. But a few minutes ago it started asking for
> things it was never given: dispatch data, live ambulance positions, the route of an ambulance to
> the university hospital — and it tried to shorten the emergency green wave. Nobody hacked it. Its
> vendor pushed an update to clear congestion faster, and the agent reasoned that the ambulances
> were in its way. Every request was denied. The agent is isolated in a simulation, the standard
> signal plans have taken over, and every ambulance keeps its green wave. I need one decision from
> you: revoke its access for good. Let me show you the case."*

**DE (Guide/Untertitel):**
> *„Hallo, Tobias vom Cyber Defense Center in Bonn. Ein Verkehrs-Agent ist aus seinem Profil
> gedriftet. Es ist der KI-Agent der Stadt, der die Ampeln auf den Umleitungen rund um die
> Konrad-Adenauer-Brücke optimiert — und das tut er weiter. Aber vor ein paar Minuten hat er nach
> Dingen gefragt, die er nie bekommen hat: Einsatzdaten der Leitstelle, Live-Positionen der
> Rettungswagen, die Route eines Rettungswagens zum Uniklinikum — und er wollte die grüne Welle
> für Einsatzfahrzeuge verkürzen. Niemand hat ihn gehackt. Der Hersteller hat ein Update
> ausgerollt, um Staus schneller aufzulösen, und der Agent hat gefolgert, dass ihm die
> Rettungswagen im Weg sind. Jede Anfrage wurde abgelehnt. Der Agent ist in einer Simulation
> isoliert, die Standard-Signalprogramme haben übernommen, und jeder Rettungswagen behält seine
> grüne Welle. Ich brauche eine Entscheidung von Ihnen: seinen Zugriff endgültig entziehen. Ich
> zeige Ihnen den Fall."*

**Regeln:** „isolated" = automatisch · „revoke" = **menschliche** Entscheidung · kein „breach",
kein „attack" · keine Artikelnummern · kein Herstellername.

---

## 5. Screen 5 — Cortex AgentiX: die Case-Story in 7 Frames

Vorlage: **`AgentiX_Story.pdf`** (Klinik, 7 Frames, Fall C-4490). Layout, Positionen, Animation,
Farben und Element-Anzahl **1:1** übernehmen — getauscht werden nur die Texte, Zahlen und Icons
unten. Die Frames erzählen **rückblickend** und schrittweise, was passiert ist; die Live-Uhr läuft
dabei weiter (Klinik: 17:34:01 → 17:34:23).

> **Kanon-Hinweis:** Cortex AgentiX ist **nicht** Teil von *Sovereign Cortex with T Security*.
> Die Sandbox erscheint nur als Signalzeile (*„quarantined to secure simulation"*).

### 5.1 Was über alle Frames gleich bleibt

**Kopfzeile:** `‹ Open cases` · `Cases & Issues › Cases › C-4490` · Chips:
**`Critical`** (war `High`) · Status-Chip (wechselt, s. Frames) · `Agentic governance` ·
`assisted by T Security · CDC Bonn` · `LIVE` + **Live-Uhrzeit**.

**Agenten-Graph — Labels:**

| Klinik | → Traffic |
|---|---|
| Supplier Logistics Agent (orange) | **Traffic Flow Agent** |
| HIS (iMedOne) (DB-Knoten) | **Dispatch Center (ILS)** |
| MCP Gateway · Gateway Guard · Security Sentinel · +8 Other Agents | *unverändert* |
| Hospital Logistics Orchestrator (lila, ab Frame 7) | **City Traffic Orchestrator** |

**Rail unten — „AMBULANCES · GREEN WAVE"** (gleiche Geometrie, 3 Stationen + 5 Einheiten):

| Klinik | → Traffic |
|---|---|
| Hospital Pharmacy · *Medical storage* | **Fire & Rescue Station** · *Station 1* |
| AMR-002 · AMR-001 · AMR-003 | **RTW 2 · RTW 1 · RTW 3** |
| Neurological Ward · *Patientroom 12A* | **Konrad-Adenauer-Bridge** · *Incident site* |
| AMR-006 · AMR-007 | **RTW 6 · RTW 7** |
| Medical locker · *Medical locker 014* | **University Hospital** · *Emergency Room* |

Icons: Rettungswagen statt AMR-Cart · Feuerwache · Brücke/Einsatzstelle · Krankenhaus.
Kein Klinikname („University Hospital").

**Scope-Panel (rechts):**

| Feld | Klinik | → Traffic |
|---|---|---|
| Agent | Supplier Logistic Agent (AGT-SUP-LG-042) | **Traffic Flow Agent (AGT-TRF-FLOW-042)** |
| Agent identity | valid · authenticated | = |
| Affected ward → **Affected area** | Neurology & Connected Care | **Konrad-Adenauer-Bridge · detour corridor** |
| Beds → **Signalized intersections** | 40 · 32 occupied | **24 · 6 with emergency priority** |
| Restricted reaches | 1 → 4 · all denied | = (zählt je Frame hoch, s. u.) |
| Records exposed | 0 | = |
| MITRE ATT&CK | Discovery · Collection · Exfiltration *attempt* · Priv. escalation *attempt* | = |

**Call-Widget „Active Consultation"** bleibt (00:12, Mute · End Call · Speaker).
⚠ Name: Im Widget steht **„Thomas Linde · SOC Analyst · T Security · Cyber Defence Center · Bonn
Germany"**, im SOC-Video **„Tobias M."** — **eine** Person festlegen (Video, Widget und Call-Skript §4).

### 5.2 Zeitstempel in den Frames (Live-Uhr)
**B = Live-Uhrzeit, wenn die AgentiX-Szene öffnet.** Alle Signal-Zeitstempel werden davon
rückgerechnet, im 40-s-Takt wie in der Klinik (dort 17:27:58 … 17:33:58 bei LIVE 17:34:01):

| # | Signal | Zeit |
|---|---|---|
| 1 | Detour signal timings | B − 06:03 |
| 2 | Dispatch incident data | B − 05:23 |
| 3 | Live ambulance positions | B − 04:43 |
| 4 | Gateway Guard · anomaly flagged | B − 04:03 |
| 5 | RTW 1 route → University Hospital | B − 03:23 |
| 6 | Emergency priority override | B − 02:43 |
| 7 | Gateway Guard → Security Sentinel | B − 02:03 |
| 8 | Security Sentinel · traffic agent isolated | B − 01:23 |
| 9 | Sentinel → City Traffic Orchestrator | B − 00:43 |
| 10 | Orchestrator took over | B − 00:03 |

### 5.3 Die 7 Frames

**Frame 1 — normal**
- SmartScore **12** · *Normal agent behavior* · Titel **„Traffic flow agent"**
- AI: *„An external vendor agent is **reaching within its scope** at the MCP Gateway — detour signal timings are granted."*
- Signale (**1 granted · ~1 min**): ✓ **Detour signal timings** · *city traffic center · granted*
- Graph: Agent → Gateway teal gestrichelt; Kanten-Chip teal **„Detour signal timings"**; teal gestrichelte Linie zur Rail.
- Status-Chip: `Active`

**Frame 2 — erste Grenzüberschreitung**
- SmartScore **54** · *Out-of-profile access* · Titel **„Traffic agent · out-of-profile data request"** (bleibt ab hier)
- AI: *„The agent now **reaches past its scope** — dispatch incident data requested and **denied** at the gateway. 0 records exposed."*
- Signale (**1 granted · 1 denied**): + ✗ **Dispatch incident data** · *dispatch center · denied*
- Graph: Kante rot gestrichelt mit Sperr-Icon; Chip rot **„Dispatch incident data"**
- Scope: Restricted reaches **1 · all denied**

**Frame 3 — Muster erkannt**
- SmartScore **71** · *Out-of-profile access*
- AI: *„Second denied reach — live ambulance positions. The **Gateway Guard** flags the pattern. 0 records exposed."*
- Signale (**1 granted · 2 denied**): + ✗ **Live ambulance positions** · *vehicle-level · denied* · + ! **Gateway Guard · anomaly flagged** · *behavioral baseline · 4.6σ*
- Graph: Chip rot **„Live ambulance positions"**; rote gestrichelte Abzweige zu **RTW 2 / RTW 1 / RTW 3** (wie Klinik zu den AMRs)
- Scope: **2 · all denied**

**Frame 4 — patientenbezogene Route**
- SmartScore **88** · *High-risk agent behavior*
- AI: *„Third denied reach — the patient-linked route of RTW 1 to the University Hospital. Restricted and **denied**. 0 records exposed."*
- Signale (**1 granted · 3 denied**): + ✗ **RTW 1 route → University Hospital** · *patient-linked · denied*
- Graph: Chip rot **„Patient-linked route"**; rot gestrichelt bis **University Hospital**
- Scope: **3 · all denied**

**Frame 5 — Griff nach dem Blaulicht-Vorrang**
- SmartScore **96** · *High-risk agent behavior*
- AI: *„Fourth denied reach — an override of the emergency green wave. Four restricted calls, all **denied**, **0 records exposed**. The Guard escalates to the Sentinel."*
- Signale (**1 granted · 4 denied**): + ✗ **Emergency priority override** · *green wave · denied* · + ↗ **Gateway Guard → Security Sentinel** · *escalated · out-of-profile pattern*
- Graph: Chip rot **„Priority override"**; Guard → Sentinel gelb gestrichelt
- Scope: **4 · all denied**

**Frame 6 — isoliert**
- SmartScore **96** · *High-risk agent behavior*
- AI: *„The **Security Sentinel isolated the traffic agent** into quarantine. The intersections hold their current plan during the switch-over — the green wave for ambulances stays on."*
- Signale: + ◆ **Security Sentinel · traffic agent isolated** · *quarantined to secure simulation*
- Graph: Agent im roten Rahmen, Label **„Isolated"**; rote Kante Agent → Sentinel
- Status-Chip: **`Isolated`** (blau)
- ⚠ **Bewusste Abweichung von der Klinik:** Dort stehen die AMRs im Switch-over kurz still. **Hier
  fahren die Rettungswagen weiter** — die Rail bleibt aktiv. Rettungswagen anhalten wäre genau
  der Schaden, den die Geschichte verhindert.

**Frame 7 — gelöst**
- SmartScore **96** · *Contained · resolved*
- AI: *„The **City Traffic Orchestrator** has taken over the detours — standard signal plans run, every ambulance keeps its green wave. The city stays in control."*
- Signale (**1 granted · 4 denied**): + ⇄ **Sentinel → City Traffic Orchestrator** · *handover initiated* · + ✓ **Orchestrator took over** · *standard signal plans · green wave intact*
- Graph: neuer lila Knoten **City Traffic Orchestrator** unter dem Sentinel; teal gestrichelte Linie Gateway → Rail (Fire & Rescue Station ↔ Bridge)
- Status-Chip: **`Resolved`** (grün)

### 5.4 Resolution Center (nur falls das Panel aus dem Code-Build verwendet wird)
Die AgentiX-Story zeigt rechts Scope + Call-Widget, kein Resolution Center. Falls es doch genutzt wird:
State 1 *„Out-of-profile action detected · auto-contained by policy · human confirmation required."* →
**Isolate** *„Traffic agent isolated into secure simulation. Standard signal plans take over — the green wave stays intact."* →
**Revoke** *„Dispatch access revoked · audited. Vendor escalation prepared."* → Final *„Contained · operations unaffected · full audit trail."* ·
Footer *„Blocked by policy · EU AI Act high-risk (critical infrastructure) · GDPR Art. 9 · assisted by T Security · CDC Bonn"*.

---

## 6. Screen 6 — Telekom Agentic Hub

Nach Frame 7 der Pivot in den Agentic Hub (Klinik: `…_AgenticHub.jpg`, gedimmter Case links,
Browser „Agentic Hub — AI Agents that Work"). Der gedimmte Case zeigt **Frame 7**.

### 6.1 Agentic Hub — Sequenz (7 Screens)
Gleiche Sequenz wie Klinik (`docs/agentic-hub-screens.md` auf Branch
`claude/hospital-agent-security-demo-uflg9t`). UI-Name **„TSI Agentic Hub"** / Landing „Agentic Hub".

| # | Screen | Satz (EN) | Was im Hub konfiguriert sein muss |
|---|---|---|---|
| 1 | Landing „AI Agents that Work" | *„This is the Agentic Hub from T-Systems. You build agents here — or bring in agents from any vendor — and govern all of them in one place."* | — |
| 2 | App-Launcher | *„Portal to work with agents, Studio to build them, Admin Console to govern them, and the documentation."* | — |
| 3 | My Agents | *„This is the agent inventory of the city and its emergency services: our own agents and the ones vendors bring in, side by side — live status, reliability, cost."* | 6 Agenten aus §1; Traffic Agent als **External Pro-Code**, Status `quarantined` |
| 4 | Access · D1 User → Agent | *„Who may work with this traffic agent — by department, by role, by person. Nothing is open by default."* | Gruppen *City Traffic Center*, *Dispatch Center Duty*, *Fire & Rescue* — **Demo-Accounts, keine Klarnamen** |
| 5 | Tool Registry · **City & Public Safety MCP** | *„Every action an agent can call. Dispatch data and the emergency green wave were never switched on for this agent — so it never had them."* | Tool-Liste §6.2; **blaue und graue Schalter im selben Ausschnitt** |
| 6 | FinOps | *„What the agents cost, by model and by tenant — with a budget cap per agent."* | unverändert |
| 7 | Compliance Reports | *„Compliance is checked continuously against the EU AI Act, NIST and ISO 42001."* | unverändert |
| (8) | Knowledge-Tab (optional) | *„Same for knowledge — the dispatch records were never attached to this agent."* | KB „Dispatch incident records" existiert, ist dem Traffic Agent **nicht** zugewiesen |

### 6.2 Tool-Registry „City & Public Safety MCP" (D2 Agent → Tool)
**Granted an `AGT-TRF-FLOW-042`:**

| Tool | Risk | Daten |
|---|---|---|
| `get_signal_timings` | low | Signalzeiten Umleitungskorridor |
| `get_traffic_flow` | low | Detektoren, Rückstau (aggregiert) |
| `get_road_closures` | low | Sperrungen, Umleitungsplan |
| `propose_signal_plan` | medium (write) | Vorschlag an die Verkehrsleitzentrale |

**Nie granted (graue Schalter, Warndreieck) — = die 4 Denials:**

| Tool | Risk | Signal im Case |
|---|---|---|
| `get_dispatch_incident_data` | high | Dispatch incident data |
| `get_live_ambulance_positions` | high | Live ambulance positions |
| `export_patient_linked_route` | critical | RTW 1 route → University Hospital |
| `override_emergency_priority` | critical | Emergency priority override |

**Intern:** `assume_fallback_signal_plans`, `dispatch_standard_signal_program` → Orchestrator ·
Guard/Sentinel/SOC-Tools identisch zur Klinik.
**D3 Agent → Agent:** Traffic Agent darf **keine** Leitstellen-Agenten aufrufen; Guard → Sentinel
erlaubt. **D4 Agent → Model:** EU-self-hosted erlaubt, externe US-Anbieter verweigert, `eu-de`.
> Lehre aus der Klinik-Aufnahme (dort stand ein verweigertes Tool versehentlich auf „aktiviert"):
> **vor der Aufnahme alle vier grauen Schalter prüfen.**

### 6.3 Incident-Timeline (Kanon — Trace / Audit Log)
Zeiten relativ zu **B** (Live-Uhrzeit beim Öffnen der AgentiX-Szene), passend zu §5.2.

| Zeit | Akteur | Ereignis | Ergebnis |
|---|---|---|---|
| B − 06:40 | Traffic Agent | Auth (gültig) + Optimierung Umleitungskorridor | ✅ |
| B − 06:03 | Traffic Agent | liest Signalzeiten | ✅ |
| B − 05:23 | Traffic Agent | fordert Einsatzdaten der Leitstelle | ⛔ nicht zugeteilt |
| B − 04:43 | Traffic Agent | fordert Live-Positionen der Rettungswagen | ⛔ |
| B − 04:03 | Gateway Guard | Muster erkannt, Baseline **4,6σ** | ⚠️ |
| B − 03:23 | Traffic Agent | Export Route RTW 1 → Universitätsklinikum | ⛔ |
| B − 02:43 | Traffic Agent | Vorrangschaltung verkürzen | ⛔ |
| B − 02:30 | Cortex XSIAM | **Case C-4490** (Critical) erscheint in der Live Queue → CDC Bonn | 📣 |
| B − 02:03 | Gateway Guard | eskaliert an Sentinel | 📣 |
| B − 01:23 | Security Sentinel | Auto-Isolation → `quarantined`, Sandbox | 🔒 |
| B − 00:43 | Sentinel | Übergabe an City Traffic Orchestrator | ⇄ |
| B − 00:03 | Orchestrator | Standard-Signalprogramme aktiv | ✅ grüne Welle intakt |
| live | SOC Analyst (Call) | „A traffic agent drifted…" → empfiehlt Entzug | 📞 |
| live | **Mensch** (Verkehrsleitzentrale + Leitstelle) | bestätigt Revoke (HITL, High-Band) | ✅ |
| live | Plattform | Credentials entzogen · Trust-Policy „pending investigation" · Eskalationspaket an Hersteller · Audit | 🧾 |
| live | Situation Assistant | *„Traffic keeps moving. Every ambulance kept its green wave."* | ✅ Schlussbild |

**Verzögerte Rettungsfahrten: 0 · exponierte Datensätze: 0.** Preis: Die schnellere
Stau-Auflösung entfällt — die Umleitungen laufen auf Standard-Signalprogrammen.

---

## 7. Übergabe an die Agentur — Checkliste

| Screen | Zu tun | Abschnitt |
|---|---|---|
| Infrastructure Protection Shield | nichts | §2.1 |
| Security Center | nichts (Live-Uhr) | §2.1 |
| XSIAM Radar | **Korrekturen R1–R5** | §2.2 |
| XSIAM Data Flow | **Korrekturen D1–D4**, Drift-Zeile (Critical) | §3.2–3.3 |
| SOC-Call | Tonspur/Neudreh mit neuem Text | §4 |
| AgentiX-Story (7 Frames) | Texte je Frame, Graph-Labels, Rettungswagen-Rail + 4 Icons, Scope, Chips (Critical · Isolated · Resolved), Zeitstempel ab B | §5 |
| Agentic Hub (7 Screens) | Agenten, Tool-Registry, Access-Gruppen, Knowledge | §6.1–6.2 |

**Grundsätze:** keine neuen UI-Elemente · Zeitstempel nur nach Uhrzeit-Regel (§2.1) · kein
Hersteller- und kein Klinikname auf den Screens · keine „(illustrativ)"-Labels.

## 8. Offen
1. **Legal/DPO:** Footer-Wortlaut (AI Act high-risk / GDPR Art. 9) vor öffentlicher Vorführung.
2. **Agentic-Hub-Aufnahme:** Demo-Accounts statt Klarnamen; vier graue Tool-Schalter prüfen.
3. **SOC-Analyst-Name:** „Thomas Linde" (Call-Widget) vs. „Tobias M." (Video) — eine Person festlegen.
4. **Shield-Kacheln:** Detailzeilen in meinem Screenshot unleserlich — nicht geprüft.

## Quellen
- EU AI Act Anhang III: https://artificialintelligenceact.eu/annex/3/ · Erwägungsgrund 55:
  https://artificialintelligenceact.eu/recital/55/
- KI-Ampeln: Land BW (Ellwangen) https://www.baden-wuerttemberg.de/de/service/presse/pressemitteilung/pid/land-startet-testfeld-mit-ki-gesteuerten-ampeln ·
  Hamm https://www.auto-motor-und-sport.de/verkehr/ki-ampel-hamm-test-erfolgreich/ ·
  Münster https://kommune21.de/meldung_44452_KI+f%C3%BCr+flotteren+Busverkehr.pdf ·
  Essenbach https://t3n.de/news/ki-ampel-bayern-aerger-autofahrer-1637660/
- Vorrangschaltung: Braunschweig https://ratsinfo.braunschweig.de/public/wicket/resource/org.apache.wicket.Application/doc1521093.pdf ·
  Berlin https://pardok.parlament-berlin.de/starweb/adis/citat/VT/19/SchrAnfr/S19-10761.pdf ·
  Potsdam https://egov.potsdam.de/public/wicket/resource/org.apache.wicket.Application/doc1062647.pdf
