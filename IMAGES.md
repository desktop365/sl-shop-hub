# Bildspezifikation (images.json v2)

Maßgebliche Spezifikation für alle Produktbilder des Shops. Ersetzt das frühere Modell mit starrer
MSKU-Benennung. Kurzfassung auch in KONZEPT.md Abschnitt 9.

## Idee in einem Satz
Nicht jede Produktvariante bekommt eigene Fotos. Es gibt ein Fotoset je Bildmodell, und jede MSKU wird
über eine Zuordnung auf ihr Bildmodell verwiesen.

## Warum
Der Distributor liefert viele Varianten je Gerät (CPU, RAM, Speicher, OS, Konnektivität), die sich
optisch nicht unterscheiden. Ein Bildmodell steht für eine einzigartige Kombination aus Familie,
Generation, Bildschirmgröße und Farbe. So genügen rund 25 Fotosets für den ganzen Katalog.

## Rollen
- Der Bild-Chat besitzt und pflegt images.json und erzeugt die Bilddateien.
- Die Preis-Pipeline liefert nur stabile MSKUs in products.json, keine Bildlogik.
- Der Shop-Resolver liest beide Dateien und verbindet sie über die MSKU.

## Schema von data/images.json
```
{
  "version": 2,
  "models": {
    "<slug>": {
      "family": "<familySlug>",      // z. B. surface-laptop, surface-pro, zubehoer
      "main":  "<datei>.webp",        // Hauptbild
      "thumb": "<datei>_thumb.webp",  // Vorschaubild
      "gallery": ["<datei>_open.webp", "..."]  // weitere Ansichten, kann leer sein
    }
  },
  "map": {
    "<MSKU>": "<slug>"                 // jede Varianten-MSKU zeigt auf ein Bildmodell
  }
}
```

## Dateinamen und Format
- Dateien sind je Bildmodell benannt (slug), nicht nach MSKU. Galeriebilder tragen sprechende Suffixe,
  zum Beispiel _open, _closed, _back, _left, _right, _top, _angle, _ports, _pen, _detail. Keine reinen
  Nummern.
- Nur Kleinbuchstaben, Ziffern und Bindestriche im slug, keine Leerzeichen, Umlaute oder Sonderzeichen.
  Groß- und Kleinschreibung der Dateinamen bleibt unverändert, die Auslieferung ist case-sensitiv.
- WebP, Qualität etwa 80. Kein PNG für Produktbilder, JPEG nur als Notfall.
- Hauptbild: quadratische Leinwand bis 1200 x 1200, Gerät proportional einpassen, nicht beschneiden,
  gleichmäßiger Rand. Vorschaubild bis 400 x 400, gleiches Motiv und Framing.
- Hintergrund transparent oder reines Weiß, Farbraum sRGB, Metadaten entfernen. Alle Geräte gleich groß
  im Bild, gleicher relativer Rand, gleiche Ausrichtung.
- Richtgröße Hauptbild unter etwa 200 KB, Vorschau unter etwa 40 KB.

## Aufnahmelisten je Familie
- Clamshell-Laptops: hero (Hauptbild), open, closed, back, left, right, top, optional detail.
- Tablets: hero mit Cover, tablet-only, back, angle, ports, optional pen.
- Zubehör: hero, optional eine zweite Ansicht.

## Fallback-Bilder
- Je Gerätefamilie ein Ersatzbild _fallback-{familySlug}.webp, zum Beispiel _fallback-surface-laptop.webp,
  _fallback-surface-pro.webp, _fallback-zubehoer.webp.
- Ein generisches _fallback.webp als letzte Stufe.

## Resolver im Shop
1. MSKU im map nachschlagen, ergibt den slug.
2. Modell im models-Block holen, Hauptbild und Vorschau anzeigen, Galerie optional.
3. Fehlt der Eintrag, Fallback über die Familie (_fallback-{familySlug}.webp), sonst _fallback.webp.
Dateinamen kommen immer aus images.json, nie starr aus der MSKU konstruiert.

## Ablage und Aufruf
- Alle Dateien nach gs://slshopv2-media/images/. Upload über Google Cloud Shell.
- Öffentliche URL je Datei: https://storage.googleapis.com/slshopv2-media/images/{Dateiname}.

## Offene Fragen, vor der finalen Bildmatrix zu klären
- Surface Pro 12 Zoll Snapdragon gegen Surface Pro 13 Zoll Intel, wirklich unterschiedliche
  Bildschirmgröße oder ein Bildmodell.
- Surface Laptop 13 Zoll, gibt es die Farbe Schwarz.
- Surface Laptop 5G, welche Generation, teilt er die Fotos mit dem Laptop 8.
- Slim-Pen-Bundles, eigene Bundle-Fotos oder erben sie das Tastaturbild.

## Workflow
Quellbilder entweder ins GitHub-Repo committen zum Abholen und Verarbeiten, oder als ZIP in den
Bild-Chat geben. Der Upload in den Bucket erfolgt durch Sascha über Cloud Shell.
