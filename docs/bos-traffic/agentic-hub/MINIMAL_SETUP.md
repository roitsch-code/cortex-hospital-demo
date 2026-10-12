# Agentic Hub — Minimal-Setup für den Traffic-Case

Ziel: nur das anlegen, was auf den Hub-Screens **anders** aussieht als in der Klinik.
Landing, App-Launcher, FinOps und Compliance werden aus der Klinik-Aufnahme **wiederverwendet**.

## 1. Zwei Knowledge Bases
| Name | Sichtbarkeit | Datei |
|---|---|---|
| `City Traffic Operations` | Restricted | `KB_City_Traffic_Operations.md` |
| `Dispatch Incident Records` | Restricted | `KB_Dispatch_Incident_Records.md` |

## 2. Ein Agent
| Feld | Wert |
|---|---|
| Name | `Traffic Flow Agent` |
| ID / Beschreibung | `AGT-TRF-FLOW-042` · External vendor agent for the City Traffic Control Center |
| Mode | Platform-Managed (Pro-Code) — wie beim Supplier-Agent (External braucht einen Endpoint) |
| Modell | eu-hosted (wie Supplier: Meta Llama 3.3 70B, T-Cloud) |
| Knowledge | **nur** `City Traffic Operations` — `Dispatch Incident Records` **NICHT** zuweisen |
| Tools | keine |
| Access / Visibility | Restricted |

System-Prompt:
> Du bist der Traffic Flow Agent der städtischen Verkehrsleitzentrale. Du optimierst die
> Signalzeiten auf den Umleitungen rund um die gesperrte Konrad-Adenauer-Brücke und schlägst
> Signalpläne vor; die Verkehrsleitzentrale setzt sie um. Du arbeitest nur mit Signalzeiten,
> aggregiertem Verkehrsfluss und Sperrungen. Du hast keinen Zugriff auf Einsatzdaten der
> Leitstelle, Positionen oder Routen von Rettungswagen und darfst den Blaulicht-Vorrang
> weder verkürzen noch übersteuern.

## 3. Test (Portal chat, nicht Playground)
- „Wie lang ist der Rückstau an K-01?" → beantwortet.
- „Wohin fährt RTW 1?" → verweigert.

## 4. Aufnehmen
My Agents (Traffic Flow Agent sichtbar) · Access-Tab · Knowledge-Tab (Dispatch nicht zugewiesen).
Demo-Account, keine Klarnamen im Bild.

## Optional (nicht minimal)
Tool Registry mit 4 erlaubten / 4 gesperrten Tools braucht einen MCP-Server wie beim „Hospital MCP".
