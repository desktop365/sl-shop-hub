# Baustein-Verzeichnis, Detailseiten und Anfragestrecke

Prototyp: `slshop-startseite-premium.html`, Tabs "Produkt neu", "Refurbished Abo", "Anfrage".
Alle Bausteine nur mit `var(--sf-*)`-Tokens, beide Storefronts über `data-sf`.

## Komponenten

### Vertragsart-Umschalter (`.seg.seg-ct`)
Segment Leasing / Finanzierung. Wechsel blendet die passende Laufzeitreihe ein und übernimmt deren aktive Rate.
Daten: Vertragsarten aus `rates` (products.json). Zustände: aktiv (weiß, Kartenschatten), Ruhe, Fokus.

### Laufzeit-Auswahl (`.seg.seg-terms`)
Leasing 15/24/32/36, Finanzierung 15/24/36. Vorauswahl Leasing 36, sofort eine Rate sichtbar.
Daten: `[laufzeit, netto]` je Vertragsart, fertige Raten, kein Rechner. Zustände: aktiv, Ruhe, Fokus, (deaktiviert vorgesehen).

### Menge (`.qty.qty-dev`)
Stepper ab 1, wirkt live auf die Monatssumme. Zustände: Ruhe, Hover, Minimum (bleibt bei 1).

### Add-on-Zeile (`.addon`)
Eine Position: Name, Kurztext, "+ X,XX € mtl.", Hinzufügen/Entfernen, bei Lizenzen Platz-Stepper (erscheint erst nach Hinzufügen).
Daten: id, Name, Erklärung, Rate (oder null → "auf Anfrage"), seat-Flag. Gruppen: Bundles (vorgeschnürt, eine Gesamt-Zusatzrate), Zubehör, Software und Lizenzen, Services.
Zustände: Ruhe, hinzugefügt (Ink-Rahmen, Button invertiert, Rate fett), auf Anfrage (kein Betrag, Weg bleibt offen), Fokus.

### Ratenfeld (`.ratebox`)
Netto groß in `--sf-accent-strong` (Tabellenziffern), brutto klein (× 1,19), Aufschlüsselung "Gerät X € × n, Add-ons Y €", wechselnde Unterzeile ("Leasing, 36 Monate"), Hauptaktion volle Breite, Mikrozeile je Lane. Pulst einmal als weicher Ring beim Ratenwechsel, Rate zählt in 260 ms hoch/runter.
Daten: `data-base` = gewählte Geräterate; Summe = base × Menge + Add-ons. Zustände: Ruhe, Flash beim Wechsel, laden (Hauptaktion `.loading`).

### Im Preis enthalten (Rundum-sorglos, kompakt)
Häkchenliste: Beschaffung/Einrichtung/Rollout, Support/Reparatur/Austausch, Versand/Rückholung, Laufzeitende. Schlusszeile "Ein Ansprechpartner, ein Vertrag, eine Rate." Ausführlich auf der Startseite ("Mehr als das Gerät", Lifecycle 01–04).

### Querverweis (`.xref`)
Neu → "Dasselbe Modell refurbished, ab X € mtl.", Refurbished → "Als Neugerät konfigurieren, ab Y € mtl.". Nie markenübergreifend.

### Anfragekorb (`.count`, Korb-Karte, `.cline`)
Zähler im Header und in der mobilen Bottom-Bar (Akzent, versteckt bei 0). Persistenz in `localStorage` je Storefront (`slshop-cart-surface|lenovo`), übersteht Reload.
Position (`.cline`): Bild, Name, Spezifikation/Vertragszeile, Mengen-Stepper, Zeilenrate ("auf Anfrage" möglich), Entfernen-Knopf.
Zustände: leer (Einladung + "Zum Katalog", kein trauriger Zustand), n Positionen, nach Reload gefüllt, gesendet (geleert).

### Schritt-Indikator (`.steps`)
Vier Schritte: Gerät, Konfiguration, Übersicht, Kontakt. Aktiv = Kreis in `--sf-accent`, erledigt = Haken und klickbar (zurück). Mobil nur aktive Beschriftung.

### Wizard-Strecke
Schritt 3 Übersicht: Korb als Seite (einspaltig, max 720px), Summe netto + brutto, Hauptaktion "Weiter zum Kontakt".
Schritt 4 Kontakt: Formular (Pflicht Firma, Name, E-Mail; Telefon und Nachricht optional; DSGVO; Turnstile im Bau vorgesehen) + mitlaufende Übersichts-Karte mit "Positionen ändern". Hauptaktion "Anfrage senden" mit Ladezustand ("Wird gesendet…").
Bestätigung: grünes Häkchen, Anfrage-ID SL-JJJJMMTT-XXXXXX, was als Nächstes passiert, Korb geleert.
Schnellster Pfad: Gerät → In Anfrage übernehmen → Weiter zum Kontakt → Anfrage senden.

### Refurbished-Weiche
Abo-Modell Flexibel/12/24 statt Vertragsart, Hauptaktion "Abo starten", Mikrozeile "Sichere Zahlung über Stripe" (Kasse Phase zwei). Zustandszeile "geprüft, Zustand sehr gut".

## Bewegungsnotizen
Rate zählt 260 ms (`--sf-dur-2`), Ratenfeld-Ring 550 ms, Segmente/Buttons 150 ms, Herzpuls 3,5 s nur surface, Reveals einmalig 550 ms. `prefers-reduced-motion` schaltet alles ab.

## Designbegründung, kurz
Die Signatur sitzt in genau zwei Momenten: dem lebenden Herz und dem Rundum-sorglos-Gefühl (Häkchenliste + "Ein Ansprechpartner, ein Vertrag, eine Rate" direkt unter der Hauptaktion). Alle Steuermodule bleiben monochrom und ruhig — Ink-Markierungen statt Akzentfarbe, damit Cyan seine drei Träger behält (aktiver Schritt, Rate, Hauptaktion) und die Rate als typografischer Held unangefochten bleibt. Der Korb ist nie Sackgasse: jede Ansicht hat genau einen Weiterweg und einen Rückweg.
