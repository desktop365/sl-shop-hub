# Datenvertrag products.json

Stand 24.11.2026, angeglichen nach B2 (Board 7875) und P08. Erzeugt von der Preis-Pipeline, Herkunft und Ausgabe in contracts/PRICING.md. Kanonischer Dateiname im Bucket: products.json, siehe INFRA.md. Beispiel zum Bauen: data/products.sample.json, die Raten darin sind erfunden.

Die Laufzeiten 24, 36 und 48 sowie `rate_from` über 48 Monate gelten ab dem ersten Pipeline-Lauf nach P08, also ab dem Nachtlauf am 25.11.2026. Bis dahin trägt die Datei noch 60 und 72 Monate und `rate_from` über 36 Monate.

## Grundsätze
- Öffentlich sind nur fertige Monatsraten. Keine EK-, VK- oder Faktorwerte, weder in `meta` noch in den Produkten. Die Pipeline prüft das vor jedem Upload. Schlägt die Prüfung fehl, lädt sie nicht hoch, und die letzte gute Version bleibt live.
- `net` ist der B2B-Standard, `gross` (net mal 1,19, kaufmännisch gerundet) liegt als Komfortfeld dabei.
- Nie raten: Was die Pipeline nicht sicher erkennt, fehlt als Feld. Es wird nicht mit null oder einem Schätzwert gefüllt.
- Defensiv bauen, optionale Felder können fehlen.

## Aufbau
```
{ "meta": { ... }, "products": [ ... ] }
```

## meta
- `source`, neutrale Herkunft, „Preisliste Lieferant“. Der Lieferant wird öffentlich nie genannt (E-092).
- `generated_at`, Bauzeitpunkt mit Zeitzone, ISO 8601.
- `source_date`, optional, Datenstand der Preise als Datum, Europe/Berlin.
- `note`, optional, Hinweis im Klartext, etwa wenn die Preise aus einer älteren Quelle stammen.
- `currency`, `"EUR"`.
- `vat_rate`, `1.19`.
- `contract_types`, genau `{ "leasing": [24, 36, 48] }`.
- `count`, Zahl der Produkte.

## Felder je Produkt

### Pflicht
- `sku`, `msku`, `manufacturer`
- `name` (bereinigt), `title_raw` (Original)
- `rates.leasing[]`, je `{ term, net, gross }`, genau die Laufzeiten 24, 36 und 48
- `rate_from { net, contract, term }`, die Rate über 48 Monate Leasing: `contract` ist `"leasing"`, `term` ist `48`, `net` gleich der 48-Monats-Rate aus `rates.leasing`. Sie ist ausdrücklich nicht die günstigste Rate.

Ausnahme: Ist für ein Produkt keine Rate berechenbar, ist `rates.leasing` leer und `rate_from` null. Der Shop zeigt dann keine Rate.

### Optional
- `category`, einer von `"geraet"`, `"zubehoer"`, `"ersatzteil"`. Fehlt, wenn die Zuordnung unsicher ist.
- `size_inch`, `os`, `is_5g`, `without_charger`, aus dem Rohtitel.
- `listed`, wahr für die Standardausführung: mit Netzteil, bei Laptops mit deutschem Tastaturlayout. Varianten ohne Netzteil oder mit anderem Layout sind kuratierte Dubletten, bleiben in der Datei mit `listed: false` und sind auf Anfrage erhältlich (SICHTBARKEIT.md). Der Shop listet nur `listed: true`. Fehlt das Feld, gilt der Artikel als gelistet.
- `availability { status, stock }`, `status` in `in_stock`, `incoming`, `out_of_stock`. `stock` ist optional und öffentlich nur als weiche Stufe anzuzeigen. Ist der Status unbekannt, fehlt das Feld, der Shop zeigt dann „auf Anfrage“.
- `display_name`, gepflegter Anzeigename.
- `specs`, nur bei `category` `"geraet"`. Jeder Schlüssel steht nur mit sicherem Wert da:
  - `model`, Modellschlüssel aus der gepflegten Tabelle, siehe MODELLE.md
  - `platform`, `intel`, `snapdragon` oder `nvidia`
  - `family`, Slug der Gerätereihe: `surface-pro`, `surface-laptop`, `surface-laptop-studio`, `surface-laptop-ultra`, `surface-laptop-go`, `surface-go`, `surface-studio`, `surface-hub`
  - `generation`, Zeichenkette, die Edition, wie Microsoft sie zählt, etwa `"8"` beim Surface Laptop (8. Edition) oder `"2"` beim Surface Pro 12 Zoll (2. Edition)
  - `size_inch`, Zahl
  - `cpu`, voller Name, eindeutig je Wahlmöglichkeit im Modell, etwa `"Intel Core Ultra 7 366H"`, `"Snapdragon X2 Plus (10 Kerne)"`, `"NVIDIA RTX Spark N1X (20 Kerne, 6144 GPU-Kerne)"`
  - `copilot_plus`, wahr, wenn die Ausführung die Copilot+-Regel erfüllt: NPU des Prozessors laut Microsoft-Datenblatt mindestens 40 TOPS, mindestens 16 GB RAM und mindestens 256 GB SSD. Unklar heißt falsch.
  - `ram_gb`, `storage_gb`, ganze Zahlen in GB
  - `color`, Klartext, etwa `"Platin"`, `"Schwarz"` oder `"Nightfall"`
  - `display`, `"lcd"`, `"oled"` oder `"mini-led"`, nur wo das Modell eine Wahl bietet
  - `privacy_screen`, `smartcard`, wahr oder falsch, nur wo das Modell eine Wahl bietet
  - `keyboard_layout`, nur Laptops, etwa `"de"`, `"emea"`, `"ch"`
  - `screen_inch`, nur aus der gepflegten Zuordnung

  Gepflegte Werte je MSKU gehen dem Parser vor. Angereichert wird nur in der Pipeline, nie im Browser.
- `fits`, nur bei `category` `"zubehoer"`: Liste der Geräteschlüssel, zu denen der Artikel passt, etwa `surface-pro-11-13` (E-106). Fehlt die Liste, bietet der Shop den Artikel nicht an. Regeln und Schlüssel in BAUSTEINE.md.
- `art`, nur bei `category` `"zubehoer"`: Art des Zubehörs, einer von `pen`, `tastatur`, `dock`, `maus`, `tasche`, `netzteil`, `sonstiges`. Der Shop wählt damit Titel und Nutzensatz aus dem Copy-Baukasten. Fehlt `art`, zeigt der Shop nur `display_name` ohne Nutzensatz.

## Nicht in products.json
- Demo-, OPENBOX- und Vorführgeräte, siehe PRICING.md Abschnitt 7.
- Geprüfte Geräte aus eigenem Bestand, siehe PRICING.md Abschnitt 4.
- Finanzierung und andere Laufzeiten als 24, 36 und 48 Monate.

## Vertragsarten und Laufzeiten
Nur Leasing, 24, 36 und 48 Monate (E-099). Was der Shop wählbar macht und bewirbt, steht in PRICING.md Abschnitt 6.

## Begleitdateien
- product-overrides.json  handgepflegt: featured, badge, priority, marketing je MSKU
- images.json             version 2, maßgebliche Bildschicht (models plus map), siehe IMAGES.md
- bausteine.json          Lizenzen, Garantie und Managed Workplace mit Raten, siehe BAUSTEINE.md
- modelle.json            Modelle mit Schlüssel, Titel, Edition, Plattform, Größen, dazu die Reihen der Reihenseiten, siehe MODELLE.md
- specs.json              Datenblatt und Funktionen je Modellschlüssel, siehe SPECS.md
