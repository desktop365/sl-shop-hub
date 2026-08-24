# Designsprache V2.1, SL Shop, zwei Einmarken-Storefronts

Nachfolger von DESIGN.md, gilt zusammen mit UX.md, DETAILS.md, PROJECT.md und den Kontrakten
(DATA-CONTRACT, IMAGES, STOREFRONTS, MARKETS). Gilt fuer beide Storefronts (surface, lenovo) auf einer
Codebasis. Theming ist ausschliesslich ein Token-Tausch: `<html data-sf="surface|lenovo">` laedt
`tokens.surface.css` bzw. `tokens.lenovo.css`. Komponenten kennen nur `var(--sf-*)`, nie Markenwerte,
nie `data-sf`-Selektoren. Kein Einzelfall-CSS je Marke.

## 0. Korrekturen gegenueber V2, aus den Kontrakten uebernommen

- Laufzeiten und Vertragsarten fuer Neugeraete kommen aus DATA-CONTRACT.md: Leasing 15, 24, 32, 36
  Monate, Finanzierung 15, 24, 36 Monate. Das Produktdetail bekommt deshalb zwei Umschalter,
  Vertragsart und Laufzeit, Vorauswahl Leasing 36, damit sofort eine Rate dasteht.
- Netto prominent, Brutto als Komfortwert sekundaer im Ratenfeld (mal 1,19).
- Anfrage-ID im Format SL-JJJJMMTT-XXXXXX mit sechs hexadezimalen Grossbuchstaben.
- Telefon als Marken-Vanity (DETAILS.md): sichtbar "0800-SURFACE", echte Ziffern nur bei Hover oder
  Fokus dezent eingeblendet, tel-Link immer +498007873223. In Kopf, Footer und mobiler Bottom-Bar.
- Mobile fuehrt eine globale Sticky-Bottom-Bar mit Konfigurator-Einstieg, Anfragekorb und Telefon.
- Slogan optional klein neben dem Herz: "work love balance", klein geschrieben.
- Footer: Herz, Slogan, Telefon, E-Mail (sales@surface.love), Links Impressum, Datenschutz, AGB,
  Widerruf, Markenhinweise.
- Startseiten-Teaser und beworbene Geraete werden aus product-overrides.json (featured, badge)
  gespeist, die Slots dafuer sind im Layout vorgesehen.

## 1. Richtung

Mobil-first, ruhig, premium, und bildgetragen: die Startseite und die Produkt-Hauptseiten verkaufen
ein Arbeitserlebnis im Modern Workplace, nicht nur Geraete. Die Monatsrate ist ueberall der
typografische Held, in Tabellenziffern und in der Akzentfarbe. Genau eine Hauptaktion je Bildschirm
bleibt Gesetz. Zwei Marken, ein System:

- **surface**: leicht und luftig. Display in Gewicht 300, Pillen-Buttons, weiche 18px-Karten, kuehle
  Grautoene, Cyan chirurgisch. Signatur ist das lebende Herz mit Doppel-Herzschlag, zugleich
  Ladeindikator. Eyebrow-Pille "Surface as a Service".
- **lenovo** (Platzhalter-Identitaet "Carbon und Karmin"): technisch und kompakt. Display in 600,
  12px-Karten, 10px-Buttons, warme Greige-Neutrale, Karmin als Akzent, kein Puls, neutrale
  Platzhalter-Kachel als Marke bis zur Freigabe.

## 2. Akzent, geschaerft in zwei Stufen

Das bisherige Cyan #00A3E0 hat auf Weiss nur rund 2,6:1 Kontrast. Der Akzent wird gestuft, bleibt aber
ein einziger Akzent mit genau drei Traegern: aktiver Schritt, die Rate, die Hauptaktion.

| Token | Rolle | surface | lenovo |
|---|---|---|---|
| `--sf-accent` | Markenfarbe: Logo-Puls, aktiver Schritt, Tint-Basis | #00A3E0 | #D0342C |
| `--sf-accent-strong` | Textakzent: Links, die Rate, 4,5:1 auf Weiss | #007DB8 | #A82519 |
| `--sf-accent-weak` | Tint-Hintergrund, Eyebrow-Pille | #E6F6FD | #FBEBE8 |
| `--sf-action` / `-hover` / `-ink` | Fuellung Hauptaktion | #007DB8 / #006CA0 / #FFF | #D0342C / #B32A21 / #FFF |
| `--sf-tint` | Staerke des Marken-Duotons auf Bildern | 14% | 12% |

Statusfarben (gruen verfuegbar, bernstein im Zulauf, grau auf Anfrage) sind nie Akzent.

## 3. Typografie

Fluid per clamp, eine Skala, zwei Stimmungen ueber Gewicht und Groesse:

| Rolle | Token | surface | lenovo |
|---|---|---|---|
| Display | `--sf-text-display` | 36 bis 56, Gewicht 300, -0.02em | 32 bis 48, Gewicht 600, -0.01em |
| H1 | `--sf-text-h1` | 28 bis 36 | 26 bis 32 |
| H2 | `--sf-text-h2` | 22 bis 26 | 20 bis 24 |
| H3 | `--sf-text-h3` | 20 | 18 |
| Fliesstext | `--sf-text-body` | 17 | 16 |
| Klein / Mikro | `--sf-text-small/micro` | 14 / 12 | 14 / 12 |

Schriften: surface behaelt den Segoe-Stapel, lenovo nutzt Inter (in der App selbst gehostet) mit
Segoe- und System-Fallback. Raten und alle Betraege mit `font-variant-numeric: tabular-nums`.
Beschriftungen in normaler Gross- und Kleinschreibung, kein breites letter-spacing, deutsche Texte
mit echten Umlauten, keine langen Gedankenstriche.

## 4. Bildsprache

Zwei Bildwelten, klar getrennt:

**Produktbilder** nach contracts/IMAGES.md: quadratische Leinwand, transparent oder reines Weiss,
gleiche relative Groesse und Ausrichtung, WebP, aus images.json aufgeloest (models plus map, Fallbacks
je Familie). Sie leben auf `--sf-surface-2`-Flaechen (Karten, Galerie-Hauptansicht).

**Lifestyle- und Marketingbilder** kommunizieren das Arbeitserlebnis im Modern Workplace: echte
Arbeitssituationen, natuerliches Licht, Geraete in Benutzung, Menschen im Team, keine sterile
Stock-Optik. Einheitlich wird ein leichter Marken-Duoton als Overlay gelegt, Staerke ueber
`--sf-tint` (color-mix mit `--sf-accent`), damit beide Storefronts trotz gleicher Motivwelt sofort
ihre Marke tragen.

**Bewegtbild (V3, Startseite nach dem Vorbild microsoft.com/de-de/surface)**: die Startseite ist
videogetragen. Jeder Video-Slot ist eine Komponente mit fester Fallback-Kette: Video, sonst
Posterbild, sonst Szene im Duoton. Regeln fuer alle Videos: stumm (muted), Endlosschleife (loop),
playsinline, preload metadata, object-fit cover. Autoplay nur im Hero, alle anderen Slots starten
und pausieren ueber IntersectionObserver bei Sichtbarkeit. Der Hero traegt eine sichtbare
Pause/Play-Steuerung unten rechts (rund, Glas-Optik, aria-Label wechselt). prefers-reduced-motion
unterbindet Autoplay komplett und zeigt Poster oder Szene. Kein Ton, nie Steuerleisten des
Browsers, Text liegt immer auf einem Scrim, nie direkt auf dem Video.

**Video- und Bildslots** (Formate als Richtwert):
| Slot | Ort | Medium | Format |
|---|---|---|---|
| home-hero-video | Startseite, Vollbild-Buehne hinter der Headline | Video, 1920x1080 | 16:9, deckt |
| home-vcard-1..4 | Startseite, Reihe "Gemacht fuer Ihren Arbeitstag" | Video, 1080x1350 | 4:5 |
| home-acc-1..4 | Startseite, Video-Akkordeon "Ein Geraet, alles drin" | Video, 1680x1344 | 5:4 |
| home-refurb | Startseite, Refurbished-Split | Bild | 4:3 |
| katalog-promo | Promo-Kachel im Katalogsraster | Bild | 16:9 |
| pdp-usecase | Produktdetail, Abschnitt "Im Modern Workplace" | Bild | 4:3 |
| pdp-gallery | Produktdetail, Lifestyle-Ansichten in der Galerie | Bild | 4:3 |

Ablagevorschlag: `gs://slshopv2-media/images/marketing/{storefront}/{slot}.webp` fuer Bilder und
`.../videos/{storefront}/{slot}.mp4` plus `{slot}-poster.webp` fuer Bewegtbild, referenziert ueber
einen `marketing`-Block in images.json (v2.1) oder eine parallele marketing.json. Bis eigenes
Material vorliegt, rendert die Komponente "Szene" einen gestalteten Platzhalter im Duoton mit
Beschriftung, so bleibt das Layout ehrlich und baubar, und die Dreh- und Foto-Bestellliste ergibt
sich direkt aus den Slots.

**Lizenzhinweis**: der Prototyp verlinkt in den Video-Slots der Surface-Storefront die
Referenzvideos der Microsoft-Surface-Seite (Contentful-CDN), jeweils sichtbar markiert mit
"Referenz Microsoft, vor Livegang ersetzen". Sie dienen nur der internen Designabnahme. Vor jedem
oeffentlichen Einsatz werden sie durch eigenes Material oder durch offiziell ueber das
Microsoft-Partnerprogramm freigegebene Assets ersetzt; die Lenovo-Storefront erhaelt grundsaetzlich
keine Microsoft-Medien und zeigt bis dahin die Szenen-Fallbacks.

## 5. Raster, Raum, Container

4px-Basisraster, Stufen 4/8/12/16/24/32/48/64/96 als `--sf-space-1..9`. Container 1200px, Gutter
`clamp(20px, 4vw, 32px)`. Layouts sind mobil einspaltig und wachsen ueber Container-Queries:
Katalog 2 Spalten mobil, 3 ab 760, 4 ab 1020, Produktdetail und Anfrage ab 760/900 zweispaltig mit
mitlaufender Seitenkarte, das Workplace-Band laeuft vollbreit.

## 6. Form und Tiefe

| Token | surface | lenovo |
|---|---|---|
| `--sf-radius` (Karten) | 18px | 12px |
| `--sf-radius-sm` (Eingaben, innere Flaechen) | 12px | 8px |
| `--sf-radius-btn` (Buttons, Chips, Segmente) | Pille | 10px |

Tiefe hat genau zwei Ebenen: `--sf-shadow-card` als kaum sichtbare Grundtiefe, `--sf-shadow-float`
nur fuer Schwebendes (Bottom-Bar, Hero-Karte, Ratenpille, Sheets). Alles andere trennt eine
Hairline `--sf-border`. Header mit leichtem Blur ueber Inhalt.

## 7. Bewegungs-Spielbuch

Leicht, orchestriert, nie dekorativ um der Bewegung willen. Eine Kurve `--sf-ease`, drei Dauern.

| Moment | Effekt | Dauer / Token |
|---|---|---|
| Seitenladen (Hero) | Headline, Subline, Aktionen, Buehne faden gestaffelt ein (8px Rise, 80ms Versatz) | `--sf-dur-3` |
| Scrollen | Abschnitte und Karten erscheinen einmalig per Reveal (Fade plus 16px Rise), Karten im Raster gestaffelt | `--sf-dur-3`, IntersectionObserver |
| Lifestyle-Szenen | sehr langsamer Ken-Burns-Zoom (Scale 1 bis 1,06, 26s, alternierend), nur auf grossen Flaechen | eigene Keyframes |
| Hero-Video | Autoplay stumm in Schleife, Pause/Play-Steuerung unten rechts, Text auf Scrim | nativ, kein Autoplay bei reduced motion |
| Video-Slots im Fluss | Wiedergabe startet und pausiert per Sichtbarkeit, nur das aktive Akkordeon-Video laeuft | IntersectionObserver |
| Video-Akkordeon | Buehnenwechsel per Crossfade, aktiver Punkt klappt Text auf, Markierung in Ink | 450ms |
| Produktkarte Hover | Float-Schatten, Bild skaliert 1,03 und hebt 3px, Pfeil im Link schiebt 3px | `--sf-dur-2` |
| Raten-Umschalter | Rate zaehlt hoch oder runter, Unterzeile wechselt, Ratenfeld pulst einmal als weicher Ring im Akzent | `--sf-dur-2` |
| Galerie | Ansichten wechseln per Crossfade | 450ms |
| Herz (nur surface) | Doppel-Herzschlag alle `--sf-pulse` 3,5s, Einzelschlag bei Hover, zugleich Ladeindikator | `--sf-pulse` |
| Telefon-Vanity | echte Ziffern gleiten bei Hover/Fokus neben "0800-SURFACE" auf | 350ms |
| Buttons | Hover dunkelt auf `--sf-action-hover`, Aktiv versetzt 1px | `--sf-dur-1` |

`prefers-reduced-motion` schaltet alles ab, Reveals sind dann sofort sichtbar. lenovo hat keinen
Marken-Puls (`--sf-pulse: 0s`), alle uebrigen Effekte gelten markenuebergreifend.

## 8. Icon-Sprache

Umriss-Icons, 1,8px Strich, runde Kappen, 24er-Raster (Lucide-kompatibel), Faerbung nur ueber
currentColor. Status als 8px-Punkt plus Text.

## 9. Seitenaufbau

**Startseite (V3, videogetragen)**: Header, dann Vollbild-Hero-Video (Scrim von links und unten,
Eyebrow-Pille invertiert, Display-Headline in Weiss, Subline, Hauptaktion plus Glas-Sekundaeraktion,
Vertrauenszeile, Pause/Play-Steuerung unten rechts), Reihe "Gemacht fuer Ihren Arbeitstag" mit vier
Hochformat-Videokarten (4:5, Titel und Kurztext darunter, Wiedergabe bei Sichtbarkeit),
Geraetefamilien "Finden Sie Ihr Geraet" als vier Karten mit ab-Rate (Laptops, 2 in 1, Zubehoer,
Refurbished im Abo), interaktives Video-Akkordeon "Ein Geraet, alles drin" (links Buehne mit
Crossfade, rechts vier Punkte, aktiver Punkt mit Ink-Markierung und aufklappendem Text, nur das
aktive Video laeuft), Sorglos-Paket als vier Vorteilskacheln (aus PROJECT.md), Geraete-Spotlight auf
Flaeche 2 (grosses Geraet, Name, ab-Rate, Sekundaeraktion), Refurbished-Split mit Bild, Kundenzitat,
Footer. Beworbene Geraete und Spotlight speisen sich aus product-overrides.json (featured, badge).

**Katalog**: Kopf, Lane-Segment und Typ-Chips, Raster mit Produktkarten und einer redaktionellen
Promo-Kachel (Bildslot katalog-promo, ab 760 ueber zwei Spalten).

**Produktdetail neu**: Galerie (Produktansicht plus Lifestyle-Ansichten, Crossfade), Titel,
Spezifikations-Chips, Verfuegbarkeit, Vertragsart-Umschalter (Leasing, Finanzierung), Laufzeit je
Vertragsart, Ausstattung, Ratenfeld (netto gross, brutto sekundaer, Hauptaktion, Mikrozeile),
Abschnitt "Im Modern Workplace" (Bild plus Sorglos-Punkte), Leistungsliste. Mobil Raten-Dock.

**Refurbished-Abo**: wie Produktdetail, Abo-Modell Flexibel/12/24 statt Vertragsart und Laufzeit,
Zustandszeile, Hauptaktion "Abo starten", Mikrozeile Stripe.

**Anfrage**: Schritt-Indikator (4 Schritte), Positionsliste mit Stepper, Summe, kurzes Formular
(Pflicht Firma, Name, E-Mail, optional Telefon, DSGVO, Turnstile), Bestaetigung mit Anfrage-ID und
"was passiert als Naechstes".

**Desktop-Spezifika**: Header ab 900px zusaetzlich mit Telefon-Vanity und dem primaeren Einstieg in
den Konfigurator (DETAILS.md), Katalog vierspaltig, mitlaufende Karten im Anfrage- und Produktlayout,
alle Hover-Zustaende aktiv. Mobil ersetzt die Bottom-Bar diese Kopfelemente.

## 10. Komponenten, Spezifikation und Zustaende

**Header.** Sticky, 60px, Blur, Hairline. Markenzeichen (surface nur Herz, lenovo Platzhalter-Kachel,
nie ein Wortname), Navigation ab 760, Telefon-Vanity ab 760, Anfragekorb mit Zaehler im Akzent,
primaerer Konfigurator-Einstieg ab 900, mobil Menue-Button. Zustaende: Zaehler 0/n, Menue offen.

**Mobile Bottom-Bar.** Sticky unten, Blur, Hairline oben, drei Elemente: Telefon (Vanity),
Konfigurator-Einstieg als Hauptaktion, Anfragekorb mit Zaehler. Auf dem Produktdetail ersetzt durch
das Raten-Dock (Rate plus Hauptaktion). Verschwindet ab 760.

**Szene (Bildslot).** Traeger fuer Lifestyle-Medien: Duoton-Flaeche aus `--sf-accent` mal
`--sf-tint`, Korn-Overlay, optional Ken-Burns, Beschriftungs-Pille "Bildslot: ...". Nimmt spaeter das
echte Foto als Hintergrund und behaelt Duoton-Overlay und Verhalten. Varianten: hero, team, focus,
detail. Zustaende: Platzhalter, Foto geladen, reduzierte Bewegung.

**Video-Slot.** Traeger fuer Bewegtbild mit Fallback-Kette Video, Poster, Szene. Video stumm, loop,
playsinline, cover; Beschriftungs-Pille zeigt Herkunft ("Referenz Microsoft, vor Livegang ersetzen"
oder "Videoslot: eigenes Material folgt"). Bei Ladefehler tauscht der Slot selbststaendig auf die
Szene. Zustaende: spielt, pausiert (durch Nutzer oder Unsichtbarkeit), Poster, Szene, reduzierte
Bewegung.

**Hero-Video.** Vollbreiter Video-Slot mit Scrim (links und unten), Inhalt in Weiss, genau eine
Hauptaktion, Sekundaeraktion als Glas-Button, Pause/Play-Steuerung unten rechts (42px, rund,
Blur-Glas, Icon und aria-Label wechseln). Mindesthoehe clamp(500px, 62cqw, 700px).

**Video-Karte.** Hochformatiger Video-Slot 4:5 mit Titel (600) und Kurztext darunter, im Raster zu
viert (mobil zu zweit). Wiedergabe nur bei Sichtbarkeit. Kein Link-Zwang, reine Markenkommunikation.

**Video-Akkordeon.** Buehne (5:4, Crossfade-Ebenen) plus Punktliste. Aktiver Punkt: linke Markierung
in Ink, Titel bleibt, Text klappt auf, zugehoeriges Video spielt, alle anderen pausieren. Mobil
Buehne oben, Liste darunter. Zustaende je Punkt: aktiv, Ruhe, Hover, Fokus.

**Produktkarte.** Bild 4:3 auf `--sf-surface-2`, Badge, Name 600, Spezifikationszeile,
Verfuegbarkeitspunkt, Rate "ab X,XX € mtl. netto" in `--sf-accent-strong`. Zustaende: Ruhe, Hover
(Float, Bild 1,03), Fokus, nicht verfuegbar (gedimmt, Rate bleibt).

**Promo-Kachel.** Karte im Katalograster mit Szene statt Produktbild und redaktioneller Botschaft,
ab 760 ueber zwei Spalten, dann liegend. Kein Preis, genau ein Link.

**Vertragsart-Umschalter.** Segment Leasing/Finanzierung. Wechsel blendet die zugehoerige
Laufzeitreihe ein (Leasing 15/24/32/36, Finanzierung 15/24/36) und uebernimmt deren aktive Rate.
Zustaende: aktiv, Ruhe, Fokus.

**Raten-Umschalter (Laufzeit / Abo-Modell).** Segment auf `--sf-surface-2` in `--sf-radius-btn`.
Aktiv weiss mit Kartenschatten, nie Akzent. Rate zaehlt animiert, Unterzeile wechselt ("Leasing,
36 Monate", "monatlich kuendbar"). Zustaende: aktiv, Ruhe, Fokus, deaktiviert.

**Ratenfeld.** Panel `--sf-surface-2`, grosse Netto-Rate in `--sf-accent-strong` mit
Tabellenziffern, daneben "pro Monat, netto", darunter Brutto als Komfortwert und die wechselnde
Unterzeile, Hauptaktion in voller Breite, Mikrozeile je Lane (neu: "Unverbindlich, Angebot folgt per
E-Mail.", Abo: "Sichere Zahlung ueber Stripe."). Pulst einmal beim Ratenwechsel.

**Galerie.** Hauptflaeche 4:3 mit Ebenen (Produktansicht auf `--sf-surface-2`, Lifestyle-Ansichten
als Szene), Crossfade, Thumbnails mit aktiver Tintenkontur. Ansichten je IMAGES.md-Aufnahmeliste
plus Lifestyle-Slots. Zustaende: aktiv je Thumbnail, Fokus.

**Hauptaktion.** Fuellung `--sf-action`, genau eine je Bildschirm, Wirkung im Text ("In Anfrage
uebernehmen", "Abo starten", "Anfrage senden", "Geraet anfragen"). Zustaende: Ruhe, Hover, Aktiv,
Fokus, Laden (surface: Herzpuls im Button), deaktiviert. Sekundaer als Outline, auf Bildern invers
weiss.

**Anfragekorb.** Desktop mitlaufende Karte, mobil Teil der Bottom-Bar bzw. Raten-Dock. Positionen
mit Stepper, Zeilenrate, Gesamtzeile in `--sf-accent-strong`, Mikrozeile "Netto, unverbindlich".
Zustaende: leer (mit Weg in den Katalog), n Positionen, nach Reload gefuellt, gesendet.

**Badges.** "Neu" neutral, "Refurbished" gruenlich, plus Zustandsklasse. 12px, 600, normale
Schreibung, Radius `--sf-radius-btn`.

**Schritt-Indikator.** Vier Schritte, erledigt Haken und klickbar, aktiv Kreis in `--sf-accent`,
mobil nur aktive Beschriftung.

**Vorteils-Kachel.** Icon in `--sf-accent-weak`-Kreis mit `--sf-accent-strong`-Strich, Titel 600,
zwei Zeilen Text. Vier Stueck als Sorglos-Paket, Reveal gestaffelt.

**Telefon-Vanity.** Sichtbar "0800-SURFACE" (je Storefront konfiguriert), echte Ziffern gleiten bei
Hover/Fokus auf, tel-Link immer die echte Nummer. Kopf, Footer, Bottom-Bar.

**Eyebrow-Pille.** Kleine Pille in `--sf-accent-weak` mit `--sf-accent-strong`-Text, sentence case,
z. B. "Surface as a Service". Genau eine, nur im Hero.

**Formularfeld.** Beschriftung klein 600, Feld `--sf-radius-sm`, Fokusring, Fehler direkt am Feld,
"optional" als Zusatz.

**Storefront-Theming.** Nur `var(--sf-*)` in Komponenten, verboten sind Hex-Werte, Markennamen und
`data-sf`-Selektoren. Markeneigenheiten tragen Tokens (`--sf-pulse: 0s` schaltet den Puls ab).
Abnahme jeder Komponente: Screenshot unter beiden Attributwerten ohne Komponentenaenderung.

## 11. Qualitaetsboden

Responsive bis 360px, sichtbarer Tastaturfokus, Text 4,5:1, Hauptaktion 4,5:1 in beiden Storefronts,
Touch-Ziele mindestens 40px, `prefers-reduced-motion` respektiert, Bilder mit Alt-Texten aus dem
Anzeigenamen, Netto immer mit Zusatz und "unverbindlich" gemaess UX.md, nie Einkauf, Verkauf oder
Faktoren.
