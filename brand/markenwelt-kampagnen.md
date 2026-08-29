# Markenwelt und Kampagnenflächen, Ergänzung zur v6-Runde

Strom 50, Stand 2026-08-29. Entschieden von Sascha im Review am 29.08.:
Use-Case-Kacheln auf Startseite und Geräte-Seite, das Microsoft-Hero-Video
bleibt und die Kampagne wird zweite Bühne darunter, Umsetzung integriert in
die anstehende v6-Design-Runde (zusammen mit refurbished-ux-r6.md). Dieses
Dokument ist die zweite Grundlage des v6-Auftrags an Claude Design.

Leitgedanke: Der Shop verkauft eine Art zu arbeiten, nicht nur Geräte.
work love balance ist wörtlich die Kampagnenbotschaft. Emotion und
Konversion trennen sich dabei sauber: Stimmungsflächen tragen nie einen
Primärbutton, jeder Screen behält genau eine Hauptaktion, und das
Gerätefoto im Konfigurator bleibt die Produktwahrheit (E-019),
Kampagnenmotive sind Ambiente und Markenwelt.

## 1. Kampagnenflächen sind Daten, nicht Code

Vier Slot-Flächen, gepflegt als Kurations-Daten ohne Deploy (E-011-Geist):

| Slot | Fläche | Format | Inhalt |
|---|---|---|---|
| buehne2 | Kampagnen-Bühne unter dem Hero | sehr breit, ca. 21:9 | ein Motiv, Headline, Subzeile, sekundärer Link |
| mood | Mood-Band zwischen den Sektionen | breit, ca. 21:9 | Motiv mit einem Satz Haltung, optional Link |
| usecase | Use-Case-Kacheln | 4:5, vier Motive | Arbeitssituationen, je ein Ziel im Konfigurator |
| inspiration | Teaser-Reihe vor dem Footer | 3:2, drei Motive | redaktionelle Inhalte, Texte aus Strom 95 |

Datensatz je Slot: slot_id, flaeche, storefront, bildmodell_ref oder
asset_ref, headline, subzeile, link_ziel, zeitraum_von, zeitraum_bis,
aktiv. Use-Case-Kacheln zusätzlich: ziel_familie, optional ziel_groesse
(Vorbelegung im Konfigurator). Beide Storefronts nutzen dieselben Slots
mit eigenen Assets, die Lenovo-Storefront ohne jedes Microsoft-Medium.

## 2. Startseiten-Architektur v6

Konsolidierung statt Stapelung, die Seite wird nicht länger:

1. Hero mit Microsoft-Video, unverändert.
2. NEU Kampagnen-Bühne (Slot buehne2): eigene Markenwelt, ruhige Headline
   in Kampagnensprache, sekundärer Link, kein Primärbutton.
3. Drei Familienkarten plus Refurbished-Band (aus r6), unverändert früh.
4. ERSETZT Use-Case-Kacheln "So arbeitet Ihr Team" an der Stelle der
   bisherigen vier Microsoft-Videokarten, gleiches 4:5-Raster: Unterwegs,
   Im Büro, Beim Kunden, Nach Feierabend. Klick öffnet den Konfigurator
   mit passender Familie und Größen-Vorbelegung. Die Kacheln sind damit
   der Ersatz für die Referenzvideos, nicht eine zusätzliche Sektion.
5. Video-Akkordeon, unverändert (Referenz bis eigenes Material vorliegt).
6. ERSETZT Mood-Band (Slot mood) auf der durch r6 freigewordenen Fläche
   des früheren Refurbished-Splits, mit einem der eigenen Motive (Lounge,
   ICE) und einem Satz Haltung, ohne Produktpitch.
7. Sorglos-Kacheln, Texte menschlicher im Dexity-Ton ("Wir antworten
   selbst, schnell und direkt", die Vanity-Nummer gehört hierher).
8. Spotlight, unverändert.
9. NEU Inspirations-Teaser (Slot inspiration): drei redaktionelle Karten,
   Inhalte liefert Strom 95, im Prototyp Demo-Platzhalter mit Kennzeichnung.
10. Kundenzitat und Footer, unverändert.

## 3. Geräte-Seite

Die Use-Case-Kacheln erscheinen als zweite Einstiegsreihe unterhalb des
direkten Vergleichs, kompakter als auf der Startseite (schmalere Kacheln,
gleiche vier Motive und Ziele). Reihenfolge der Seite: Familienkarten,
Vergleich, Use-Case-Kacheln, Service-Split, Refurbished-Lane. Die
Ein-Berührungspunkt-Regel für Refurbished bleibt unberührt.

## 4. Bildbedarf an Strom 40

Je Storefront und Slot, Sichtung der Partner-Gallery-Assets (Surface)
beziehungsweise Higgsfield-Produktion (Lenovo, Lücken bei Surface):
buehne2 ein Motiv ca. 21:9, mood ein bis zwei Motive ca. 21:9, usecase
vier Motive 4:5 (Unterwegs, Büro, Kundentermin, Feierabend), inspiration
drei Motive 3:2. Die vorhandene Higgsfield-Serie (Lounge, ICE, Hotel,
Restaurant) deckt die Use-Case-Reihe für Surface bereits als Entwurf.
Kampagnenmotive zeigen Arbeitssituationen, in denen das Gerät natürlich
vorkommt, nie als Produktfreisteller (der bleibt E-019-Territorium des
Konfigurators).

## 5. Ergänzung des v6-Auftrags an Claude Design

Zusätzlich zu den sieben Punkten aus refurbished-ux-r6.md Teil B:

8. NEU Kampagnen-Bühne unter dem Hero als Slot-Komponente mit Demo-Motiv
   und Demo-Kennzeichnung, kein Primärbutton.
9. ERSETZT die vier Videokarten durch die Use-Case-Kacheln (Startseite)
   und ergänzt die kompakte Kachelreihe auf der Geräte-Seite, Klickziel
   Konfigurator mit Vorbelegung.
10. ERSETZT die neutrale Ex-Refurb-Fläche durch das Mood-Band als
    Slot-Komponente.
11. NEU Inspirations-Teaser vor dem Footer, drei Demo-Karten.
12. Sorglos-Kacheln textlich menschlicher, Vanity-Nummer sichtbar.

Zusätzliche Abnahmekriterien: Kampagnenflächen tragen keinen Primärbutton
und keine Akzentfarbe außer auf ihren erlaubten Trägern, alle Slots werden
aus einem Demo-Datenblock gerendert (kein Hardcode im Markup), beide
Storefronts zeigen dieselben Slot-Flächen mit eigenen Assets, die
Lenovo-Seite ohne Microsoft-Medien, alle Demo-Motive und -Texte tragen
die Demo-Kennzeichnung.
