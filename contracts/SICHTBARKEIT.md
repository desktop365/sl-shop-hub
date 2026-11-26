# SICHTBARKEIT v2, Verfuegbarkeit als spaeter Check statt Ausblendefilter

## Farbregel, entschieden 26.11.2026 (E-195)

Gilt vor allen folgenden Abschnitten, wo sie widersprechen. Der Leitsatz
„Das Sortiment ist immer sichtbar“ gilt nur für Platin, Schwarz und Geräte ohne
bekannte Farbe.

### 1. Grundsatz
Der Shop verkauft nur an Unternehmen und zeigt deshalb nur Geräte in **Platin**
und **Schwarz**. Andere Farben sind Consumer-Geräte und werden ausgeblendet.
Ein Artikel ohne bekannte Farbe bleibt sichtbar, ohne Farbangabe.

### 2. Welche Werte zählen
Geprüft wird der Farbwert des Artikels, bei Geräten `specs.color`
(DATA-CONTRACT.md). Vor dem Vergleich wird der Wert getrimmt und klein
geschrieben, Bindestrich und Leerzeichen gelten gleich.

| Angezeigt als | Gleiche Schreibweisen |
|---|---|
| Platin | `platin`, `platinum`, `platinfarben` |
| Schwarz | `schwarz`, `black`, `mattschwarz`, `matt schwarz`, `schwarz matt`, `matte black`, `matt black` |

- **Ohne bekannte Farbe** heißt: das Feld fehlt oder ist leer. Der Artikel ist
  sichtbar, Filter, Ausführungsliste, Warenkorb und Anfrage nennen keine Farbe.
- **Jeder andere nicht leere Wert ist eine andere Farbe** und wird ausgeblendet,
  etwa Graphit, Saphir, Dune, Wald, Ozean, Violett, Silber, Grau, Sandstein,
  Slate oder Burano, in jeder Sprache und Schreibweise.
- Angezeigt wird immer „Platin“ oder „Schwarz“, nie die Schreibweise aus dem Feed.
- Neue Schreibweisen für Platin oder Schwarz kommen nur über diese Tabelle dazu,
  nicht über den Code.

**Offen, FRAGE an den Master (8122): Nightfall.** Das Surface Laptop Ultra kommt
im Feed nur in Nightfall und ist eine der drei Einstiegskarten nach E-194,
Punkt 7. Bis zur Antwort gilt Nightfall wie ein Gerät ohne bekannte Farbe:
sichtbar, ohne Farbangabe. Die Preis-Pipeline schreibt für Nightfall heute keinen
Farbwert.

### 3. Wo ausgeblendet wird
- **Geräteliste und Vergleich:** keine Ausführung in anderer Farbe. Die Rate
  „ab …“ eines Modells und einer Reihe rechnet sich nur aus sichtbaren
  Ausführungen. Ein Modell ohne sichtbare Ausführung erscheint weder in der
  Liste noch im Vergleich noch in der Sitemap, für seine Adresse gilt
  ROUTEN-UND-SEO.md.
- **Modellseite und Konfigurator:** der Filter Farbe (VARIANTEN.md) bietet nur
  Platin und Schwarz an und erscheint weiter nur bei mehr als einem Wert. Die
  Ausführungsliste enthält keine andere Farbe.
- **Ausstattung:** gilt für jeden Artikel mit bekannter Farbe, auch für Zubehör.
  Zubehör trägt in `products.json` heute keinen Farbwert und bleibt deshalb
  sichtbar, bis die Preis-Pipeline einen liefert.
- **Warenkorb und Anfrage:** Eine Position in anderer Farbe, etwa aus einem
  geteilten Link (`?pos=`), übernimmt der Warenkorb nicht, er zeigt einen
  Hinweis. Die Prüfung der Anfrage (ANFRAGE.md) nimmt keine Ausführung in
  anderer Farbe an.
- **Alternativen im späten Check** (Abschnitt Alternativen-Rangfolge): „andere
  Farbe“ heißt nur Platin oder Schwarz.
- **Bilder und Filme:** Produktfotos in `images.json` werden für andere Farben
  nicht gezeigt. Lifestyle, Filme und die Medien der Startseite (IMAGES.md,
  Nachtrag Startseite) zeigen Geräte nur in Platin oder Schwarz. Die Erbregel
  „andere Farbe erbt Platinum“ (IMAGES.md, Bildmodell-Matrix) ist für den Shop
  damit ohne Wirkung.

### 4. Wo nicht
- Ausgeblendet wird im Shop. `products.json` und HubSpot bleiben von dieser
  Regel unberührt.

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
