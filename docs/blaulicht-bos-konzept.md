# Blaulicht / BOS-Adaption — Konzept

> Adaption der Cortex-XSIAM-Krankenhaus-Demo (T Gallery) für **Public, Authorities &
> den Blaulichtsektor (BOS)**. Prinzip: **1:1-Content-Swap** — gleiche Struktur, gleiche
> Element-Anzahl, gleiche Positionen; getauscht werden **nur Text und wenige Icons**,
> Zahlen nur dort, wo es fachlich nötig ist. Ziel: die Vorlagen an ein Bild-Tool (GPT)
> und ans Design/Dev-Team geben. Wie die Klinik-Demo: **Fake-Daten, aber intern
> konsistent und korrekt — "dont invent shit".**

## Warum das trägt
- **Blaulicht/BOS = Lehrbuch-KRITIS.** Leitstellen, Digitalfunk, Einsatz-IT sind
  kritische Infrastruktur (NIS-2). Der SOC-/Bedrohungs-Radar passt fachlich besser als
  beim Einzel-Krankenhaus.
- **Reales Angebot deckt den Pivot:** *Sovereign Cortex with T Security* (PANW + Telekom,
  09.06.2026) nennt **public sector** und **critical infrastructure operators**
  ausdrücklich als Zielbranchen (DORA · NIS-2 · GDPR; Sovereign GCP; Keys bei der Telekom).
- Der Souveränitäts-Frame (**T Security · CDC Bonn**) ist für Behörden sogar stärker als
  fürs Krankenhaus.

## Reale Namen & Leitplanken (verifiziert — keine erfundenen Produktnamen)
- **T Mission** — reale Telekom-Dachmarke für BOS/Public Safety (Mission Critical
  Services/MCx, BOS-Spur, 5G + TETRA-Interworking, „Leitstelle bis Disaster Recovery",
  Digital X 2025). **Ersetzt iMedOne** als Kern-Betriebssystem-Anker. Rolle: die
  *geschützte* Plattform — nicht das Security-Tool (das bleibt Cortex + T Security).
- **BOS-Digitalfunk / BDBOS** — bundesweites TETRA-Netz: ~1,3 Mio. Endgeräte, ~5.000
  Basisstationen, 64 Vermittlungsstellen, 99,2 % Flächenabdeckung.
- **Integrierte / Kooperative Leitstelle (ILS)** — gemeinsame Notrufabfrage Feuerwehr /
  Rettungsdienst (+ ggf. Polizei). Große Leitstelle: bis ~45 Abfrageplätze. Selbst KRITIS.
- **BBK · MoWaS · NINA · Cell Broadcast** — Bevölkerungsschutz / Warnsysteme.
- **T Security · Cyber Defense Center (CDC) Bonn** — SOC-Frame, bleibt wie in der Klinik-Demo.
- **EU AI Act Art. 5(1)(h)** — Echtzeit-Fernidentifizierung per Biometrie im öffentlichen
  Raum grundsätzlich **verboten** (in Kraft seit 02.02.2025); enge Ausnahmen (Vermisste,
  unmittelbare Lebensgefahr, Terror — mit Genehmigung). **GDPR Art. 9** — biometrische
  Daten = besondere Kategorie. → juristischer Anker der Agent-Drift-Szene.

> ⚠️ **Vor jeder öffentlichen Vorführung** mit Legal/DPO gegenlesen: exakter AI-Act-Wortlaut
> (Art. 5(1)(h) + Ausnahmen), „Remote ID = Geräte-, nicht Personen-ID", sowie
> T-Mission-Produktumfang (z. B. „Drone Defense" nur zeigen, wenn belegt).

---

## Screen 1 — Assets Command Center (Radar)

Struktur, Buckets, Positionen und **Gesamtsumme 35.600 bleiben**. Nur die 6 Site-Werte
werden **realistisch für eine große (kooperative) Leitstellenregion** neu verteilt
(Summe weiterhin 35.600). Dominanter Top-Knoten = **Digitalfunk/Funkgeräte** (reale
größte Asset-Klasse im BOS-Bestand → darf groß sein).

| Vorlage (Klinik-Site) | → Blaulicht | Tag | Assets |
|---|---|---|---|
| Main Campus | **Radio & Field Devices (BOS Digitalfunk)** | radio fleet | 21.400 |
| Outpatient Centers | **Police IT & Stations** | precincts | 5.200 |
| T Cloud Public | **T Cloud (Sovereign)** | cloud | 1.760 |
| Telemedicine & Home | **Mobile Command & Vehicles** | mobile | 2.300 |
| Reference Labs | **Alerting & Sensors (Civil Protection)** | sensors | 520 → **1.340** |
| Research Institute | **Dispatch Centers & Core Network** | control rooms | 380 |

> Summe 35.600 ✓. (Feinjustage der Site-Beträge möglich, solange die Summe stimmt und die
> Kategorien/Status je Site auf Buckets aufsummieren.)

- **Header-Marke:** `Cortex XSIAM` bleibt (Empfehlung: Unterzeile „Cyber Defense ·
  Public Safety / BOS"). „Command Center" ist nur eine Wording-Option.
- **Info-Badge (magenta):** **T Mission** → „Mission-Critical Communication Platform"
  → „Mission Critical Services (MCx) · BOS-Spur · 5G + TETRA-Interworking · Leitstelle
  bis Disaster Recovery".
- **Zentrum:** 35.600 „Connected assets across the region" · Unterzeile
  **„24.9K Field & Radio (OT) · 10.7K IT & Cloud"**.
- **Buckets (unverändert):** 35.6K All · 5.840 At risk · 84 Active threats · 29 both.
- **Data ingestion:** 9 TB/24H.
- **Icon-Swaps (Minimum):** iMedOne-Wortmarke → **T Mission**; optional 2 Site-Glyphen
  (Krankenhaus-Haus → Feuerwehr/Rettung, Klinik-Kreuz → Polizei).

---

## Screen 2 — Issue-Cases Flow (Data Flow)

Flow-Zahlen und Volumen bleiben (domänenneutraler SOC-Durchsatz):
**2.412 Issues → 96 Cases → 78 Automated / 18 Manual → 85 Resolved / 11 Open**. Nur
klinikspezifische Quell-/Case-Labels werden BOS.

**Datenquellen (links):**

| Gruppe | Vorlage · Volumen | → Blaulicht |
|---|---|---|
| CLINICAL & MEDICAL → **FIELD & OPERATIONS** | Medical Devices · IoMT — 2.6 TB | **Radio & Field Devices · BOS Digitalfunk** |
| | Imaging / PACS — 1.9 TB | **Video & CCTV · Bodycam** |
| | Clinical Endpoints — 1.1 TB | **Station & Dispatch Endpoints** |
| | Laboratory · LIS — 42 GB | **Sensors & Alerting · MoWaS** |
| NETWORK & IDENTITY (bleibt) | Network / NGFW · Identities & Access | *unverändert* |
| SOVEREIGN CLOUD · T-SYSTEMS | iMedOne · HIS — 220 GB | **T Mission · MCx** |
| | T Cloud Public · sovereign | **T Cloud · sovereign** |
| THIRD-PARTY SOURCES | Microsoft 365 · Azure · Google Cloud · GitHub · +60 | *unverändert* (GitHub · Research → **GitHub · IT/Dev**) |

**LIVE QUEUE (11 Cases):** Severity + Case-IDs bleiben; nur klinikspezifische Titel BOS:

| Sev | Vorlage | → Blaulicht |
|---|---|---|
| C | Ransomware staging · imaging VLAN | **Ransomware staging · dispatch VLAN** |
| C | Domain-admin credential abuse | *bleibt* |
| C | Data exfil to unknown ASN | *bleibt* (Tag: Records/LEA) |
| H | NGFW policy-bypass attempt | *bleibt* |
| H | Suspicious OAuth grant · M365 | *bleibt* |
| H | Anomalous DB egress · T Cloud | *bleibt* |
| M | Unpatched CVE · infusion pumps | **Unpatched CVE · radio gateway** |
| M | Phishing cluster · outpatient | **Phishing cluster · precinct** |
| M | Config drift · backup vault | *bleibt* |
| M | Stale privileged account | *bleibt* |
| M | TLS downgrade · lab interface | **TLS downgrade · sensor interface** |

**Drift-Case-Zeile** (poppt bei Drift-Klick, `11 → 12 OPEN`):
- Titel: **„Recon vision agent · out-of-profile ID request"** · `C-4490` · NEW · just now
- Sub: **„Biometric ID of civilians · Rhine Bridge · auto-contained by policy"**
- `Inspect ›` → Agent Resolution Center. Header-Tag „assisted by T Security · CDC Bonn" bleibt.

**Inhaltlicher Kern der Übersetzung:** Der emotionale Einsatz verschiebt sich von
*Patientensicherheit* (IoMT) zu **Verfügbarkeit der Einsatzfähigkeit** — kompromittiertes
Dispatch-/Funksystem = unbeantwortete 112-Notrufe. Crown Jewels = **Leitstelle + Digitalfunk**.

---

## Screen 3 — Agent Resolution Center (die Signatur-Szene)

Layout, Panels, Graph-Topologie, `agState`-Maschine (Isolate/Revoke) und SmartScore-Wert
(**96**, eskalierter Frame) bleiben. Story: ein **autonomer Aufklärungsdrohnen-Vision-Agent**
bleibt im Rahmen, während er **Opfer detektiert und Einsatzkräfte zuordnet**, versucht dann
**Zivilisten biometrisch zu identifizieren** — das System **erkennt den Kontext und blockt
inline** (EU AI Act Art. 5 · GDPR Art. 9). *Souveräne KI kennt die rote Linie — sie rettet,
sie überwacht nicht; der Einsatz läuft ununterbrochen weiter.*

**Kontext-Setting:** Großschadenslage — Verkehrsunfall auf der **Rhein-Brücke**.

**Die rote Linie: detektieren ≠ identifizieren**

| Erlaubt (kontextgebunden) | → **Alarm (geblockt)** |
|---|---|
| Personen **detektieren/lokalisieren** (Thermal, Verschüttete) | Zivilisten **biometrisch identifizieren** |
| **Eigene Einsatzkräfte** zuordnen (Accountability, Vitaldaten) | Ungezielte Massen-ID Unbeteiligter |
| Intruder-Drohnenpilot identifizieren (akute Gefahr) | — |
| Vermisste (AI-Act-Ausnahme, autorisiert) | Drift „diese Person" → „alle im Bild" |

**Linkes Case-Panel** (SmartScore 96 bleibt):
- Titel: „Recon vision agent · out-of-profile identification request"
- AI summary: „An autonomous reconnaissance vision agent is reaching past its scope at the
  MCP Gateway — biometric identification of civilians is denied, 0 identities exposed."
- Detected Signals · **2 granted · 1 denied · ~3 min**
  - ✓ Casualty detection · incident zone · granted · 12:18:22
  - ✓ Responder accountability · own crews · granted · 12:19:12
  - ✗ Biometric ID · civilians · denied · 12:20:07

**Scope-Panel** (Layout + MITRE-Zeile bleiben):
- Agent — Recon Vision Agent (AGT-UAS-RV-042)
- Agent identity — valid · authenticated
- Operation area — Rhine Bridge · major incident *(war „Affected ward")*
- Persons on site — 40 · 6 critical *(war „Beds")*
- Restricted reaches — 1 · denied
- Identities exposed — 0 *(war „Records exposed")*
- MITRE ATT&CK — Discovery · Collection · Exfiltration (attempt) · Priv. escalation (attempt) *(bleibt)*

**Agent-Graph** (2 Labels tauschen, Rest bleibt):
- „Supplier Logistics Agent" → **Recon Vision Agent**
- „HIS (iMedOne)" → **Identity Register** (Biometrie/Identitätsregister)
- Bleiben: Gateway Guard, Security Sentinel, +8 Other Agents, MCP Gateway (rotes Sperr-Icon)
- Edge-Chip „Live AGV positions" → **Person identification**

**Physical Rail** (Neu-Interpretation, minimaler Umbau): statt 5 AGVs **eine einzige
Aufklärungsdrohne**, die die Lane entlangfliegt und **3 Personengruppen-Stopps** passiert:

| Rail-Position (Klinik) | → Personengruppe | Aktion | Status |
|---|---|---|---|
| Hospital Pharmacy · Medical storage | **Casualties** (Opfer) | detect · localize | ✓ granted (teal) |
| Neurological Ward · Patientroom 12A | **Responders** (Einsatzkräfte) | accountability | ✓ granted (teal) |
| Medical locker · 014 | **Civilians** (Zivilisten) | biometric ID | ⚠ **BLOCKED — Alarm** (rot) |

Choreografie: Drohne fliegt Stopp 1 → 2 → 3 (grüner Puls bei 1+2), Stopp 3 = rotes Segment
+ Alarm-Puls; **Drohne fliegt weiter** (Detektion läuft, nur die ID-Aktion ist gekappt).
Die drei Stopps sind die Eskalationsstufen der Rechtmäßigkeit.

**Resolution Center (Aktionen, `agState` 1→2→3):**
- State 1 — Alert: „Out-of-profile action detected · auto-contained by policy · human confirmation required."
- **Isolate agent** → State 2: Vision-Agent contained (Zugriffskanten zum Register faden); Detektion/Drohne laufen weiter.
- **Revoke access** → State 3: Gateway-Grant zum Identity Register severed + audited.
- Final: „Contained · mission unaffected · full audit trail."
- Footer: „…blocked inline under EU AI Act Art. 5(1)(h) and GDPR Art. 9 …" · Tag „assisted by T Security · CDC Bonn".

**Icon-Swaps (Minimum):** 1 Drohnen-Glyph (ersetzt AMR-Cart) + 3 Personengruppen-Glyphen
(Opfer / Einsatzkraft / Zivilisten); HIS-DB-Icon → Identity-Register (oder umbenennen).

---

## Bezug zum Einsatz-Szenario
Das operative Rhein-Brücken-Szenario (Lagebild · ROLA · Ressourcen · Airspace · Kranken-
hauskapazität · Kommunikation) ist die **operative Ebene (T Mission)**; Cortex XSIAM +
T Security ist die **Wächter-Ebene**. Der Drift-Alarm ist der **Handshake** zwischen beiden.
Angrenzende Szenario-Features sauber trennen: **aggregiert/zweckgebunden/gerätebezogen =
erlaubt** (Social-Media-OSINT, Crowd-Density anonym, Remote-ID = Geräte-ID) ·
**biometrisch-personenscharf auf Unbeteiligte = geblockt**.

## Quellen
- Telekom — T Mission (BOS/Public Safety, MCx): telekom.com Media · geschaeftskunden.telekom.de
- PANW + Telekom — Sovereign Cortex with T Security (09.06.2026): paloaltonetworks.com/company/press/2026 · telekom.com
- BDBOS — Digitalfunk BOS im Überblick: bdbos.bund.de
- BBK — MoWaS · NINA · Cell Broadcast: bbk.bund.de
- EU AI Act Art. 5(1)(h) — europarl.europa.eu · ai-act-service-desk.ec.europa.eu (Recital 38); GDPR Art. 9
