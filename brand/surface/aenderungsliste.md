# surface.love, Änderungsliste

Einzelheiten je Version in `project/AENDERUNGEN-v10.md` bis `-v18.md`.

| Version | Änderung |
|---|---|
| V10 | Prototyp auf das Designsystem V2-2026 umgestellt, Inhalte und Abläufe wie V9. |
| V11 | Startseite mit weißer Karte unter dem Film. Von Sascha verworfen. |
| V12 | Zwei Hero-Varianten mit Text auf dem Film, Reseller-Logo. |
| V13 | Aufbau wieder wie V10, Hero aus V12, Text auf Bildern mit blauem Verlauf. Von Sascha gebilligt. |
| V14 | Grundzeile im Fuß gekürzt, Impressum als eigene Seite. |
| V15 | Rate, Einheit und Kurzaussagen im Band auf einer Schriftlinie. |
| V16 | Hero auf Variante A festgelegt. Eingefroren. |
| V17 | Übergabestand nach E-098: Zitat und Community als Platzhalter ohne erfundenen Inhalt, Gerüst für Impressum und Datenschutz, USt-IdNr. und Registerdaten aus der Datei entfernt, Readme auf V2-2026 und Betreiberin korrigiert. |
| V18 | Nacharbeit nach E-099: Platzhalter statt Demo, Laufzeiten 24, 36, 48, Raten als Daten, geprüfte Geräte 12 Monate, stille Kauf-Option, A5, B1, B2, „Empfohlen“. |

## Gegenüber dem Designsystem im Paket

Neu ist der Token `schleier` in `tokens.css` und `tokens.json`, er steht auch im Designsystem. Schriften sind unverändert. In `tokens.json` ist außerdem genau eine Beispielzeile geändert: Das `sample` des Stils `fine` nannte die Registernummer, Begründung: keine Firmenangaben im Paket und im öffentlichen Hub. Neu ist nur `sf-bruecke.css` mit den Shop-Namen `--sf-*` und den Bewegungswerten, Begründung steht in der Datei. Dazu die Lizenz `fonts/OFL-OpenSans.txt`, weil das Designsystem sie nicht führt.
