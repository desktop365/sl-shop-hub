# Bildspezifikation (images.json v2)

Maßgebliche Spezifikation für alle Produktbilder des Shops. Ersetzt das frühere Modell mit starrer
MSKU-Benennung.

## Idee in einem Satz
Nicht jede Produktvariante bekommt eigene Fotos. Es gibt ein Fotoset je Bildmodell, und jede MSKU wird
über eine Zuordnung auf ihr Bildmodell verwiesen.

## Warum
Der Distributor liefert viele Varianten je Gerät (CPU, RAM, Speicher, OS, Konnektivität), die sich
optisch nicht unterscheiden. Ein Bildmodell steht für eine einzigartige Kombination aus Familie,
Generation, Bildschirmgröße und Farbe. So genügen rund 25 Fotosets für den ganzen Katalog.

## Rollen
- Der Bild-Chat besitzt und pflegt images.json und erzeugt die Bilddateien.
- Die Preis-Pipeline liefert nur stabile MSKUs in products.json, keine Bildlogik.
- Der Shop-Resolver liest beide Dateien und verbindet sie über die MSKU.

## Schema von data/images.json
```
{
  "version": 2,
  "models": {
    "<slug>": {
      "family": "<familySlug>",      // z. B. surface-laptop, surface-pro, zubehoer
      "main":  "<datei>.webp",        // Hauptbild
      "thumb": "<datei>_thumb.webp",  // Vorschaubild
      "gallery": ["<datei>_open.webp", "..."]  // weitere Ansichten, kann leer sein
    }
  },
  "map": {
    "<MSKU>": "<slug>"                 // jede Varianten-MSKU zeigt auf ein Bildmodell
  }
}
```

## Dateinamen und Format
- Dateien sind je Bildmodell benannt (slug), nicht nach MSKU. Galeriebilder tragen sprechende Suffixe,
  zum Beispiel _open, _closed, _back, _left, _right, _top, _angle, _ports, _pen, _detail. Keine reinen
  Nummern.
- Nur Kleinbuchstaben, Ziffern und Bindestriche im slug, keine Leerzeichen, Umlaute oder Sonderzeichen.
  Groß- und Kleinschreibung der Dateinamen bleibt unverändert, die Auslieferung ist case-sensitiv.
- WebP, Qualität etwa 80. Kein PNG für Produktbilder, JPEG nur als Notfall.
- Hauptbild: quadratische Leinwand bis 1200 x 1200, Gerät proportional einpassen, nicht beschneiden,
  gleichmäßiger Rand. Vorschaubild bis 400 x 400, gleiches Motiv und Framing.
- Hintergrund transparent oder reines Weiß, Farbraum sRGB, Metadaten entfernen. Alle Geräte gleich groß
  im Bild, gleicher relativer Rand, gleiche Ausrichtung.
- Richtgröße Hauptbild unter etwa 200 KB, Vorschau unter etwa 40 KB.

## Aufnahmelisten je Familie
- Clamshell-Laptops: hero (Hauptbild), open, closed, back, left, right, top, optional detail.
- Tablets: hero mit Cover, tablet-only, back, angle, ports, optional pen.
- Zubehör: hero, optional eine zweite Ansicht.

## Fallback-Bilder
- Je Gerätefamilie ein Ersatzbild _fallback-{familySlug}.webp, zum Beispiel _fallback-surface-laptop.webp,
  _fallback-surface-pro.webp, _fallback-zubehoer.webp.
- Ein generisches _fallback.webp als letzte Stufe.

## Resolver im Shop
1. MSKU im map nachschlagen, ergibt den slug.
2. Fehlt die MSKU im map, den Schlüssel aus den Merkmalen des Artikels bilden (F-49, 24.11.2026):
   `specs.family`, `specs.generation`, `specs.size_inch` und `specs.color` aus products.json, in dieser
   Reihenfolge, als Slug wie oben, Größe mit Bindestrich statt Komma (13,8 wird 13-8). Gesucht wird
   absteigend: alle vier Teile, dann mit Farbe „platin“ (Erbregel 2), dann ohne Farbe, dann Reihe und
   Generation, dann Reihe allein. Der erste Treffer im models-Block gilt.
3. Modell im models-Block holen, Hauptbild und Vorschau anzeigen, die Galerie zeigt alle Ansichten
   des Modells.
4. Gibt es keinen Treffer, Fallback über die Familie (_fallback-{familySlug}.webp), sonst _fallback.webp.
Dateinamen kommen immer aus images.json, nie starr aus der MSKU konstruiert. Derselbe Schlüssel löst
auch das Datenblatt in specs.json auf (F-46).

## Ablage und Aufruf
- Alle Dateien nach gs://slshopv2-media/images/. Hochgeladen wird nach Fassung 3, Punkt 6 und 7.
- Öffentliche URL je Datei: https://storage.googleapis.com/slshopv2-media/images/{Dateiname}.

## Bildmodell-Matrix, entschieden 25.08.2026

Vier Festlegungen, sie beantworten die offenen Fragen weiter unten und sind
normativ.

1. **Surface Pro 12 Zoll und 13 Zoll sind getrennte Bildmodelle.** Die
   Bildschirmgröße ist Teil des Schlüssels, ein gemeinsames Fotoset gibt es
   nicht.
2. **Eine Farbe ohne beschaffbares Herstellerfoto erbt das Bildmodell von
   Platinum derselben Reihe und Größe** und wird als `foto_fehlt` geführt. Die
   Erbregel wird erst angewandt, wenn feststeht, dass zu einer Farbe kein Foto
   zu bekommen ist. Platinum wird deshalb zuerst fotografiert.
3. **5G ist ein Attribut, kein eigenes Bildmodell.** Ein 5G-Gerät erbt das
   Bildmodell von Generation und Größe.
4. **Slim-Pen-Bundles bekommen nur mit echtem Hersteller-Bundle-Foto ein
   eigenes Modell.** Sonst erben sie das Bildmodell der Tastatur.

Der Schlüssel eines Bildmodells lautet `familie-generation-groesse-farbe`,
Zubehör bekommt je Produkt ein eigenes Modell. Was sich aus dem Titel nicht
sicher bestimmen lässt, bleibt leer und wird als unsicher ausgewiesen, es wird
nicht geraten. Die abgeleitete Matrix und die Beschaffungsliste liegen im
privaten Repo `sl-bilder` unter `data/matrix.json` und
`docs/bildbedarf-2026-08-25.md`.

## Ableitung v2, entschieden 26.08.2026

Ergebnis des Abgleichs der Bildspezifikation v5 gegen diesen Kontrakt und die
Pipeline, Vorlage `berichte/bilder-v5-abgleich.md`. Diese fünf Punkte gehen den
älteren Abschnitten **Schema**, **Dateinamen und Format** und **Aufnahmelisten**
vor, wo sie ihnen widersprechen. Alles dort, was hier nicht angefasst wird,
gilt unverändert weiter.

1. **Ausgabemodell.** Je Bildmodell und Ansicht ein Breitenset 160, 400, 800 und
   1200 als WebP. 1600 und 2400 nur für die Leitansicht. Rückwärtskompatibel:
   `{key}.webp` bleibt Alias der 1200er Hauptansicht, `{key}_thumb.webp` Alias
   der 400er. Der bestehende Resolver läuft dadurch unverändert weiter, `main`
   und `thumb` im Schema behalten ihre Bedeutung. AVIF darf zusätzlich entstehen,
   wenn die Kodier-Umgebung es trägt, es blockiert WebP nie: fällt AVIF aus,
   wird trotzdem ausgeliefert.
2. **Hintergrund.** Transparent ist verbindlich, Kontaktschatten liegt im
   Alphakanal. Voraussetzung sind freigestellte Quellen, geprüft wird das am
   Beweismodell, bevor die Strecke breit läuft. Eine Quelle, die sich nicht
   freistellen lässt, bekommt ausnahmsweise Weiß und wird in der Matrix
   vermerkt, damit die Ausnahme sichtbar bleibt und nicht zur Regel wird.
3. **Benennung.** Matrix-Schlüssel plus Ansichtsvokabular aus v5, einfacher
   Bindestrich, Breite vor der Endung:
   `{key}-{ansicht}-{breite}.webp`. Ansichten sind `front-open`,
   `three-quarter`, `side-closed`, `detail`, `back`. Beispiel:
   `surface-laptop-8-13-8-platin-front-open-1200.webp`. Keine doppelten
   Bindestriche, keine Breite im Schlüsselteil.
4. **Manifest.** Es gibt genau **eine** `images.json` in Version 2, und sie trägt
   beide Ebenen. `map` bleibt unangetastet, jede MSKU zeigt auf ein Bildmodell,
   das ist die Brücke von der Preis-Seite zum Bild. `models` wird um die je
   Modell verfügbaren Ansichten und Breiten erweitert, damit der Konfigurator
   seine Slots füllen kann. Ein separates v5-Manifest wird nicht geführt, es
   verlöre die MSKU-Brücke.
5. **Farben.** Der Konfigurator zeigt nur Farben, die Feed und Matrix kennen,
   derzeit platin und schwarz. Consumer-Farben ohne B2B-Artikel werden nicht
   vorgehalten, weder als Auswahl noch als Bildmodell.

## Fassung 3, entschieden 24.11.2026 (E-168 bis E-171)

Gilt vor allen älteren Abschnitten, wo sie widersprechen. Was hier nicht
angefasst wird, gilt weiter.

### 1. Schlüssel
Der Schlüssel eines Bildmodells bleibt `familie-generation-groesse-farbe`.
`generation` ist die Edition, wie Microsoft sie zählt, genau wie in
`specs.generation` (MODELLE.md). Beispiel: Surface Pro 12 Zoll, 2. Edition,
Platin heißt `surface-pro-2-12-platin`. Die Brücke von der MSKU zum Bildmodell
bleibt `map`, sie hängt nicht am Schlüsselschema.

### 2. Drei Bildarten
| Bildart | Katalog | Inhalt |
|---|---|---|
| Produktfoto | `images.json` v2 | freigestelltes Gerät oder Zubehör, transparent, quadratische Leinwand, Ansichten nach Ableitung v2 |
| Lifestyle | `medien.json` je Modell | Gerät im Einsatz, mit Menschen oder Umgebung, für die Kapitel der Modellseite |
| Film | `medien.json` je Modell, Datei je Reihe | kurzer Produktfilm, einmal je Reihe |

Ein Lifestyle-Motiv steht nie als Produktfoto in `images.json`. Karten,
Konfigurator, Anfrage und Fotokatalog zeigen nur Produktfotos.

### 3. medien.json
Eine Datei je Modell unter `media/modelle/{modellschluessel}/medien.json` im
Bucket slshopv2-media, Modellschlüssel nach MODELLE.md. Pfade gelten ab der
Bucket-Wurzel.
```
{ "version": 1,
  "modell": "surface-laptop-8-intel",
  "stand": "2026-11-24",
  "kapitel": [
    { "thema": "alltag",            // tastatur | anschluesse | display | kamera | alltag
      "alt": "Kurzer deutscher Alt-Text",
      "quer": { "verhaeltnis": "3:2", "breiten": [800, 1200, 1600],
                "dateien": { "800": "media/modelle/<modell>/alltag-1-quer-800.webp" } },
      "hoch": { "verhaeltnis": "4:5", "breiten": [800, 1200],
                "dateien": { "800": "media/modelle/<modell>/alltag-1-hoch-800.webp" } } } ],
  "film": { "alt": "...",
            "quer": { "datei": "media/reihen/<reihe>/film-quer.mp4", "breite": 1920, "hoehe": 1080,
                      "dauer_s": 28, "poster": "media/reihen/<reihe>/film-quer-poster.webp" },
            "hoch": { "datei": "media/reihen/<reihe>/film-hoch.mp4", "breite": 1080, "hoehe": 1350,
                      "dauer_s": 28, "poster": "media/reihen/<reihe>/film-hoch-poster.webp" } } }
```
- `kapitel`: 0 bis 6 Einträge, mehrere je Thema erlaubt. Fehlt ein Thema, gibt es
  kein Ersatzbild.
- `breiten` nennt nur, was wirklich erzeugt wurde. Es wird nie hochskaliert.
- `film`: liegt einmal je Reihe unter `media/reihen/{reihe}/`, Reihen nach
  MODELLE.md. Ohne Film steht dort `null`.
- Keine Herkunftsangaben, keine Paketnamen, keine Lieferantennamen.
- Welches Kapitel welches Motiv zeigt, legt der Modelltext im Shop fest
  (`content/de/modelle/{modell}.json`, Feld `medium` mit dem Thema). Fehlt
  `medium`, gilt das Feld `bild` mit einer Ansicht aus `images.json`.

### 4. Plätze im Shop und Breiten
Der Shop baut `srcset` aus den Breiten, die im Katalog stehen, und gibt je Platz
`sizes` an. Der Server kodiert die Bilder nicht neu, sie sind schon fertig
kodiert.

| Platz | Quelle | Breiten im srcset | Handy |
|---|---|---|---|
| Modellkarte, Übersicht und Vergleich | Produktfoto, Leitansicht | 400, 800, 1200 | dasselbe Motiv |
| Ausführungsliste, Anfrage, Korb, Zubehörkarte | Produktfoto | 160, 400, 800 | dasselbe Motiv |
| Fotokatalog der Modellseite | Produktfoto, alle Ansichten | 800, 1200, 1600, 2400 | dasselbe Motiv |
| Daumen im Fotokatalog | Produktfoto | 160 | dasselbe Motiv |
| Kapitel der Modellseite | Lifestyle | quer 800, 1200, 1600 | hoch 4:5, 800, 1200 |
| Film der Modellseite | Film | quer 1920×1080 | hoch 1080×1350 |

Die Grenze zwischen Handy und Desktop liegt für Lifestyle und Film bei 800 px
Breite. Filme laufen stumm, starten erst im Sichtbereich, zeigen vorher das
Poster und respektieren `prefers-reduced-motion`.

### 5. Qualität und Richtwerte
- Bilder als WebP, Qualität etwa 80, sRGB, ohne Metadaten, nie hochskaliert.
- Produktfoto: 1200 unter etwa 200 KB, 400 unter etwa 40 KB.
- Lifestyle: 1600 unter etwa 350 KB.
- Film: H.264, CRF 28, höchstens 30 Sekunden, ohne Tonspur, `faststart`,
  unter etwa 8 MB je Datei. Poster als WebP.
- Originale aus dem Partnerportal sind Druckdaten und gehen nie in den
  öffentlichen Bucket.

### 6. Ablage
**Öffentlich, slshopv2-media** (der Shop liest nur hier):
- `images.json` im Root, Produktfotos unter `images/`.
- Lifestyle und `medien.json` unter `media/modelle/{modell}/`.
- Filme und Poster unter `media/reihen/{reihe}/`.

**Privat, slshopv2-assets** (nie öffentlich):
- `zip/{datum}/` die Pakete aus dem Partnerportal, so wie geladen.
- `archiv/{datum}/{paket}/` die entpackten Originale in voller Auflösung.
- `build/{datum}/` der vollständige Bau eines Laufs, für Neuaufbau und Rückweg.
- `backup/{datum}/` die Kataloge vor jedem Upload.
- `_katalog.json` als Inhaltsverzeichnis für alle vier Bereiche: Datum, Paket,
  Bildmodell oder Modell, Größe, Prüfsumme.

Cache-Control: Bilder und Filme `public, max-age=86400`, Kataloge
(`images.json`, `medien.json`) `public, max-age=300`. Hochgeladen wird in dieser
Folge: Dateien, dann `medien.json`, zuletzt `images.json`.

### 7. Lokal und Git
- Das Repo der Bild-Strecke enthält Skripte, Tests, Dokumente und die
  Datendateien (Zuordnung, Bedarf, Matrix, Abdeckung, dazu eine Kopie von
  `images.json` und den `medien.json` für die Historie). Keine ZIPs, keine
  Originale, keine erzeugten WebP- oder MP4-Dateien. Ausnahme bleibt das kleine
  Fallback-Set.
- Lokal liegt nur der Stapel, der gerade bearbeitet wird. Jede Datei geht zuerst
  in den privaten Bucket, die Prüfsumme wird verglichen, erst dann wird die
  lokale Kopie gelöscht. Wer eine Datei wieder braucht, holt sie aus dem Bucket.
- Hochgeladen wird mit dem Upload-Dienstkonto der Bild-Strecke (INFRA.md,
  Abschnitt 3).

### 8. Abdeckungsbericht
Nach jedem Upload ein Bericht am Board, Story der Bilder, Tabelle je Modell:
gelistete Ausführungen, Bildmodelle, Farben, Ansichten, Lifestyle-Motive, Film,
Lücken mit Grund. Dieselben Zahlen stehen maschinenlesbar in der
Abdeckungsdatei im Repo der Bild-Strecke. Für alle anderen Chats ist die Wahrheit
`images.json` und `medien.json` im öffentlichen Bucket.

### 9. Sichtbar im Shop
- `images.json` kommt über den Katalog-Sync ins Leseabbild des Shops. Der Sync
  läuft nach jedem Nachtlauf. Ein Upload vor 04:00 UTC ist am Morgen sichtbar.
- `medien.json` liest der Shop zur Laufzeit, mit Neuvalidierung nach höchstens
  einer Stunde.

## Nachtrag Bausteine und Dienste, entschieden 25.11.2026 (E-185, W6)

### 1. Herkunft und Recht
Surface.Love ist Microsoft-CSP-Partner und Surface Authorized Reseller. Auf
dieser Grundlage zeigt der Shop Microsofts App-Logos und Bilder zu den Produkten,
die er anbietet (Entscheidung Sascha, 25.11.2026). Microsoft-Medien liegen nur im
privaten Repo der Bild-Strecke und im Bucket slshopv2-media, nie in diesem Hub.
Das Hub nennt nur Schlüssel, Pfade und Regeln.

### 2. Darstellung der Logos
- Unverändert: nicht verzerren, nicht beschneiden, nicht umfärben.
- Größe im Shop 32 px, nie unter 16 px. Alle Logos einer Reihe gleich breit und
  senkrecht mittig. Liegt ein Rasterbild kleiner als 32 px vor, steht es in seiner
  Originalgröße mittig im 32er Feld und wird nie hochskaliert. SVG wird auf 32 px
  gezeigt.
- Der Name neben dem Logo lautet so, wie Microsoft ihn auf seiner Planseite neben
  dem Logo führt, zum Beispiel „Word“, „Microsoft Teams“, „Microsoft Entra ID“,
  „Windows 11“. Der Shop liest ihn aus `content/de/bausteine/dienste.json`, Feld
  `name`. Für `copilot` lautet er „Microsoft 365 Copilot“.
- Der Name steht immer als Text daneben, das Logo trägt ein leeres `alt`. Der
  Abstand zum Namen ist mindestens ein Viertel der Logobreite, bevorzugt die
  Hälfte. Der Name steht in `ink` oder `ink-muted`, nie in der Farbe des Produkts.
- Logos stehen nur im Raster „Enthalten“ der Produktseiten und in der
  Schnellansicht, nicht als Schmuck und nie größer als unsere eigene Marke.
- Im Text steht bei der ersten Nennung „Microsoft“ vor dem App-Namen. Nie „M365“.
  Kein Satz deutet eine Empfehlung durch Microsoft an.

### 3. Ablage im Bucket slshopv2-media
- Logos unter `media/dienste/dienst-{schluessel}.svg`, nur wo Microsoft kein SVG
  anbietet als `.png` mit der größten verfügbaren Kantenlänge. Schlüssel wie in
  BAUSTEINE.md, Abschnitt Produktseiten.
- Katalog `media/dienste/dienste.json`:
  `{ "version": 1, "stand": "JJJJ-MM-TT", "dienste": { "word": { "datei": "media/dienste/dienst-word.svg", "breite": 48, "hoehe": 48 } } }`.
  Fehlt ein Schlüssel, zeigt der Shop nur den Namen, mit gleich breitem leerem Platz.
- Aufmacher der Produktseiten sind Lifestyle (Fassung 3, Punkt 2) und liegen unter
  `media/bausteine/{seite}/` mit einer `medien.json` nach Fassung 3, Punkt 3.
  `modell` ist der Seitenschlüssel, das einzige Kapitel hat `thema: "aufmacher"`,
  quer 3:2 in 800, 1200, 1600, hoch 4:5 in 800, 1200. Reicht die Quelle für hoch
  nicht, steht dort `null`, und das Handy zeigt die Fassung quer.
- Kleine Bilder der Bausteine für Ausstattung, Schnellansicht und Warenkorb kommen
  in `images.json` v2: Modelle mit `family: "baustein"`, nur die Ansicht
  `front-open`, Breiten 160, 400, 800, 1200. Dazu der optionale Block
  `bausteine`, er bildet den Baustein-Schlüssel auf den Slug im Block `models` ab.
  `map` bleibt MSKU zu Slug. Fehlt ein Eintrag, zeigt der Shop das bisherige Symbol.
- Cache-Control und Upload-Folge wie Fassung 3, Punkt 6: Dateien, dann
  `dienste.json` und `medien.json`, zuletzt `images.json`.

### 4. Bilder im Warenkorb
Der Warenkorb speichert keine Bildadressen. Er löst das Bild beim Anzeigen auf,
für Geräte über `map` und die MSKU, für Bausteine über `bausteine`. So bekommen
auch Positionen aus einem geteilten Link (`?pos=`) ihr Bild.

## Nachtrag Startseite, entschieden 26.11.2026 (E-194)

Gilt für die Medien der Startseite nach der Bauspezifikation Startseite
(E-194). Was hier nicht steht, gilt aus Fassung 3. Microsoft-Medien sind nach
E-185 erlaubt, liegen aber nur im Repo der Bild-Strecke und im Bucket, nie in
diesem Hub (Nachtrag Bausteine, Punkt 1). Es zeigt nur Geräte in Platin oder
Schwarz (SICHTBARKEIT.md, Farbregel E-195).

### 1. Datei und Pfade
- Katalog: `media/startseite/medien.json` im Bucket slshopv2-media.
- Jede Datei, auf die der Katalog zeigt, liegt unter `media/startseite/`.
  Pfade gelten ab der Bucket-Wurzel, wie in Fassung 3.
- Bilder als WebP nach Fassung 3, Punkt 5, Freisteller mit Alphakanal.
- Filme als MP4 ohne Tonspur, sonst wie Fassung 3, Punkt 5. Poster als WebP.
- `breiten` nennt nur, was wirklich erzeugt wurde. Es wird nie hochskaliert,
  auch nicht, wenn eine Richtbreite unten größer ist als die Quelle.
- Cache-Control und Upload-Folge wie Fassung 3, Punkt 6: erst die Dateien,
  zuletzt `medien.json`. Der Shop liest die Datei zur Laufzeit wie Fassung 3,
  Punkt 9.

### 2. Zwei Formen, dieselben wie Fassung 3, Punkt 3
**Fassung**, ein Bild in mehreren Breiten:
```
{ "verhaeltnis": "3:2", "breiten": [800, 1600],
  "dateien": { "800": "media/startseite/<datei>-800.webp",
               "1600": "media/startseite/<datei>-1600.webp" } }
```
`verhaeltnis` ist das echte Seitenverhältnis der Dateien, gekürzt, als
`"Breite:Höhe"`. Zu jeder Breite in `breiten` gibt es genau einen Eintrag in
`dateien`.

**Film**, eine Datei:
```
{ "datei": "media/startseite/<film>.mp4", "breite": 1920, "hoehe": 1080,
  "dauer_s": 12, "poster": "media/startseite/<film>-poster.webp" }
```
Die Felder heißen wie im Film von Fassung 3 (`datei`, nicht `src`), damit der
Shop für beide Kataloge denselben Leser nutzt.

### 3. Schema
```
{ "version": 1,
  "stand": "2026-11-26",
  "einstieg": {
    "surface-pro":          <Fassung>,
    "surface-laptop":       <Fassung>,
    "surface-laptop-ultra": <Fassung> },
  "buehne": [
    { "id": "prozessor",  "alt": "...", "quer": <Fassung>, "hoch": <Fassung> | null, "film": <Film> | null },
    { "id": "sicherheit", ... }, { "id": "akku", ... }, { "id": "display-kamera", ... } ],
  "ki": [
    { "id": "...", "alt": "...", "film": <Film>, "standbild": <Fassung> } ],
  "schutz": { "alt": "...", "quer": <Fassung>, "quadrat": <Fassung> } }
```

| Platz | Abschnitt der Bauspezifikation | Inhalt | Richtwerte |
|---|---|---|---|
| `einstieg` | 4, Einstiegskarten | je Reihe ein Freisteller mit Alphakanal, Schlüssel wie `specs.family` (DATA-CONTRACT.md). Kein `alt`: die Karte trägt den Namen, das Bild steht mit leerem `alt` | Breiten 572 und 1144, soweit die Quelle reicht |
| `buehne` | 6, Scroll-Bühne | genau die vier `id` in dieser Reihenfolge: `prozessor`, `sicherheit`, `akku`, `display-kamera`. `quer` für die Fläche ab 1024 Breite, `hoch` für die Karten darunter, `film` nur ab 1024 Breite | `quer` 29:16 in 1160 und 2320, `hoch` 4:3 in 780, Film höchstens 1920 breit |
| `ki` | 7, Kartenreihe KI und Copilot | drei bis fünf Karten in der Reihenfolge der Anzeige. `id` ist ein kurzer Schlüssel aus Kleinbuchstaben und Bindestrich, eindeutig in der Liste. `standbild` steht vor dem Start und bei reduzierter Bewegung | Film 4:5, 928 × 1160, Standbild 4:5 |
| `schutz` | 8, Support und Schutz | `quer` ab 1024 Breite, `quadrat` darunter | `quer` 16:9 in 1280 und 2560, `quadrat` 1:1 in 780 und 1000 |

- `alt` ist ein kurzer deutscher Alt-Text, wie in Fassung 3. Für Filme gilt der
  `alt` des Eintrags für das Poster, der Film selbst ist `aria-hidden`.
- Keine Herkunftsangaben, keine Paketnamen, keine Lieferantennamen, keine
  Dateinamen der Quelle (Fassung 3, Punkt 3).
- Welche Texte und Kennzahlen zu einer `id` gehören, steht in den Texten des
  Shops (`content/de/`), nicht in diesem Katalog.

### 4. Wenn etwas fehlt
Der Shop zeigt die Startseite immer, ohne Fehler und ohne Platzhalterbild.
- **Datei fehlt oder ist nicht lesbar:** alle Abschnitte stehen ohne diese
  Medien. Der Shop schreibt einen Hinweis ins Log, nie auf die Seite.
- **Ein Platz fehlt oder ist `null`:** der Abschnitt steht ohne Medien.
  Einstiegskarte ohne Bild: nur Text. Bühne ohne Medium: die Folie auf
  `surface-deep`. Schutz ohne Bild: Text auf `surface-deep`.
- **`hoch` ist `null`:** die Karte unter 1024 Breite zeigt einen Ausschnitt aus
  `quer`.
- **`film` ist `null`:** es steht das Bild aus `quer`.
- **KI-Karte ohne lesbaren `film`:** es steht das `standbild`. Fehlt auch das,
  entfällt die Karte.
- **Unbekannte `id` in `buehne`:** wird nicht gezeigt. Fehlt eine der vier,
  zeigt die Bühne die übrigen.

## Offene Fragen, vor der finalen Bildmatrix zu klären
**Alle vier am 25.08.2026 entschieden, siehe Abschnitt Bildmodell-Matrix. Der
Wortlaut bleibt als Beleg stehen, welche Frage womit beantwortet wurde.**
- Surface Pro 12 Zoll Snapdragon gegen Surface Pro 13 Zoll Intel, wirklich unterschiedliche
  Bildschirmgröße oder ein Bildmodell.
- Surface Laptop 13 Zoll, gibt es die Farbe Schwarz.
- Surface Laptop 5G, welche Generation, teilt er die Fotos mit dem Laptop 8.
- Slim-Pen-Bundles, eigene Bundle-Fotos oder erben sie das Tastaturbild.

## Workflow
Abgelöst durch Fassung 3, Punkt 6 und 7. Quellbilder kommen nicht mehr ins Repo, der Upload läuft
über die Bild-Strecke selbst.
