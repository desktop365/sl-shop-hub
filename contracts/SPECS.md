# Datenblatt und Funktionen (specs.json)

Stand 24.11.2026, F-46 und F-49 (Story C5 und C9), angepasst an E-161. Erzeugt von der Preis-Pipeline,
liegt im Bucket neben products.json, jede Nacht neu geschrieben.

## Zweck
Die Modellseite zeigt ein Datenblatt und eine Liste der
Funktionen als Ausklapper. Die Werte der gewählten Ausführung (Prozessor,
Arbeitsspeicher, Speicher, Farbe) kommen aus `specs` in products.json, alles, was
für das Modell gilt, aus specs.json.

## Schlüssel
Der Modellschlüssel nach MODELLE.md, etwa `surface-laptop-8-intel`. Werte, die je
Größe abweichen, stehen je Größe getrennt (siehe Aufbau).

## Aufbau
```
{ "meta": { "generated_at", "count" },
  "models": {
    "<schluessel>": {
      "datenblatt": [
        { "gruppe": "Display", "zeilen": [
          { "name": "Auflösung", "werte": { "13.8": "2304 x 1536 (201 PPI)", "15": "3270 x 2180 (262 PPI)" } },
          { "name": "Bildwiederholrate", "wert": "bis 120 Hz" } ] }
      ],
      "funktionen": [
        { "titel": "…", "text": "…" }
      ]
    }
  } }
```

- `datenblatt`: Gruppen in dieser Reihenfolge: Prozessor, NPU, Grafik, Arbeitsspeicher
  und Speicher, Display, Größe und Gewicht, Akku, Sicherheit, Kameras, Audio,
  Stromversorgung, Netzwerk und Anschlüsse, Software, Barrierefreiheit,
  Nachhaltigkeit, Wartung, Gehäuse und Farben, Sensoren, Lieferumfang, Garantie.
  Eine Gruppe ohne gesicherten Wert fehlt.
- Eine Zeile hat entweder `wert` (gilt für alle Größen des Modells) oder `werte`
  (Größe als Schlüssel, wie `size_inch`, als Zeichenkette).
- `wert` und jeder Eintrag in `werte` ist fertiger Anzeigetext auf Deutsch mit Einheit, deutsches Zahlenformat.
- `funktionen`: drei bis acht Einträge, Titel kurz, Text ein bis drei Sätze.

## Regeln
- Alle Texte in eigenen Worten, nie die Formulierung des Herstellers oder eines
  Händlers (Master 06.10.2026). Werte sind Fakten und dürfen übernommen werden.
- Nur gesicherte Werte. Was die Quellen nicht eindeutig belegen, fehlt.
- Keine Preise, keine Raten, keine Firmen- oder Lieferantennamen, keine Quellpfade.
- Fehlt specs.json oder der Schlüssel, blendet der Shop Datenblatt und Funktionen aus.
