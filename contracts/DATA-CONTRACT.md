# Datenvertrag products.json

Quelle: Azure-Pipeline, Distributor Continue, Rechenlogik in contracts/PRICING.md. Stand, gebaut, aber noch nicht End-zu-End bewiesen, der Bucket ist leer, Bestandsaufnahme vor dem Bau. Kanonischer Dateiname im Bucket: products.json. Beispiel zum Bauen: data/products.sample.json.

## Grundsaetze
- Oeffentlich sind NUR fertige Monatsraten. Keine EK-, VK- oder Faktorwerte.
- net ist B2B-Standard, gross (mal 1,19) liegt als Komfortfeld dabei.
- rate_from ist die guenstigste Rate ueber alle Kombinationen, fuer die Anzeige "ab X pro Monat".
- Defensive bauen: optionale Felder koennen fehlen.

## Felder je Produkt
- sku, msku, manufacturer (Pflicht)
- name (bereinigt), title_raw (Original)
- rates.leasing[] und rates.finanzierung[] mit je {term, net, gross}
- rate_from {net, contract, term}
- optional: size_inch, os, is_5g, without_charger

## Vorwaertskompatible Felder (kommen spaeter aus der Pipeline)
- availability { status, stock }  status in: in_stock | incoming | out_of_stock. stock optional,
  oeffentlich nur als weiche Stufe anzeigen. Ist der Status unbekannt, wird das Feld weggelassen, der
  Shop zeigt dann auf Anfrage.
- display_name  sauberer, lesbarer Anzeigename
- specs { cpu, ram_gb, storage_gb, color, screen_inch, generation }
Anreicherung pipelineseitig ueber eine MSKU-Mapping-Tabelle, nicht im Browser parsen.

## Vertragsarten und Laufzeiten
Leasing 15, 24, 32, 36. Finanzierung 15, 24, 36.

## Begleitdateien
- product-overrides.json  handgepflegt: featured, badge, priority, marketing je MSKU
- images.json             version 2, massgebliche Bildschicht (models plus map), siehe IMAGES.md
- licenses.json, services.json  spaeter, gleiches Schema (meta, items, rates)
