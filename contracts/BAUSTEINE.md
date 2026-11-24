# Bausteine der Ausstattung (bausteine.json)

Stand 24.11.2026, F-49. Grundlage: Checkout-Baukasten bk1 (Treppe), E-065, E-076, E-099, E-103, E-105, E-106, E-156, E-157.

## Zweck
Die Ausstattungsseite zwischen Gerät und Anfrage bietet in fester Reihenfolge an: Zubehör, Lizenzen, Garantie, Managed Workplace. Alle Raten kommen fertig aus der Preis-Pipeline, der Shop rechnet nicht (E-099). Der Shop zeigt nur Bausteine, die zur gewählten Laufzeit eine Rate in den Daten haben.

## Quellen
- **Zubehör:** Artikel mit `category: "zubehoer"` in products.json. Die Passung steht in `fits`, einer Liste von Geräteschlüsseln (E-106). Ohne `fits` wird der Artikel nicht angeboten.
- **Lizenzen, Garantie, Managed Workplace:** bausteine.json im Bucket neben products.json, jede Nacht von der Preis-Pipeline geschrieben.

## Geräteschlüssel
`familie-generation-groesse`, etwa `surface-pro-11-13` oder `surface-laptop-8-13-8`. Größe mit Bindestrich statt Komma. `*` steht für alle Geräte.

## Aufbau bausteine.json
```
{ "meta": { "generated_at", "currency", "vat_rate", "contract_types": { "leasing": [24, 36, 48] }, "count" },
  "items": [ ... ] }
```

Je Eintrag:
- `id`: stabiler Slug des Eintrags.
- `baustein`: Schlüssel aus dem Konzept, er bestimmt Texte und Regeln im Shop. Erlaubt sind `lizenz_m365_standard`, `lizenz_m365_premium`, `lizenz_copilot`, `garantie_1`, `garantie_2`, `garantie_3`, `garantie_2_plus`, `garantie_3_plus`, `managed_modell_a` und `managed_modell_b`.
- `kategorie`: `lizenz`, `garantie` oder `managed`.
- `msku`: optional, die Artikelnummer, wo es eine gibt.
- `name`: Artikelbezeichnung, im Shop nur als Nebenzeile. Titel und Nutzensatz kommen aus dem Copy-Baukasten (F-19).
- `gilt_fuer`: Liste von Geräteschlüsseln oder `["*"]`.
- `je`: `geraet` oder `platz`. Die Startmenge ist die Gerätemenge.
- `benoetigt`: optional, Liste von Bausteinen, von denen mindestens einer gewählt sein muss.
- `schliesst_aus`: optional, Liste von Bausteinen, die nicht zugleich gewählt sein dürfen.
- `rates.leasing`: je `{ "term", "net", "gross" }` genau für 24, 36 und 48 Monate. `gross` ist `net` mal 1,19, kaufmännisch gerundet.

Fehlt eine Rate zur gewählten Laufzeit, erscheint der Baustein bei dieser Laufzeit nicht. Es gibt keinen Schätzwert und kein „Preis auf Anfrage“ im Baukasten (bk1, Zustand 7).

## Regeln
- Garantie gibt es nur zusammen mit einem Neugerät, nie im Weg der geprüften Geräte (F-37).
- Die Garantien schließen sich gegenseitig aus. Empfohlen ist `garantie_2` bei 36 Monaten und `garantie_3` bei 48 Monaten, bei 24 Monaten gibt es keine Empfehlung (E-103). Die Plus-Varianten tragen keine Empfehlung.
- Lizenzen werden auf volle Jahre gerechnet (E-076) und stecken in der Rate (E-065). Die Pipeline bildet daraus die Raten je Laufzeit.
- `lizenz_copilot` setzt `lizenz_m365_standard` oder `lizenz_m365_premium` voraus.
- Managed Workplace setzt `lizenz_m365_premium` voraus. Wählt der Kunde Managed, wählt der Shop Premium sichtbar mit. Wählt er Premium ab, entfällt Managed, mit Hinweiszeile (bk1, Zustand 6).
- Nichts ist vorausgewählt (bk1, rote Linie 1). „Komplett ausstatten“ wählt die empfohlenen Bausteine, jede Zeile bleibt einzeln abwählbar.

## In der Anfrage
Jeder Baustein ist eine eigene Position direkt hinter seinem Gerät, mit derselben Laufzeit (E-105). In HubSpot wird er eine Deal-Position mit dem Schlüssel `baustein` und der Menge.

## Nicht in bausteine.json
Keine EK-, VK- oder Faktorwerte (E-092). Keine Texte außer `name`.
