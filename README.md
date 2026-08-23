# sl-shop-hub, Brücke und Quelle der Wahrheit

Hub-Repo für Surface.Love. Hier liegen Specs, Kontrakte, Marke und Prompts. Alle Oberflächen, der
Strategie-Strang, Claude Code und die Betriebs-Agenten, lesen von hier, statt Vorgaben hin und her zu
kopieren. Kein Code, keine Secrets, keine internen Preise.

## Einstieg, in dieser Reihenfolge
1. [ARBEITSWEISE.md](ARBEITSWEISE.md), das Betriebshandbuch. Welche Oberfläche was tut, welche Repos es
   gibt, welche Verträge in welcher Form, wo alles liegt, welche Leitplanken gelten.
2. [LANDKARTE.md](LANDKARTE.md), die Architektur-Landkarte. Module, zwei Geschäftsmodelle, Preis-Engine,
   Promotions, Phasen, offene Entscheidungen.
3. [CLAUDE.md](CLAUDE.md), die kurze Arbeitsanweisung für dieses Repo.

Bei Widerspruch gilt ARBEITSWEISE.md.

## Inhalt
- ARBEITSWEISE.md   Betriebshandbuch, Repo- und Ordnerstruktur
- LANDKARTE.md      Architektur-Landkarte
- PROJECT.md        Zielbild, Positionierung, Branding-Regeln
- DESIGN.md         Designsprache und Tokens
- UX.md             Anfrage-Wizard und Bedienregeln
- archive/          abgeloeste Dokumente aus dem ersten Anlauf, siehe Hinweis in den Dateien
- DETAILS.md        Feinvorgaben, leicht zu übersehende Punkte
- contracts/        die verbindlichen Kontrakte, siehe unten
- data/             Beispiel- und handgepflegte Datendateien
- brand/            Herz-Logo, Farb- und Schrift-Tokens
- STATUS.md         Uebergabe nach Phase 0, aktueller Stand
- PLAN.md           Lehren aus dem ersten Anlauf, historisch, siehe Hinweis in der Datei

## Die Kontrakte
- [contracts/DATA-CONTRACT.md](contracts/DATA-CONTRACT.md)  products.json, Neu-Katalog und Raten
- [contracts/IMAGES.md](contracts/IMAGES.md)                images.json, Bildmodelle und Zuordnung
- [contracts/DB-SCHEMA.md](contracts/DB-SCHEMA.md)          MySQL, Leseabbild, Bestand, Abo
- [contracts/HUBSPOT.md](contracts/HUBSPOT.md)              Felder, Pipeline-Stufen, kaufmännischer Master
- [contracts/MARKETS.md](contracts/MARKETS.md)              Sprachen, Währungen, Vertragsarten je Markt
- [contracts/PROMOS.md](contracts/PROMOS.md)                Aktionsregeln
- [contracts/STOREFRONTS.md](contracts/STOREFRONTS.md)      Marken-Auftritte je Domain, surface und lenovo
- [contracts/PRICING.md](contracts/PRICING.md)  Preisquelle und Rechenweg der Neu-Raten
- [contracts/ANFRAGE.md](contracts/ANFRAGE.md)  Anfrage-Endpunkt und Schluessel
- [contracts/INFRA.md](contracts/INFRA.md)  Infrastruktur, Google-Projekte, Bucket, Cloudflare, Hosting

## Datenfluss, kurz
- Den Live-Katalog erzeugt die Preis-Pipeline und legt products.json im Objektspeicher ab, der Shop liest
  von dort und synchronisiert nach MySQL, nie aus diesem Repo.
- Die Bildschicht images.json kommt aus der Bild-Pipeline, die Bilddateien liegen im Objektspeicher.
- Dieses Repo hält die Schemata, kleine Beispieldateien zum Bauen und die handgepflegten Dateien
  product-overrides.json und images.json.
- Der Objektspeicher ist der GCS-Bucket slshopv2-media, entschieden, siehe contracts/INFRA.md.

## Roh-Zugriff für Chats und Tools
https://raw.githubusercontent.com/desktop365/sl-shop-hub/main/<pfad>

## Regeln, nicht verhandelbar
- Nie Secrets in dieses Repo. Keine Graph-, HubSpot-, Stripe- oder Turnstile-Schlüssel.
- Keine Einkaufs-, Verkaufs- oder Faktorwerte. Öffentlich sind ausschließlich fertige Monatsraten.
- Produktdaten nie von Hand pflegen, nur über die Pipeline. Von Hand nur product-overrides.json,
  images.json, Texte und Brand-Assets.
- Nichts löschen. Abgelöste Dokumente bleiben stehen und bekommen oben einen Hinweis.
