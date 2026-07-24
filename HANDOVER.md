# Übergabe / Handover — Cortex Hospital Demo (T Gallery)

_Stand: 2026-07-24 · Branch `claude/cortex-demo-handover-0tpnha` · Build verifiziert (keine JS-Fehler, Zahlen konsistent)_

> Dieses Dokument ist die **Übergabe an die Agentur**. Es erklärt in Deutsch, **was das
> Projekt ist, wie man es ansieht und wie man daran weiterarbeitet.** Die vollständige
> technische Design-Spezifikation liegt in **`CLAUDE.md`** (Englisch) — das ist die
> „Bibel" des Projekts und **Pflichtlektüre vor jeder Code-Änderung.**

---

## 1. Was ist das? (in einem Absatz)

Eine **cinematische, interaktive Security-Operations-Demo** in der visuellen Sprache von
Palo Alto Networks **Cortex XSIAM 3.0** (dunkel, leuchtend, animiert), inhaltlich adaptiert
auf ein **generisches großes Uniklinikum** (~1.300 Betten, Forschung + globale Kooperationen)
und mit Deutsche-Telekom-**T-Security**-Branding gerahmt.

Sie ist gebaut für die **T Gallery** (Ausstellungsraum der Deutschen Telekom) und läuft dort
auf einem Laptop oder einer großen Wand. Es ist **kein Produkt und keine PowerPoint**, sondern
ein **design-getriebenes Erlebnis** — der Look zählt genauso viel wie der Inhalt. Alle Daten
sind **fiktiv, aber in sich stimmig und fachlich korrekt**.

**Technisch:** eine einzige, in sich geschlossene `index.html`. Kein Build-Schritt, keine
Frameworks, keine Netzwerkaufrufe. **Läuft offline** — Datei doppelklicken genügt.

---

## 2. WICHTIG ZUERST — welcher Branch / welcher Stand ist „die Demo"?

Das Repo enthält aus dem Entwicklungsprozess **mehrere experimentelle Branches**. Damit sich
niemand in einem alten Stand verirrt:

- ✅ **Dieser Branch — `claude/cortex-demo-handover-0tpnha` — ist der aktuelle, vollständige
  Build PLUS diese deutsche Übergabe.** Wenn die Agentur genau diesen Branch klont, hat sie
  alles: die fertige Demo und die Doku. **Empfehlung: mit diesem Branch starten.**
- Der ursprüngliche „kanonische" Entwicklungs-Branch ist `claude/flow-layout-21-9-ivhesc`
  (identischer Build). Die `CLAUDE.md`-Kopfzeile nennt ihn als Referenz — das ist historisch
  und in Ordnung.
- ⚠️ **Ältere Parallel-Linie (NICHT verwenden):** `cdc-case-numbers`, `cdc-cases-command-center`,
  `issues-cases-flow-refine`, `cortex-xsiam-research`. Diese zeigen einen älteren Stand
  (nur 1440-Layout, kein 32:9-Flow, kein Agent Resolution Center). Woran man den falschen
  Branch erkennt: kein „Inspect ›"/Resolution Center, deutlich schmaleres Layout.
- `main` enthält derzeit einen **älteren Upload-Stand**, nicht die fertige Demo.

> **Empfehlung an den Auftraggeber:** Vor der Weitergabe den aktuellen Build auf `main`
> konsolidieren, damit die Agentur beim reinen `git clone` ohne Branch-Wissen sofort die
> richtige Demo sieht. Details siehe Abschnitt 9.

---

## 3. Demo ansehen & starten (keine Installation nötig)

Alle drei Wege zeigen dasselbe. Empfohlener Browser: **Chrome/Edge** (aktuell).

| Weg | Befehl / Aktion | Ergebnis |
|-----|-----------------|----------|
| **Offline (am einfachsten)** | `index.html` doppelklicken | Läuft direkt im Browser, kein Server |
| **Lokaler Server (Python)** | `python3 -m http.server 8000` | http://localhost:8000 |
| **Lokaler Server (Node)** | `npm start` | http://localhost:3000 |

Für die **Ausstellung** ist das Zielformat ein **32:9-Ultrawide** (iiyama ProLite XCB4594DQSU,
5120×1440). Die Demo skaliert sich automatisch auf die Fenstergröße — für die beste Wirkung im
Vollbild (F11) auf einem breiten Monitor zeigen.

---

## 4. Was man sieht — zwei Views, ein State-Machine-Flow

Die Navigation ist eine kleine Zustandsmaschine: `showView('assets' | 'flow')`.

### 4.1 Assets Command Center (Einstiegsbild, 16:9)
Zentrales Radar, organisiert **nach Standort** (nicht Abteilung): **Main Campus** dominant oben,
Satelliten drumherum (Outpatient Centers, T Cloud Public, Telemedizin & Home, Reference Labs,
Research Institute). Links der **iMedOne®**-Anker (echtes Telekom-Krankenhausinformationssystem).
Vier verschachtelte **Buckets** (Alle ⊃ At Risk ⊃ Active Threats ⊃ At Risk+Threats) tönen das
Radar um und zählen die Mitte hoch. Ein **magentafarbener Radar-Sweep** streicht über das Feld.
Klick auf einen Standort → Detail-Slide-in. **`Show Issues ›`** → wechselt in den Flow.

### 4.2 Issue-Cases Flow (Hauptpipeline, 32:9)
Links → rechts: **Sources** (Klinik-Systeme) → Partikelströme durch geschwungene Ribbons →
zentraler **Correlation Core** (konzentrische Ringe, Zahlen zählen hoch) → **Cases** → rechts
die **Live Queue** offener Fälle. Oben rechts ein **24H ⇄ 30D**-Umschalter, der den ganzen Flow
tauscht.

Im **24H**-Modus öffnen die drei Achsen-Anker jeweils eine **eigene Drill-down-Overlay** (`.dv`,
mit `‹ Flow`-Zurück und Esc):
- **Issues → Data Inventory** (gruppierte Quellen + Volumen/Sparklines)
- **Correlation Core → Dynamic View** (Automations-Donut + orbitale Quellenmarken + Live-Feed)
- **Cases → Cases Overview** (Lifecycle-Funnel + Handling-Bars + MITRE ATT&CK nach Taktik)

Im **30D**-Modus öffnet die Mitte die **Prioritization**-Overlay.

### 4.3 Das Kern-Szenario: Agent-Drift → Agent Resolution Center
Klick auf den **leeren Flow-Hintergrund** löst das **Agent-Drift-Szenario** aus: ein **roter
Licht-Glow** wandert über den Flow, und oben in der Live Queue erscheint ein neuer **kritischer
Fall** — *„Supplier agent · out-of-profile data request"* (C-4490), *„auto-contained by policy"*.
Dessen **`Inspect ›`** öffnet das **Agent Resolution Center** (`openAgent()`): die polierte
Kern-Szene mit Case-Header, einem **AI-Orchestration-Agents**-Graph (Lieferanten-Agent → Scoped
API-Gateway → Delivery/Stock → Route- & Traffic-Control) mit animierten Partikeln, einer
**AGV-Schiene** (fahrende Medikamenten-Transportroboter) und einem **Resolution-Center**-Panel.
Zwei manuelle Aktionen (**Isolate**, **Revoke**) treiben eine 1→2→3-Zustandsmaschine.
Dies ist die eigentliche Telekom-Agentic-Hub-Governance-Story.

---

## 5. Repo-Struktur

| Pfad | Was |
|------|-----|
| **`index.html`** | Die komplette Demo (HTML + CSS + JS + inline SVG, alles in einer Datei). **Hier wird editiert.** |
| **`CLAUDE.md`** | Vollständige technische Design-Spezifikation (EN): Zahlenmodell, harte Design-Regeln, „Tuning Map" (wo welche Stellschraube im Code liegt). **Vor jeder Änderung lesen.** |
| **`HANDOVER.md`** | Dieses Dokument (DE) — Übergabe / Onboarding. |
| **`README.md`** | Kurzer Repo-Einstieg. |
| **`docs/`** | Marken/Logos: `tsec-logo-white.svg` (echtes Telekom-T), Cortex-Mark, PAN-Logo, iMedOne-Wordmark, Vendor-Logos (M365/Azure/Google/GitHub, als webp). |
| **`reference/`** | Ursprüngliche Cortex-Command-Center-Optik als Look-Referenz. |
| **`package.json`** | Nur die zwei Serve-Skripte (`start`/`dev`). Keine Dependencies. |

---

## 6. Design-Regeln — **NICHT verhandelbar** (bitte an die Agentur weitergeben)

Diese Regeln sind der Grund, warum die Demo funktioniert. Ein früherer Umbau in ein „dichtes
Boxen-Diagramm" wurde als *„beschissene PowerPoint"* verworfen. Also:

1. **Cortex-Ästhetik halten:** fast-schwarzer Hintergrund, **Teal `#2fd6c0`** als Primärglühen,
   fließende SVG-Ribbons, Partikelschwarm, radiale/orbitale Layouts, weiche Schatten. Der Core
   muss **klar & farbig** lesen, nicht vernebelt.
2. **KEIN dichtes „Boxen-in-Bändern"-Architekturdiagramm.** Detail-Ansichten bleiben **reduziert**
   (wenige leuchtende Knoten, viel Negativraum).
3. **Es ist ein geführter Flow, keine Folie** — Szenen mit Übergängen und Interaktion.
4. **Telekom-Magenta `#E20074` ist nur Akzent** (T-Security-Branding, iMedOne + T Cloud, Radar-
   Sweep, ein Magenta-Partikelstrang). **Teal bleibt primär.**
5. **Alignment ist Pflicht.** Jedes Label, Icon, Badge, jeder Wert **vertikal zentriert** mit
   seiner Zeile; Spalten fluchten. Vor jedem Commit per Screenshot prüfen. Schiefe Elemente sind
   ein harter Defekt — nicht ausliefern.
6. **Animation ist LANGSAM**, klare Links-nach-rechts-Choreografie. `prefers-reduced-motion` wird
   respektiert (alle Count-ups/Partikel springen dann sofort in den Endzustand).
7. **Souveränität:** Klinik-/Klinische Systeme sind die Primärquellen; **T Cloud Public bleibt
   magenta/souverän und wird nie durch einen Hyperscaler ersetzt oder überrangt.** Vendor-Logos
   erscheinen nur als untergeordnete graue Drittquellen (Data Inventory + Dynamic View).

---

## 7. Nur echte Namen — **„dont invent shit"**

Es dürfen **keine Produktnamen erfunden** werden. Verwendet (und beizubehalten) sind ausschließlich:

- **iMedOne®** — echtes Telekom-Krankenhausinformationssystem (HIS).
- **T Cloud Public** — Hosting für iMedOne + Cloud-Standort/-Quelle.
- **T Security** — DT-Security-Arm im *Sovereign Cortex with T Security* (PANW + DT). Header-Brand + assistierender SOC.
- **Cyber Defense Center (CDC) Bonn** — echtes DT-Cyber-Defense-/Security-Operations-Center (größtes in Europa). Der assistierende SOC.
- **Magenta Security** — DT-*Endkunden*-MDR-Produktlinie. In dieser souveränen Rahmung **bewusst nicht** on-screen.

On-screen-SOC-Tag: **„assisted by T Security · Cyber Defense Center Bonn"**.
Das Krankenhaus bleibt generisch **„Main Campus"** — **kein** realer Klinikname im UI.

> Vor jeder öffentlichen Vorführung Produktstatus neu verifizieren (telekom.com / paloaltonetworks.com).

---

## 8. Das Zahlenmodell (einzige Wahrheitsquelle — alles muss zusammenpassen)

Wenn eine Zahl geändert wird, **müssen** ihr Detail-Popover in `detailHTML()` und jede Mini-Legende
mitgezogen werden. Kurzfassung (Vollmodell in `CLAUDE.md`):

- **Assets (verschachtelt):** Alle **35.600** ⊃ At Risk **5.840** ⊃ Active Threats **84** ⊃
  At Risk+Threats **29**. Standorte summieren auf 35.600 (Campus 30.200 · Outpatient 2.100 ·
  T Cloud 1.760 · Telemedizin 640 · Labs 520 · Research 380). Data Ingestion **9 TB/24H**.
- **Flow 24H:** **2.412** Issues → **96** Cases (**78** Automated / **18** Manual → **85**
  Resolved / **11** Open). (Drift-Szenario: 11 → **12** offen, transienter Demo-Zustand.)
- **Flow 30D:** **148K** → **34K** unique → **312** Cases; MTTR **26 Tage**; Prioritization
  148K → 34K → 4,8K → 312 (99,8 % Reduktion).

_(In der heutigen Verifikation stimmten alle sichtbaren Zahlen mit diesem Modell überein.)_

---

## 9. Weitergabe an die Agentur — konkret

Der Auftraggeber (Repo-Eigentümer) macht das Repo per **GitHub-Collaborator-Einladung** zugänglich:

1. GitHub → `roitsch-code/cortex-hospital-demo` → **Settings → Collaborators** (ggf. „Manage access").
2. **Add people** → GitHub-Benutzernamen oder E-Mail der Agentur eingeben → Rolle wählen
   (**Write** zum Mitentwickeln, **Read** nur zum Ansehen) → einladen.
3. Die Agentur nimmt die E-Mail-Einladung an und klont dann:
   ```bash
   git clone https://github.com/roitsch-code/cortex-hospital-demo.git
   cd cortex-hospital-demo
   git checkout claude/cortex-demo-handover-0tpnha   # aktueller Build + diese Doku
   open index.html                                    # oder: python3 -m http.server 8000
   ```
4. Erste Lektüre für die Agentur: **dieses `HANDOVER.md`**, danach **`CLAUDE.md`**.

**Empfohlene Aufräum-Option (optional, sauberster Handover):** den aktuellen Build auf `main`
bringen, damit ein reines `git clone` ohne Branch-Wissen sofort die richtige Demo zeigt, und die
alten Parallel-Branches archivieren/löschen. Das reduziert Verwirrung durch die vielen `claude/*`-
Branches erheblich. (Auf Wunsch übernehmen wir diese Konsolidierung.)

---

## 10. Weiterarbeiten — Checkliste vor jedem Commit

- **Nur `index.html` editieren.** Positionen sind für 1440×810 (Assets/Overlays) bzw. 2880×810
  (Flow) **von Hand gesetzt** — nach jedem Layout-Edit **neu screenshotten**.
- **Verifizieren** (siehe `CLAUDE.md` › „Verifying a change"):
  1. `<script>` extrahieren und `node --check` — **keine Syntaxfehler**.
  2. Serven (`python3 -m http.server 8000`) und mit Playwright screenshotten (Chromium unter
     `/opt/pw-browsers/`, Viewport 1440×810 / 2880×810, deviceScaleFactor 2). Assets-View, 24H-Flow,
     30D-Flow und jedes berührte Popover prüfen. **`pageerror` mithören — es dürfen KEINE JS-Fehler
     auftreten** (der favicon-404 in der Konsole ist harmlos).
  3. Zahlen gegen das Modell prüfen, keine erfundenen Produktnamen.
- **Git:** auf dem vereinbarten Branch entwickeln; Push mit `-u origin <branch>`, bei Netzfehlern
  mit Backoff wiederholen. **Keine PR ohne Aufforderung.** Commit-Footer siehe `CLAUDE.md` (Git).
- Kein Modell-Identifier in Commits/PRs/Code oder anderen gepushten Artefakten.

---

## 11. Offene Punkte / Ideen (nicht gebaut)

- **Logos:** Vendor-Marken liegen als Raster-`.webp` inline vor. Für vektor-perfekte Marken echte
  `.svg` in `docs/` ablegen und `LOGO` umbiegen. `docs/imedone.png` (echtes Wordmark) ist als
  optionaler Ersatz für das CSS-iMedOne vorhanden.
- Produkt-/Markenstatus (Telekom/PANW) vor jeder öffentlichen Vorführung neu prüfen.
- Optional: Konsolidierung auf `main` + Bereinigung der Alt-Branches (siehe Abschnitt 9).

---

_Detaillierte technische Referenz: **`CLAUDE.md`** (Englisch). Bei Fragen zum Handover an den
Auftraggeber wenden._
