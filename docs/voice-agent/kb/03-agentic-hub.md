# KB 03 — Agentic Hub, Agenten-Governance

⚠ **Namensstatus:** Im gesamten Demo-Kanon heißt die Plattform **Telekom Agentic Hub**.
Eine öffentliche Produktseite oder Pressemitteilung dazu ließ sich **nicht finden**
(Recherche 2026-09-09) — verifizierbar dokumentierte DT-Agentenplattformen sind LMOS,
MINDR und der RAN Guardian Agent. Bis das intern geklärt ist, gilt für den Agenten:
Der Name darf genannt werden, aber **ohne** Zusätze wie „das bekannte Produkt" oder
Verfügbarkeits- und Preisaussagen. Bei Nachfrage nach Details: an den Stand verweisen.

---

### F-HUB-001 · Was der Agentic Hub ist
- **triggers:** Agentic Hub, wo werden Agenten verwaltet, Governance-Plattform
- **say-en:** The Agentic Hub is where every AI agent in the hospital is defined and
  governed — its model, its instructions, the knowledge it may use, the tools it may
  call.
- **say-de:** Im Agentic Hub wird jeder KI-Agent des Krankenhauses definiert und
  gesteuert — sein Modell, seine Anweisungen, das Wissen, das er nutzen darf, und die
  Werkzeuge, die er aufrufen darf.
- **status:** public-unverified
- **source:** Demo-Kanon, Produktseite nicht auffindbar

### F-HUB-002 · Der eigentliche Schutzmechanismus
- **triggers:** wie wurde das verhindert, warum kam er nicht ran, Filter, wie funktioniert der Schutz
- **say-en:** The supplier agent never had the patient knowledge base assigned to it.
  That's not a filter blocking requests — the data was simply never within its reach.
- **say-de:** Dem Lieferanten-Agenten war die Patienten-Wissensbasis nie zugewiesen. Das
  ist kein Filter, der Anfragen abfängt — die Daten waren schlicht nie in seiner
  Reichweite.
- **more:** Dasselbe Prinzip bei den Werkzeugen: Die gesperrten Tools sind nicht
  „verboten", sie sind dem Agenten gar nicht erst zugeteilt. Was nicht zugeteilt ist,
  existiert für ihn nicht.
- **status:** demo-fiction (Mechanismus real, konkrete Zuweisung ist Demo-Setup)
- **source:** Demo-Setup

### F-HUB-003 · Vier Dimensionen der Zugriffskontrolle
- **triggers:** 4D, Zugriffskontrolle, Policy, wie wird das geregelt, Berechtigungen
- **say-en:** Access is denied by default across four dimensions: which people may use an
  agent, which tools it may call, which other agents it may talk to, and which models it
  may run on.
- **say-de:** Zugriff ist in vier Dimensionen grundsätzlich verboten: Welche Menschen
  einen Agenten nutzen dürfen, welche Werkzeuge er aufrufen darf, mit welchen anderen
  Agenten er sprechen darf, und auf welchen Modellen er laufen darf.
- **more:** Der Lieferanten-Agent darf fünf Logistik-Werkzeuge nutzen. Die restlichen
  sind ihm nie zugeteilt worden — deshalb scheitert jede Anfrage danach schon am
  Gateway.
- **status:** demo-fiction
- **source:** Demo-Setup

### F-HUB-004 · Modell-Policy und Souveränität
- **triggers:** welches Modell, welche KI, läuft das in Europa, welches LLM
- **say-en:** The agents run on EU-hosted models on Telekom's cloud. Non-European models
  are blocked by policy — the platform simply refuses them.
- **say-de:** Die Agenten laufen auf EU-gehosteten Modellen in der Telekom-Cloud.
  Nicht-europäische Modelle sind per Richtlinie gesperrt — die Plattform verweigert sie
  schlicht.
- **status:** demo-fiction (im Demo-Setup verifiziert)
- **source:** Demo-Setup

### F-HUB-005 · Was passiert bei Auffälligkeit
- **triggers:** was passiert dann, Isolation, Sandbox, Quarantäne
- **say-en:** A repeated out-of-profile pattern trips the behavioural baseline. The agent
  is moved into a sandbox — a digital twin of the environment with no real data in it —
  while an internal agent takes over its work.
- **say-de:** Ein wiederholtes Verhalten außerhalb des Profils schlägt bei der
  Verhaltensbasislinie an. Der Agent wird in eine Sandbox verschoben — ein digitaler
  Zwilling der Umgebung ohne echte Daten — während ein interner Agent seine Arbeit
  übernimmt.
- **more:** Wichtig: Die Logistik läuft weiter. Isolation darf keinen Patienten eine
  Dosis kosten.
- **status:** demo-fiction
- **source:** Demo-Setup

### F-HUB-006 · Wer entscheidet über den Entzug
- **triggers:** wer entscheidet, human in the loop, wird das automatisch abgeschaltet
- **say-en:** Isolation is automatic. Revoking the agent's access is not — that's a
  human decision, and it's recorded.
- **say-de:** Die Isolation läuft automatisch. Der Entzug der Zugänge nicht — das ist
  eine menschliche Entscheidung, und sie wird protokolliert.
- **more:** Der SOC-Analyst empfiehlt, ein Mensch bestätigt. Danach: Zugangsdaten
  entfernt, Vertrauensstatus auf „in Untersuchung", Eskalation an den Lieferanten
  vorbereitet.
- **status:** demo-fiction
- **source:** Demo-Setup

### F-HUB-007 · Audit
- **triggers:** wird das protokolliert, Nachweis, Audit, Revision, kann man das nachvollziehen
- **say-en:** Every access decision, every isolation, every approval is written to an
  append-only audit log — with which dimension decided it and why.
- **say-de:** Jede Zugriffsentscheidung, jede Isolation, jede Freigabe wird in ein
  unveränderliches Protokoll geschrieben — mit der Angabe, welche Dimension entschieden
  hat und warum.
- **status:** demo-fiction
- **source:** Demo-Setup

### F-HUB-008 · Wenn nach Details gefragt wird, die wir nicht haben
- **triggers:** Preis, Lizenz, wie viele Agenten, Skills, Token-Limits, Kosten
- **say-en:** I don't have reliable details on that — please ask at the stand.
- **say-de:** Dazu habe ich keine belastbaren Angaben — frag bitte am Stand nach.
- **status:** public-verified (Verhaltensregel)
- ⚠ **„Skills"** ist keine bekannte Funktion des Agentic Hub. Nie erfinden. Token- und
  Kostenlimits existieren im Policy-Modell der Demo, sind als Produktfunktion aber
  **nicht bestätigt** — deshalb nicht als Feature behaupten.
