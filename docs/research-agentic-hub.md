# Recherche — T-Systems Agentic Hub

Stand **2026-09-10**. Quellen am Ende.

> ## ⚠ Korrektur meiner früheren Aussage
> In `docs/research-telekom-soc.md` und `docs/video-soc-script.md` hatte ich notiert, der
> „Telekom Agentic Hub" ließe sich öffentlich **nicht verifizieren**. **Das war falsch.**
> Ich hatte nach „Telekom Agentic Hub" gesucht; das Produkt läuft unter
> **T-Systems** als **Agentic Hub** bzw. **T-AI Agentic Hub**. Es ist real, hat eine
> erreichbare Produktoberfläche, drei benannte Module und ein Launch-Datum.
> Die betroffenen Stellen sind korrigiert.

---

## 1. Was es ist

Eine **Orchestrierungs- und Governance-Schicht**, um KI-Agenten in Unternehmensgröße
auszurollen, zu verketten und zu steuern. Positioniert für Unternehmen und den
öffentlichen Sektor — also für regulierte, compliance-lastige Umgebungen.

- **Eigene Tagline:** *„AI Agents that Work — Delivering Real Business Impact"*
- **Launch:** **15. Juli 2026**
- **Allgemeine Verfügbarkeit:** angestrebt **Q4 2026**
- Teil des breiteren T-Systems-Stacks neben **T Cloud Public** und **Industrial AI Cloud**

Kerngedanke: Agenten sind **wiederverwendbare, komponierbare Bausteine** mit definierten
Ein- und Ausgaben, nicht Einzellösungen. Mehrere spezialisierte Agenten lassen sich zu
mehrstufigen Workflows verketten, wobei jeder Baustein Experte für seine Domäne ist.

---

## 2. Die drei Module — und warum das für uns wichtig ist

| Modul | Zweck |
|---|---|
| **Agent Studio** | Entwicklung der Agenten |
| **Agent Admin** | Governance und Policies |
| **Agent Portal** | Zugang für die Nutzer |

**Das deckt sich exakt mit `hospital-agent-demo/scenario/screen_mapping.md`**, wo seit
jeher „Studio", „Admin Console" und „Agent Portal — Approvals" stehen. Der Demo-Kanon
war also von Anfang an am realen Produkt gebaut — ich hatte ihn zu Unrecht als
unbelegt markiert.

---

## 3. Governance-Funktionen (bestätigt)

- **Nachvollziehbarkeit, Audit, menschliche Aufsicht**
- **Human-in-the-Loop für kritische Geschäftsentscheidungen** — ausdrücklich benannt
- **EU-AI-Act-Ausrichtung** über Klassifizierung, Kontrollmechanismen und
  Audit-Dokumentation.
  ⚠ Wichtige Einschränkung aus der Quelle selbst: Die Plattform **garantiert
  Compliance nicht allein** — Organisationen müssen ihre Use Cases weiterhin selbst
  klassifizieren und Risiken bewerten. Diese Ehrlichkeit sollten wir übernehmen.
- **FinOps:** Budgetzuweisung, **Ausgabenlimits**, **Kostenüberwachung pro Agent**

> ### ⚠ Zweite Korrektur
> Zur Frage „kann man Tokens und Ausgaben begrenzen?" hatte ich geantwortet, das sei
> **nicht bestätigt** und solle nicht behauptet werden. **Auch das war falsch.**
> Kostenkontrolle pro Agent inklusive Ausgabenlimits ist eine dokumentierte Funktion.
> Die ursprüngliche Formulierung des Nutzers war korrekt.

---

## 4. Offenheit und Protokolle

- **MCP (Model Context Protocol)** und **A2A (Agent-to-Agent)** werden unterstützt,
  die Plattform ist offen für weitere Standards.
  → Das **MCP Gateway** in unserer Demo hat damit eine reale Grundlage.
- Integration in bestehende Systeme und vorhandene Automatisierungswerkzeuge
- Offene Architektur für mehrere Frameworks: **LangGraph, CrewAI, AutoGen, n8n**

---

## 5. Souveränität und Modelle

- **Modelle in Deutschland auf T Cloud gehostet**; Open-Source-Modelle laufen intern,
  Daten verlassen die geschützte Umgebung nicht. Bei proprietären Modellen hängen die
  Bedingungen vom jeweiligen Anbieter ab — auch das sagt die Quelle offen.
- **Souveräne Deployment-Option:** Kunden können intern auf eigener Infrastruktur
  hosten statt cloud-only.
- **Model-Routing über T-Systems AI Foundation Services (AIFS):** Zugriff auf
  **30+ große Sprachmodelle** über eine **OpenAI-kompatible API**; Anfragen lassen sich
  nach **Kosten, Leistung, Datenschutz oder Compliance** auf das jeweils passende Modell
  routen.

**AIFS im Detail** (eigene Produktseite): Ende-zu-Ende-Plattform für maßgeschneiderte
KI-/LLM-Lösungen, läuft ausschließlich auf **T Cloud**, ausgelegt auf regulierte Branchen
(Gesundheitswesen, Versicherung, öffentlicher Sektor). Komponenten: **LLM Serving ·
AI SmartChat · RAG · Fine-Tuning**.

---

## 6. Der europäische Modell-Unterbau: Teuken-7B

Für die Souveränitätserzählung relevant, weil es zeigt, dass „europäisch" hier bis zum
Modell selbst reicht:

- **Teuken-7B** — von Grund auf in **allen 24 EU-Amtssprachen** trainiert, 7 Mrd.
  Parameter, **Apache-2.0**, veröffentlicht 26.11.2024.
- Entstanden im **EU-Projekt OpenGPT-X**, gefördert vom **BMWK**, Konsortium unter
  Führung der **Fraunhofer-Institute IAIS und IIS** mit TU Dresden, DFKI und
  Forschungszentrum Jülich; trainiert auf dem Jülicher Supercomputer **JUWELS**.
- Rund **50 % nicht-englische Trainingsdaten** aus 23 europäischen Ländern.
- **Die Deutsche Telekom war der erste Anbieter, der Teuken-7B kommerziell angeboten
  hat** — Forschung in Produkt überführt.

---

## 7. Sven Giesselbach

Öffentlich dokumentiertes berufliches Profil (keine Kontaktdaten, keine privaten Angaben).

- **Rolle:** In einem T-Systems-Fachbeitrag vom **17.03.2026** als **CTO der AI-&-Data-Unit
  bei T-Systems International** ausgewiesen. Andere öffentliche Quellen führen ihn als
  **Senior Advisor AI & Agentic Solutions, T-Systems International** (Siegburg).
  ⚠ Die beiden Titel widersprechen sich; welcher aktuell ist, sollte vor einer Nennung
  geklärt werden. Schreibweise beruflich durchgehend **Giesselbach** (nicht „Gießelbach").
- **Vorher:** Aufbau und Leitung des Teams **Natural Language Understanding am
  Fraunhofer IAIS**, fünf Jahre, über 30 KI-Projekte in öffentlichem Sektor,
  Gesundheitswesen und Recht. Master Informatik, Universität Bonn, 2014. Promotion zu
  einer Projektmethodik für Data-Science-Projekte mit Foundation Models.
- **Zugehörigkeiten:** **Lamarr-Institut**, **OpenGPT-X**.
- **Publikation:** Mitautor von *„Foundation Models for Natural Language Processing"*
  (Paaß/Giesselbach, Springer).
- **Öffentliche Auftritte:** Podcast *Das Gelbe vom AI* Folge 64 („Vom Fraunhofer-Labor
  zu T-Systems … über Teuken und KI-Souveränität", 35 min) · Sprecher **KI.Summit 2026**
  (Fraunhofer IAO), Thema „AI & Agentic Solutions" · Rise of AI · Deutscher
  Kommunalkongress.
- **Themen, die er öffentlich vertritt:** sichere KI-Angebote auf der Open Telekom Cloud,
  Teuken-7B und europäische KI-Souveränität, Kombination aus **Fine-Tuning und RAG**,
  Einsatz in regulierten Branchen.

---

## 8. Sein Gesundheits-Beitrag — die direkte Parallele zu unserer Demo

Fachbeitrag **„Wenn KI im Schockraum mitdenkt"** (T-Systems, 17.03.2026, Autor
Giesselbach). Inhaltlich fast eine Schwesterdemo zu unserer:

- **Projekt:** KI-Unterstützung im **Schockraum**. Start **September 2025**. Partner:
  **Deutsche Telekom, Fraunhofer IAIS, Krankenhaus Merheim (Köln)**. Förderung über das
  EU-Programm **IPCEI-CIS**. Training an realistischen Trauma-Simulationen.
- **Funktion:** transkribiert die Gespräche des Schockraum-Teams in Echtzeit,
  strukturiert sie entlang des **ABCDE-Schemas**, senkt die kognitive Last bei
  „Information Bursts", automatisiert die Dokumentation für Qualitätsregister und zeigt
  dem Team eine strukturierte Statusansicht.
- **Architektur:** **Cloud-Edge-Continuum** — die KI läuft **lokal im Krankenhaus,
  vollständig offline lauffähig**, angebunden an eine souveräne europäische Cloud für
  Skalierung und Modelltraining.
- **„Talk to your data":** komplexe Analysen, die früher bis zu **sechs Stunden**
  dauerten, gelingen in **unter einer Stunde**.
- **Magenta Health AI Box:** souveräne KI-Plattform für Krankenhäuser und Krankenkassen —
  AI Receptionist, Patient Summary, Datenintegration, T-Cloud-Infrastruktur, modulare
  Automatisierungs- und Entscheidungsbausteine, DSGVO-konform.
- **Infrastruktur:** T Cloud mit **10.000 NVIDIA-GPUs der Blackwell-Generation**;
  der Schockraum-Agent läuft auf **NVIDIA DGX Spark**.
- **Sein Satz, der auch über unserer Demo stehen könnte:** *„KI im Schockraum darf kein
  Black-Box-Experiment sein. Sie muss erklärbar, robust und verlässlich funktionieren."*
  Und: die Technologie müsse sich den klinischen Abläufen anpassen, nicht umgekehrt.

---

## 9. Was das für unsere Demo ändert

| Bisher | Jetzt |
|---|---|
| „Agentic Hub nicht verifizierbar" | **Real**, T-Systems, Launch 15.07.2026, GA Q4 2026 |
| Studio/Admin/Portal = Demo-Erfindung | **Reale Modulnamen** (Agent Studio · Agent Admin · Agent Portal) |
| MCP Gateway = Erzählmittel | **MCP wird real unterstützt**, ebenso A2A |
| Kosten-/Token-Limits „nicht behaupten" | **Reale FinOps-Funktion** — Budgets, Ausgabenlimits, Kosten pro Agent |
| Modellpolitik = Demo-Setup | **AIFS-Model-Routing** über 30+ Modelle nach Kosten/Datenschutz/Compliance ist real |
| — | **EU AI Act** kommt als Compliance-Rahmen dazu — bisher nirgends im Kanon |

**Benennung:** Das Produkt gehört zu **T-Systems**. „Agentic Hub" oder
„T-AI Agentic Hub" sind belegt; **„Telekom Agentic Hub"** (so im hospital-agent-demo-Repo)
ist es nicht wörtlich. Für den Sprechertext ist **„the Agentic Hub from T-Systems"** die
saubere Formulierung — genau so, wie der Nutzer es ursprünglich vorgeschlagen hatte.

**Noch offen:** ob „Skills" eine Funktion ist (weiterhin **kein** Beleg) · Preise ·
ob der Hub im Gesundheitswesen bereits produktiv eingesetzt wird · das Verhältnis
zwischen Agentic Hub und der **Magenta Health AI Box**.

---

## 10. Quellen

- [Agentic Hub — Produktoberfläche T-Systems](https://ui.pre-sales.agentichub.ai.t-systems.net/)
- [T-Systems: AI Foundation Services](https://www.t-systems.com/de/en/artificial-intelligence/solutions/ai-foundation-services)
- [T-Systems: Was ist agentische KI](https://www.t-systems.com/de/de/kuenstliche-intelligenz/was-ist-agentische-ki)
- [T-Systems: Industrial AI Cloud](https://www.t-systems.com/de/en/artificial-intelligence/solutions/industrial-ai-cloud)
- [Giesselbach: Souveräne KI für das Gesundheitswesen — „Wenn KI im Schockraum mitdenkt" (17.03.2026)](https://www.t-systems.com/de/de/insights/newsroom/experten-blogs/wenn-ki-im-schockraum-mitdenkt-1149822)
- [La Ecuación Digital: T-Systems lanza una plataforma soberana para gestionar agentes de IA (15.07.2026)](https://www.laecuaciondigital.com/tecnologias/inteligencia-artificial/t-systems-plataforma-soberana-ia-agentica/)
- [Telekom: From six hours to 60 minutes — AI agent accelerates analysis work](https://www.telekom.com/en/media/media-information/archive/from-six-hours-to-60-minutes-ai-agent-accelerates-analysis-work-1103316)
- [Telekom: OpenGPT-X Language Model „Made in Germany"](https://www.telekom.com/en/media/media-information/archive/opengpt-x-language-model-made-in-germany-1084484)
- [Fraunhofer IAIS: OpenGPT-X veröffentlicht Teuken-7B (26.11.2024)](https://www.iais.fraunhofer.de/en/press-events/press-releases/press-release-241126.html)
- [Teuken-7B Model Card (Hugging Face)](https://huggingface.co/openGPT-X/Teuken-7B-instruct-commercial-v0.4)
- [Podcast „Das Gelbe vom AI" #64 mit Dr. Sven Giesselbach](https://das-gelbe-vom-ai.webflow.io/episode/64-vom-fraunhofer-labor-zu-t-systems-dr-sven-giesselbach-uber-tolken-und-ki-souveranitat)
- [KI.Summit 2026, Fraunhofer IAO — Sprecherliste](https://www.iao.fraunhofer.de/de/veranstaltungen/2026/ki-summit-2026.html)
- [Foundation Models for Natural Language Processing (Paaß/Giesselbach, Springer)](https://www.amazon.de/Foundation-Models-Natural-Language-Processing/dp/3031231899)
