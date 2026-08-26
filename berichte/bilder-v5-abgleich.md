# Abgleich Bildspezifikation v5 gegen IMAGES.md und Pipeline

Vorschlag des Bilder-Chats, Stand 26.08.2026. Gehoert nach berichte/ im Hub.
Regel laut Master: bei Widerspruch gilt contracts/IMAGES.md, dies ist ein
Aenderungsvorschlag, keine einseitige Umstellung.

## Was uebereinstimmt, bleibt
- Quadratischer Master fuer alle Kontexte.
- 1200 px reicht fuer alle regulaeren Kontexte, groesster ist rund 570 px.
- Proportional einpassen, zentriert, nie hochskalieren, Metadaten entfernen.
- WebP als Hauptformat.

## Konflikt 1, Ausgabemodell
IMAGES.md und bilder_bauen.py: zwei Dateien, {key}.webp und {key}_thumb.webp.
v5: Breitenset 160/400/800/1200/1600, plus 2400 nur fuer die Leitansicht, plus
AVIF neben WebP, PNG-Fallback nur fuer 1200.
Vorschlag: bilder_bauen.py auf ein Breitenset umstellen, rueckwaertsvertraeglich.
Thumbnail entfaellt, die 160er und 400er Stufe ersetzen es. AVIF zusaetzlich, wenn
die ARM-Umgebung es beim Kodieren mittraegt, sonst WebP zuerst, AVIF nachziehen.

## Konflikt 2, Hintergrund
IMAGES.md: weiss oder transparent. v5: transparent, Kontaktschatten im Alphakanal.
Vorschlag: transparent verbindlich machen. Voraussetzung, die Quell-PNG sind
freigestellt. Am Beweismodell zuerst pruefen, ob der Alphakanal sauber ist.

## Konflikt 3, Benennung
Matrix: surface-laptop-8-13-8-platin, Suffixe _open _closed _back _left _right.
v5: surface-laptop--jade--front-open--1200.webp, doppelte Bindestriche, Breite im
Namen, Ansichten front-open three-quarter side-closed detail.
Vorschlag: eine der beiden Konventionen verbindlich waehlen. Empfehlung, das
Ansichtsvokabular von v5 uebernehmen, weil es sprechender ist, aber bei einfachem
Bindestrich und der Matrix-Schluesselstruktur bleiben. Breite als Suffix vor der
Endung. Beispiel: surface-laptop-8-13-8-platin-front-open-1200.webp.

## Konflikt 4, Manifest, der wichtigste Punkt
IMAGES.md v2: models plus map, map zeigt jede MSKU auf ein Bildmodell. Das ist die
Aufloesung Variante zu Bild, die der Shop braucht.
v5: flaches Manifest geraet, farbe, ansicht, breite, datei, ohne MSKU.
Ein reines v5-Manifest verliert die MSKU-Bruecke.
Vorschlag: ein Manifest, das beide Ebenen traegt.
- map: MSKU zeigt auf ein Bildmodell, wie bisher.
- models: je Bildmodell die verfuegbaren Ansichten und Breiten als Liste, sodass
  der Konfigurator seine Slots ueber geraet, farbe, ansicht, breite fuellen kann.
So bleibt die Preis-Seite ueber die MSKU bedient und die Design-Seite ueber die
Slots, aus einer Datei.

## Konflikt 5, Farben, kein Technikproblem sondern Datenlage
v5 rechnet mit sechs Farben: Platin, Saphir, Graphit, Jade, Dune, Schwarz, pro
Farbe ein echtes Ger"aet.
Feed und Matrix kennen zwei: platin und schwarz. Saphir, Jade, Dune, Graphit sind
Consumer-Farben, im B2B-Sortiment nicht vorhanden, weder als Artikel noch als
Herstellerfoto.
Vorschlag: fuer Surface B2B nur platin und schwarz vorsehen. Der Konfigurator
zeigt nur real verkaufte Farben. Das Sechs-Farben-Modell fuer eine spaetere
Marke oder Consumer-Linie zuruueckstellen. Entscheidung liegt bei Master und
Design, nicht beim Bilder-Chat.

## Beruehrt nicht die Archiv-Stufe
All dies betrifft nur Stufe zwei, die Ableitung fuer den Shop. Das Archiv der
Original-Renders in voller Aufloesung ist davon unberuehrt und laeuft sofort,
sobald der private Bucket steht.
