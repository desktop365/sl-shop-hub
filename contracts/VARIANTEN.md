# VARIANTEN, das zweistufige Produktmodell

## Modell
Der Katalog kennt zwei Ebenen. Oben die Modellreihe (Surface Laptop, Surface
Pro, weitere nach Sortiment), darunter die Varianten mit den Dimensionen
Bildschirmgroesse, Prozessor, Hauptspeicher, Speicherkapazitaet, Farbe.
Der Katalog zeigt Modellreihen, die Produktseite ist der Variantenwaehler.
Zubehoer bleibt einstufig.

## Herkunft der Struktur
Der Feed liefert flache Artikel je MSKU. Die Zuordnung MSKU zu Modellreihe
plus Attributen entsteht in einer Zuordnungsschicht: automatisch geparst wo
verlaesslich, kuratiert im Admin wo noetig (Ausbaustufe laut ADMIN.md,
Anzeigenamen und MSKU-Zuordnung). Faellt eine MSKU durch die Zuordnung,
erscheint sie einstufig mit Rohnamen, nie gar nicht.

## Wirkung
Bildmatrix (IMAGES.md) und Variantenmodell teilen denselben Schnitt je
Reihe, Generation, Groesse, Farbe. Raten kommen unveraendert je MSKU aus
products.json, das Variantenmodell ordnet nur an, es rechnet nie.
