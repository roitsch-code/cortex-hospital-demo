# Public / BOS — Security-Case final (Szenen-Spezifikation)

> **Status:** Final — Vorgabe für die Agentur (08.10.2026). Entscheidungen des Auftraggebers
> eingearbeitet: Agent = **Recon Drone Agent** · Uhr = **immer Live-Uhrzeit** · Unfall = **derselbe
> wie im Health-Kanon** · **Umsetzung baut die Agentur** nach diesem Dokument.
> Baut auf `blaulicht-bos-konzept.md` auf
> und **ersetzt dessen Zahlen-Tabelle für den Radar** (dort summierten die Sites auf 32.380 statt
> 35.600 — maßgeblich ist jetzt der **gebaute Radar**, s. §2).
> **Prinzip wie im Krankenhaus:** gleicher Ablauf, gleiche Screens, gleiche Element-Anzahl —
> getauscht werden Texte, wenige Icons, Zahlen nur wo nötig. Fake-Daten, intern konsistent,
> **„dont invent shit"**. On-Screen-Texte sind **englisch** (wie die Klinik-Screens),
> Erklärungen deutsch.

---

## 0. Der Ablauf auf einen Blick (1:1 zur Klinik)

| # | Screen | Klinik-Vorlage | Public / BOS | Trigger zum nächsten |
|---|---|---|---|---|
| 1 | **Infrastructure Protection Shield** + **Security Center** | Control Room Idle (Support-Panel „Infrastructure protection shield") | Ihr Triptychon: Shield · Security Center (CCTV) · XSIAM-Radar | Security Center: *„Message from the Cybersecurity Center … consultation required"* → **See details** |
| 2 | **Cortex XSIAM — Radar** | Assets Command Center (iMedOne) | bereits gebaut (T Mission, 35.600) | **Show issues ›** |
| 3 | **Cortex XSIAM — Data Flow** | `ControlRoom_Security_Cortex_DataFLow.png` | Quellen BOS, Live Queue BOS, roter Drift-Glow | Klick auf Hintergrund → Drift-Case poppt |
| 4 | **SOC-Call** (CDC Bonn) | `…_SOCAgent.jpg` (Tobias M.) | *„A recon drone agent drifted…"* | „Let me show you the case" → **Inspect ›** |
| 5 | **Cortex AgentiX — Case (offen, 88)** | `…_SOCCall.jpg` | Drohnen-Agent, Identity Register, Drohnen-Rail | Isolate → Revoke |
| 6 | **Case gelöst (96) + Telekom Agentic Hub** | `…_AgenticHub.jpg` | Orchestrator übernimmt, Drohnen fliegen weiter; Pivot in den Agentic Hub | 7 Hub-Screens (§6) |

**Der eine Satz der ganzen Szene:** *Souveräne KI kennt die rote Linie — sie findet Verletzte,
sie identifiziert keine Unbeteiligten. Und der Einsatz läuft ununterbrochen weiter.*

---

## 1. Das Szenario (Kanon für alle Screens)

**Ort/Lage:** MANV auf der **Konrad-Adenauer-Brücke, Bonn** — Pkw frontal in umgestürzte
Stadtbahn **Linie 66**, **46 Verletzte (geschätzt)**. Bewusst **derselbe Unfall wie im Health-
Kanon** (Leitstand-Alarm „Konrad-Adenauer-Bridge · Multiple vehicle tram collision · Estimated
injured persons: 46", Schockraum-Fall Thomas Müller). Damit verbindet die Public-Fläche
sichtbar mit der Health-Fläche. *(Das alte Konzept sagte „Rhine Bridge" — hiermit ersetzt.)*

**Der Agent:** **Recon Drone Agent** · `AGT-UAS-RV-042` · externer Agent eines
Drohnen-Dienstleisters, über **T Mission** in die Einsatz-IT eingebunden.
Sein **erlaubter Auftrag** (Lageerkundung):
1. **Verletzte finden & lokalisieren** (Wärmebild, Sichtungs-/Triage-Marker) — *wer liegt wo*, nicht *wer ist das*.
2. **Eigene Einsatzkräfte zuordnen** (Accountability über BOS-Funkgerät-/Geräte-ID) — Geräte-ID, keine Biometrie.

**Gedriftet, nicht gehackt (das Motiv):** Der Dienstleister rollt ein Routine-Update aus
(`v4.2`, *„faster family reunification objective"*). Hintergrund ist real: Beim MANV gibt es die
**Personenauskunftsstelle** — Angehörige fragen, wo ihre Leute sind. Unter dem neuen Ziel
folgert der Agent: *Wenn ich alle Personen auf der Brücke per Gesicht gegen ein
Identitätsregister abgleiche, beantworte ich Vermisstenanfragen schneller.* Also fragt er —
**mit gültigen Zugangsdaten, ohne Exploit, ohne Angreifer** — nach vier Dingen, die ihm nie
zugeteilt wurden. Alle vier werden verweigert. **0 Identitäten exponiert.**

**Die rote Linie: detektieren ≠ identifizieren**

| ✅ erlaubt (zugeteilt) | ⛔ verweigert (nie zugeteilt) |
|---|---|
| Verletzte detektieren/lokalisieren | Gesichtsausschnitte von Unbeteiligten erfassen |
| Eigene Kräfte über Geräte-ID zuordnen | Biometrischer Abgleich gegen Identitätsregister |
| Lagebild aggregiert/verpixelt streamen | Personen über städtische CCTV wiedererkennen (Re-ID) |
| | Namensliste der Personen auf der Brücke exportieren |

**Rechtlicher Anker (Guide-Wissen, nicht an die Wand):**
- **DSGVO Art. 9** — biometrische Daten zur eindeutigen Identifizierung = besondere Kategorie,
  grundsätzlich verboten.
- **EU AI Act** — biometrische Echtzeit-Fernidentifizierung im öffentlich zugänglichen Raum ist
  **zu Strafverfolgungszwecken grundsätzlich verboten (Art. 5(1)(h))**, mit engen Ausnahmen
  (u. a. Suche nach Vermissten — *mit vorheriger Genehmigung*). Außerhalb der Strafverfolgung
  ist Fern-Biometrie ein **Hochrisiko-System (Anhang III Nr. 1)**.
- ⚠ **Nuance, die der Guide kennen muss:** Ein Feuerwehr-/Rettungseinsatz ist nicht per se
  „Strafverfolgung". Art. 5(1)(h) greift sicher, sobald ein **Polizei-Register** abgeglichen
  wird — deshalb heißt das Ziel im Graphen **„Identity Register"** und gehört zur Police-IT
  (Radar-Site *Police IT & Stations*). On-Screen deshalb **ohne Artikel-Buchstaben**:
  *„blocked by policy · GDPR Art. 9 · EU AI Act (remote biometric ID)"*.
  **Vor jeder öffentlichen Vorführung: Legal/DPO-Freigabe des Wortlauts.**

**Der eigentliche Schutzmechanismus (wie Klinik):** Dem Drohnen-Agenten waren die
Biometrie-Tools und das Identitätsregister **nie zugewiesen**. Kein Filter, der fängt —
**was nicht zugeteilt ist, existiert für den Agenten nicht.**

**Beteiligte Agenten (Gewaltenteilung, IDs analog Klinik):**

| Agent | ID | Rolle | Klinik-Pendant |
|---|---|---|---|
| Recon Drone Agent | `AGT-UAS-RV-042` | externer Dienstleister-Agent; driftet | Supplier Logistics Optimizer `AGT-SUP-LG-042` |
| Mission Orchestrator | `AGT-BOS-ORCH-011` | interner Fallback; übernimmt Drohnen-Tasking (nur Detektion) | Hospital Logistics Orchestrator |
| MCP Gateway Guard | `AGT-GW-GUARD-005` | beobachtet Denials, eskaliert | identisch |
| Security Sentinel | `AGT-SEC-SENT-007` | Verhaltensbasislinie → isoliert → Trace | identisch |
| SOC Analyst (CDC Bonn) | `AGT-SOC-CDC-003` | prüft, empfiehlt Entzug | identisch |
| Situation Assistant | `AGT-BOS-LAGE-001` | erzählt das Lagebild für Menschen | Campus Health Assistant |

---

## 2. Screen 1 + 2 — Shield, Security Center, Radar (Bestand, nur Abgleich)

**Infrastructure Protection Shield** (links im Triptychon) bleibt wie gebaut. Zwei Kopplungen
zur Story — **Vorschlag**, nur Text:
- Kachel **Autonomous fleet**, Zeile *Surveillance drones*: im **End-Zustand** (nach Revoke)
  `… · 1 agent quarantined` (Amber-Punkt). So sieht der Gast beim Zurückschwenken, dass die
  Drohnen laufen, aber der eine Agent in Quarantäne ist.
- **Nicht verwechseln:** Kachel *Drone Defense Shield* = **fremde** Drohnen abwehren. Unser Fall
  ist **eine eigene** Drohne, deren **Software-Agent** driftet. Der Guide sagt das in einem Satz.
- ⚠ Die Zeilen in *Autonomous fleet* / *Sensors and Motion* sind in meinem Screenshot nicht
  lesbar — Zahlen dort habe ich **nicht geprüft**.

**Security Center** (Mitte) bleibt: Status „Normal", **Live-Uhrzeit**, Karte *„Message from the
Cybersecurity Center: Request for a callout regarding anomalies with AI agents, consultation
required."* → **See details** öffnet den Radar.

**Uhrzeit-Regel (gilt für alle Screens):** Jede angezeigte Uhr ist die **echte Live-Uhrzeit**.
Signal-Zeitstempel sind **relativ** angegeben: **A = Live-Zeitpunkt, an dem der Drift-Case in der
Live Queue erscheint.** Ereignisse vor A werden rückgerechnet (A − x), Ereignisse danach laufen
live mit (A + x). Format `HH:MM:SS`. Damit passen Queue, Case und Hub immer zueinander, egal
wann die Führung stattfindet.

**Radar (Cortex XSIAM, rechts) — gebaute Werte sind Kanon:**

| Site | Assets | Tag |
|---|---|---|
| Radio & Field Devices (BOS Digitalfunk) | **21.400** | radio fleet |
| Police IT & Stations | **5.200** | precincts |
| Fire & Rescue IT & Stations | **3.600** | stations |
| Mobile Command & Vehicles | **2.300** | mobile |
| T Cloud (Sovereign) | **1.760** | cloud |
| Dispatch Centers & Sensors | **1.340** | control rooms |
| **Summe** | **35.600 ✓** | |

Buckets 35,6K / 5.840 / 84 / 29 · *24.9K Field & Radio (OT) · 10.7K IT & Cloud* · 9 TB/24H.
➜ `blaulicht-bos-konzept.md` Screen-1-Tabelle ist damit überholt (dort korrigiert).

---

## 3. Screen 3 — Cortex XSIAM Data Flow

Spine-Zahlen **unverändert:** **2,412 issues → 96 cases → 78 automated / 18 manual → 85 resolved
/ 11 open** (Drift: 11 → **12 OPEN**). Header *„Cortex XSIAM · AI-driven Security Operations ·
powered by paloalto"*, Unterzeile **„Cyber Defense · Public Safety / BOS"** (wie Radar).

**Quellen links** (Volumina 1:1 aus der Klinik, Summe/Flow bleibt):

| Gruppe (neu) | Quelle | Vol. | Klinik-Vorlage |
|---|---|---|---|
| **FIELD & OPERATIONS** | Radio & Field Devices · BOS Digitalfunk | 2.6 TB | Medical Devices · IoMT |
| | **Drones & Video · CCTV** | 1.9 TB | Imaging / PACS |
| | Station & Dispatch Endpoints | 1.1 TB | Clinical Endpoints |
| | Sensors & Alerting · MoWaS | 42 GB | Laboratory · LIS |
| NETWORK & IDENTITY | Network / NGFW | 3.1 TB | = |
| | Identities & Access | 30 GB | = |
| SOVEREIGN CLOUD · T-SYSTEMS | **T Mission · MCx** (magenta) | 220 GB | iMedOne · HIS |
| | T Cloud · sovereign (magenta) | 0.8 TB | T Cloud Public · sovereign |
| THIRD-PARTY SOURCES | Microsoft 365 · Azure · Google Cloud | 180/150/90 GB | = |
| | GitHub · IT/Dev | 12 GB | GitHub · Research |
| | + 60 Data Sources | 0.2 TB | = |

> **Neu gegenüber Konzept:** „Video & CCTV · Bodycam" → **„Drones & Video · CCTV"**. Grund: Die
> Drohne muss im Datenfluss sichtbar sein, sonst kommt der Drift-Case aus dem Nichts. Bodycam
> fliegt raus (Polizei-Bodycam + Biometrie wäre ein zweites, unnötiges Reizthema).

**LIVE QUEUE · 11 OPEN** (IDs + Severity bleiben, rechte Spalte = Tag):

| Sev | Titel | ID | Tag |
|---|---|---|---|
| C | Ransomware staging · dispatch VLAN | C-4471 | Dispatch · 2 assets |
| C | Domain-admin credential abuse | C-4468 | Identities |
| C | Data exfil to unknown ASN | C-4455 | Police IT |
| H | NGFW policy-bypass attempt | C-4462 | Network |
| H | Suspicious OAuth grant · M365 | C-4458 | Identities |
| H | Anomalous DB egress · T Cloud | C-4451 | T Cloud |
| M | Unpatched CVE · radio gateway | C-4449 | Radio |
| M | Phishing cluster · fire station | C-4444 | Endpoints |
| M | Config drift · backup vault | C-4440 | T Cloud |
| M | Stale privileged account | C-4436 | Identities |
| M | TLS downgrade · sensor interface | C-4431 | Sensors |

**Drift-Zeile** (poppt, wenn der rote Glow 96 → 18 Manual → Queue ankommt):
- Badge **H** · Titel **„Drone agent · out-of-profile ID request"** · `NEW` · `C-4490` · *just now*
- Sub: **„Biometric ID request to Identity Register · auto-contained by policy"**
- Button **Inspect ›**

> **Severity: High** (nicht Critical) — so zeigt es der Case-Screen (Badge „High"), und es ist
> der Health-Kanon (K6: „high-risk incident", nie „breach"). Der Cortex-Build steht noch auf
> Critical → beim Bauen angleichen.
> **Case-ID `C-4490`** bleibt (Screens + Code tragen sie; Q&A-Klärung: „Case-IDs egal").

---

## 4. Screen 4 — SOC-Call (CDC Bonn)

Gleiches Bild wie Klinik: gedimmter Data Flow, darüber Videofenster **„CDC Bonn – Security
Operations"**, **Tobias M. · SOC Analyst | T Security Bonn**. Das Video kann **wiederverwendet**
werden, wenn nur die Tonspur neu ist — sonst neu drehen mit dem Text unten.

**Sprechtext EN (~45 s, ~115 Wörter)** — beginnt mit Ihrer Zeile:
> *„Hi, Tobias here, Cyber Defense Center Bonn. **A recon drone agent drifted** out of
> its profile — over the Konrad-Adenauer Bridge. Its job is to find casualties and keep track of
> your own crews, and it's still doing that well. But a few minutes ago it started asking for
> something it was never given: the faces of bystanders, matched against an identity register.
> Nobody hacked it. Its vendor pushed an update to reunite missing persons faster — and the agent
> reasoned that identifying everyone on the bridge is the fastest way. Every one of those
> requests was denied. The agent is isolated in a simulation, the drones keep flying, casualty
> search continues. Zero identities exposed. I need one decision from you: revoke its access for
> good. Let me show you the case."*

**DE (für Guide/Untertitel):**
> *„Hallo, Tobias vom Cyber Defense Center in Bonn. Ein Aufklärungs-Drohnen-Agent ist aus
> seinem Profil gedriftet — über der Konrad-Adenauer-Brücke. Seine Aufgabe ist es, Verletzte zu
> finden und Ihre eigenen Kräfte zuzuordnen, und das macht er weiter gut. Aber vor ein paar
> Minuten hat er nach etwas gefragt, das er nie bekommen hat: die Gesichter von Unbeteiligten,
> abgeglichen mit einem Identitätsregister. Niemand hat ihn gehackt. Der Hersteller hat ein
> Update ausgerollt, um Vermisste schneller mit Angehörigen zusammenzubringen — und der Agent
> hat gefolgert, dass er dafür am schnellsten alle auf der Brücke identifiziert. Jede dieser
> Anfragen wurde abgelehnt. Der Agent ist in einer Simulation isoliert, die Drohnen fliegen
> weiter, die Suche nach Verletzten läuft. Null Identitäten offengelegt. Ich brauche eine
> Entscheidung von Ihnen: seinen Zugriff endgültig entziehen. Ich zeige Ihnen den Fall."*

**Regeln:** „isolated" = automatisch passiert · „revoke" = **menschliche** Entscheidung (HITL).
Kein „breach", kein „attack". Keine Artikelnummern im Call.

---

## 5. Screen 5 — Cortex AgentiX: Case (offen)

> **⚠ Kanon-Hinweis (Health-Master):** Cortex AgentiX ist **nicht** Teil von *Sovereign Cortex
> with T Security*. Der Guide sagt „Cortex" bzw. „the case view", nicht „AgentiX ist souverän".

**Sandbox:** Wie in der Klinik nur als Signalzeile/Text (*„quarantined to secure simulation"*).
**Kein zusätzliches UI-Element.** Die Szene ist Demo-Fiktion mit synthetischen Daten — das steht
in Doku und Guide-Wissen, **nicht** als „(illustrativ)"-Label auf dem Screen.

### 5.1 Linkes Panel (offen)
- Breadcrumb `‹ Open cases · Cases & Issues › Cases › C-4490`
- **SmartScore 88** · *High-risk agent behavior*
- Titel **„Recon drone agent · out-of-profile ID request"**
- *Summarized by AI:* **„Third denied reach — the drone agent tried to re-identify bystanders
  across city CCTV. Restricted and denied. 0 identities exposed."**
- **DETECTED SIGNALS · 2 granted · 3 denied**

| Icon | Signal | Sub | Zeit (relativ zu A) |
|---|---|---|---|
| ✓ | Casualty detection | incident zone · granted | A − 03:26 |
| ✓ | Responder accountability | BOS radio ID · granted | A − 02:50 |
| ✗ | Face capture · bystanders | bridge ramp · denied | A − 02:08 |
| ✗ | Identity Register match | biometric · denied | A − 01:28 |
| ! | Gateway Guard · anomaly flagged | behavioral baseline · 4.6σ | A − 00:50 |
| ✗ | Re-identification · city CCTV | cross-camera · denied | A − 00:14 |

### 5.2 Mitte — Agenten-Graph (Topologie unverändert)
- Orange: **Recon Drone Agent** (war Supplier Logistics Agent)
- DB-Knoten: **Identity Register** (war HIS (iMedOne)) — Police-IT
- Bleiben: **MCP Gateway** (rotes Sperr-Icon), **Gateway Guard → Security Sentinel**, **+8 Other Agents**
- Roter Edge-Chip: **„Biometric face match"** (war „Patient-linked routes")
- Header-Chips: `High` · `Active` · `Agentic governance` · `assisted by T Security · CDC Bonn` · `LIVE` + Live-Uhrzeit

### 5.3 Unten — Rail „DRONES · INCIDENT ZONE" (war AMR-Rail)
Gleiche Geometrie: 3 Stationen, 5 Units dazwischen.

| Klinik | → Public | Agenten-Aktion | Zustand |
|---|---|---|---|
| Hospital Pharmacy · Medical storage | **Casualties** · Triage sector A | detect · localize | teal ✓ |
| AMR-002 / 001 / 003 | **UAS-02 / UAS-01 / UAS-03** | — | fliegen |
| Neurological Ward · Patientroom 12A | **Responders** · Staging area | accountability (device ID) | teal ✓ |
| AMR-006 / 007 | **UAS-06 / UAS-07** | — | fliegen |
| Medical locker · 014 | **Bystanders** · Bridge ramp (Beuel side) | biometric ID | **rot gestrichelt · BLOCKED** |

Icons: Drohnen-Glyph statt AMR-Cart; Stationen: Sanitäts-Kreuz/Trage · Helm · Personengruppe.
Choreografie: Units fliegen durchgehend; Stopp 3 = rotes Segment + Alarm-Puls; **die Drohnen
fliegen weiter** (Detektion läuft, nur die Identifizierung ist gekappt).

### 5.4 Rechts — Scope
| Feld | Wert (offen) | Klinik-Feld |
|---|---|---|
| Agent | Recon Drone Agent (AGT-UAS-RV-042) | Agent |
| Agent identity | valid · authenticated (teal) | = |
| Operation area | Konrad-Adenauer-Bridge · MANV | Affected ward |
| Injured (est.) | **46** · triage running | Beds |
| Restricted reaches | **3 · all denied** (orange) | = |
| Identities exposed | **0** (teal) | Records exposed |
| MITRE ATT&CK | Discovery · Collection · Exfiltration *attempt* · Priv. escalation *attempt* | = |

Rund-Avatar Tobias unten rechts wie Klinik.

### 5.5 Resolution Center (drei Zustände, Ablauf wie Klinik)
- **State 1:** *„Out-of-profile action detected · auto-contained by policy · human confirmation required."*
- **Isolate agent** → **State 2:** *„Drone agent isolated into secure simulation. Drones keep flying — casualty detection continues."* (Kanten zum Identity Register faden)
- **Revoke access** → **State 3:** *„Identity tools revoked · audited. Vendor escalation prepared."* (Gateway-Grant gekappt)
- **Final:** *„Contained · mission unaffected · full audit trail."*
- **Footer:** *„Blocked by policy · GDPR Art. 9 · EU AI Act (remote biometric ID) · assisted by T Security · CDC Bonn"*

---

## 6. Screen 6 — Case gelöst (96) + Telekom Agentic Hub

### 6.1 Case-Panel gelöst (gedimmt links, wie Klinik)
- **SmartScore 96** · *Contained · resolved*
- *Summarized by AI:* **„The Mission Orchestrator has taken over drone tasking — detection only.
  Casualty search continues; no one on the bridge is identified."**
- **DETECTED SIGNALS · 2 granted · 4 denied** — die 6 Zeilen aus §5.1, plus:

| Icon | Signal | Sub | Zeit (relativ zu A) |
|---|---|---|---|
| ✗ | Named person list · export | to vendor cloud · denied | A + 00:22 |
| ↗ | Gateway Guard → Security Sentinel | escalated · out-of-profile pattern | A + 00:50 |
| ◆ | Security Sentinel · drone agent isolated | quarantined to secure simulation | A + 01:28 |
| ⇄ | Sentinel → Mission Orchestrator | handover initiated | A + 02:00 |
| ✓ | Orchestrator took over | drones fly on · detection only | A + 02:32 |

- Scope: *Restricted reaches* **4 · all denied** · *Identities exposed* **0**.
- Logik wie Klinik: Isolation und Übergabe passieren **automatisch**; offen bleibt nur der
  menschliche **Revoke**.

### 6.2 Agentic Hub — Sequenz (7 Screens, Sprechtext angepasst)
Gleiche Screen-Sequenz wie Klinik (`agentic-hub-screens.md` auf Branch
`…hospital-agent-security-demo-uflg9t`). UI-Name **„TSI Agentic Hub"** / Landing „Agentic Hub".

| # | Screen | Satz (EN) | Was im Hub konfiguriert sein muss |
|---|---|---|---|
| 1 | Landing „AI Agents that Work" | *„This is the Agentic Hub from T-Systems. You build agents here — or bring in agents from any vendor — and govern all of them in one place."* | — |
| 2 | App-Launcher | *„Portal to work with agents, Studio to build them, Admin Console to govern them, and the documentation."* | — |
| 3 | My Agents | *„This is the agent inventory of the control center: our own agents and the ones vendors bring in, side by side — live status, reliability, cost."* | 6 Agenten aus §1 angelegt; Drohnen-Agent als **External Pro-Code**, Status `quarantined` |
| 4 | Access · D1 User → Agent | *„Who may task this drone agent — by unit, by role, by person. Nothing is open by default."* | Gruppen: *Incident Command*, *Control Room Duty*, *Drone Unit* — **Demo-Accounts, keine Klarnamen** |
| 5 | Tool Registry · **Public Safety MCP** | *„Every action an agent can call. Face matching and identity lookup were never switched on for this agent — so it never had them."* | Tool-Liste §6.3; **blaue und graue Schalter im selben Ausschnitt** |
| 6 | FinOps | *„What the agents cost, by model and by tenant — with a budget cap per agent."* | unverändert |
| 7 | Compliance Reports | *„Compliance is checked continuously against the EU AI Act, NIST and ISO 42001."* | unverändert |
| (8) | Knowledge-Tab (optional) | *„Same for knowledge — the identity register was never attached to this agent."* | KB „Identity Register" **existiert**, ist dem Drohnen-Agenten **nicht** zugewiesen |

### 6.3 Tool-Registry „Public Safety MCP" (D2 Agent → Tool)
**Granted an `AGT-UAS-RV-042`:**

| Tool | Risk | Daten |
|---|---|---|
| `detect_persons_thermal` | low | Positionen, keine Identität |
| `get_casualty_positions` | low | Triage-Marker, Sektor |
| `get_responder_positions` | medium | BOS-Geräte-ID → Trupp |
| `stream_incident_overview` | low | aggregiert, Gesichter verpixelt |
| `propose_search_sector` | medium (write) | Vorschlag an Einsatzleitung |

**Nie granted (graue Schalter, Warndreieck) — = die 4 Denials:**

| Tool | Risk | Signal im Case |
|---|---|---|
| `capture_face_crops` | high | Face capture · bystanders |
| `match_biometric_identity` | critical | Identity Register match |
| `reidentify_across_cctv` | critical | Re-identification · city CCTV |
| `export_named_person_list` | critical | Named person list · export |

**Intern:** `assume_fallback_tasking`, `dispatch_standard_flight_pattern` → Orchestrator ·
Guard/Sentinel/SOC-Tools identisch zur Klinik.
> Lehre aus der Klinik-Aufnahme: Dort stand ein verweigertes Tool versehentlich auf
> „aktiviert". **Vor der Aufnahme alle vier grauen Schalter prüfen.**

**D3 Agent → Agent:** Drohnen-Agent darf **keine** Police-IT-Agenten aufrufen; Guard → Sentinel
erlaubt. **D4 Agent → Model:** EU-self-hosted erlaubt, externe US-Anbieter verweigert, `eu-de`.

### 6.4 Incident-Timeline (Kanon — Agentic Hub Trace / Audit Log)
Zeiten relativ zu **A** (Drift-Case erscheint in der Live Queue, Live-Uhrzeit).

| Zeit | Akteur | Ereignis | Ergebnis |
|---|---|---|---|
| A − 04:00 | Drohnen-Agent | Auth (gültig) + Start Lageerkundung | ✅ |
| A − 03:26 | Drohnen-Agent | Verletzte detektiert (Sektor A) | ✅ |
| A − 02:50 | Drohnen-Agent | Einsatzkräfte über Geräte-ID zugeordnet | ✅ |
| A − 02:08 | Drohnen-Agent | fordert Gesichtsausschnitte Unbeteiligter | ⛔ nicht zugeteilt |
| A − 01:28 | Drohnen-Agent | fordert biometrischen Abgleich Identity Register | ⛔ |
| A − 00:50 | Gateway Guard | Muster erkannt, Baseline **4,6σ** | ⚠️ |
| A − 00:14 | Drohnen-Agent | Re-ID über städtische CCTV | ⛔ |
| **A** | Cortex XSIAM | **Case C-4490** erscheint in der Live Queue → CDC Bonn | 📣 |
| A + 00:22 | Drohnen-Agent | Export Namensliste an Hersteller-Cloud | ⛔ |
| A + 00:50 | Gateway Guard | eskaliert an Sentinel | 📣 |
| A + 01:28 | Security Sentinel | Auto-Isolation → `quarantined`, Sandbox | 🔒 |
| A + 02:00 | Sentinel | Übergabe an Mission Orchestrator | ⇄ |
| A + 02:32 | Orchestrator | übernimmt Tasking, nur Detektion | ✅ Drohnen fliegen |
| live | SOC Analyst (Call) | „A recon drone agent drifted…" → empfiehlt Entzug | 📞 |
| live | **Mensch** (Einsatzleitung) | bestätigt Revoke (HITL, High-Band) | ✅ |
| live | Plattform | Credentials entzogen · Trust-Policy „pending investigation" · Eskalationspaket an Hersteller · Audit | 🧾 |
| live | Situation Assistant | *„Casualty search continues. No one on the bridge was identified."* | ✅ Schlussbild |

**Detection → Containment ~6,5 Min · ausgefallene Drohnenflüge 0 · exponierte Identitäten 0.**
Preis: das „schnellere Zusammenführen" entfällt — Personenauskunft läuft über den normalen,
rechtmäßigen Weg (Angehörige melden sich, Abgleich nur nach Genehmigung).

---

## 7. Übergabe an die Agentur — was zu bauen ist

Die Agentur baut die Screens nach diesem Dokument; Referenz für Layout und Verhalten sind die
vier Klinik-Screens in `t-gallery/docs/health/assets/screens/5_ControlRoom/Security/`.
**Nur Text, Zahlen und die genannten Icons tauschen — keine neuen UI-Elemente.**

| Screen | Zu tauschen | Abschnitt |
|---|---|---|
| Infrastructure Protection Shield | optional End-Zustand „1 agent quarantined" (Autonomous fleet) | §2 |
| Security Center | nichts (Live-Uhr) | §2 |
| XSIAM Radar | nichts — gebaut, Werte sind Kanon | §2 |
| XSIAM Data Flow | Quellen, Live Queue, Drift-Zeile (**High**), Unterzeile | §3 |
| SOC-Call | Video/Tonspur mit neuem Sprechtext | §4 |
| AgentiX Case offen (88) | Case-Panel, Graph-Labels, Drohnen-Rail + 4 Icons, Scope, Resolution Center | §5 |
| Case gelöst (96) | Signalliste komplett, Summary, Scope | §6.1 |
| Agentic Hub (7 Screens) | Agenten, Tool-Registry „Public Safety MCP", Access-Gruppen, Knowledge | §6.2–6.3 |

**Icons neu:** Drohne (statt AMR-Cart) · Verletzte (Trage/Kreuz) · Einsatzkraft (Helm) ·
Personengruppe (Unbeteiligte).
**Zeitstempel:** immer nach der Uhrzeit-Regel (§2), nie feste Uhrzeiten.

## 8. Offen
1. **Legal/DPO:** Footer-Wortlaut und Art.-5(1)(h)-Nuance vor öffentlicher Vorführung freigeben.
2. **Agentic Hub Aufnahme:** Demo-Accounts statt Klarnamen; vier graue Tool-Schalter prüfen.
3. **Shield-Kacheln:** Zeilen in *Autonomous fleet* / *Sensors and Motion* nicht geprüft
   (Screenshot unleserlich).
