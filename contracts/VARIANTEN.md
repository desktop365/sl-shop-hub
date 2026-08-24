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

## Kuratierte Ausstattungsstufen (Ergaenzung 24.08. abends, aus UX-VARIANTEN-KONZEPT.md)
Prozessor, Hauptspeicher und Speicherkapazitaet werden dem Kunden nicht einzeln
angeboten, sondern zu zwei bis drei benannten Stufen je Produkt und Groesse
gebuendelt (essential, advanced, performance), jede mit Empfehlungssatz in
Kundensprache und voller Spezifikation als Nebenzeile. Nicht jede lieferbare
Kombination wird angeboten, Exoten bleiben auf Anfrage ueber den Vertrieb.

Kurations-Daten, kein Hardcode: die Zuordnung MSKU zu Stufe, die
Empfehlungstexte, das Beliebt-Flag der Vorauswahl UND die Produktkarten der
Ebene 1 selbst (welche Modellreihen als Karte erscheinen, inkl. Zustand
"demnaechst verfuegbar" fuer Reihen ohne bestellbare Varianten im Feed, z. B.
Surface Laptop Ultra vor Marktstart) werden im Admin gepflegt, Erstbefuellung
durch uns. Delta-Raten an nicht gewaehlten Optionen sind Differenzen
oeffentlicher Raten aus products.json, bezogen auf die aktuelle Auswahl samt
Vertragsart und Laufzeit, nie auf eine veraltete Basis, es wird nie gerechnet,
was nicht aus products.json kommt.
