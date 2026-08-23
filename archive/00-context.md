> Abgelöst und archiviert. Beschreibt den ersten Anlauf mit FastAPI auf Google Cloud Run aus der AI-Studio-Zeit, keine Vorgabe mehr. Gültig sind LANDKARTE.md, ARBEITSWEISE.md, STATUS.md und die Kontrakte unter contracts. Die wertvollen Teile, Rechenlogik und Anfrage-Logik, stehen jetzt in contracts/PRICING.md und contracts/ANFRAGE.md.

# Kontext-Block, jedem AI-Studio-Prompt voranstellen

Projekt slshopv2, Google Cloud Run, Region europe-west1, Python mit FastAPI, zustandsloser Container.
Sprich Deutsch in der Oberflaeche. Keine langen Bindestriche, echte Umlaute.

## Architektur, strikt
- Keine persistenten Daten lokal im Container.
- Produktdaten und Medien aus dem GCS-Bucket slshopv2-media, Bibliothek google-cloud-storage.
- Produktdaten: products.json aus dem Bucket (von der Pipeline erzeugt, Variante A). Beim Bauen gegen
  die lokale data/products.sample.json in der Form aus contracts/DATA-CONTRACT.md. Spaeter nur die Quelle auf den
  Bucket umstellen.
- Bilder: images/{MSKU}.webp und images/{MSKU}_thumb.webp, Gross- und Kleinschreibung unveraendert
  (Linux case-sensitiv). Aufruf https://storage.googleapis.com/slshopv2-media/images/{name}.
  Resolver: erst {MSKU}.webp, sonst _fallback-{familySlug}.webp, sonst _fallback.webp.
- Secrets nie im Code. Graph, HubSpot, Turnstile kommen aus Secret Manager bzw. Umgebungsvariablen.
- Kategorien, Filter und Konfigurator-Schritte aus den Daten ableiten, nichts hart verdrahten.

## Design und UX
Siehe DESIGN.md und UX.md. Kurz: nur das Herz als Logo (Doppel-Herzschlag), Wort surface.love nirgends
sichtbar, Cyan #00A3E0 nur fuer aktiven Schritt, Rate und primaeren Button, Segoe-Schriftstapel, vier
Wizard-Schritte mit Indikator, immer sichtbarer Anfragekorb, genau eine Hauptaktion, kurzes Formular.

## Arbeitsregeln, aus den Fehlern des ersten Anlaufs
- Eine Sorge pro Prompt. Nie ein grosser Mehrzweck-Umbau (der i18n-Mega-Prompt hat alles zerlegt).
- Nach jeder Phase: testen, dann in GitHub pushen, dann benannten Checkpoint setzen.
- Bricht etwas, sofort auf den letzten guten Stand zurueck, nicht auf kaputtem Stand weiterreparieren.
