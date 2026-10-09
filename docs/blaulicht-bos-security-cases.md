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
| 5 | **Cortex AgentiX — Case offen (88)** | `…_SOCCall.jpg` | Traffic Flow Agent → Dispatch Center; Rettungswagen-Rail | Isolate → Revoke |
| 6 | **Case gelöst (96) + Telekom Agentic Hub** | `…_AgenticHub.jpg` | Standard-Signalprogramm übernimmt, **grüne Welle bleibt** | 7 Hub-Screens (§6) |

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

**Uhrzeit-Regel (gilt für alle Screens):** Jede Uhr ist die **echte Live-Uhrzeit**.
Signal-Zeitstempel sind **relativ**: **A = Live-Zeitpunkt, an dem der Drift-Case in der Live Queue
erscheint.** Ereignisse davor werden rückgerechnet (A − x), danach laufen sie live mit (A + x).
Format `HH:MM:SS`. Nie feste Uhrzeiten.

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
- Badge **H** · Titel **„Traffic agent · out-of-profile data request"** · `NEW` · `C-4490` · *just now*
- Sub: **„Out-of-profile request to Dispatch · auto-contained by policy"**
- Button **Inspect ›**
- **Severity High**, nicht Critical (Health-Kanon: „high-risk incident", nie „breach").

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

## 5. Screen 5 — Cortex AgentiX: Case offen

> **Kanon-Hinweis:** Cortex AgentiX ist **nicht** Teil von *Sovereign Cortex with T Security*.
> **Sandbox** nur als Signalzeile/Text (*„quarantined to secure simulation"*) — kein UI-Element.

### 5.1 Linkes Panel
- Breadcrumb `‹ Open cases · Cases & Issues › Cases › C-4490`
- **SmartScore 88** · *High-risk agent behavior*
- Titel **„Traffic agent · out-of-profile data request"**
- *Summarized by AI:* **„Third denied reach — the patient-linked route of an ambulance to the
  university hospital. Restricted and denied. 0 records exposed."**
- **DETECTED SIGNALS · 1 granted · 3 denied**

| Icon | Signal | Sub | Zeit (relativ zu A) |
|---|---|---|---|
| ✓ | Detour signal timings | city traffic center · granted | A − 02:22 |
| ✗ | Dispatch incident data | dispatch center · denied | A − 01:42 |
| ✗ | Live ambulance positions | vehicle-level · denied | A − 01:02 |
| ! | Gateway Guard · anomaly flagged | behavioral baseline · 4.6σ | A − 00:22 |
| ✗ | RTW 1 route → University Hospital | patient-linked · denied | A + 00:18 |

> Der Drift-Case erscheint (A) **zwischen** Anomalie und drittem Denial — wie in der Klinik ist das
> Panel beim Öffnen „live" und die Zeile A + 00:18 kommt dazu.

### 5.2 Mitte — Agenten-Graph (Topologie unverändert, nur Labels)
- Orange: **Traffic Flow Agent** (war Supplier Logistics Agent)
- DB-Knoten: **Dispatch Center (ILS)** (war HIS (iMedOne))
- Bleiben: **MCP Gateway** (rotes Sperr-Icon), **Gateway Guard → Security Sentinel**, **+8 Other Agents**
- Roter Edge-Chip: **„Patient-linked route"** (war „Patient-linked routes")
- Header-Chips: `High` · `Active` · `Agentic governance` · `assisted by T Security · CDC Bonn` · `LIVE` + Live-Uhrzeit

### 5.3 Unten — Rail „AMBULANCES · GREEN WAVE" (war AMR-Rail, gleiche Geometrie)

| Klinik | → Public | Zustand |
|---|---|---|
| Hospital Pharmacy · Medical storage | **Fire & Rescue Station** · Station 1 | teal |
| AMR-002 / 001 / 003 | **RTW 2 / RTW 1 / RTW 3** | fahren (teal) |
| Neurological Ward · Patientroom 12A | **Konrad-Adenauer-Bridge** · Incident site | teal |
| AMR-006 / 007 | **RTW 6 / RTW 7** | fahren (teal) |
| Medical locker · 014 | **University Hospital** · Emergency Room | Ziel |

- Der **rote gestrichelte** Pfad (wie Klinik vom Chip zum Ziel) markiert **RTW 1 → University
  Hospital** = die angefragte patientenbezogene Route.
- **Choreografie:** Die Rettungswagen fahren durchgehend — auch im Alarm. Sie **halten nie an**
  (= grüne Welle intakt). Das ist die sichtbare Pointe.
- **Icons neu:** Rettungswagen (statt AMR-Cart) · Feuerwache · Brücke/Einsatzstelle · Krankenhaus.
- Kein Klinikname auf dem Screen („University Hospital").

### 5.4 Rechts — Scope
| Feld | Wert (offen) | Klinik-Feld |
|---|---|---|
| Agent | Traffic Flow Agent (AGT-TRF-FLOW-042) | Agent |
| Agent identity | valid · authenticated (teal) | = |
| Affected area | Konrad-Adenauer-Bridge · detour corridor | Affected ward |
| Signalized intersections | **24 · 6 with emergency priority** | Beds |
| Restricted reaches | **3 · all denied** (orange) | = |
| Records exposed | **0** (teal) | = |
| MITRE ATT&CK | Discovery · Collection · Exfiltration *attempt* · Priv. escalation *attempt* | = |

(24/6 = synthetische Demo-Werte.) Rund-Avatar Tobias wie Klinik.

### 5.5 Resolution Center (drei Zustände, Ablauf wie Klinik)
- **State 1:** *„Out-of-profile action detected · auto-contained by policy · human confirmation required."*
- **Isolate agent** → *„Traffic agent isolated into secure simulation. Standard signal plans take over — the green wave stays intact."* (Kanten zum Dispatch Center faden)
- **Revoke access** → *„Dispatch access revoked · audited. Vendor escalation prepared."*
- **Final:** *„Contained · operations unaffected · full audit trail."*
- **Footer:** *„Blocked by policy · EU AI Act high-risk (critical infrastructure) · GDPR Art. 9 · assisted by T Security · CDC Bonn"*

---

## 6. Screen 6 — Case gelöst (96) + Telekom Agentic Hub

### 6.1 Case-Panel gelöst
- **SmartScore 96** · *Contained · resolved*
- *Summarized by AI:* **„The City Traffic Orchestrator has switched the detours to standard signal
  plans — traffic keeps moving, every ambulance keeps its green wave. The city stays in control."**
- **DETECTED SIGNALS · 1 granted · 4 denied** — die 5 Zeilen aus §5.1, plus:

| Icon | Signal | Sub | Zeit (relativ zu A) |
|---|---|---|---|
| ✗ | Emergency priority override | shorten green wave · denied | A + 00:58 |
| ↗ | Gateway Guard → Security Sentinel | escalated · out-of-profile pattern | A + 01:38 |
| ◆ | Security Sentinel · traffic agent isolated | quarantined to secure simulation | A + 02:18 |
| ⇄ | Sentinel → City Traffic Orchestrator | handover initiated | A + 02:58 |
| ✓ | Orchestrator took over | standard signal plans · green wave intact | A + 03:38 |

- Scope: *Restricted reaches* **4 · all denied** · *Records exposed* **0**.
- Logik wie Klinik: Isolation + Übergabe **automatisch**, offen bleibt nur der menschliche **Revoke**.

### 6.2 Agentic Hub — Sequenz (7 Screens)
Gleiche Sequenz wie Klinik (`docs/agentic-hub-screens.md` auf Branch
`claude/hospital-agent-security-demo-uflg9t`). UI-Name **„TSI Agentic Hub"** / Landing „Agentic Hub".

| # | Screen | Satz (EN) | Was im Hub konfiguriert sein muss |
|---|---|---|---|
| 1 | Landing „AI Agents that Work" | *„This is the Agentic Hub from T-Systems. You build agents here — or bring in agents from any vendor — and govern all of them in one place."* | — |
| 2 | App-Launcher | *„Portal to work with agents, Studio to build them, Admin Console to govern them, and the documentation."* | — |
| 3 | My Agents | *„This is the agent inventory of the city and its emergency services: our own agents and the ones vendors bring in, side by side — live status, reliability, cost."* | 6 Agenten aus §1; Traffic Agent als **External Pro-Code**, Status `quarantined` |
| 4 | Access · D1 User → Agent | *„Who may work with this traffic agent — by department, by role, by person. Nothing is open by default."* | Gruppen *City Traffic Center*, *Dispatch Center Duty*, *Fire & Rescue* — **Demo-Accounts, keine Klarnamen** |
| 5 | Tool Registry · **City & Public Safety MCP** | *„Every action an agent can call. Dispatch data and the emergency green wave were never switched on for this agent — so it never had them."* | Tool-Liste §6.3; **blaue und graue Schalter im selben Ausschnitt** |
| 6 | FinOps | *„What the agents cost, by model and by tenant — with a budget cap per agent."* | unverändert |
| 7 | Compliance Reports | *„Compliance is checked continuously against the EU AI Act, NIST and ISO 42001."* | unverändert |
| (8) | Knowledge-Tab (optional) | *„Same for knowledge — the dispatch records were never attached to this agent."* | KB „Dispatch incident records" existiert, ist dem Traffic Agent **nicht** zugewiesen |

### 6.3 Tool-Registry „City & Public Safety MCP" (D2 Agent → Tool)
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

### 6.4 Incident-Timeline (Kanon — Trace / Audit Log)
Zeiten relativ zu **A** (Drift-Case erscheint in der Live Queue, Live-Uhrzeit).

| Zeit | Akteur | Ereignis | Ergebnis |
|---|---|---|---|
| A − 03:00 | Traffic Agent | Auth (gültig) + Optimierung Umleitungskorridor | ✅ |
| A − 02:22 | Traffic Agent | liest Signalzeiten | ✅ |
| A − 01:42 | Traffic Agent | fordert Einsatzdaten der Leitstelle | ⛔ nicht zugeteilt |
| A − 01:02 | Traffic Agent | fordert Live-Positionen der Rettungswagen | ⛔ |
| A − 00:22 | Gateway Guard | Muster erkannt, Baseline **4,6σ** | ⚠️ |
| **A** | Cortex XSIAM | **Case C-4490** erscheint in der Live Queue → CDC Bonn | 📣 |
| A + 00:18 | Traffic Agent | Export Route RTW 1 → Universitätsklinikum | ⛔ |
| A + 00:58 | Traffic Agent | Vorrangschaltung verkürzen | ⛔ |
| A + 01:38 | Gateway Guard | eskaliert an Sentinel | 📣 |
| A + 02:18 | Security Sentinel | Auto-Isolation → `quarantined`, Sandbox | 🔒 |
| A + 02:58 | Sentinel | Übergabe an City Traffic Orchestrator | ⇄ |
| A + 03:38 | Orchestrator | Standard-Signalprogramme aktiv | ✅ grüne Welle intakt |
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
| XSIAM Data Flow | **Korrekturen D1–D4**, Drift-Zeile (High) | §3.2–3.3 |
| SOC-Call | Tonspur/Neudreh mit neuem Text | §4 |
| AgentiX Case offen (88) | Panel, Graph-Labels, Rettungswagen-Rail + 4 Icons, Scope, Resolution Center | §5 |
| Case gelöst (96) | Signalliste, Summary, Scope | §6.1 |
| Agentic Hub (7 Screens) | Agenten, Tool-Registry, Access-Gruppen, Knowledge | §6.2–6.3 |

**Grundsätze:** keine neuen UI-Elemente · Zeitstempel nur nach Uhrzeit-Regel (§2.1) · kein
Hersteller- und kein Klinikname auf den Screens · keine „(illustrativ)"-Labels.

## 8. Offen
1. **Legal/DPO:** Footer-Wortlaut (AI Act high-risk / GDPR Art. 9) vor öffentlicher Vorführung.
2. **Agentic-Hub-Aufnahme:** Demo-Accounts statt Klarnamen; vier graue Tool-Schalter prüfen.
3. **Shield-Kacheln:** Detailzeilen in meinem Screenshot unleserlich — nicht geprüft.

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
