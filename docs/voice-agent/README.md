# Voice Agent — Security Expert (GPT Realtime)

Wissensbasis und System-Prompt für einen **sprechenden Security-Experten** auf der
T-Gallery-Fläche. Er beantwortet Besucherfragen zum **SOC / T Security**, zur
**Kooperation Deutsche Telekom × Palo Alto Networks (Sovereign Cortex)**, zum
**Telekom Agentic Hub** und zur **Demo selbst**.

> Der Nutzer nannte ihn „Advantage Hub" — im gesamten Kanon heißt er
> **Agentic Hub**. Hier durchgehend so benannt.

---

## Aufbau

```
docs/voice-agent/
  README.md              ← du bist hier: Schema, Ingest-Protokoll, Realtime-Settings
  SYSTEM_PROMPT.md       ← zum Einfügen in die Realtime-Session (instructions)
  kb/
    00-guardrails.md     ← Was NIE gesagt werden darf. Zuerst lesen.
    01-soc-t-security.md ← SOC Bonn, T Security, Zahlen
    02-cortex-palo-alto.md ← Cortex, XSIAM, AgentiX, Sovereign Cortex
    03-agentic-hub.md    ← Agentic Hub, Agent-Governance, 4D-Policy
    04-demo-and-scenario.md ← Was die Besucher gerade auf den Screens sehen
```

---

## Kartenformat

Jeder Fakt ist eine **eigenständige Karte**. Nicht zusammenhängender Fließtext — der
Realtime-Agent zieht sich sonst zufällige Halbsätze heraus.

```markdown
### F-SOC-003 · Angriffsvolumen
- **triggers:** wie viele Angriffe, Angriffsvolumen, attacks per minute, Traffic
- **say-en:** Bonn sees thirty to forty thousand attack attempts every minute. Up to
  ninety-five million a day.
- **say-de:** In Bonn sind das dreißig- bis vierzigtausend Angriffsversuche pro Minute.
  Bis zu 95 Millionen am Tag.
- **more:** Zusätzlich 70 Millionen Angriffe täglich auf die Honeypot-Systeme. Rund 800
  Botnet-Server werden pro Monat identifiziert.
- **status:** public-verified
- **source:** DT-Pressemitteilung 10.09.2024 · CR-Report 2024
```

**Feldregeln**

| Feld | Regel |
|---|---|
| `###` ID | `F-<THEMA>-<NR>`. Stabil — nie neu vergeben, nur ergänzen. |
| `triggers` | Wörter, mit denen ein Besucher danach fragen würde. DE und EN gemischt. |
| `say-en` / `say-de` | **Maximal zwei Sätze.** Zahlen ausgeschrieben, wie man sie spricht. Das ist die Antwort, keine Zusammenfassung davon. |
| `more` | Nur bei Nachfrage. Auch hier kurz. Optional. |
| `status` | `public-verified` · `public-unverified` · `internal-do-not-say` · `demo-fiction` |
| `source` | Woher. Bei `internal-do-not-say` **keine URL**, nur „intern". |

**`status` ist die wichtigste Zeile.** Der Agent darf ausschließlich
`public-verified`, `public-unverified` (mit Kennzeichnung) und `demo-fiction`
(als Demo gekennzeichnet) aussprechen. Siehe `kb/00-guardrails.md`.

---

## Ingest-Protokoll — wie du mir Infos schickst

Schick sie einfach roh. Ich brauche pro Block nur drei Dinge, damit ich sauber
einsortieren kann:

1. **Woher** — Pressemitteilung / Produktseite / Intranet / Mail / „hat mir jemand gesagt".
2. **Öffentlich oder intern?** Wenn du es nicht weißt, sag das — dann landet es auf
   `public-unverified` und der Agent sagt es nicht als Fakt.
3. **Stand/Datum**, falls bekannt. Zahlen ohne Jahr sind bei diesem Thema gefährlich —
   die SOC-Kennzahlen haben sich zwischen 2017 und 2024 um Größenordnungen verändert.

Ich mache daraus Karten, halte Widersprüche zu Bestehendem fest (statt sie zu glätten)
und sage dir, was dadurch auf die „Never-Say"-Liste muss.

**Dieses Repo ist öffentlich.** Interne Quellen kommen nicht hier hinein — ihre
Schlussfolgerungen ggf. anonymisiert, die Belege nicht. Wenn wir viele interne Fakten
brauchen, legen wir `kb/internal/` an und tragen es in `.gitignore` ein.

---

## Realtime-Session — empfohlene Einstellungen

| Einstellung | Wert | Warum |
|---|---|---|
| Modalität | Audio + Text | Text-Transkript fürs Debugging auf der Fläche |
| Turn detection | Server-VAD, eher empfindlich | Messehalle: Besucher unterbrechen, das muss gehen |
| Temperature | niedrig | Es ist ein Faktenagent. Kreativität ist hier ein Defekt. |
| Sprache | automatisch nach Besucher | DE und EN kommen beide vor |
| Max response | kurz halten | Siehe Antwortlänge unten |

**Wissenszugriff:** Bei diesem Umfang (wenige Dutzend Karten) die Karten **komplett in
die `instructions`** legen — kein RAG. Das ist billiger, schneller und deutlich
zuverlässiger als Retrieval, und es verhindert, dass eine Karte mit
`internal-do-not-say` versehentlich abgerufen wird. Erst wenn die Wissensbasis über
~15.000 Tokens wächst, lohnt sich Function-Calling gegen eine Suche.

**Antwortlänge:** zwei bis drei Sätze. Auf einer Ausstellungsfläche steht der Besucher —
er hört keinen Absatz zu Ende. Nachfragen sind erwünscht, dafür ist `more` da.
