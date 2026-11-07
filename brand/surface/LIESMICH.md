# Übergabepaket surface.love

Für CC-Shop nach E-098, Nacharbeit nach E-099. Stand 06.11.2026, Prototyp V18, Artifact-Version 24. Ziel im Hub: `brand/surface/`, das Hub ist öffentlich.

| Datei | Inhalt |
|---|---|
| `tokens.css`, `tokens.json` | Designsystem Surface.Love V2-2026, Werte unverändert, neu der Token `schleier`, in `tokens.json` eine Beispielzeile neutralisiert, siehe `aenderungsliste.md` |
| `sf-bruecke.css` | Shop-Namen `--sf-*` auf die Rollen, dazu Bewegung, gesetzt über `data-sf="surface"` |
| `fonts/` | Open Sans 300, 400, 600, 700, Lizenz SIL OFL |
| `bausteine-und-zustaende.md` | Jeder Baustein mit Zuständen, Tokens, Handy und Desktop, Bewegung |
| `seitenliste.md` | Seiten, Datei, Version, Zustände |
| `aenderungsliste.md` | Was sich je Version geändert hat |
| `offene-punkte.md` | Einordnung des Masters, noch Ausstehendes, Prüfbefunde |

Vor dem Bau `offene-punkte.md` lesen.

Beim Einbinden: `tokens.css` setzt ihre Werte auf `:root`. lenovo.online nutzt dieselben Namen `--font-sans`, deshalb je Shop unter `[data-sf]` einbinden und nur die eigenen Schriften laden.
