# sl-shop-hub - zentrale Datenablage Surface as a Service Shop

Single source of truth fuer den Shop "slshopv2". Alle Beteiligten (Google AI Studio fuer die App,
die VS Code Chats fuer Pipeline und Bilder, und Claude) ziehen sich Vorgaben und Beispieldaten von
hier, statt sie ueber den PC hin und her zu kopieren.

## Inhalt
- PROJECT.md         Zielbild, Positionierung, Branding-Regeln
- DESIGN.md          Designsprache und Tokens
- UX.md              Anfrage-Wizard und Bedienregeln
- PLAN.md            Phasenplan und Lehren aus dem ersten Anlauf
- DATA-CONTRACT.md   verbindliche Form der Produktdaten
- data/              Beispiel- und handgepflegte Datendateien
- brand/             Herz-Logo, Farb- und Schrift-Tokens
- prompts/           Kontext-Block und AI-Studio-Prompts je Phase

## Datenfluss, wichtig
- Die LIVE-Produktdaten (alle rund 358 Artikel, nur fertige Raten) erzeugt die Azure-Pipeline und
  laedt sie als products.json in den GCS-Bucket slshopv2-media (Variante A). Die App liest immer
  aus dem Bucket, nie aus diesem Repo.
- Dieses Repo haelt: den Datenvertrag, eine Beispieldatei (data/products.sample.json) zum Bauen,
  sowie die handgepflegten Dateien product-overrides.json (Hervorhebungen) und images.json
  (Bild-Zuordnung). Diese beiden werden nach Aenderung in den Bucket synchronisiert.
- Bilder liegen im Bucket unter images/{MSKU}.webp und images/{MSKU}_thumb.webp.

## Roh-Zugriff fuer Chats und Tools
https://raw.githubusercontent.com/<OWNER>/<REPO>/main/<pfad>

## Regeln, nicht verhandelbar
- NIE Secrets in dieses Repo. Keine Graph-, HubSpot-, Turnstile-Schluessel. Keine EK- oder
  VK-Werte. Oeffentlich sind ausschliesslich fertige Monatsraten.
- Produktdaten nie von Hand pflegen, nur ueber die Pipeline. Von Hand nur product-overrides.json,
  images.json, Texte und Brand-Assets.
