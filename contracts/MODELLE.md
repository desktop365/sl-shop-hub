# Modelle (modelle.json)

Stand 28.11.2026, E-161, E-162 und mit den Reihenseiten E-217 (R1, 8152), E-238 (R1b, 8163), E-244 (R8, 8170) und E-254 (R13, 8183). Erzeugt von der Preis-Pipeline aus einer
gepflegten Tabelle, liegt im Bucket neben products.json, jede Nacht neu geschrieben.

## Begriffe
- **Reihe** heißt in den Verträgen nur noch die Reihe der Reihenseiten: ein
  Eintrag im Block `reihen`, heute `surface-pro`, `surface-laptop` und
  `surface-laptop-ultra` (Abschnitt Reihen, E-254).
- **Modellreihe** heißt das Feld `reihe` am Modell in `items`, etwa
  `surface-pro-12-zoll`. Es ist feiner als die Reihe und bildet den ersten
  Teil des Modellschlüssels. Der Feldname bleibt `reihe`, er wird nicht
  umbenannt.
- **Familie** heißt `specs.family` in products.json (DATA-CONTRACT.md). Sie ist
  weder Reihe noch Modellreihe und dient vor allem der Zuordnung von Bildern
  (IMAGES.md).

## Drei Ebenen
1. **Modellreihe**, etwa Surface Pro, Surface Pro 12 Zoll, Surface Laptop
   Ultra. Für die Reihenseiten fasst der Block `reihen` sie gröber zu Reihen
   zusammen, siehe unten.
2. **Modell**, Modellreihe plus Größenklasse, Edition und Plattform. Jedes Modell hat
   eine eigene Produktseite und einen eigenen Konfigurator. Intel, Snapdragon und
   NVIDIA sind immer getrennte Modelle.
3. **Ausführung**, die einzelne MSKU in products.json mit `specs.model`.

## Modellschlüssel
`{reihe}-{edition}-{plattform}`.
- `reihe`, die Modellreihe: `surface-pro`, `surface-pro-12-zoll`,
  `surface-laptop`, `surface-laptop-13-zoll`, `surface-laptop-ultra`. Neue
  Modellreihen nur über diesen Kontrakt. Dass `surface-pro`,
  `surface-laptop` und `surface-laptop-ultra` hier auch als Modellreihe
  vorkommen, ist erlaubt: ein
  Modellschlüssel hat immer Edition und Plattform dahinter und gleicht deshalb
  nie einem Reihenschlüssel.
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
      "gruppe": "13-8-und-15-zoll",
      "neu": false,
      "vorgaenger": false,
      "reihenfolge": 20 } ] }
```

- `neu`: wahr, solange Microsoft das Modell als neu führt.
- `vorgaenger`: wahr, wenn es eine neuere Edition derselben Reihe und Plattform gibt.
  Vorgänger stehen im Shop unter „Weiterhin erhältlich“.
- `reihenfolge`: kleiner zuerst, innerhalb der Reihe.
- `gruppe` (E-244): optional, Schlüssel einer Gruppe aus `gruppen` der Reihe,
  in der das Modell steht. Nur für Reihen mit Gruppen, siehe Abschnitt Reihen.
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
  { "key": "surface-laptop",
    "titel": "Surface Laptop",
    "gruppen": [ { "key": "13-zoll", "titel": "13 Zoll" }, … ],
    … },
  { "key": "surface-laptop-ultra",
    "titel": "Surface Laptop Ultra",
    "aktuell": ["surface-laptop-ultra-1-nvidia"],
    "vorgaenger": [],
    "rampenlicht": "surface-laptop-ultra-1-nvidia",
    … } ]
```

- `key`: Reihenschlüssel und Adresse der Reihenseite, `/de/geraete/{key}`.
  Heute genau `surface-pro`, `surface-laptop` und `surface-laptop-ultra`
  (ROUTEN-UND-SEO.md, Abschnitt 2, E-254). Neue Reihen nur über diesen
  Kontrakt.
- `titel`: Anzeigename der Reihe ohne Marke „Surface.Love“.
- `reihenfolge`: kleiner zuerst, etwa in der Geräteübersicht.
- `aktuell`: Liste der Modellschlüssel der aktuellen Modelle, in der
  Reihenfolge der Anzeige. Mindestens ein Eintrag.
- `vorgaenger`: Liste der Modellschlüssel, die die Seite unter „Weiterhin
  erhältlich“ zeigt. Darf leer sein.
- `rampenlicht`: genau ein Modellschlüssel aus `aktuell`, das Modell im
  Abschnitt Rampenlicht der Seite.
- `gruppen` (E-244): optional, die Gruppen der Modellwahl in der Reihenfolge
  der Anzeige. Je Gruppe `key` (Kleinbuchstaben, Ziffern, Bindestrich,
  eindeutig in der Reihe) und `titel`, der Name der Gruppe als Text, etwa
  „13 Zoll“. Fehlt das Feld oder ist es leer, hat die Reihe keine Gruppen und
  die Modellwahl steht wie bisher (Surface Pro).
- **Gruppe am Modell:** Hat eine Reihe Gruppen, trägt jedes Modell in
  `aktuell` ein Feld `gruppe` mit einem `key` aus `gruppen`. Die Pipeline
  prüft das vor dem Upload und lädt sonst nicht hoch. In der Gruppe stehen
  die Modelle in der Reihenfolge von `aktuell`. Eine Gruppe ohne gezeigtes
  Modell entfällt samt Überschrift. Bei Modellen in `vorgaenger` und in
  Reihen ohne Gruppen liest der Shop `gruppe` nicht.
- **Zuordnung:** Jedes Modell steht in höchstens einer Reihe, entweder in
  `aktuell` oder in `vorgaenger`. Surface Laptop 13 Zoll gehört zu
  `surface-laptop`, Surface Pro 12 Zoll zu `surface-pro`.
  **Einzige Ausnahme (E-254):** `surface-laptop-ultra-1-nvidia` steht in
  `aktuell` von `surface-laptop-ultra` und zugleich in `aktuell` von
  `surface-laptop`, dort als eigene Gruppe. Die Pipeline lässt genau diese
  doppelte Zuordnung zu und lehnt jede andere ab.
  Das Feld `reihe` eines Modells (Modellreihe) bleibt, wie es ist. Es ist
  feiner als der Reihenschlüssel und dient nur dem Modellschlüssel.
- **`umfasst` gehört nicht in `modelle.json`.** CC-Pricing darf die Reihe in
  der gepflegten Tabelle über die Modellreihen bilden, die sie umfasst.
  Ausgegeben werden nur `aktuell` und `vorgaenger`, der Shop liest nichts
  anderes.
- **Ein Reihenschlüssel ist nie zugleich ein Modellschlüssel,** und umgekehrt.
  Beide teilen sich das Segment `/de/geraete/`. Die Pipeline prüft das vor
  dem Upload und lädt sonst nicht hoch.
- Ein Modellschlüssel in `reihen`, den `items` nicht führt oder der keine
  gelistete Ausführung hat, wird übergangen. Hat eine Reihe dann kein
  aktuelles Modell mehr, leitet ihre Adresse dauerhaft mit 301 auf
  `/de/geraete` weiter, nicht 404, und fällt aus der Sitemap. So behält die
  Adresse, was sie sich erarbeitet hat (SL SEO 16177375, ROUTEN-UND-SEO.md,
  Abschnitt 8).
- **Die ab-Rate der Reihe wird ausgewählt, nicht gerechnet (E-099).** Der
  Shop nimmt je gelisteter Ausführung der Modelle in `aktuell` die beworbene
  ab-Rate nach PRICING.md, Abschnitt 6, also aus `rates.leasing` mit der
  beworbenen Laufzeit des Markts, nicht aus `rate_from`. Die kleinste davon
  zeigt er mit „ab“.
  **Vorgänger zählen nicht,** auch wenn ein Modell in `vorgaenger` günstiger
  ist. Kein Mittelwert, keine Rundung, keine eigene Rechnung. `reihen` trägt
  keine Rate.

### Reihe Surface Laptop Ultra (E-254)
- **Eine Reihe mit genau einem Modell.** `aktuell` trägt nur
  `surface-laptop-ultra-1-nvidia`, `rampenlicht` ist dasselbe Modell.
  `vorgaenger` ist leer, solange es keine ältere Edition gibt. Die Reihe hat
  keine `gruppen`. Die Daten liefert CC-Pricing (R14).
- **Reihenseite und Modellseite bleiben getrennt.** Die Reihenseite liegt
  unter `/de/geraete/surface-laptop-ultra`, die Modellseite mit Konfigurator
  bleibt unverändert unter `/de/geraete/surface-laptop-ultra-1-nvidia`.
  Konfiguriert wird nur auf der Modellseite.
- **Vorlage** ist die Reihenseite Surface Pro (Bauvorgabe R2 v2.2). Ob die
  Modellwahl mit einem einzigen Modell eine eigene Form braucht, entscheidet
  sich am Bild mit Claude Design (E-226), bevor gebaut wird. Bis dahin gilt
  die Modellwahl wie bei Surface Pro, ohne Gruppen.
- **ab-Rate** wie oben: die kleinste beworbene ab-Rate der gelisteten
  Ausführungen des einen Modells. Sie ist damit dieselbe wie auf der
  Modellseite.
- **Auf der Seite Surface Laptop bleibt die Gruppe Ultra** mit dem Modell
  und bekommt einen Verweis auf die neue Reihenseite, siehe Texte,
  `modellwahl.verweise`.
- **Live** geht die Seite erst, wenn alle drei Reihenseiten fertig sind,
  zusammen mit den Kacheln (E-239, E-254). Bis dahin leitet die Adresse nach
  der Regel oben mit 301 auf `/de/geraete`, weil ihre Texte fehlen.

### Modellwahl, Etikett und Vergleich der Reihenseite (E-244)
- **Überschriften:** H2 aus `modellwahl.h2` der Texte. Mit Gruppen trägt
  jede Gruppe ihren `titel` als H3, jede Karte darin ist eine H4. Der Name
  der Gruppe steht als echter Text im HTML der ersten Antwort, nie als Bild
  und nie im Code (SL SEO 16181284).
- **Raster:** Die Gruppen stehen nebeneinander in einem Raster, die
  Überschriften in einer Zeile, die n-te Karte jeder Gruppe in derselben
  Zeile. Unter 768 Breite stehen die Gruppen untereinander, jede mit ihrer
  H3. Aufbau in `brand/surface/bausteine-und-zustaende.md`, Reihenseite.
- **Etikett „Copilot+ PC“:** Eine Modellkarte trägt es nur, wenn alle
  gelisteten Ausführungen (`listed`) des Modells `copilot_plus` tragen
  (DATA-CONTRACT.md). Trägt es nur ein Teil, steht an der Karte keines. Die
  Ausführung selbst trägt es weiter nach VARIANTEN.md. Gilt für jede
  Modellkarte.
- **Vergleich:** Die Spalten folgen der Reihenfolge der Gruppen, darin der
  Reihenfolge von `aktuell`. Eine Zeile entfällt, wenn kein Modell der
  Tabelle den Wert hat, bei Surface Laptop etwa 5G. Hat ihn nur ein Teil der
  Modelle, bleibt die Zeile, und für die übrigen steht nichts ohne Beleg
  (SPECS.md).

## Texte der Reihenseite (content/de/reihen)
Die Texte stehen im Shop unter `content/de/reihen/{reihe}.json`, eine Datei je
Reihenschlüssel. CC-Marketing schreibt sie (R3, 8154), gegliedert nach dem
Konzept der Reihenseiten (P2, Abschnitt 4), seit E-238 nach der Bauvorgabe
v2.1 von Claude Design (R2, 8153). Titel und Beschreibung nach
ROUTEN-UND-SEO.md, Abschnitt 9.

```
{ "meta": { "titel": "…", "beschreibung": "…" },
  "hero": { "h1": "…", "erster_satz": "…", "rate_satz": "…",
            "sprung": { "id": "…", "text": "…" } },
  "leiste": { "name": "…" },
  "modellwahl": { "h2": "…", "satz": "…",
                  "lizenzkarte": { "seite": "…", "etikett": "…", "titel": "…",
                                   "zeile": "…", "satz": "…", "knopf": "…" },
                  "verweise": [ { "gruppe": "…", "reihe": "…", "text": "…" } ] },
  "kapitel_knopf": "…",
  "kapitel": [
    { "id": "…", "titel": "…", "satz": "…",
      "kennzahl": "…", "kennzahl_zeile": "…",
      "link": { "text": "…", "ziel": "/de/stories/…" } } ],
  "sicherheit": { "h2": "…", "karten": [ { "id": "…", "titel": "…", "satz": "…", "ziel": "…" } ] },
  "ki":         { "h2": "…", "karten": [ … wie sicherheit … ] },
  "service":    { "h2": "…", "karten": [ … wie sicherheit … ] },
  "rampenlicht": { "h2": "…", "satz": "…" },
  "tabelle":    { "h2": "…" },
  "zubehoer":   { "h2": "…", "satz": "…" },
  "andere":     { "h2": "…", "satz": "…" },
  "weiterhin":  { "h2": "…", "satz": "…" },
  "faq": [ { "frage": "…", "antwort": "…" } ],
  "abschluss": { "h2": "…", "zeile": "…", "knopf": "…" },
  "fussnoten": [ { "id": "…", "text": "…" } ] }
```

| Feld | Regel |
|---|---|
| `meta` | `titel` ohne Marke, höchstens 50 Zeichen, das Wichtigste in den ersten 45 (ROUTEN-UND-SEO.md, Abschnitt 9). `beschreibung` 120 bis 155 Zeichen. Keine Rate darin |
| `hero` | `h1` ist die einzige H1 der Seite. Zwei Felder statt des früheren `satz` (E-238): `erster_satz` steht unter der H1, genau ein Satz, ohne Rate. `rate_satz` steht im Band unter dem Hero, mit `{ab_rate}` und „netto im Monat“. Der Shop trennt nie selbst am ersten Punkt. `sprung` ist der Knopf zu einem Abschnitt der Seite, `id` ist die `id` dieses Abschnitts. `h1` steht als ein Element, am Handy bricht sie nur nach dem Namen der Reihe um (E-244, `bausteine-und-zustaende.md`, Reihenseite) |
| `leiste` | `name` steht in der klebenden Leiste unter dem Kopf, dem Band, links neben `rate_satz` aus `hero` |
| `kapitel_knopf` | Text des Knopfs in jeder Kapitelbox, etwa „Modell wählen“ (E-238). Ziel ist immer `#modelle`, es steht nicht im Text. Fehlt das Feld, steht in den Boxen kein Knopf |
| `modellwahl` | optional, „Modellwahl kurz“ (Konzept P2, Abschnitt 4, Nr. 2). `h2`, `satz` optional. Die Modellkarten kommen aus `aktuell` in `reihen` und aus `products.json`, nicht aus dem Text, die Gruppen aus `gruppen` in `reihen` |
| `modellwahl.lizenzkarte` | optional, Kartenart „Lizenz“ (E-244), eine Karte, die keine Modellkarte ist. `seite` ist der `slug` einer Seite aus `seiten` in `bausteine.json` (BAUSTEINE.md, Produktseiten), nie ein Pfad. Der Shop bildet daraus die Adresse nach ROUTEN-UND-SEO.md, Abschnitt 2. Fehlt die Seite in `seiten` oder ist `bausteine.json` nicht lesbar, entfällt die Karte, sie zeigt nie auf eine 404. `titel` ist die H4 und trägt den Link, der sich über die ganze Karte spannt. `knopf` führt zum selben Ziel, es bleibt bei zwei Links mit sichtbarem Text. `etikett`, `zeile` und `satz` sind optional. Keine Rate, kein Knopf „Konfigurieren“, keine Zahl im Text. Mit Gruppen steht die Karte als letzte in der letzten Gruppe, ohne Gruppen nach der letzten Modellkarte. Medium in IMAGES.md, Nachtrag Reihenseiten |
| `modellwahl.verweise` | optional, Verweis einer Gruppe auf eine eigene Reihenseite (E-254). Heute genau einer: auf der Seite `surface-laptop` die Gruppe Ultra auf `surface-laptop-ultra`. `gruppe` ist ein `key` aus `gruppen` dieser Reihe, `reihe` ein `key` aus `reihen`, nie ein Pfad. Der Shop bildet daraus `/de/geraete/{reihe}`. **Platz:** am Ende der Gruppe, nach ihren Modellkarten und vor einer Lizenzkarte, falls die Gruppe sie trägt. Ein Textlink mit sichtbarem `text`, kein Knopf, keine eigene Überschrift, keine Rate. Unter 768 Breite steht er unter der letzten Karte der Gruppe. **Wortlaut** schreibt CC-Marketing (R15, 8185), SL SEO prüft ihn. Fehlt die Gruppe, wird die Reihenseite nicht ausgeliefert oder leitet sie weiter, entfällt der Verweis (ROUTEN-UND-SEO.md, Regel 4.5). Ob der Platz am Bild so bleibt, entscheidet Claude Design mit Sascha (E-226) |
| `kapitel` | 4 bis 6 Einträge in der Reihenfolge der Anzeige. `id` ist ein kurzer Schlüssel aus Kleinbuchstaben und Bindestrich, eindeutig in der Datei, und verbindet das Kapitel mit seinen Medien (IMAGES.md, Nachtrag Reihenseiten). Die ids sind Sprungziele und je Reihe fest (E-244): `surface-pro` `leistung`, `display`, `zwei-in-eins`, `kamera`, `akku`, `surface-laptop` `leistung`, `display`, `tastatur`, `kamera`, `akku`. Für `surface-laptop-ultra` (E-254) sind sie noch nicht festgelegt, sie kommen mit R15 über diesen Kontrakt, bevor CC-Bilder die Medien der Kapitel liefert (R16). Ändern nur über diesen Kontrakt. `kennzahl` und `kennzahl_zeile` sind optional und stehen nur zusammen. `link` ist optional, mit `text` und `ziel`: ein Pfad im Shop ohne Host, etwa eine Story, der nicht weiterleitet (ROUTEN-UND-SEO.md, Regel 4.5). Fehlt eines der beiden Felder, steht kein Link |
| `sicherheit`, `ki`, `service` | je `h2` und Karten mit `id`, `titel`, `satz`. `ziel` ist optional, ein interner Pfad ohne Host, der nicht weiterleitet (ROUTEN-UND-SEO.md, Regel 4.5) |
| `rampenlicht` | `h2` und `satz`. Das Modell kommt aus `rampenlicht` in `reihen` |
| `tabelle` | nur `h2`. Die Zeilen kommen aus den Daten (`modelle.json`, `specs.json`). Eine Zeile entfällt, wenn kein Modell der Tabelle den Wert hat (E-244, Abschnitt Reihen) |
| `zubehoer`, `andere` | je `h2` und `satz`. `andere` verweist auf die anderen Reihen, seit E-254 sind es je Seite zwei |
| `weiterhin` | optional, „Weiterhin erhältlich“ (Konzept P2, Abschnitt 4, Nr. 9). `h2`, `satz` optional. Die Karten kommen aus `vorgaenger` in `reihen` und aus `products.json`. Ist `vorgaenger` leer, steht der Abschnitt nicht auf der Seite |
| `faq` | 10 bis 15 Einträge mit `frage` und `antwort` (E-232). Jede Frage ist echt, die Antwort steht im ersten Satz, keine Frage doppelt eine Frage der Modellseiten |
| `abschluss` | optional, das Abschlussband in `surface-deep` vor den Fußnoten (E-238). `h2` ist die Überschrift, `zeile` eine Zeile mit `{ab_rate}`, `knopf` der Text des Knopfs. Ziel ist immer `#modelle`. Fehlt der Block, steht kein Band |
| `fussnoten` | `id` und `text`. Verweise im Text auf eine Fußnote wie in `content/de/modelle/` |

- **Raten nur als Platzhalter `{ab_rate}`.** Der Shop setzt die ab-Rate der
  Reihe aus dem Abschnitt Reihen ein. Nie eine Zahl im Text (E-099). Fehlt
  die Rate, lässt der Shop den Satz mit dem Platzhalter weg.
- **Was der Shop einsetzt:** nur den Betrag mit Euro-Zeichen, im deutschen
  Format mit zwei Nachkommastellen und geschütztem Leerzeichen vor dem €,
  etwa „12,34 €“ (Beispiel erfunden). „ab“ und „netto im Monat“ stehen im
  Text um den Platzhalter, nicht im eingesetzten Wert.
- **Ohne Rate:** Fehlt die Rate, steht im Band nur `name` und im
  Abschlussband nur `h2` und Knopf.
- **Im HTML der ersten Antwort (SL SEO 16177375):** `erster_satz` unter der
  H1 und `rate_satz` im Band, mit eingesetzter Rate, stehen als echter Text
  im HTML, das der Server zuerst ausliefert. Nie per Skript nachgeladen oder
  erst im Browser eingesetzt.
- **`hero.satz` aus R1 entfällt.** CC-Marketing stellt die Texte mit R3 auf
  `erster_satz` und `rate_satz` um, bevor der Shop die Reihenseite baut
  (E-238, Reihenfolge der Merges). Der Shop liest `hero.satz` nicht.
- Fehlt ein optionaler Abschnitt, steht er nicht auf der Seite. Pflicht sind
  `meta`, `hero`, `kapitel` und `faq`. Fehlt die Datei, leitet die
  Reihenseite wie eine Reihe ohne aktuelles Modell mit 301 auf `/de/geraete`
  weiter und fällt aus der Sitemap (SL SEO 16177375).
- Microsoft-Namen nach IMAGES.md, Punkt 2. Keine Preise von Microsoft, keine
  Firmen- oder Lieferantennamen.

## Kacheln der Geräteübersicht (E-244, E-254)
Über „Alle Modelle“ auf `/de/geraete` stehen drei Kacheln als Einstieg. Die
Texte stehen in `content/de/devices.json`, CC-Marketing schreibt sie (R10,
8172).

**E-254 ändert E-244:** Die dritte Kachel, Surface Laptop Ultra, zeigt auf
die neue Reihenseite `/de/geraete/surface-laptop-ultra` statt auf die
Modellseite. Sie trägt deshalb `reihe` statt `modell`. Ihre `id` bleibt
`surface-laptop-ultra`, das Bild aus `kacheln.json` bleibt gültig.

```
"kacheln": {
  "liste": [ { "id": "surface-pro", "reihe": "surface-pro", "name": "…",
               "rate_satz": "…", "kurz": "…" },
             { "id": "surface-laptop", "reihe": "surface-laptop", … },
             { "id": "surface-laptop-ultra", "reihe": "surface-laptop-ultra",
               "name": "…", "rate_satz": "…", "kurz": "…" } ],
  "alle_modelle": "…" }
```

| Feld | Regel |
|---|---|
| `id` | Schlüssel der Kachel, verbindet sie mit ihrem Bild (IMAGES.md, Nachtrag Reihenseiten, Punkt 7) |
| `reihe` oder `modell` | genau eines. `reihe` ist ein `key` aus `reihen`, Ziel ist die Reihenseite. `modell` ist ein Modellschlüssel, Ziel ist die Modellseite. Seit E-254 tragen alle drei Kacheln `reihe`, auch Surface Laptop Ultra. Die frühere Festlegung „ein Modell und keine Reihe“ (SL SEO 16181284, E-244) ist damit abgelöst. `modell` bleibt im Schema für spätere Kacheln |
| `name` | Name der Reihe oder des Modells, H2 der Kachel und Linktext. Der Link sitzt in der H2 und spannt sich über die Kachel |
| `rate_satz` | Zeile unter dem Namen mit `{ab_rate}` und „netto im Monat“. Bei einer Reihe die ab-Rate der Reihe (Abschnitt Reihen), bei einem Modell die ab-Rate seiner Modellseite. Fehlt die Rate, entfällt die Zeile |
| `kurz` | optional, kurze Fassung des Linktexts von 768 bis 1279 Breite |
| `alle_modelle` | H2 über den Reitern und Karten der heutigen Übersicht |

- **Reihenfolge der Seite:** die H1 der Übersicht bleibt der erste Text,
  darunter die Kacheln in der Reihenfolge von `liste`, darunter
  `alle_modelle` als H2. Keine verborgene Überschrift über den Kacheln.
- **Wann sie stehen:** nur, wenn alle drei Reihenseiten ausgeliefert werden,
  also alle drei Reihen ein aktuelles Modell und ihre Texte haben (E-239,
  E-254). Sonst
  steht keine Kachel und `alle_modelle` entfällt mit. Fehlt das Ziel einer
  einzelnen Kachel, entfällt nur diese.
- Raten nur als Platzhalter, wie in den Texten der Reihenseite (E-099).

## Nicht in modelle.json
Keine Texte außer `title`, `title_short` und `titel` in `reihen` und in `gruppen`. Einleitung, Prozessor-Hinweis,
Kapitel, Vorteile, FAQ und Fußnoten pflegt der Shop unter content/de/modelle/.
Keine Preise, keine Raten, keine Firmen- oder Lieferantennamen.
