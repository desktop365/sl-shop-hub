# Detailvorgaben und Feinheiten

Ergänzung zu DESIGN.md, UX.md und PROJECT.md. Hält die feinen, leicht zu übersehenden
Vorgaben fest, die im ersten Anlauf erarbeitet wurden.

## Marke und Kontakt
- Logo: nur das Herz, kein Wortbild. Cyan #00A3E0 auf hellem Grund, weiß auf dunklem Grund, gelöst
  über currentColor, keine getrennten Dateien nötig.
- Slogan optional klein neben dem Herz: "work love balance", klein geschrieben. Überschreibt die ältere
  Schreibweise "Work Love Balance".
- Telefon als Marken-Vanity: sichtbar steht "0800-SURFACE". Die echten Ziffern 0800 7873223 erscheinen
  nur bei Mouseover oder Fokus, dezent eingeblendet oder als Tooltip. Der tel-Link ist immer
  +498007873223, damit das Handy beim Tippen direkt wählt. Gilt in Kopf, Footer und mobiler Bottom-Bar.
- Öffentliche Kontakt-E-Mail: sales@surface.love. Anfragen-Antworten (Reply-To) gehen ebenfalls dorthin.
  Der technische Absender shop@surface.love wird nie angezeigt. Falls stattdessen sales.de@ gewünscht
  ist, hier ändern.

## Schreibweise
- Keine Großbuchstaben-Labels. Durchgehend normale Schreibweise (sentence case), kein breites
  letter-spacing. Gilt für Status, Kategorien, Sortierung, Footer und die Eyebrow-Pille.

## Anfrage und IDs
- Anfrage-ID-Format: SL-JJJJMMTT-XXXXXX, sechs hexadezimale Großbuchstaben.

## Layout-Feinheiten
- Mobile: Sticky Header und Sticky Bottom-Bar mit Konfigurator, Anfragekorb und 0800-SURFACE.
- Kopf am Desktop später: neben der Nummer ein Anfragekorb-Icon mit Zähler und der primäre Einstieg in
  den Konfigurator. Kommt mit der Korb-Phase.
- Footer: Herz, Slogan, Telefon, E-Mail, Links Impressum, Datenschutz, AGB, Markenhinweise.

## Recht
- DDG statt TMG. Die ODR-Plattform ist eingestellt und wird nicht mehr verlinkt.

## Bewusst auf später, jetzt NICHT bauen
- EHS- und ADP-Schutz- und Versicherungslogik
- Vergleichsfunktion
- Beratungsassistent "Welches Surface passt zu mir"
- FAQ-Chatbot
- ROI-Rechner auf der Vorteilsseite
HubSpot und der serverseitige Mailversand sind bereits konzipiert, siehe contracts/ANFRAGE.md.

## Homepage-Marketing, kommt mit den Bildern
- Main-Teaser und beworbene Geräte auf der Startseite, gespeist aus product-overrides.json (featured,
  badge). Echte Marketing- und Gerätebilder kommen über den Bucket, siehe Bildkonzept. Den Platz dafür
  jetzt vorsehen, Inhalt folgt, sobald die Bilder da sind.
