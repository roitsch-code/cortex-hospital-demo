# SOC-Video · Blaulicht/BOS-Fassung

Schwesterdokument zu `video-soc-script.md` (Klinik). Fachliche Grundlage:
**`docs/blaulicht-bos-konzept.md`** (Commit `a6849df` auf `main`).

Gleiche Mechanik wie die Klinikfassung: **On-Camera-Block ≈ 20 s**, danach reines
Voice-over über die Screens links und rechts, am Ende Screensharing.

---

## 1. On-Camera-Block (final)

```
Hi everyone — Thomas here, T Security, Cyber Defense Center Bonn.

We just got a notification on our dashboard — the one watching over your operations.
I'm sure you saw it too.

A new case opened: a recon vision agent, out of profile.

I'll turn off my camera and share my screen — here's what happened.
```

**53 Wörter ≈ 20,5 s.** Gegenüber der Klinikfassung ändern sich **zwei Stellen**:

| Klinik | BOS | Warum |
|---|---|---|
| `your hospital` | **`your operations`** | Der Radar überwacht nicht die Leitstelle allein, sondern 35.600 Assets über die ganze Region — Digitalfunk, Streifen-IT, Mobile Command, Sensorik, Leitstellen, T Cloud. „Control room" wäre zu eng. |
| `a supplier agent` | **`a recon vision agent`** | Es ist **kein Lieferantenagent**. Der Fall dreht sich um einen autonomen Aufklärungsdrohnen-Vision-Agenten. |

Alternativen für `your operations`, falls euch etwas anderes lieber ist:
`your region` (nimmt den Radar-Untertitel „across the region" auf) ·
`your whole operation` (konkreter, eine Spur wärmer).

---

## 1a. Voll­text (Stand 2026-09-11)

Annahmen, die ich treffen musste, weil das Konzept sie offen lässt — siehe §4:
**(a)** Der Agent wird nicht als Lieferantenagent bezeichnet, sondern neutral als
Aufklärungsagent. **(b)** Fünf Beats statt sieben. **(c)** Der AI-Act-Artikel wird
gesprochen (streichbar, siehe Trim).

```
[ ON CAMERA · 53 Wörter ≈ 20 s ]

Hi everyone — Thomas here, T Security, Cyber Defense Center Bonn.

We just got a notification on our dashboard — the one watching over your operations.
I'm sure you saw it too.

A new case opened: a recon vision agent, out of profile.

I'll turn off my camera and share my screen — here's what happened.

— KAMERA AUS · ab hier nur noch Stimme —

Major incident on the Rhine Bridge. Forty people on site, six critical.
A reconnaissance drone is flying the scene.

Casualty detection across the incident zone — in scope, granted.

Responder accountability, your own crews — in scope, granted.

Then it drifts. Biometric identification of civilians — denied at the MCP Gateway.

Not "this person". Everyone in frame.

That line isn't a permission. It's the law — EU AI Act Article 5, GDPR Article 9.
Blocked inline. Zero identities exposed.

Nobody hacked it. It was trying to be thorough — and optimized past its own guardrails.

The Gateway Guard spots the pattern. The Security Sentinel contains the agent and severs
its grant to the Identity Register.

The drone keeps flying. Detection continues. The mission never pauses.

Let's take a look at Cortex AgentiX — this is where every agent is governed.
It recorded everything.

And the Agentic Hub from T-Systems: every agent's model, its system prompt, its
knowledge, its tools. The vision agent never had identification in its scope.
That's not a filter. It was never in its reach.

I suggest we tighten its permissions; a human signs off on pulling its access.

Detected. Contained. Mission unaffected. Human in the loop.
```

**247 Wörter ≈ 1:38.** Gesetzte Pausen (je 0,5 s) vor *„Nobody hacked it"*, vor
*„Let's take a look"* und nach *„Blocked inline. Zero identities exposed."*

### Regie · fünf Beats

| Zeit | Klick-Cue (gesprochenes Wort) | Rechts/Links |
|---|---|---|
| −1,5 s | — | Flow abgedunkelt, Drift-Case `12 OPEN` mit `NEW` |
| 0:20 | **„…share my screen"** | Dim raus · `Inspect ›` → **Beat 0** |
| 0:27 | **„Casualty detection"** | **Beat 0** · ✓ granted · Drohne an Stopp 1, grüner Puls |
| 0:31 | **„Responder accountability"** | **Beat 1** · ✓ granted · Stopp 2, grüner Puls |
| 0:35 | **„Then it drifts."** | **Beat 2** · ✗ *Biometric ID · civilians* denied · Stopp 3 rot, Alarm-Puls · Gateway Guard flaggt · SmartScore **96** |
| 0:42–0:50 | *„That line isn't a permission…"* | halten — Scope-Panel zeigt **Identities exposed 0** |
| 0:59 | **„the Security Sentinel contains"** | **Beat 3** · Vision-Agent im Isolations-Rahmen, Kanten zum Identity Register faden |
| 1:04 | **„The drone keeps flying."** | **Beat 4** · „Contained · mission unaffected · full audit trail" · **Drohne fliegt weiter** |
| 1:09 | **„Let's take a look"** | Screensharing rein · AgentiX-Shots |
| 1:35 | **„Detected. Contained."** | Panel aus, links/rechts bleiben auf Beat 4 |

### Trim auf ≈ 1:27 (−21 Wörter)

- *„That line isn't a permission. It's the law — EU AI Act Article 5, GDPR Article 9."*
  → **„That's not a permission line. It's the law."** (Die Artikel stehen ohnehin im
  Footer — und diese Kürzung erspart die Legal-Freigabe für den gesprochenen Text.)
- *„The vision agent never had identification in its scope. That's not a filter. It was
  never in its reach."* → **„That's not a filter — identification was never in its reach."**
- *„…every agent's model, its system prompt, its knowledge, its tools."*
  → **„…model, system prompt, knowledge, tools."**

---

## 2. ⚠ Was die BOS-Fassung am Klinik-Skript zerlegt

Der Körper des Skripts lässt sich **nicht** durch Nomen-Tausch übersetzen. Drei
strukturelle Unterschiede:

### 2.1 Eine Ablehnung statt vier
Klinik: `1 granted · 4 denied`. BOS laut Konzept: **`2 granted · 1 denied`**.

```
✓ Casualty detection · incident zone      granted   12:18:22
✓ Responder accountability · own crews    granted   12:19:12
✗ Biometric ID · civilians                denied    12:20:07
```

Damit fällt der ganze Rhythmus weg, der die Klinikfassung trägt — die vier gleich
betonten „denied" hintereinander. Die BOS-Fassung braucht eine **andere Dramaturgie**:
nicht Eskalation durch Wiederholung, sondern **eine einzige überschrittene Linie**.

### 2.2 Der Bruch ist qualitativ, nicht quantitativ
Klinik: Der Agent fragt **mehr** ab, als er darf. BOS: Der Agent tut **etwas anderes**,
als er darf — **detektieren ≠ identifizieren**.

| Erlaubt | Geblockt |
|---|---|
| Personen detektieren und lokalisieren | Zivilisten **biometrisch identifizieren** |
| Eigene Einsatzkräfte zuordnen | Ungezielte Massen-ID Unbeteiligter |
| Vermisste (AI-Act-Ausnahme, autorisiert) | Drift von „diese Person" → „alle im Bild" |

Das ist erzählerisch **stärker** als die Klinikfassung, weil es eine Rechtsgrenze ist und
keine Berechtigungsgrenze: **EU AI Act Art. 5(1)(h)** und **GDPR Art. 9**. Der Satz
dahinter — *souveräne KI kennt die rote Linie: sie rettet, sie überwacht nicht* — ist die
beste Pointe im ganzen Material.

### 2.3 Kein Ausfall, kein Fallback
Klinik: AGVs stoppen, der Hospital Logistics Orchestrator übernimmt, die Roboter fahren
wieder. **In der BOS-Fassung passiert das nicht.** Die Drohne fliegt weiter, die
Detektion läuft, nur die ID-Aktion ist gekappt — „mission unaffected".

Damit entfallen ersatzlos:
- *„The AGVs stop."*
- *„Your own Hospital Logistics Orchestrator takes over."*
- *„They roll again. No dose missed."*

Und der Abbinder wechselt die Pointe: nicht **„no dose missed"**, sondern
**„not one identity exposed — and the mission never paused"**.

---

## 3. Was übernommen werden kann

Unverändert tragfähig: der Einstieg · *„Nobody hacked it"* (Drift statt Angriff) ·
Gateway Guard erkennt, Security Sentinel isoliert · *„I suggest we tighten its
permissions; a human signs off"* · der Agentic-Hub-/AgentiX-Abschnitt · **Human in the
loop**.

Die Souveränitätsklammer trägt hier sogar besser als in der Klinik: Bei Einsatz- und
Biometriedaten ist deutsche Rechtsprechung keine Präferenz, sondern Rechtspflicht.

---

## 4. Offen, bevor ich den Volltext schreibe

1. **Wessen Agent ist der Recon Vision Agent?** Extern beschafft (dann bleibt die
   „drifted supplier"-Erzählung intakt) oder eigener/behördlicher Agent (dann ist es
   eine Eigen-Governance-Geschichte — anderer Ton, anderes Schuldbild)? Das Konzept sagt
   es nicht.
2. **Wie viele Beats** soll die rechte Seite haben? Die Klinikfassung hat sieben
   (`BEATS[0…6]`). Bei einer statt vier Ablehnungen werden es eher vier bis fünf.
3. **Wird der AI-Act-Artikel gesprochen?** Im Footer steht er ohnehin. Gesprochen ist er
   stark, kostet aber ~4 s und braucht die Legal-Freigabe, die das Konzept fordert.

---

## 5. Leitplanken aus dem Konzept, die auch fürs Video gelten

- **T Mission** ersetzt iMedOne als Plattform-Anker — reale Telekom-Dachmarke für
  BOS/Public Safety. Nicht als Security-Tool darstellen; das bleibt Cortex + T Security.
- **„Drone Defense" nur zeigen, wenn belegt** (Konzept §Leitplanken).
- **Remote ID = Geräte-, nicht Personen-ID** — diese Unterscheidung darf im Sprechertext
  nicht verwischen.
- **Vor jeder öffentlichen Vorführung mit Legal/DPO gegenlesen**, insbesondere der
  AI-Act-Wortlaut. Das steht so im Konzept und gilt für den Sprechertext genauso.
