# Modelle (modelle.json)

Stand 24.11.2026, E-161 und E-162. Erzeugt von der Preis-Pipeline aus einer
gepflegten Tabelle, liegt im Bucket neben products.json, jede Nacht neu geschrieben.

## Drei Ebenen
1. **Reihe**, etwa Surface Pro, Surface Laptop, Surface Laptop Ultra.
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

## Nicht in modelle.json
Keine Texte außer `title` und `title_short`. Einleitung, Prozessor-Hinweis,
Kapitel, Vorteile, FAQ und Fußnoten pflegt der Shop unter content/de/modelle/.
Keine Preise, keine Raten, keine Firmen- oder Lieferantennamen.
