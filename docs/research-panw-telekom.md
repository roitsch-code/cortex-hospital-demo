# Recherche — Deutsche Telekom × Palo Alto Networks: Cortex & Souveränität

Stand **2026-09-10**. Öffentliche Quellen, jede Aussage mit Datum. Quellen am Ende.
Ergänzt `docs/research-telekom-soc.md` (SOC-Seite) und speist `docs/voice-agent/kb/02-*`.

---

## 1. Die Partnerschaft ist sechs Jahre alt, nicht drei Monate

Sovereign Cortex ist **kein Erstkontakt**, sondern die dritte Stufe einer laufenden
Zusammenarbeit. Das ist für die Erzählung wichtig: Es ist eine gereifte Partnerschaft,
kein Pressemitteilungs-Handschlag.

| Datum | Was |
|---|---|
| **April 2020** | **Strategische Partnerschaft** PANW × Telekom Security. Gemeinsam gebaute und betriebene Managed-Security-Services für Cloud- und Netzsicherheit sowie Security Operations — u. a. managed virtuelle Next-Generation-Firewalls und **SOC-Managed-Services auf Basis der Cortex-Suite**. |
| **September 2021** | **T-Systems × Google Cloud**: Sovereign Cloud für Deutschland — ausdrücklich für Unternehmen, **öffentlichen Sektor und Gesundheitswesen**. Betrieb und Service-Management durch T-Systems. |
| **September 2022** | Managed **Secure Service Edge** mit **Prisma Access** (ZTNA 2.0). |
| **später** | Air-gapped Google Cloud, gehostet von T-Systems. Google-Cloud-Partnerschaft bis **2030** verlängert. T-Systems betreibt **16 Rechenzentren** in Deutschland, rund **130 MW**, fünf weitere Standorte Ende 2024 angekündigt. |
| **9. Juni 2026** | **Sovereign Cortex with T Security**. |

---

## 2. Was Sovereign Cortex with T Security ist

Die **Cortex-Plattform für KI-gestützte Security Operations**, gebracht in die am
stärksten regulierten Branchen Europas — mit Souveränitätskontrollen, die **die Telekom
unabhängig verwaltet**.

**Enthaltene Fähigkeiten** (so in der Pressemitteilung benannt):
**SIEM** · **Threat Intelligence Platform (TIP)** · **XDR** · **Endpoint Protection
Platform (EPP)**.

**Rollenteilung:**

| Palo Alto Networks | Deutsche Telekom / T Security |
|---|---|
| Die agentische SOC-Plattform und die KI-Sicherheitstechnik | **SOC-Services** und **Identity-Management-Services** |
| | Hält die **Key-Encryption-Keys in eigenen Rechenzentren** |
| | Betreibt die **Sovereign Google Cloud Platform**, auf der die Lösung läuft |
| | Agiert als **europäischer Vertrauensanker** |

**Der technische Kern der Souveränität:** Die Telekom verwaltet die Verschlüsselung über
den **External Key Manager von Google Cloud** und hält die Schlüssel **außerhalb der
Kontrolle von Palo Alto Networks *und* Google**. Die Telekom beschreibt das als
„alleinige Hoheit über den Datenzugriff".

**Zielbranchen:** Gesundheitswesen · öffentlicher Sektor · Finanzdienstleistungen ·
Betreiber kritischer Infrastruktur.

**Regulatorik:** DSGVO · **NIS2** · **DORA** · **KRITIS**.

**Verfügbarkeit:** erste Release **Q3 2026**, zunächst begrenzt auf die genannten
Branchen, breitere Verfügbarkeit danach. **Keine Preise veröffentlicht.**

---

## 3. Die fünf Souveränitätskontrollen (Palo Altos eigenes Raster)

Palo Alto formuliert das als Rahmenwerk — nützlich, weil es die Frage „was heißt
souverän eigentlich?" in fünf prüfbare Punkte zerlegt:

1. **Datenresidenz** — Kunden- *und* Systemdaten (Telemetrie) werden in Europa
   gespeichert und verarbeitet, und nur von Personal **in der Region** abgerufen.
2. **Schlüsselverwaltung** — die Verschlüsselungsschlüssel liegen **extern** unter
   Kontrolle des Kunden.
3. **Auditierbarkeit** — Datenzugriffe werden unabhängig geprüft, protokolliert,
   sichtbar gemacht und sind auditierbar.
4. **Lokaler Betrieb** — Site Reliability Engineers und Support sitzen in Europa.
5. **Rechtsraum** — Verträge werden von einer **europäischen Rechtsperson** geschlossen
   und unterliegen **europäischem Recht**.

Die Leitidee in Palo Altos eigenen Worten: **„verifizierbare Kontrolle statt weiterer
vertraglicher Zusagen"** — Souveränität nicht als Compliance-Übung, sondern als
Konstruktionsprinzip.

---

## 4. Zitate (für Zitierbarkeit, nicht zum Vorlesen durch den Voice-Agent)

- **Helmut Reisinger**, CEO EMEA, Palo Alto Networks: Europäische Organisationen
  brauchen KI-gestützte Echtzeitsicherheit **und** verifizierbare
  Datensouveränitätskontrollen — sie sollen sich nicht entscheiden müssen.
- **Thomas Tschersich**, CEO Deutsche Telekom Security GmbH und CSO Deutsche Telekom AG:
  Das gemeinsame Angebot sei **„in dieser Qualität derzeit einzigartig in Europa"**; man
  erfülle NIS2-, DORA- und KRITIS-Anforderungen, **ohne** dass Kunden bei der Wirksamkeit
  der Cyberabwehr Abstriche machen.

⚠ Für den Voice-Agent gilt Guardrail G-3: **keine Personennamen aussprechen.** Die
Aussagen dürfen sinngemäß wiedergegeben werden („die Telekom bezeichnet …").

---

## 5. Eine Zahl aus der Pressemitteilung, die gut auf die Fläche passt

**72 Minuten** von der Erstkompromittierung bis zur Datenexfiltration — **viermal
schneller als im Vorjahr**. Das ist das beste verfügbare Argument dafür, warum
Automatisierung im SOC keine Bequemlichkeit ist: Ein rein manueller Prozess ist gegen
72 Minuten strukturell zu langsam.

---

## 6. ⚠ Was **nicht** veröffentlicht ist — relevant für unsere Demo

**Cortex AgentiX wird in der Sovereign-Cortex-Ankündigung nicht genannt.**
Die benannten Fähigkeiten sind SIEM, TIP, XDR und EPP. AgentiX (die Plattform zum Bauen,
Ausrollen und Steuern von KI-Agenten, Nachfolger von Cortex XSOAR) taucht dort **nicht**
auf.

Unser Video sagt aber im Screensharing-Teil *„Let's take a look at Cortex AgentiX"* —
innerhalb einer Demo, die durchgehend souverän gerahmt ist. Beides ist einzeln korrekt,
zusammen ist es eine **Annahme über den Funktionsumfang, die öffentlich nicht gedeckt
ist**.

Das ist kein Blocker — die Demo spielt bewusst eine nahe Zukunft (Q3 2026), und
AgentiX ist ein reales Cortex-Produkt. Aber:

- Nicht behaupten, AgentiX sei Teil des souveränen Pakets.
- Wenn ein Besucher nachfragt: *„AgentiX ist ein Cortex-Produkt; welche Komponenten im
  souveränen Paket enthalten sind, steht in der Ankündigung nur für SIEM, TIP, XDR und
  EPP. Frag am Stand nach dem aktuellen Umfang."*
- Für den Voice-Agent als eigene Karte hinterlegt (F-CTX-010).

**Ebenfalls nicht veröffentlicht:** Preise · welche konkreten Cortex-SKUs (XSIAM,
Cortex Cloud …) auf die genannten Fähigkeiten abgebildet werden · Referenzkunden ·
und ob bzw. wie das **CDC Bonn** operativ eingebunden ist — die Pressemitteilungen
erwähnen Bonn nicht. Unsere Demo-Aussage „assisted by T Security · CDC Bonn" ist
plausibel (T Security liefert laut Ankündigung die SOC-Services, und Bonn ist deren
Master SOC), aber **es ist eine Verknüpfung, die so nirgends steht**.

---

## 7. Warum das für unsere Demo genau passt

| Demo-Element | Deckung durch die Ankündigung |
|---|---|
| Universitätsklinikum | **Gesundheitswesen** ist eine der vier ausdrücklich genannten Zielbranchen |
| iMedOne auf **T Cloud Public**, Region `eu-de` | Datenresidenz Europa, Betrieb durch die Telekom |
| „assisted by **T Security** · CDC Bonn" | T Security liefert laut Ankündigung die **SOC-Services** (Bonn selbst wird nicht genannt, s. o.) |
| Modell-Policy „nur EU-gehostete Modelle" | Datenresidenz + lokaler Betrieb |
| DSGVO-Argument beim Patientendaten-Zugriff | **DSGVO, NIS2, DORA, KRITIS** ausdrücklich adressiert |
| Cortex-XSIAM-Oberfläche im Flow | **SIEM/XDR-Fähigkeiten** sind Teil des Pakets |
| Cortex AgentiX im Screensharing | **nicht gedeckt** — siehe Abschnitt 6 |

---

## 8. Quellen

**Palo Alto Networks**
- [Pressemitteilung: Advanced Sovereignty Controls for European Regulated Industries (09.06.2026)](https://www.paloaltonetworks.com/company/press/2026/palo-alto-networks-and-deutsche-telekom-bring-ai-driven-security-with-advanced-sovereignty-controls-for-european-regulated-industries)
- [Investor-Fassung derselben Meldung](https://investors.paloaltonetworks.com/news-releases/news-release-details/palo-alto-networks-and-deutsche-telekom-bring-ai-driven-security)
- [Blog: European Digital Sovereignty Starts With Trust (09.06.2026)](https://www.paloaltonetworks.com/blog/2026/06/trust-is-the-foundation-of-sovereignty/)
- [Strategische Partnerschaft mit Telekom Security (April 2020)](https://www.paloaltonetworks.com/company/press/2020/palo-alto-networks-announces-strategic-partnership-with-deutsche-telekoms-security-services-business-telekom-security)
- [Managed Secure Service Edge mit Prisma Access (September 2022)](https://www.paloaltonetworks.com/blog/2022/09/dt-launch-managed-secure-service-edge/)
- [Cortex AgentiX](https://www.paloaltonetworks.com/cortex/agentix)
- [Cortex XSIAM](https://www.paloaltonetworks.com/cortex/cortex-xsiam)

**Deutsche Telekom / T-Systems**
- [Data Sovereign Cyber Defence Managed Service (09.06.2026)](https://www.telekom.com/en/media/media-information/archive/data-sovereign-cyber-defence-managed-service-1105502)
- [T-Systems and Google Cloud Partner to Deliver Sovereign Cloud for Germany (September 2021)](https://www.telekom.com/en/media/media-information/archive/sovereign-cloud-from-t-systems-and-google-cloud-635314)
- [Ultra-secure, air-gapped Google Cloud – hosted by T-Systems](https://www.telekom.com/en/media/media-information/archive/ultra-secure-air-gapped-google-cloud-hosted-by-t-systems-1054484)
- [Sovereign Cloud Powered by Google Cloud (Produktseite)](https://www.t-systems.com/de/en/sovereign-cloud/solutions/sovereign-cloud-powered-by-google-cloud)

**Fachpresse**
- [TelecomTV — DT, Palo Alto pitch sovereign cloud cybersecurity](https://www.telecomtv.com/content/security/dt-palo-alto-pitch-sovereign-cloud-cybersecurity-55631/)
- [Telecompaper — DT partners Palo Alto Networks to offer Sovereign Cortex with T-Security](https://www.telecompaper.com/news/deutsche-telekom-partners-palo-alto-networks-to-offer-sovereign-cortex-with-t-security--1573494)
- [Telecom Review Europe — Sovereign AI Security Platform for Europe](https://www.telecomrevieweurope.com/articles/telecom-operators/palo-alto-networks-deutsche-telekom-launch-sovereign-ai-security-platform-for-europe/)
- [SDxCentral — Deutsche Telekom Taps Palo Alto Networks' Managed Security (2020)](https://www.sdxcentral.com/news/deutsche-telekom-taps-palo-alto-networks-managed-security/)
- [DCD — T-Systems and Google partner for German Sovereign Cloud project](https://www.datacenterdynamics.com/en/news/t-systems-and-google-partner-for-german-sovereign-cloud-project/)
