# Bildspezifikation SL Shop V5, Antwort an den Bilder-Chat

Bezug: `slshopv5-prototyp.html`. Alle Zahlen sind aus dem Layout gemessen, nicht geschätzt.
Rechenbasis Desktop: Inhaltsbreite 1160 px (Container 1240, Gutter 40).

## 1. Kontexte und gerenderte Pixelgrößen

| Kontext | CSS-Breite des Bildes | Nötig für 2x | Seitenverhältnis der Fläche |
| --- | --- | --- | --- |
| Korbzeile im Anfrage-Sheet (`.line-thumb`) | 55 px | 110 px | 1:1 |
| Gerätebahn Startseite, 3-spaltig | 324 px | 648 px | 4:3,4 |
| Gerätebahn mobil, Snap-Karussell | 370 px | 740 px | 4:3,4 |
| Konfigurator-Bühne (`.kstage`) | 451 px, max 560 | 1120 px | 1:1 |
| Geräteseite, Blatt (`.leaf .dev-field`) | 499 px | 998 px | 4:3,4 |
| Lightbox, geplant | 900 bis 1100 px | 2200 px | frei |

Größter regulärer Kontext: rund 570 px CSS. Ohne Lightbox reichen 1200 px exakt aus.

## 2. Antworten auf die sechs Fragen

**Ausgabebreiten.** Bitte ein Breitenset statt Haupt- plus Vorschaubild:
`160 / 400 / 800 / 1200 / 1600`, dazu `2400` nur für die Lightbox-Kandidaten (siehe 4).
Wir binden das als `srcset` mit `sizes` ein, dann lädt jeder Kontext genau seine Stufe.

**Seitenverhältnis.** Quadratischer Master für alle Kontexte, ja. Wir setzen nur die Breite,
die Höhe läuft frei, die Fläche dahinter hat das Verhältnis, nicht das Bild. Wichtig ist
statt eines zweiten Verhältnisses eine **einheitliche Luft**: das Gerät soll rund 8 Prozent
Rand zu allen vier Seiten haben und optisch zentriert sitzen, nicht mathematisch. Sonst
springen die Geräte in der Bahn nebeneinander in der Größe.

**Hintergrund: transparent, klare Präferenz.** Unsere Bühne tönt sich live mit der gewählten
Gerätefarbe, und die Karten liegen auf einem hellen Verlauf. Wir behelfen uns derzeit mit
`mix-blend-mode: multiply`, das frisst bei dunklen Geräten (Schwarz, Graphit) die Tiefen an.
Mit Alpha fällt der Kniff weg. Bitte **Alpha erhalten, weicher Kontaktschatten mit im
Alphakanal**, kein aufgemalter weißer Boden.

**Lightbox.** Ja, bitte einplanen, aber nur für die Hauptansicht je Gerät und Farbe:
`2400` px, WebP. Für Nebenansichten nicht nötig.

**Retina.** Kein separates 2x-Paar, sondern das Breitenset oben. Ein fixes 2x zwingt kleine
Kontexte in zu große Dateien; mit `srcset` zieht die 55-px-Korbzeile die 160er und die
Bühne die 1200er.

**Format.** WebP als Hauptformat, gern zusätzlich AVIF, wir liefern beides per `<picture>`
aus. Ein PNG-Fallback nur für die 1200er Stufe.

## 3. Was wir zusätzlich brauchen, damit die Story trägt

**Pro Farbe ein Bild.** Der Konfigurator hat eine echte Farbwahl (Platin, Saphir, Graphit,
Jade, Dune, Schwarz). Beim Klick soll das Gerät wechseln, nicht nur der Hintergrund.
Dateiname bitte sprechend: `surface-laptop--jade--front-open--1200.webp`.

**Vier Ansichten je Gerät und Farbe, nach Priorität:**
1. `front-open`, leicht aus der Achse, Deckel offen, Display an — das Leitbild für Bühne und Karte
2. `three-quarter`, Dreiviertelansicht offen — für die Blätter der Geräteseite
3. `side-closed`, geschlossen von der Seite — zeigt die Bauhöhe, gutes zweites Galeriebild
4. `detail`, Tastatur, Stift oder Anschlüsse — Beleg für Verarbeitung

Nur Ansicht 1 wird in allen Farben gebraucht. Die übrigen genügen in der Leitfarbe.

**Displayinhalt.** Auf dem eingeschalteten Display bitte einen ruhigen, neutralen Desktop,
keine Werbeflächen, kein Text, der übersetzt werden müsste. Er erscheint bei uns nur
klein und soll Leben andeuten, nicht ablenken.

**Was wir nicht brauchen:** Freisteller vor Farbverlauf, Spiegelungen auf Glasboden,
gedrehte Kompositionen. Unsere Flächen bringen die Farbe selbst mit.

## 4. Ladeverhalten, damit viele Bilder schnell bleiben

- Erstes sichtbares Gerätebild `loading="eager"` mit `fetchpriority="high"`, alle übrigen `lazy`.
- Zielgewichte: 160er unter 8 KB, 400er unter 40 KB, 1200er unter 180 KB, 2400er unter 500 KB.
- Qualität 72 bis 78 reicht bei Freistellern mit ruhigem Hintergrund, gern visuell geprüft
  statt fix gesetzt.
- Farbwechsel im Konfigurator: die Bilder der übrigen Farben eines Geräts in der 400er Stufe
  vorladen, damit der Wechsel ohne Blitzer läuft, die große Stufe zieht danach nach.
- Ein Manifest bitte als `images.json` mit `geraet`, `farbe`, `ansicht`, `breite`, `datei`,
  dann können wir die Slots automatisch füllen statt Pfade zu pflegen.

## 5. Zusammengefasst

Quadratischer Master, transparent, 8 Prozent Luft, Breitenset 160/400/800/1200/1600
plus 2400 nur für die Leitansicht, WebP und AVIF, pro Farbe die Leitansicht, drei weitere
Ansichten in der Leitfarbe, Manifest als JSON.
