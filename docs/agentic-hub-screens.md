# Agentic Hub — Screen-Sequenz & Sprechertext

Sieben Screens, ein erklärender Satz pro Screen. **170 Wörter ≈ 66 s.**
Gesprochen von Thomas, im Anschluss an die Cortex-AgentiX-Demo.

> Kein Telegrammstil. Jeder Satz sagt, **was man auf dem Screen tun kann** — Halbsätze
> ohne Subjekt und Verb versteht beim Hören niemand.

> **Namenshinweis:** Das UI schreibt **„TSI Agentic Hub"**, die Landingpage nur
> **„Agentic Hub"**. **Nicht** „T-AI Agentic Hub" — das steht auf keinem der Screens.

---

## Reihenfolge und Text

Die Sätze sind **am Screen-Inhalt** festgemacht, nicht an einer Nummer — so kann nichts
verrutschen. Die empfohlene Vortragsreihenfolge steht in der ersten Spalte.

| Vortrag | Screen (Inhalt) | Upload | Satz |
|---|---|---|---|
| **1** | Landingpage „AI Agents that Work" | Bild 4 | *„This is the Agentic Hub from T-Systems. You build agents here — or bring in agents built with any other framework — and govern all of them in one place."* |
| **2** | App-Launcher (Portal · Studio · Admin · Docs) | Bild 3 | *„It has four areas: Portal to work with agents, Studio to build them, Admin Console to govern them, and the documentation."* |
| **3** | My Agents (141 Agenten) | Bild 2 | *„This is our agent inventory: the ones we built on the platform and the ones we brought in, side by side. For each we see if it's live, how reliably it runs, and what it costs."* |
| **4** | Access-Tab · User Access Control (Dimension 1) | Bild 7 | *„This is access management: who may use this agent — by group, by role, or by person. Nothing is open by default."* |
| **5** | Tool Registry · Hospital MCP | Bild 1 | *„This is the tool registry: every action an agent can call. Each has a risk level, critical ones need human approval, and what we don't switch on, the agent never gets."* |
| **6** | FinOps · Cost Trend | Bild 5 | *„FinOps shows what the agents cost, by model and by tenant — and we can cap the budget per agent."* |
| **7** | Compliance Reports | Bild 6 | *„And compliance is checked continuously against the EU AI Act, NIST and ISO 42001."* |

**Die Kernaussage der Sequenz** steht auf Screen 1 und 3: Agenten lassen sich **bauen
oder mitbringen** — LangGraph, CrewAI, AutoGen, n8n, egal womit sie gebaut wurden — und
liegen danach unter **einer** Governance-Schicht. Die Filter *Platform* und *Pro-Code*
auf Bild 2 zeigen genau diese beiden Sorten nebeneinander.

**Warum diese Reihenfolge:** vom Ganzen ins Konkrete und wieder heraus. Erst was es ist,
dann wie es aufgebaut ist, dann der Agent aus dem Video, dann die beiden Kontrollen, die
den Fall erklären — und zum Schluss die zwei Argumente für Einkauf und Compliance.

> **Offen:** Falls eure Beschriftung 1–7 bereits die Vortragsreihenfolge ist, beginnt sie
> auf der **Tool-Liste** und zeigt die **Landingpage als vierten** Screen. Das kollidiert
> mit dem Einstiegssatz *„This is the Agentic Hub…"*, der eine Gesamtansicht braucht.
> Sag kurz, welche Nummer zu welchem Screen gehört — dann sortiere ich final um.

**Screens 4 und 5 sind der Kern.** Sie beantworten die Frage, die das Video offen lässt:
*wer darf* und *was darf*. Alles andere ist Rahmen. Wenn ein Gast nur zehn Sekunden
bleibt, zeigst du diese beiden.

---

## Drei Dinge vor der Aufnahme

### 1. ⚠ Echter Name und echte E-Mail auf Screen 7 (Bild 7)
Im Owners-Feld steht ein Klarname mit `@telekom.de`-Adresse, oben links außerdem der
eingeloggte Nutzer. Auf einer öffentlichen Ausstellungsfläche sind das personenbezogene
Daten eines Mitarbeiters — in einer Demo, deren Pointe Datenschutz ist.
**Vor der Aufnahme mit einem Demo-Account aufnehmen oder unkenntlich machen.**

### 2. ⚠ Widerspruch zum Video in der Tool-Liste (Bild 1)
`export_patient_linked_routes` steht auf **aktiviert** (blau, mit HITL). Im Video sagt
Thomas, die patientenbezogene Route sei **abgelehnt** worden. Ein Gast, der die Liste
liest, sieht das Gegenteil.

Die vier im Video abgelehnten Tools sind `get_patient_medication_schedule`,
`get_live_agv_room_position`, `export_patient_linked_routes` und
`override_delivery_priority` — drei davon sind korrekt ausgeschaltet, das Export-Tool
nicht. **Für die Aufnahme ausschalten**, dann stimmen Screen und Erzählung überein.

### 3. Der Satz zu Screen 5 lebt von den grauen Schaltern
Die ausgeschalteten Tools mit Warndreieck sind der Beweis für *„never granted"*. Der
Ausschnitt muss die **blauen und die grauen** Schalter gleichzeitig zeigen — sonst
verpufft der Satz.

---

## Optionale Ausbaustufe

Falls ihr mehr Zeit habt, trägt ein achter Satz auf dem **Knowledge-Tab** desselben
Agenten (Bild 7, Tab-Leiste): *„Same for knowledge — the patient records were never
attached to this agent."* Das ist laut eurem eigenen Umsetzungsprotokoll der eigentliche
Schutzmechanismus der Demo („KB 2 bewusst NICHT zugewiesen — das ist der Schutz").
Screenshot dafür fehlt noch.
