# SICHTBARKEIT v2, Verfuegbarkeit als spaeter Check statt Ausblendefilter

## Leitsatz
Das Sortiment ist immer sichtbar. Verfuegbarkeit blendet nichts aus, sie
informiert, sortiert und prueft am Ende der Anfrage-Strecke. Entschieden am
24.08.2026, ersetzt die Fassung vom selben Tag (Ausblenderegel mit
Beruhigung), die als verworfen dokumentiert bleibt, siehe unten.

## Sichtbarkeit
Modellreihen und Varianten sind sichtbar, solange sie im Sortiment sind.
Ausblenden koennen nur Kuration (ADMIN.md) und Sortimentsende. Verfuegbarkeit
erscheint als Badge je Variante: sofort verfuegbar, zulaufend mit erwartetem
Datum, sonst auf Anfrage. Sortierung in Listen: sofort verfuegbar zuerst.

## Der spaete Check in der Anfrage-Strecke (Neugeraete-Spur)
Der Kunde durchlaeuft die Anfrage ungehindert. Kurz vor dem Absenden wird
die gewaehlte Variante geprueft: sofort verfuegbar ODER zulaufend mit
erwartetem Lieferdatum innerhalb des Lieferfensters, Standard 28 Tage,
Schluessel sichtbarkeit.lieferfenster_tage in der steuerung-Tabelle.
Besteht die Variante, geht die Anfrage normal raus. Faellt sie durch,
werden Alternativen angeboten, per Klick uebernehmbar, mit ihrer Rate,
die Anfrage geht danach mit der uebernommenen Variante raus. Ein Kunde,
der bei seiner Variante bleiben will, darf das, die Anfrage traegt dann
den Verfuegbarkeitsvermerk fuer die Bearbeitung.

## Alternativen-Rangfolge
Nur Varianten derselben Modellreihe, die den Check bestehen. Naehe in
dieser Reihenfolge: erst andere Farbe, dann Speicherkapazitaet und
Hauptspeicher aufwaerts, zuletzt Prozessor und Bildschirmgroesse. Nie
stillschweigend schlechter ausstatten, Abwaertsvorschlaege nur als klar
gekennzeichnete letzte Option. Hoechstens drei Vorschlaege.

## Datenfluss
Halbstuendlicher Verfuegbarkeitsstand als eigene kleine Datei der Pipeline
(Spezifikation beim Preislisten-Chat), products.json bleibt unberuehrt.
Der Shop uebernimmt ihn ueber eine schlanke Sync-Route in die Tabelle
verfuegbarkeit (DB-SCHEMA.md). Badges lesen aus der Tabelle, der spaete
Check liest den frischesten Stand ohne Daempfung. Die Beruhigungslogik
(zuletzt_regel_erfuellt) dient nur noch der Badge-Stabilitaet, nicht mehr
dem Ausblenden. Refurbished-Spur unberuehrt, eigener Bestand.

## Verworfene Varianten, dokumentiert
1. Nur sofort verfuegbare Artikel positiv auszeichnen, sonst nichts anzeigen
   oder verbergen, verworfen am 24.08. vormittags.
2. Harte Ausblenderegel, Artikel ohne Verfuegbarkeit binnen 28 Tagen aus
   Listen, Suche, Empfehlungen und Sitemap entfernen, mit 24h-Beruhigung,
   verworfen am 24.08. nachmittags zugunsten des spaeten Checks, weil sie
   den Katalog schrumpft und Konfigurationsluecken erzeugt.

## Offene Vorbedingungen
Nachtmessung vom 25.08. (Datumsdichte bei W-Artikeln, Realismus des
28-Tage-Fensters). Zuordnungsschicht aus VARIANTEN.md mindestens fuer die
Kernreihen. Distributor-Rueckfrage zum Lieferzeiten-Feld. Der Anfrage-
Endpunkt selbst laut ANFRAGE.md, der spaete Check ist Teil von dessen Bau.
