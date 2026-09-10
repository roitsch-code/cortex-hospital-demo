# Interne Karten — nicht im Repo

`roitsch-code/cortex-hospital-demo` ist **öffentlich**. Faktenkarten aus internen
Quellen (Decks, Intranet, Mail, unveröffentlichte Roadmaps, interne Kennzahlen und
Benchmarks) gehören deshalb **nicht** hierher.

Dieser Ordner ist per `.gitignore` vollständig ausgenommen — nur diese README und die
`.gitignore` selbst sind versioniert. Lege interne Karten hier lokal ab
(`03b-agentic-hub-internal.md` o. ä.); sie werden beim Zusammenbauen des System-Prompts
mitgeladen, aber nie gepusht.

**Beim Zusammenbauen des Realtime-Prompts gilt:** Karten mit
`status: internal-do-not-say` werden **nicht** in die `instructions` aufgenommen. Sie
existieren nur, damit das Team weiß, was bekannt ist und **warum** es nicht gesagt wird.
Karten mit `status: needs-clearance` erst nach interner Freigabe auf
`public-verified` umstellen.
