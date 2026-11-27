# Modelle (modelle.json)

Stand 27.11.2026, E-161, E-162 und mit den Reihenseiten E-217 (R1, 8152). Erzeugt von der Preis-Pipeline aus einer
gepflegten Tabelle, liegt im Bucket neben products.json, jede Nacht neu geschrieben.

## Drei Ebenen
1. **Reihe**, etwa Surface Pro, Surface Laptop, Surface Laptop Ultra. Für die
   Reihenseiten fasst der Block `reihen` sie gröber zusammen, siehe unten.
2. **Modell**, Reihe plus Größenklasse, Edition und Plattform. Jedes Modell hat
   eine eigene Produktseite und einen eigenen Konfigurator. Intel, Snapdragon und
   NVIDIA sind immer getrennte Modelle.
3. **Ausführung**, die einzelne MSKU in products.json mit `specs.model`.

## Modellschlüssel
`{reihe}-{edition}-{plattform}`.
- `reihe`: `surface-pro`, `surface-pro-12-zoll`, `surface-laptop`,
  `surface-laptop-13-zoll`, `surface-laptop-ultra`. Neue Reihen nur über diesen
  Kontrakt.
- `edition`: die Edition, wie Microsoft sie zählt, etwa `8` beim Surface Laptop
  13,8 und 15 Zoll (8. Edition), `2` beim Surface Pro 12 Zoll (2. Edition).
- `plattform`: `intel`, `snapdragon`, `nvidia`.

Beispiele: `surface-laptop-8-intel`, `surface-laptop-13-zoll-2-snapdragon`,
`surface-pro-12-zoll-2-snapdragon`, `surface-laptop-ultra-1-nvidia`.

Der Modellschlüssel ist die Adresse der Modellseite: `/de/geraete/{schluessel}`.
Der Shop bildet ihn nie selbst, er liest ihn aus `specs.model`.

## Aufbau modelle.json
```
{ "meta": { "generated_at", "count" },
  "reihen": [ … siehe Abschnitt Reihen … ],
  "items": [
    { "key": "surface-laptop-8-intel",
      "reihe": "surface-laptop",
      "title": "Surface Laptop, 13,8 und 15 Zoll (8. Edition) | Intel",
      "title_short": "Surface Laptop 8 | Intel",
      "generation": "8",
      "platform": "intel",
      "sizes": [13.8, 15],
      "neu": false,
      "vorgaenger": false,
      "reihenfolge": 20 } ] }
```

- `neu`: wahr, solange Microsoft das Modell als neu führt.
- `vorgaenger`: wahr, wenn es eine neuere Edition derselben Reihe und Plattform gibt.
  Vorgänger stehen im Shop unter „Weiterhin erhältlich“.
- `reihenfolge`: kleiner zuerst, innerhalb der Reihe.
- Ein Modell ohne gelistete Ausführung (`listed`) erscheint nicht.

## Reihen (E-217)
Die Reihenseiten `/de/geraete/{reihe}` lesen den Block `reihen` in
`modelle.json`. Die Daten liefert CC-Pricing mit der Preis-Pipeline (R5, 8156)
aus derselben gepflegten Tabelle wie die Modelle.

```
"reihen": [
  { "key": "surface-pro",
    "titel": "Surface Pro",
    "reihenfolge": 10,
    "aktuell": ["surface-pro-12-zoll-2-snapdragon", "…"],
    "vorgaenger": ["…"],
    "rampenlicht": "surface-pro-12-zoll-2-snapdragon" },
  { "key": "surface-laptop", … } ]
```

- `key`: Reihenschlüssel und Adresse der Reihenseite, `/de/geraete/{key}`.
  Heute genau `surface-pro` und `surface-laptop` (ROUTEN-UND-SEO.md,
  Abschnitt 2). Neue Reihen nur über diesen Kontrakt.
- `titel`: Anzeigename der Reihe ohne Marke „Surface.Love“.
- `reihenfolge`: kleiner zuerst, etwa in der Geräteübersicht.
- `aktuell`: Liste der Modellschlüssel der aktuellen Modelle, in der
  Reihenfolge der Anzeige. Mindestens ein Eintrag.
- `vorgaenger`: Liste der Modellschlüssel, die die Seite unter „Weiterhin
  erhältlich“ zeigt. Darf leer sein.
- `rampenlicht`: genau ein Modellschlüssel aus `aktuell`, das Modell im
  Abschnitt Rampenlicht der Seite.
- **Zuordnung:** Jedes Modell steht in höchstens einer Reihe, entweder in
  `aktuell` oder in `vorgaenger`. Surface Laptop Ultra und Surface Laptop
  13 Zoll gehören zu `surface-laptop`, Surface Pro 12 Zoll zu `surface-pro`.
  Das Feld `reihe` eines Modells bleibt, wie es ist. Es ist feiner als der
  Reihenschlüssel und dient nur dem Modellschlüssel.
- **Ein Reihenschlüssel ist nie zugleich ein Modellschlüssel,** und umgekehrt.
  Beide teilen sich das Segment `/de/geraete/`. Die Pipeline prüft das vor
  dem Upload und lädt sonst nicht hoch.
- Ein Modellschlüssel in `reihen`, den `items` nicht führt oder der keine
  gelistete Ausführung hat, wird übergangen. Hat eine Reihe dann kein
  aktuelles Modell mehr, antwortet ihre Seite mit 404 und fällt aus der
  Sitemap.
- **Die ab-Rate der Reihe wird ausgewählt, nicht gerechnet (E-099).** Der
  Shop nimmt das kleinste `rate_from.net` unter den gelisteten Ausführungen
  der Modelle in `aktuell` aus `products.json` und zeigt es mit „ab“. Kein
  Mittelwert, keine Rundung, keine eigene Rechnung. `reihen` trägt keine Rate.

## Texte der Reihenseite (content/de/reihen)
Die Texte stehen im Shop unter `content/de/reihen/{reihe}.json`, eine Datei je
Reihenschlüssel. CC-Marketing schreibt sie (R3, 8154), gegliedert nach dem
Konzept der Reihenseiten (P2, Abschnitt 4). Titel und Beschreibung nach
ROUTEN-UND-SEO.md, Abschnitt 9.

```
{ "meta": { "titel": "…", "beschreibung": "…" },
  "hero": { "h1": "…", "satz": "…", "sprung": { "id": "…", "text": "…" } },
  "leiste": { "name": "…" },
  "kapitel": [
    { "id": "…", "titel": "…", "satz": "…",
      "kennzahl": "…", "kennzahl_zeile": "…" } ],
  "sicherheit": { "h2": "…", "karten": [ { "id": "…", "titel": "…", "satz": "…", "ziel": "…" } ] },
  "ki":         { "h2": "…", "karten": [ … wie sicherheit … ] },
  "service":    { "h2": "…", "karten": [ … wie sicherheit … ] },
  "rampenlicht": { "h2": "…", "satz": "…" },
  "tabelle":    { "h2": "…" },
  "zubehoer":   { "h2": "…", "satz": "…" },
  "andere":     { "h2": "…", "satz": "…" },
  "faq": [ { "frage": "…", "antwort": "…" } ],
  "fussnoten": [ { "id": "…", "text": "…" } ] }
```

| Feld | Regel |
|---|---|
| `meta` | `titel` ohne Marke, höchstens 45 Zeichen, `beschreibung` 120 bis 155 Zeichen. Keine Rate darin |
| `hero` | `h1` ist die einzige H1 der Seite. `sprung` ist der Knopf zu einem Abschnitt der Seite, `id` ist die `id` dieses Abschnitts |
| `leiste` | `name` steht in der klebenden Leiste unter dem Kopf |
| `kapitel` | 4 bis 6 Einträge in der Reihenfolge der Anzeige. `id` ist ein kurzer Schlüssel aus Kleinbuchstaben und Bindestrich, eindeutig in der Datei, und verbindet das Kapitel mit seinen Medien (IMAGES.md, Nachtrag Reihenseiten). `kennzahl` und `kennzahl_zeile` sind optional und stehen nur zusammen |
| `sicherheit`, `ki`, `service` | je `h2` und Karten mit `id`, `titel`, `satz`. `ziel` ist optional, ein interner Pfad ohne Host, der nicht weiterleitet (ROUTEN-UND-SEO.md, Regel 4.5) |
| `rampenlicht` | `h2` und `satz`. Das Modell kommt aus `rampenlicht` in `reihen` |
| `tabelle` | nur `h2`. Die Zeilen kommen aus den Daten (`modelle.json`, `specs.json`) |
| `zubehoer`, `andere` | je `h2` und `satz`. `andere` verweist auf die andere Reihe |
| `faq` | 10 bis 15 Einträge mit `frage` und `antwort`, nicht dieselben wie auf den Modellseiten |
| `fussnoten` | `id` und `text`. Verweise im Text auf eine Fußnote wie in `content/de/modelle/` |

- **Raten nur als Platzhalter `{ab_rate}`.** Der Shop setzt die ab-Rate der
  Reihe aus dem Abschnitt Reihen ein. Nie eine Zahl im Text (E-099). Fehlt
  die Rate, lässt der Shop den Satz mit dem Platzhalter weg.
- Fehlt ein optionaler Abschnitt, steht er nicht auf der Seite. Pflicht sind
  `meta`, `hero`, `kapitel` und `faq`. Fehlt die Datei, antwortet die
  Reihenseite mit 404.
- Microsoft-Namen nach IMAGES.md, Punkt 2. Keine Preise von Microsoft, keine
  Firmen- oder Lieferantennamen.

## Nicht in modelle.json
Keine Texte außer `title`, `title_short` und `titel` in `reihen`. Einleitung, Prozessor-Hinweis,
Kapitel, Vorteile, FAQ und Fußnoten pflegt der Shop unter content/de/modelle/.
Keine Preise, keine Raten, keine Firmen- oder Lieferantennamen.
