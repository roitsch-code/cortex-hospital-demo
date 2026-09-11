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
