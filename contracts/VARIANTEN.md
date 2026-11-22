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
