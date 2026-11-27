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
| V18 Bau | 23.11.2026, Bauplan V18 Fassung 4 aus dem Design-Chat (E-144): Bauwerte in `sf-bruecke.css`, neue Datei `shop-basis.css`, Freigaben F01 bis F05, F07, F09 bis F12, F14 und Sand (E-145, E-146). |
| G6 | 26.11.2026, Design-Update nach E-194: Titelstufe `display-xl` 72/76 in `tokens.json`, sieben Schleier `schleier-*` in `tokens.json` und `tokens.css`, in `sf-bruecke.css` neu `--sf-text-hero`, `--sf-lh-hero`, `--sf-w-hero`, `--sf-schleier-*`, `--sf-scrim` und `--sf-scrim-solid`. Werte aus der Bauspezifikation Startseite, Abschnitt 3, 5, 6 und 8. Nichts Bestehendes umbenannt oder geändert. |
| G9 | 26.11.2026, Vollbild-Bühne nach E-222 und E-225: in `tokens.json` und `tokens.css` neu `schatten-text`, `schatten-schrift`, `abdunklung-hoch` und `abdunklung-fuss`, alle in `ink` mit Deckkraft. In `sf-bruecke.css` neu `--sf-schatten-*`, `--sf-abdunklung-*` mit Mindestlänge und die Schriftstufen `--sf-text-buehne-*`, fließend ab 1920 Breite. `schleier-buehne` bleibt, wird von der Bühne nicht mehr genutzt. Werte aus der Vorgabe G9 v3 von Claude Design, Abschnitte 3.3, 3.4 und 4. Nichts Bestehendes umbenannt oder geändert. |
| G9 Stufe 2 | 27.11.2026, Hochformat der Bühne nach E-229: in `sf-bruecke.css` neu die Zeilenhöhen `--sf-lh-buehne-*` ohne Einheit für alle drei Stufen ab 1024 Breite, Kommentare zum Hochformat. Kein neues Token, das Hochformat nutzt `abdunklung-fuss`. Werte aus der Vorgabe G9 v3.1 von Claude Design, Abschnitte 3.3 und 3.4. Nichts Bestehendes umbenannt oder geändert. |
| R1b | 27.11.2026, Reihenseite nach E-238: in `tokens.json` und `tokens.css` neu `schleier-reihe` (`surface-deep` mit 94 % Deckung, 96 px Auslauf), nur für die Reihenseite unter 1024 Breite. In `sf-bruecke.css` neu `--sf-schleier-reihe`, die Maße der Box `--sf-box-*` und die Schriftstufen `--sf-text-box-*` und `--sf-lh-box-*`. `schleier-schutz-oben` und `-unten` als abgelöst markiert (E-237), nicht gelöscht. |

## Gegenüber dem Designsystem im Paket

Neu ist der Token `schleier` in `tokens.css` und `tokens.json`, er steht auch im Designsystem. Seit G6 (E-194) kommen dazu die Typstufe `display-xl` und die Verläufe `schleier-hero-quer`, `schleier-hero-quer-unten`, `schleier-hero-hoch`, `schleier-kampagne`, `schleier-buehne`, `schleier-schutz-oben` und `schleier-schutz-unten`. Seit G9 (E-225) kommen die Schatten `schatten-text` und `schatten-schrift` und die Abdunklungen `abdunklung-hoch` und `abdunklung-fuss` dazu, in neutralem Schwarz statt in Markenfarbe. Seit R1b (E-238) kommt `schleier-reihe` dazu, nur für die Reihenseite, in `surface-deep`. `schleier-schutz-oben` und `schleier-schutz-unten` sind seit E-237 abgelöst und bleiben stehen. Sie stehen nicht im Designsystem, Begründung: Die Werte sind an den Bildern von Microsoft gemessen und gelten nur für den Shop. Anders als die Verläufe `gradient-*` sind sie in sRGB gerechnet. Schriften sind unverändert. In `tokens.json` ist außerdem genau eine Beispielzeile geändert: Das `sample` des Stils `fine` nannte die Registernummer, Begründung: keine Firmenangaben im Paket und im öffentlichen Hub. Neu ist nur `sf-bruecke.css` mit den Shop-Namen `--sf-*` und den Bewegungswerten, Begründung steht in der Datei. Dazu die Lizenz `fonts/OFL-OpenSans.txt`, weil das Designsystem sie nicht führt.
