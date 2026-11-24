# Datenblatt und Funktionen (specs.json)

Stand 24.11.2026, F-46 und F-49 (Story C5 und C6). Erzeugt von der Preis-Pipeline,
liegt im Bucket neben products.json, jede Nacht neu geschrieben.

## Zweck
Die Produktseite je Reihe und Generation zeigt ein Datenblatt und eine Liste der
Funktionen als Ausklapper. Die Werte der gewählten Ausführung (Prozessor,
Arbeitsspeicher, Speicher, Farbe) kommen aus `specs` in products.json, alles, was
für das Modell gilt, aus specs.json.

## Schlüssel
Der Bildmodell-Schlüssel nach IMAGES.md, in der Regel ohne Farbe:
`familie-generation-groesse`, etwa `surface-laptop-8-13-8`. Der Shop löst mit
derselben Kette auf wie bei den Bildern (IMAGES.md, Resolver Schritt 2): erst mit
Farbe, dann ohne Farbe, dann `familie-generation`, dann `familie`.

## Aufbau
```
{ "meta": { "generated_at", "count" },
  "models": {
    "<schluessel>": {
      "datenblatt": [
        { "gruppe": "Display", "zeilen": [ { "name": "Größe", "wert": "13,8 Zoll" } ] }
      ],
      "funktionen": [
        { "titel": "…", "text": "…" }
      ]
    }
  } }
```

- `datenblatt`: Gruppen in fester Reihenfolge Display, Prozessor und Grafik,
  Speicher, Anschlüsse, Kameras und Audio, Akku, Maße und Gewicht, Sicherheit,
  Lieferumfang. Eine Gruppe ohne gesicherten Wert fehlt.
- `wert` ist fertiger Anzeigetext auf Deutsch mit Einheit, deutsches Zahlenformat.
- `funktionen`: drei bis acht Einträge, Titel kurz, Text ein bis drei Sätze.

## Regeln
- Alle Texte in eigenen Worten, nie die Formulierung des Herstellers oder eines
  Händlers (Master 06.10.2026). Werte sind Fakten und dürfen übernommen werden.
- Nur gesicherte Werte. Was die Quellen nicht eindeutig belegen, fehlt.
- Keine Preise, keine Raten, keine Firmen- oder Lieferantennamen, keine Quellpfade.
- Fehlt specs.json oder der Schlüssel, blendet der Shop Datenblatt und Funktionen aus.
