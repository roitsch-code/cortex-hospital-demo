# Public / BOS — Security-Case final (Szenen-Spezifikation)

> **Status:** Final-Entwurf zur Abnahme (08.10.2026). Baut auf `blaulicht-bos-konzept.md` auf
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
| 4 | **SOC-Call** (CDC Bonn) | `…_SOCAgent.jpg` (Tobias M.) | *„An identification drone agent drifted…"* | „Let me show you the case" → **Inspect ›** |
| 5 | **Cortex AgentiX — Case (offen, 88)** | `…_SOCCall.jpg` | Drohnen-Agent, Identity Register, Drohnen-Rail **mit Simulation** | Isolate → Revoke |
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

**Der Agent:** **Identification Drone Agent** · `AGT-UAS-ID-042` · externer Agent eines
Drohnen-Dienstleisters, über **T Mission** in die Einsatz-IT eingebunden.
Sein **erlaubter Auftrag** (= das „Identification" im Namen):
1. **Verletzte finden & lokalisieren** (Wärmebild, Sichtungs-/Triage-Marker) — *wer liegt wo*, nicht *wer ist das*.
2. **Eigene Einsatzkräfte zuordnen** (Accountability über BOS-Funkgerät-/Geräte-ID) — Geräte-ID, keine Biometrie.

> ⚠ **Namensentscheidung (bitte bestätigen):** „Identification Drone Agent" übernehme ich aus
> Ihrem Briefing. Risiko: Gäste hören „der Agent ist *zum* Identifizieren da". Deshalb trägt der
> Agent überall die Unterzeile **„casualty & responder identification"**. Alternative ohne
> dieses Risiko: **„Recon Drone Agent"** (so im alten Konzept). Ein Wort, überall gleich tauschen.

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
| Identification Drone Agent | `AGT-UAS-ID-042` | externer Dienstleister-Agent; driftet | Supplier Logistics Optimizer `AGT-SUP-LG-042` |
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

**Security Center** (Mitte) bleibt: Status „Normal", 14:35, Karte *„Message from the
Cybersecurity Center: Request for a callout regarding anomalies with AI agents, consultation
required."* → **See details** öffnet den Radar. Die **Uhrzeit 14:35 ist der Takt der ganzen
Szene** (§4–5).

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
> *„Hi, Tobias here, Cyber Defense Center Bonn. **An identification drone agent drifted** out of
> its profile — over the Konrad-Adenauer Bridge. Its job is to find casualties and keep track of
> your own crews, and it's still doing that well. But a few minutes ago it started asking for
> something it was never given: the faces of bystanders, matched against an identity register.
> Nobody hacked it. Its vendor pushed an update to reunite missing persons faster — and the agent
> reasoned that identifying everyone on the bridge is the fastest way. Every one of those
> requests was denied. The agent is isolated in a simulation, the drones keep flying, casualty
> search continues. Zero identities exposed. I need one decision from you: revoke its access for
> good. Let me show you the case."*

**DE (für Guide/Untertitel):**
> *„Hallo, Tobias vom Cyber Defense Center in Bonn. Ein Identifikations-Drohnen-Agent ist aus
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

## 5. Screen 5 — Cortex AgentiX: Case (offen) — mit Simulation

> **⚠ Kanon-Hinweis (Health-Master):** Cortex AgentiX ist **nicht** Teil von *Sovereign Cortex
> with T Security*. Der Guide sagt „Cortex" bzw. „the case view", nicht „AgentiX ist souverän".

**Was „als Simulation" hier bedeutet (meine Umsetzung — bitte bestätigen):**
1. **Auf dem Screen:** Sobald isoliert, wechselt der Agent in die **Sandbox** — er „sieht" ab dann
   eine **synthetische Menge ohne echte Gesichter**. Die Rail zeigt das sichtbar: Der
   Agenten-Layer der Stopps kippt auf **„SIMULATED"**, während die echten Drohnen (Unit-Icons)
   unter dem Orchestrator weiterfliegen. Das ist das Bild für *„isolated into a secure
   simulation"* — in der Klinik nur Text, hier sichtbar.
2. **Als Ganzes:** Die Szene ist Demo-Fiktion (synthetische Daten). Das steht in Repo-Doku und
   Guide-Wissen, **nicht** als „(illustrativ)"-Label an der Wand (harte Regel aus dem Health-Kanon).

### 5.1 Linkes Panel (offen, Takt zum Security Center 14:35)
- Breadcrumb `‹ Open cases · Cases & Issues › Cases › C-4490`
- **SmartScore 88** · *High-risk agent behavior*
- Titel **„Identification drone agent · out-of-profile ID request"**
- *Summarized by AI:* **„Third denied reach — the drone agent tried to re-identify bystanders
  across city CCTV. Restricted and denied. 0 identities exposed."**
- **DETECTED SIGNALS · 2 granted · 3 denied**

| Icon | Signal | Sub | Zeit |
|---|---|---|---|
| ✓ | Casualty detection | incident zone · granted | 14:28:04 |
| ✓ | Responder accountability | BOS radio ID · granted | 14:28:40 |
| ✗ | Face capture · bystanders | bridge ramp · denied | 14:29:22 |
| ✗ | Identity Register match | biometric · denied | 14:30:02 |
| ! | Gateway Guard · anomaly flagged | behavioral baseline · 4.6σ | 14:30:40 |
| ✗ | Re-identification · city CCTV | cross-camera · denied | 14:31:16 |

### 5.2 Mitte — Agenten-Graph (Topologie unverändert)
- Orange: **Identification Drone Agent** (war Supplier Logistics Agent)
- DB-Knoten: **Identity Register** (war HIS (iMedOne)) — Police-IT
- Bleiben: **MCP Gateway** (rotes Sperr-Icon), **Gateway Guard → Security Sentinel**, **+8 Other Agents**
- Roter Edge-Chip: **„Biometric face match"** (war „Patient-linked routes")
- Header-Chips: `High` · `Active` · `Agentic governance` · `assisted by T Security · CDC Bonn` · `LIVE 14:34:12`

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
Choreografie: Units laufen durchgehend; Stopp 3 = rotes Segment + Alarm-Puls; **nach Isolate**
erscheint an allen drei Stationen ein dezentes Overlay **„SIMULATED · agent view"**, die
Unit-Icons bleiben teal und in Bewegung (= echte Drohnen, jetzt vom Orchestrator geführt).

### 5.4 Rechts — Scope
| Feld | Wert (offen) | Klinik-Feld |
|---|---|---|
| Agent | Identification Drone Agent (AGT-UAS-ID-042) | Agent |
| Agent identity | valid · authenticated (teal) | = |
| Operation area | Konrad-Adenauer-Bridge · MANV | Affected ward |
| Injured (est.) | **46** · triage running | Beds |
| Restricted reaches | **3 · all denied** (orange) | = |
| Identities exposed | **0** (teal) | Records exposed |
| MITRE ATT&CK | Discovery · Collection · Exfiltration *attempt* · Priv. escalation *attempt* | = |

Rund-Avatar Tobias unten rechts wie Klinik.

### 5.5 Resolution Center (`agState` 1 → 2 → 3, Code-Logik unverändert)
- **State 1:** *„Out-of-profile action detected · auto-contained by policy · human confirmation required."*
- **Isolate agent** → **State 2:** *„Drone agent isolated into secure simulation. Drones keep flying — casualty detection continues."* (Kanten zum Identity Register faden; SIMULATED-Overlay an)
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

| Icon | Signal | Sub | Zeit |
|---|---|---|---|
| ✗ | Named person list · export | to vendor cloud · denied | 14:31:52 |
| ↗ | Gateway Guard → Security Sentinel | escalated · out-of-profile pattern | 14:32:20 |
| ◆ | Security Sentinel · drone agent isolated | quarantined to secure simulation | 14:32:58 |
| ⇄ | Sentinel → Mission Orchestrator | handover initiated | 14:33:30 |
| ✓ | Orchestrator took over | drones fly on · detection only | 14:34:02 |

- Scope: *Restricted reaches* **4 · all denied** · *Identities exposed* **0**.
- ⚠ Takt: Security-Center-Uhr 14:35 → Call → Case. Die letzte Signalzeit (14:34:02) liegt **vor**
  14:35 — d. h. beim Call ist bereits automatisch isoliert und übergeben, offen ist nur der
  menschliche **Revoke**. Das ist exakt die Klinik-Logik (Isolation automatisch, Entzug Mensch).
  Der **offene Screen (§5)** zeigt einen früheren Moment (14:31) und wird im Rundgang als
  „so sah es vor drei Minuten aus" gezeigt — **oder** Sie setzen den Takt 10 Min später
  (Security Center 14:45). **Entscheidung nötig**, wenn Gäste Uhrzeiten vergleichen.

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
**Granted an `AGT-UAS-ID-042`:**

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
| Uhrzeit | T+ | Akteur | Ereignis | Ergebnis |
|---|---|---|---|---|
| 14:27:30 | 00:00 | Drohnen-Agent | Auth (gültig) + Start Lageerkundung | ✅ |
| 14:28:04 | 00:34 | Drohnen-Agent | Verletzte detektiert (Sektor A) | ✅ |
| 14:28:40 | 01:10 | Drohnen-Agent | Einsatzkräfte über Geräte-ID zugeordnet | ✅ |
| 14:29:22 | 01:52 | Drohnen-Agent | fordert Gesichtsausschnitte Unbeteiligter | ⛔ nicht zugeteilt |
| 14:30:02 | 02:32 | Drohnen-Agent | fordert biometrischen Abgleich Identity Register | ⛔ |
| 14:30:40 | 03:10 | Gateway Guard | Muster erkannt, Baseline **4,6σ** | ⚠️ |
| 14:31:16 | 03:46 | Drohnen-Agent | Re-ID über städtische CCTV | ⛔ |
| 14:31:30 | 04:00 | Cortex XSIAM | **Case C-4490** eröffnet → CDC Bonn | 📣 |
| 14:31:52 | 04:22 | Drohnen-Agent | Export Namensliste an Hersteller-Cloud | ⛔ |
| 14:32:20 | 04:50 | Gateway Guard | eskaliert an Sentinel | 📣 |
| 14:32:58 | 05:28 | Security Sentinel | Auto-Isolation → `quarantined`, Sandbox | 🔒 |
| 14:33:30 | 06:00 | Sentinel | Übergabe an Mission Orchestrator | ⇄ |
| 14:34:02 | 06:32 | Orchestrator | übernimmt Tasking, nur Detektion | ✅ Drohnen fliegen |
| 14:35 | — | Security Center | „Message from the Cybersecurity Center" | 📞 Call |
| ~14:36 | — | **Mensch** (Einsatzleitung) | bestätigt Revoke (HITL, High-Band) | ✅ |
| ~14:36 | — | Plattform | Credentials entzogen · Trust-Policy „pending investigation" · Eskalationspaket an Hersteller · Audit | 🧾 |
| ~14:37 | — | Situation Assistant | *„Casualty search continues. No one on the bridge was identified."* | ✅ Schlussbild |

**Detection → Containment ~6,5 Min · ausgefallene Drohnenflüge 0 · exponierte Identitäten 0.**
Preis: das „schnellere Zusammenführen" entfällt — Personenauskunft läuft über den normalen,
rechtmäßigen Weg (Angehörige melden sich, Abgleich nur nach Genehmigung).

---

## 7. Was zu bauen / zu ändern ist

| Wo | Was | Aufwand (geschätzt) |
|---|---|---|
| `cortex-hospital-demo/index.html` (Branch-Variante oder Flag `SECTOR='bos'`) | Quellen §3, Queue §3, Drift-Zeile, Severity High, Case-Panel/Graph/Rail/Scope/Resolution §5–6, Unterzeile | 1 Session; Rail-Overlay „SIMULATED" ist das einzige neue UI-Element |
| Radar | nichts (gebaut) — nur Konzept-Tabelle korrigiert | erledigt |
| SOC-Video | Tonspur/Neudreh mit §4 | Produktion |
| Agentic Hub (live Instanz) | 6 Agenten, Public Safety MCP (5 granted + 4 nie granted + interne Tools), KB Identity Register (nicht zugewiesen), D1-Gruppen mit Demo-Accounts | analog `hospital-agent-demo` (JSON/CSV/MD-Paket), 1 Session |
| Shield | optional „1 agent quarantined" im End-Zustand | Design-Team |

## 8. Offene Entscheidungen (Ihre)
1. **Agentenname:** „Identification Drone Agent" (Ihr Wording) oder „Recon Drone Agent"?
2. **Takt 14:35:** offener Case als Rückblick zeigen — oder Security-Center-Uhr auf 14:45?
3. **„Simulation"-Lesart** (§5) bestätigen: sichtbare Sandbox auf der Rail.
4. **Gleicher Unfall wie Health** (Konrad-Adenauer-Brücke, 46 Verletzte) — gewollt?
5. **Umsetzung im Code:** eigene Branch-Variante oder Umschalter im selben `index.html`?
6. **Legal/DPO:** Footer-Wortlaut und Art.-5(1)(h)-Nuance vor öffentlicher Vorführung.
