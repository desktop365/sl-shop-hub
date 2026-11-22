# surface.love, offene Punkte zur Übergabe

Stand 06.11.2026, Strom 50, Prototyp `slshopv18-arbeit.html` (Artifact-Version 24), Nacharbeit nach E-099. Keine E-Nummern, die vergibt der Master.

## 1. Abweichungen vom Designsystem: eingeordnet

E-099: A1 bis A4 und B1 sind als Ausnahme angenommen, A5 und B2 sind behoben.

Messung: Text ausgeblendet, Weiß gegen die hellsten Pixel im Textfeld (99. Perzentil), auf dem Standbild, Fensterbreite 1440 und Prototyp-Ansicht Mobil (372 px). Filme bewegen sich, die Werte gelten nur für das Standbild.

| Nr | Stelle | Stand | Kontrast Desktop | Kontrast Handy |
|---|---|---|---|---|
| A1 | Hero über dem Film, Verlauf `.sl-veil` | Ausnahme angenommen | Titel 5,17, Text 6,92 | Titel 5,15, Text 6,28 |
| A2 | Kampagne, Verlauf `.sl-veil` | Ausnahme angenommen | Titel 11,03, Text 12,69 | Titel 11,12, Text 13,84 |
| A3 | Use-Case-Kacheln, Verlauf `.ucard-in` | Ausnahme angenommen. Kleinster Text 12 px, im Abnahmetest erneut prüfen | Titel ab 5,70, Text ab 9,03 | Titel ab 5,70, Text ab 9,59 |
| A4 | Mood-Band Desktop, Verlauf `.sl-veil` | Ausnahme angenommen, bei Film erneut prüfen | Titel 9,75, Text 6,09 | |
| A5 | Mood-Band Handy | **Behoben**, Verlauf `0 % bei 0 %, 88 % bei 30 %, 96 % bei 100 %` | | Titel 11,71, Text 13,29 |
| B1 | Alle Verläufe auf Bildflächen | **Umgesetzt** als ein Token `schleier` im Designsystem, Regel „nur für Text auf Bild und Film“. Stopps je Stelle in `bausteine-und-zustaende.md` | | |
| B2 | Ersatz-Szene | **Behoben.** Keine gezeichnete Szene und keine Verläufe mehr. Fehlt ein Medium, steht `.slot-leer` in `surface-raised` mit Etikett | | |

Geprüft: In der Grundeinstellung aller Seiten nur noch die Verläufe aus `schleier`, keine Schatten und keine Radien außerhalb der Regeln, außer runden Punkten.

## 2. Nach E-099 erledigt, Folgepunkte

| Punkt | Stand |
|---|---|
| Kaufpreis | Stille Option nur auf der Produktseite, Kaufweg nur in der Kasse, ohne Kaufpreis keine Option. In Startseite, Geräte, Konfigurator und Katalog steht kein Kaufpreis. |
| Laufzeiten | 24, 36, 48, Voreinstellung 48, nur Leasing. Stufen ohne Rate gesperrt, ohne Preis. |
| Raten | Tabelle aus HubSpot, Stand 06.11.2026, nur als Referenz im Prototyp. Im Shop aus `products.json`, Feld `rates.leasing`. |
| Markierungen | „Empfohlen“, kuratiert. |
| Garantie | Offen: Die Empfehlung `garantie_2` und ihr Text „passend zu drei Jahren“ gelten nur bei 36 Monaten. Bei der Voreinstellung 48 gibt es keine empfohlene Garantie, die Frage nach `garantie_3` hängt daran. Bitte vom Master entscheiden lassen, Strom 50 hat nichts erfunden. |
| Für Strom 10, Katalog | Artikel „Surface Laptop 13" CU5/16GB/512GB o. Netzteil Pl“ hat 29,57 €, er liegt weit unter den übrigen und ist im Prototyp nicht verwendet. Pro 12 Zoll Performance und Laptop 13 Zoll Performance haben im Zuschnitt keine Rate, die Stufe ist dort gesperrt. |
| Firmenangaben | Die README des Designsystems enthält Steuernummer, USt-IdNr. und Bankverbindung, sie ist nicht im Paket. V10 bis V16 im Artifact enthalten die USt-IdNr. und bleiben nach E-032 unverändert. Diese Quellen nicht ins Hub übernehmen, auch nicht aus `C:\Dev\sl-ops\uebergabe\`. |
| Prototyp und öffentliches Hub | Der Prototyp enthält Raten und Platzhalter-Kaufpreise (E-042). Er liegt nicht im Paket, nur Referenz. |

## 3. Noch ausstehend

| Punkt | Wer |
|---|---|
| Texte für Impressum und Datenschutz, das Gerüst steht | Master |
| Seiten AGB, Widerruf, Markenhinweise: nicht gebaut, im Fuß ohne Link. Einwilligungen in Anfrage und Kasse nennen AGB und Datenschutz ohne Link. | Master, dann Strom 50 |
| Zitat und Community: nur mit echten Inhalten und Freigabe, sonst Abschnitt ausblenden (E-065) | Strom 95, Sascha |
| Sand auf der Startseite: mit V13 gebilligt, ausdrücklich gefragt war Sascha nicht | Sascha |
| Kontaktblock im Fuß behalten oder kürzen | Sascha |
| Co-Branding-Richtlinie von Microsoft liegt Strom 50 nicht vor, Mindestgröße und Schutzraum des Reseller-Logos ungeprüft | Master |
| Nutzung der Microsoft-Videos: schriftlicher Beleg fehlt. Microsoft-Medien und Reseller-Logo sind nicht im Paket und gehören nicht ins öffentliche Hub. | Sascha |
| Motive sind Platzhalter, teils Gerätedetails statt Arbeitssituationen | Strom 40 |
| Bausteinpreise, Bestand und Kaufpreise im Prototyp sind Platzhalter, im Shop nur aus Katalogdaten (E-016) | CC-Shop, Strom 10 |
| `DESIGN.md` im Hub beschreibt noch Segoe UI, Cyan und Radius 14 (E-098 Schritt 6.1) | Master |

## 4. Gestalterische und technische Prüfung

Geprüft mit frontend-design und animation-vocabulary. frontend-design lag in dieser Sitzung nicht als Skill vor, der Rechner war nicht erreichbar. Geprüft wurde deshalb gegen die öffentliche Fassung `anthropics/skills`, bitte gegen die Projektfassung abgleichen. Nichts davon ist in V18 geändert, außer den Punkten aus E-099.

Tragfähig: Film, Blau und Rate im Band sind der eine starke Moment, der Rest bleibt ruhig. Die Marke unterscheidet sich klar von lenovo.online.

| Befund | Stelle | Vorschlag |
|---|---|---|
| Nummern 01 bis 04 ohne Reihenfolge im Inhalt | Vorteile (`.vrow .n`) | Weglassen. Beim Lebenszyklus wäre eine Nummer sinnvoll, dort stehen Icons. |
| Dachzeile in Versalien über fast jeder Überschrift | `.lbl`, vom Designsystem als `eyebrow` gedeckt | Behalten, wo sie Information trägt, „Drei Geräte“ und „Warum zur Rate“ prüfen |
| Pfeil an Knöpfen und Links, rund 30 Stellen | `icoArr` | Nur an Wegweisern, nicht an jeder Aktion |
| Definierte Bewegung läuft nicht, weil der Prototyp das DOM neu schreibt: Anfrage-Blatt, Ausklapper, Teile von `.bst`, `.chk`, `.tierrow` | Siehe `bausteine-und-zustaende.md` | In React bauen wie definiert, sie antworten auf eine Aktion |
| Kein sichtbarer Fokus an `.sw` und `.stop.on` | Konfigurator | Fokusring ergänzen |
| Trefferflächen von `.dots` überlappen | Geräteseite | Mindestens 44 px ohne Überlappung |
| 13 px abgeschnitten bei 372 px Breite | Ausstattung | Beim Bau prüfen und beheben |
| Hover-Versatz ohne Tastatur-Gegenstück | `.thread`, `.vrow`, Kacheln | Auch bei `:focus-visible`, bei reduzierter Bewegung aus |

## 5. Grenzen dieser Prüfung

Berechnete Werte sind in Chromium gemessen, Schwellen dazwischen stammen aus dem Code. Kein Test mit Screenreader und keine Prüfung im Canvas nach dem Veröffentlichen. Ob V18 im Canvas öffnet, hat Strom 50 nicht gesehen, das Browser-Fenster ist nicht angemeldet.
