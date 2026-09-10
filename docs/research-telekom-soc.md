# Recherche — Deutsche Telekom / Telekom Security: Cyber Defense Center & SOC-Netz

Stand **2026-09-10**. Alle Angaben aus öffentlichen Quellen, jede Zahl mit Datum, weil
sich die Zahlen über die Jahre stark verändert haben. Quellen am Ende.

> **Zweck:** Grundlage für die T-Gallery-Demo. Abschnitt 8 sagt, welche Aussagen auf den
> Screen bzw. in den Sprechertext dürfen — und welche nicht.

---

## 1. Die Kurzantwort auf „es gibt wohl 15 weltweit"

**Die Zahl 15 ließ sich nicht belegen.** Es kursieren mehrere, je nach Jahr und je
nachdem, ob **Standorte** oder **Länder** gezählt werden:

| Zahl | Was genau | Quelle / Jahr |
|---|---|---|
| **17 SOCs** weltweit, Singapur als **13. Land** | Standorte | T-Systems / Telekom Security, Dez. 2019 |
| **9 SOCs** weltweit (D, ES, MX, BR, SG, ZA …) | nur die Geschäftskundensparte von T-Systems | T-Systems, ~2019 |
| **Bonn + 13 weitere Länder** = **14 Länder** | Länder | DT-Pressemitteilung + CR-Report, Sept. 2024 / 2024 |
| „SOCs across Europe, Asia, LATAM and the US" (keine Zahl) | Standorte | T-Systems Company Presentation, Mai 2025 |

**Belastbar sagen kann man heute:** *„Master SOC Bonn, vernetzt mit Zentren in 13 weiteren
Ländern"* — das ist die eigene Formulierung der Telekom von 2024 und steht so auch im
CR-Report. Wer Standorte statt Länder zählen will, landet bei **17 (Stand 2019)**.
**15 würde ich nicht sagen**, solange keine Quelle auftaucht.

**„TSAC" ließ sich nicht auflösen.** Kein Treffer als Telekom-Security-Einheit. Gemeint
ist vermutlich **T-Systems**, **Telekom Security** (Deutsche Telekom Security GmbH) oder
**TSI** (T-Systems International). Falls es ein internes Kürzel ist, bitte intern klären.

---

## 2. Wer ist wer (die Organisation)

| Einheit | Rolle |
|---|---|
| **Deutsche Telekom AG** | Konzern |
| **Deutsche Telekom Security GmbH** („Telekom Security") | Bündelt die Cybersecurity des Konzerns. Anfang **2017** als Geschäftsbereich innerhalb von **T-Systems** gegründet, seit **1. Juli 2020** eigene Gesellschaft in der DTAG. **~1.700 Spezialisten**, **>250 Mio. € Umsatz** im Cybersecurity-Geschäft, Marktführer in DE/AT/CH. |
| **T-Systems** | Geschäftskunden-IT; betreibt/vermarktet SOC-Leistungen mit. Mai 2025: **~2.500 Security-Expert:innen**, **bis zu 2,5 Mrd. Security-Events/Tag** aus **~3.300 Datenquellen**, **>36 Mio. abgewehrte Angriffe/Tag**. |
| **CERT (Cyber Emergency Response Team)** | Zentrale Meldestelle für Sicherheitsvorfälle konzernweit, **seit 2020 nach SIM3 zertifiziert**. |
| **Thomas Tschersich** | **CEO Telekom Security** und **CSO der Deutschen Telekom AG**. Öffentliches Gesicht der Telekom-Cybersicherheit. ⚠ Siehe Abschnitt 9. |

---

## 3. Das Cyber Defense Center Bonn / Master SOC

**Zwei Ausbaustufen — nicht verwechseln:**

- **2017:** „Integriertes Cyber Defense & Security Operations Center" Bonn eröffnet.
  Damals: **>200 Expert:innen**, **~1 Mrd. sicherheitsrelevante Daten/Tag** aus
  **~3.000 Quellen**, „größtes und modernstes Cyber-Abwehrzentrum Europas".
- **10. September 2024:** **Master Security Operations Center (Master SOC)** eröffnet —
  KI-gestützt, „eines der größten integrierten Cyber-Abwehrzentren Europas".

**Zahlen des Master SOC (Stand 2024, DT-eigene Angaben):**

| Kennzahl | Wert |
|---|---|
| Expert:innen in Bonn, 24/7 | **>250** |
| Vernetzung | Bonn + **13 weitere Länder** |
| Angriffsversuche | **30.000–40.000 pro Minute**, **bis zu 95 Mio./Tag** |
| Analysierte Daten | **mehrere Milliarden/Tag** aus **~250.000 Datenquellen**, nahezu vollautomatisch |
| Honeypot-Angriffe | **70 Mio./Tag** (2024) |
| Erkannte Botnet-Server | **~800 pro Monat** |
| Kunden | **>150** deutsche DAX- und Mittelstandsunternehmen (CR-Report 2024; eine ältere Quelle nennt „über 30") |
| Threat Intelligence | Threat-Intelligence-Datenbank gilt als **umfassendste Europas**; „Telekom Threat Library" mit Millionen Einträgen zu Malware, APTs, Zero-Days |
| Reifegrad | **Level 3–4** (automatisierte Detektion, strukturiertes Intelligence-Sharing, systematische Incident Response) |
| Souveränität | deutsche Jurisdiktion, **kein CLOUD-Act-Zugriff** — als Unterscheidungsmerkmal zu US-Anbietern positioniert |

⚠ **Achtung bei „~1 Mrd. Daten aus 3.000 Quellen".** Diese Zahl steht immer noch auf
mehreren T-Systems-Seiten, stammt aber aus der 2017er-Stufe. Die 2024er-Zahl ist
**„mehrere Milliarden aus 250.000 Quellen"**. Beide gleichzeitig zu zitieren ist falsch.

---

## 4. Das SOC-Netz — Standorte

**Deutschland:** Bonn (Master SOC) · Darmstadt · Kiel · Bad Kreuznach · Leipzig

**International (namentlich genannte Städte):** Budapest · Prag · Madrid · Kapstadt ·
Singapur

**Genannte Länder im Netz:** Deutschland · Ungarn · Österreich · Tschechien · Slowakei ·
Polen · Spanien · Griechenland · Südafrika · USA · Mexiko · Brasilien · Singapur

Singapur kam **2019** dazu und war „das 13. Land"; damals sprach T-Systems von einem
**Netz aus 17 SOCs**. Die Betriebsweise ist **Follow-the-Sun** über die Zeitzonen.

> Eine offizielle, vollständige und aktuelle Standortliste veröffentlicht die Telekom
> nicht. Die obige Liste ist aus mehreren Artikeln zusammengesetzt — für eine öffentliche
> Vorführung bitte intern bestätigen lassen.

---

## 5. Threat Intelligence, Honeypots, Sicherheitstacho

**Sicherheitstacho** (`sicherheitstacho.eu`) — öffentliches Live-Dashboard der Angriffe
auf die Telekom-Honeypots, entstanden mit der Allianz für Cyber-Sicherheit (BSI/Bitkom).

| Jahr | Honeypots | Angriffe/Tag |
|---|---|---|
| 2013 | 97 Systeme | bis 450.000 |
| später | 180 Honeypots in 12 Ländern | — |
| 2019 | 3.400 physische Sensoren (T-Systems-Angabe) | 46 Mio. Spitze / 31 Mio. Schnitt |
| 2024 | — | **70 Mio.** |

Weitere T-Systems-Angaben (2019): **6 Mrd. Datensätze/Tag** auf Cyberangriffe geprüft,
**100 Mio. Mails/Tag** gegen Spam/Phishing/Malware analysiert, **12 Mio. Angriffe** auf
die Honeypot-Sensoren ausgewertet.

---

## 6. Produkte, die auf dem SOC aufsetzen

| Produkt | Zielgruppe |
|---|---|
| **Magenta Security MDR Start** | Mittelstand ab 25 Endpoints; Einstieg in 24/7 Managed Detection & Response |
| **Magenta Security MDR Pro** | Enterprise; IT **und OT** plus Cloud-Infrastrukturen |
| **Managed Cyber Defense / Cyber Defense Services** | Großkunden, individuell |
| **Sovereign Cortex with T Security** | siehe Abschnitt 7 |

---

## 7. Sovereign Cortex with T Security (für die Demo zentral)

Angekündigt **9. Juni 2026** von Palo Alto Networks und Deutscher Telekom.

- Bringt die **Cortex-Plattform** (AI-driven SecOps) nach Europa, mit
  Souveränitätskontrollen, die **die Telekom unabhängig verwaltet**.
- **Hosting:** Palo Altos Sovereign-Cortex-Lösung läuft auf der **Sovereign Google Cloud
  Platform der Telekom**.
- **T Security liefert SOC- und Identity-Management-Services** und hält die
  **Key-Encryption-Keys in eigenen Rechenzentren**.
- Alle Kunden- und Systemdaten — **inklusive Telemetrie und Threat Intelligence** —
  werden ausschließlich **innerhalb Europas** gespeichert, verarbeitet und abgerufen.
  Support-Personal ausschließlich in Europa, Verträge nach europäischem Recht.
- **Zielbranchen:** Gesundheitswesen, öffentlicher Sektor, Finanzdienstleistungen,
  kritische Infrastruktur.
- **Compliance:** GDPR, **NIS2**, **DORA**, **KRITIS**.
- **Verfügbarkeit:** erste Release geplant für **Q3 2026**.
- Zitate: **Helmut Reisinger** (CEO EMEA, Palo Alto Networks) · **Thomas Tschersich**
  (CEO Deutsche Telekom Security): *„Our joint offering is currently unique in Europe at
  this level of quality."*

**Das passt exakt auf unsere Demo:** Krankenhaus = Zielbranche Gesundheitswesen, T Cloud
Public `eu-de` = Datenresidenz Europa, „assisted by T Security · CDC Bonn" = der
SOC-Service aus dem Angebot.

---

## 8. Was davon auf den Screen bzw. in den Sprechertext darf

**Sicher belegt — kann so gesagt/gezeigt werden:**
- „T Security · Cyber Defense Center Bonn" als assistierender SOC ✅
- **>250 Security-Expert:innen, 24/7 in Bonn** ✅
- **30.000–40.000 Angriffsversuche pro Minute / bis zu 95 Mio. pro Tag** ✅
- **Master SOC Bonn, vernetzt mit Zentren in 13 weiteren Ländern** ✅
- **~800 Botnet-Server pro Monat** ✅
- **Daten bleiben in Europa, Schlüssel bei der Telekom, deutsche Jurisdiktion** ✅
- **NIS2 / DORA / KRITIS / GDPR** als regulatorischer Rahmen ✅

**Nicht sagen:**
- ❌ „15 SOCs weltweit" — unbelegt
- ❌ „1 Milliarde Daten aus 3.000 Quellen" **zusammen mit** den 2024er-Zahlen — das ist
  der alte Stand von 2017
- ❌ „Magenta Security" in dieser Demo — falsche Markenebene (Kundenprodukt für
  Mittelstand), CLAUDE.md hält es bewusst off-screen
- ❌ Eine Standortliste als „vollständig" darstellen — es gibt keine offizielle

**Präzisierung zur Benennung:** Die Telekom nennt die Einrichtung offiziell
**„Master Security Operations Center"** bzw. **„integriertes Cyber Defense and Security
Operations Center"**. Unser Kurzform-Tag *„Cyber Defense Center Bonn"* ist inhaltlich
richtig, aber nicht die offizielle Eigenbezeichnung. Wer ganz sauber sein will, schreibt
**„Cyber Defense & Security Operations Center Bonn"**.

---

## 9. ⚠ Namensrisiko: unser SOC-Sprecher heißt „Thomas"

**Thomas Tschersich ist CEO von Telekom Security und CSO der Deutschen Telekom** — das
öffentliche Gesicht der Telekom-Cybersicherheit, Sprecher auf MWC und Black Hat MEA.

Ein KI-generierter Mitarbeiter, der sich mit *„Thomas here, T Security, Cyber Defense
Center Bonn"* vorstellt, kann auf einer Telekom-Ausstellungsfläche als Anspielung auf
ihn gelesen werden — oder schlimmer, als synthetisches Abbild einer realen Person.
`STORY_BIBLE.md` §3 verlangt ohnehin ausdrücklich **„never a specific real individual"**.

**Empfehlung:** anderen Vornamen wählen. Unverfänglich und ohne Kollision im gesamten
Story-Kanon wären z. B. **Jonas**, **Martin**, **Lukas** oder **Nils**. Falls „Thomas"
bleiben soll: mit der Kommunikationsabteilung abstimmen, bevor das öffentlich läuft.

(Zur Erinnerung: Der zweite Namenskonflikt bleibt bestehen — die Story Bible führt einen
Fernüberwachungs-**Patienten** „Thomas Berger".)

---

## 10. Quellen

**Deutsche Telekom (primär)**
- [Tense cyber situation: Telekom expands protection center (10.09.2024)](https://www.telekom.com/en/media/media-information/archive/telekom-expands-protection-center-1077020)
- [CR-Report 2024 — Cybersecurity and data protection](https://report.telekom.com/cr-report/2024/governance/cybersecurity-and-data-protection.html)
- [Deutsche Telekom further extends its cyber defense capabilities](https://www.telekom.com/en/media/media-information/archive/deutsche-telekom-further-extends-its-cyber-defense-capabilities-507242)
- [Thomas Tschersich — Profil](https://www.telekom.com/en/company/management-and-corporate-governance/board-of-management/profile/thomas-tschersich-574698)
- [About Telekom Security (Trust Center)](https://www.telesec.de/en/about-telekom-security)
- [Sicherheitstacho zeigt Cyber-Angriffe in Echtzeit](https://www.telekom.com/de/medien/medieninformationen/detail/sicherheitstacho-zeigt-cyber-angriffe-in-echtzeit--343586)
- [Magenta Security — Starke Verteidigung, schlank verpackt](https://www.telekom.com/en/media/media-information/archive/magenta-security-strong-defense-slim-package-1095786)
- [Deutsche Telekom and Palo Alto Networks Launch Data Sovereign Cyber Defence Managed Service](https://www.telekom.com/en/media/media-information/archive/data-sovereign-cyber-defence-managed-service-1105502)

**T-Systems**
- [SOC: Cyber Defence and Security Operations Center](https://www.t-systems.com/de/de/referenzen/security/cyber-abwehrcenter)
- [Company Presentation, Mai 2025 (PDF)](https://www.t-systems.com/resource/blob/1015132/1426a18c4e23aac670bc5c52da9335a1/DL-Company-Presentation-T-Systems-EN-05-2025.pdf)
- [T-Systems opens SOC in Singapore (FutureCIO, 2019)](https://futurecio.tech/t-systems-opens-security-operations-centre-in-singapore/)
- [T-Systems launches SOC in Singapore (Frontier Enterprise, 2019)](https://www.frontier-enterprise.com/t-systems-launches-security-operations-centre-in-singapore/)

**Palo Alto Networks**
- [Palo Alto Networks and Deutsche Telekom Bring AI-Driven Security with Advanced Sovereignty Controls (09.06.2026)](https://www.paloaltonetworks.com/company/press/2026/palo-alto-networks-and-deutsche-telekom-bring-ai-driven-security-with-advanced-sovereignty-controls-for-european-regulated-industries)
- [European Digital Sovereignty Starts With Trust (Blog, 06/2026)](https://www.paloaltonetworks.com/blog/2026/06/trust-is-the-foundation-of-sovereignty/)
- [Cortex AgentiX](https://www.paloaltonetworks.com/cortex/agentix)

**Fachpresse**
- [connect professional — Telekom baut Security Operations Center in Bonn aus (10.09.2024)](https://www.connect-professional.de/security/telekom-baut-security-operations-center-in-bonn-aus-331277.html)
- [connect professional — Deutsche Telekom erweitert Abwehrzentrum](https://www.connect-professional.de/datacenter-verkabelung/deutsche-telekom-erweitert-abwehrzentrum.319685.html)
- [infopoint-security — Telekom verstärkt Cyberabwehr durch Ausbau des SOCs](https://www.infopoint-security.de/telekom-verstaerkt-cyberabwehr-durch-ausbau-des-socs/a38235/)
- [SecurityToday — Security Operations Center: Made in Germany (18.03.2026)](https://www.securitytoday.de/en/2026/03/18/security-operations-center-made-in-germany/)
- [Telecompaper — DT partners Palo Alto Networks for Sovereign Cortex with T-Security](https://www.telecompaper.com/news/deutsche-telekom-partners-palo-alto-networks-to-offer-sovereign-cortex-with-t-security--1573494)
- [Cyber Security Cluster Bonn — Bonner IT-Sicherheitszentrum](https://cyber-security-cluster.eu/de/aktuelles/bonner-it-sicherheitszentrum-schuetzt-digitale-infrastrukturen-europa.html)
