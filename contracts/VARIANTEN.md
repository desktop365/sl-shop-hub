# VARIANTEN, Reihe, Modell, Ausführung

Stand 24.11.2026, E-161 (Sascha) und E-162 (Master). Ersetzt das zweistufige
Modell und die kuratierten Ausstattungsstufen vom 24.08.2026, siehe unten.

## Modell
Der Katalog kennt drei Ebenen wie Microsoft unter Surface for Business:
Reihe, Modell, Ausführung. Das Modell ist Reihe plus Größenklasse, Edition und
Plattform, Schlüssel und Datei in MODELLE.md. Die Ausführung ist die MSKU.
Zubehör bleibt einstufig.

## Frei konfigurierbar
- Jede gelistete Ausführung (`listed`, DATA-CONTRACT.md) ist wählbar. Es gibt
  keine Bündelung in Stufen und keine Vorauswahl.
- Filter in dieser Folge, jeder nur bei mehr als einem Wert: Größe, Prozessor,
  Farbe, Konnektivität, Besonderheit (Blickschutz, Smartcardleser, OLED).
  Arbeitsspeicher und SSD wählt der Kunde in der Liste der Ausführungen.
- Nichts springt. Ein Wert, der zur übrigen Auswahl nicht passt, ist ausgegraut
  mit Hinweis. Ändert der Kunde einen oberen Filter so, dass ein unterer nicht
  mehr passt, wird nur dieser zurückgesetzt, mit sichtbarem Hinweis.
- Verfügbarkeit steht an jeder Ausführung (SICHTBARKEIT.md).
- Copilot+ PC steht an jeder Ausführung, die `copilot_plus` trägt, und am
  Prozessor, wenn alle seine Ausführungen es tragen. An der Modellkarte steht
  es nur, wenn alle gelisteten Ausführungen des Modells es tragen (E-244,
  MODELLE.md).

## Herkunft der Struktur
Der Feed liefert flache Artikel je MSKU. Die Zuordnung MSKU zu Modell und
Merkmalen macht die Preis-Pipeline: geparst, wo verlässlich, sonst über eine
gepflegte Tabelle mit Quelle. Fällt eine MSKU durch, steht sie in der Meldung der
Pipeline und erscheint nicht im Shop.

## Wirkung
Bildmatrix (IMAGES.md) und Geräteschlüssel (BAUSTEINE.md) bleiben bei Reihe,
Generation, Größe und Farbe. Raten kommen unverändert je MSKU aus products.json,
der Shop ordnet nur an und rechnet nie (E-099).

## Abgelöst am 24.11.2026
- Zweistufiges Modell Reihe und Variante, Produktseite je Reihe und Generation.
- Kuratierte Ausstattungsstufen essential, advanced, performance mit Beliebt-Flag
  als Vorauswahl (24.08.2026). Grund: Sascha will freie Konfiguration nach dem
  Muster von Microsoft.

## Garantie-Bausteine (E-103, 07.11.2026)
Bausteine für neue Geräte. Rate und Artikel kommen aus dem Katalog, der Shop
rechnet nicht (E-099). Beträge aus dem Prototyp sind Platzhalter und gelten nicht.

| Baustein | Titel | Empfohlen bei |
|---|---|---|
| `garantie_1` | Garantie plus ein Jahr | keiner Laufzeit |
| `garantie_2` | Garantie plus zwei Jahre | 36 Monaten |
| `garantie_3` | Garantie plus drei Jahre | 48 Monaten |

- Bei 24 Monaten gibt es keine Empfehlung.
- `garantie_1`, `garantie_2` und `garantie_3` schließen sich gegenseitig aus.
- Der Satz „über die ganze Laufzeit“ steht nur am Baustein, der zur gewählten
  Laufzeit passt, also `garantie_2` bei 36 und `garantie_3` bei 48 Monaten.
- `garantie_3` folgt dem Muster von `garantie_2` und deckt die ganze Laufzeit von
  48 Monaten.
- Gibt es keinen passenden Artikel mit Rate, erscheint `garantie_3` nicht. Bei
  48 Monaten gibt es dann keine Empfehlung, bis der Artikel da ist.
- Die Kuration ist Datenpflege, kein Hardcode. Das Etikett heißt „Empfohlen“.
