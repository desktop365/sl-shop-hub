# Designsprache und Tokens

Stand 26.11.2026, nach E-098, E-144 und E-200. Surface.Love folgt dem Designsystem V2-2026, die Storefront surface.love dem Prototyp V18, gebaut nach dem Bauplan V18 Fassung 4. lenovo.online ist ein eigenes System und nicht Teil von Beta 1 (E-101).

Verbindlich für den Bau von surface.love ist das Paket `brand/surface/`:

| Datei | Inhalt |
|---|---|
| `tokens.css`, `tokens.json` | Rollen und Werte, aus `tokens.json` erzeugt, nicht von Hand ändern |
| `sf-bruecke.css` | Shop-Namen `--sf-*`, Bauwerte für Raster, Schrift, Bildformate, Ebenen und Bewegung (E-144), gesetzt über `data-sf="surface"` |
| `shop-basis.css` | Grundstile, Raster, Typografie und Kernbausteine nach dem Bauplan, nach `sf-bruecke.css` einbinden (E-144) |
| `fonts/` | Open Sans 300, 400, 600, 700, SIL OFL. Der Shop lädt nur 300, 400, 600 (K02) |
| `bausteine-und-zustaende.md` | Jeder Baustein mit Zuständen, Tokens, Handy, Desktop und Bewegung |
| `seitenliste.md`, `aenderungsliste.md`, `offene-punkte.md` | Seiten, Versionen, Nacharbeit |

Der Bauplan V18 Fassung 4 liegt mit Bausteintafel, UX-Profil und Referenz-Prototyp im privaten Shop-Repo unter `docs/design/v18/`. Rangfolge: dieser Vertrag und `brand/surface/`, dann das Logbuch am Board, dann der Bauplan, dann `bausteine-und-zustaende.md`, dann der Prototyp (E-144).

Der Prototyp liegt nicht im Hub, weil er Platzhalter-Kaufpreise enthält. Er wird im Shop übersetzt, nicht kopiert. Komponenten kennen nur `--sf-*`, die Optik kommt allein aus den Tokens, umgeschaltet über `data-sf` am Wurzelelement.

Nicht mehr maßgeblich für surface.love: `brand/DESIGN-V2.md`, `brand/tokens.css`, `brand/tokens.surface.css`, `brand/colors.md` und die älteren Prototypen unter `brand/`. Sie bleiben als Historie liegen.

## surface.love

### Farbe
- Fläche 60 Prozent `surface` und `surface-sand`, 30 Prozent Blau, 10 Prozent `marker`. Apricot ist der einzige warme Akzent.
- Zuerst die Rollen nutzen: `surface`, `heading`, `ink`, `accent-text`, `action`, `marker`. Die Reihen `blue-*`, `neutral-*`, `apricot-*` nur, wenn keine Rolle passt.
- Markenblau `blue-500` #00A3E0 (PANTONE 299 C) und Schwarz #000000 (PANTONE Black 6 C) sind verbindlich.
- Die Hauptaktion ist `action` (Apricot) mit Schrift `on-action`, nicht Blau.
- Blau als Text nur in `accent-text`, nie `brand` unter 24 px. Auf `surface-sand` wird daraus `accent-text-sand`.
- Auf `surface-brand` stehen nur Herz und Headlines ab 24 px in Weiß, das ist eine dokumentierte Ausnahme mit 2,87 : 1. Alles Kleinere steht dort in Schwarz (`on-brand`) oder wandert auf `surface-deep`.
- Raten und große Zahlen auf `surface-brand` stehen immer in Schwarz (`on-brand`, 7,31 : 1), ebenso der Titel im Fußband. `on-brand-display` (Weiß) gilt nicht für Raten (F12, E-145).
- `marker` nur auf `surface`, `surface-sand` und `surface-deep`.
- Status immer mit Wort, nie in Akzentfarbe: `success`, `warning`, `ink-subtle`.

### Verläufe
- Es gelten nur die vier Verläufe aus den Tokens: `gradient-tiefe`, `gradient-himmel`, `gradient-lagune`, `gradient-glut`. Blau wird nie in Apricot, Koralle oder Violett überblendet.
- Über Fotos und Filmen liegt keine Markenfarbe. Steht Text darauf, wird nur in neutralem Schwarz abgedunkelt, mit `schatten-text`, `abdunklung-hoch` oder `abdunklung-fuss` (`ink` mit Deckkraft, E-225). Der Kontrast hängt damit am Bild: Abgenommen wird an der hellsten Stelle hinter jedem Text, mindestens 4,5 : 1.
- Die Kennzahl der Vollbild-Bühne ist weiß wie alle Schrift dort, die aktive Linie bleibt `marker` (E-225).
- Bestand bis G10 (E-225): Hero, Kampagne, Mood und Use-Case-Karten der Startseite stehen noch auf einem Verlauf aus dem Token `schleier` (`blue-950`). Die Stopps stehen je Stelle in `bausteine-und-zustaende.md`, angenommen als Ausnahmen A1 bis A4 und B1 (E-099). Kontraste bei Filmen im Abnahmetest erneut prüfen.
- Kein Muster auf blauen Flächen. Fehlt ein Medium, steht `surface-raised` ohne Etikett (`.slot-leer`), keine gezeichnete Ersatz-Szene (B2, Bauplan 6.22).

### Schrift
- Jeder Text in Open Sans, selbst gehostet. Headlines in Light, Lesetext in Regular, Auszeichnung in SemiBold. Segoe wird nicht mehr verwendet.
- Stufen nur aus den Tokens: `--sf-text-display`, `-h1`, `-h2` fließend, alles andere fest über `--sf-fs-*` und `--sf-lh-*` (E-144). Die Vollbild-Bühne hat eigene Stufen `--sf-text-buehne-*`, fließend ab 1920 Breite (E-225). Nur die Gewichte 300, 400, 600, nichts unter 12 px. Zahlen tabellarisch, Preise ohne Umbruch.

### Form und Raum
- Flächen, Bänder, Karten und Bilder sind eckig (`radius-none`). Rund sind nur Bedienelemente (`radius-s`, 4 px) sowie Chips und Preisplaketten (`radius-pill`).
- Keine Schatten außer `focus-ring`. Tiefe entsteht durch Weiß, Sand und Blau. Ausnahme ist Text frei auf Bild und Film: Dort gelten `schatten-text` und `schatten-schrift`, dazu ein weicher Schatten in neutralem Schwarz unter der Linie des Fortschritts der Bühne (E-225). Sonst nirgends.
- Abstände aus dem 4-px-Raster. Klickziele mindestens 44 px.

### Logo
- Das Logo ist nur das Herz, zusammen mit dem Claim „work love balance“. Die Wortmarke Surface mit Herz wird nirgends mehr verwendet, der Markenname steht als Text „Surface.Love“.
- Das Herz nicht nachzeichnen, verzerren, umfärben oder mit Effekten versehen. Rundum mindestens die halbe Herzhöhe frei. Im Kopf des Surface-Shops steht es links (E-200), sonst rechts. Text und Claim beginnen links.
- Im Surface-Shop steht das Herz im Kopf links und ist der Link zur Startseite. Es schlägt im Doppelschlag, zwei Schläge und dann Ruhe, Periode `--sf-pulse` 3,5 s, ohne Ende, nur `transform`. Bei reduzierter Bewegung steht es still. Bewusste Abweichung von WCAG 2.2.2 nach E-200. Lenovo bleibt ohne Puls (`--sf-pulse:0s`).

### Bewegung
- App-Bewegung: 100, 150, 200, 300 ms (`--sf-dur-instant`, `-fast`, `-base`, `-slow`), öffnen mit `--sf-ease-out`, schließen mit `--sf-ease-in`. Nur `transform` und `opacity`, keine Überschwingkurve (K10, E-144).
- Markenbewegung nur auf Marketingflächen: Einblenden 550 ms, Rate zählt 420 ms. Nicht in Formular, Blatt und Kasse. `--sf-dur-1` bis `-3` bleiben nur für den Bestand.
- Bewegung antwortet auf eine Aktion. Was im Prototyp nur wegen des Neuschreibens nicht läuft (Anfrage-Blatt, Ausklapper, Teile von `.bst`, `.chk`, `.tierrow`), wird in React so gebaut, wie die Bausteine es beschreiben.
- Bei reduzierter Bewegung steht alles still, Medien zeigen das Standbild, Zahlen springen auf den Endwert.

### Pflicht beim Bau von Beta 1
Einordnung des Masters zu `offene-punkte.md`, Abschnitt 4 (Board 6970, 16072757):
- Fokusring auch an `.sw` und `.stop.on`.
- Trefferflächen von `.dots` mindestens 44 px, ohne Überlappung.
- Der Überlauf von 13 px in „Ausstattung“ bei 372 px Breite wird behoben.
- Jeder Hover-Versatz gilt auch bei `:focus-visible` und ist bei reduzierter Bewegung aus.
- Die Nummern 01 bis 04 bei den Vorteilen entfallen. Pfeile nur an Wegweisern, nicht an jeder Aktion.
- Abschnitte ohne freigegebenen Inhalt entfallen. Öffentlich gibt es keine Platzhalter.

### Preise in der Oberfläche
- Die Rate kommt immer fertig aus den Katalogdaten. Menge mal Rate und der Hinweis zur Mehrwertsteuer sind Anzeige, keine Preisbildung (E-099, siehe `contracts/PRICING.md`).
- Neue Geräte: 24, 36, 48 Monate, Voreinstellung 48, kein Kaufpreis. Geprüfte Geräte: siehe `contracts/REFURBISHED.md`.
- Das Etikett heißt „Empfohlen“ und ist kuratiert, nicht „Beliebt“ (E-065, E-099).
- Platzhalter heißen „Platzhalter“, nie „Demo“. „Demo“ meint nur Demo-Geräte, und die gibt es im Shop nicht.

### Sprache
- Warm, freundlich und knapp, Wir-Form, Anrede „Sie“. Überschriften in Satzanfangs-Großschreibung. Keine Ausrufezeichen, keine Emojis, keine langen Gedankenstriche.
- Immer ein Gespräch anbieten, konkret „zwanzig Minuten per Teams“.
- „Service“, nicht „Miete“ oder „Vermietung“. „Bankprüfung nicht erforderlich“, nicht „ohne Bank“.
- Im Shop nie „refurbished“, „aufbereitet“, „gebraucht“ oder „Rückläufer“, sondern „geprüft, gereinigt und mit Windows 11 Pro neu aufgesetzt“, ergänzt um „mit Gewährleistung“.
- Nie Bezugsquellen nennen. Verfügbarkeit neutral: „sofort verfügbar“.

### Medien
- Menschen beim Arbeiten in hellen, ruhigen Räumen, Geräte als Freisteller oder im Einsatz.
- Microsoft-Medien sind für den Shop freigegeben (E-104) und liegen nie in diesem Repo (E-092). Ablage nach `contracts/IMAGES.md`. Mindestgröße und Schutzraum des Reseller-Logos werden vor der Abnahme gegen die Co-Branding-Richtlinie geprüft.
- Icons im Strich des Designsystems, Farbe `icon`, keine Emojis.

### Nicht in dieses Repo
Firmenangaben gehören in die Rechtstexte der App, nicht in den Design-Vertrag (E-092). Die Tabelle „Firmenangaben“ aus der README des Designsystems wird deshalb nie übernommen. Das gilt auch für den Prototyp und für Medien.

### Stand der offenen Punkte aus `brand/surface/offene-punkte.md`
Das Paket bleibt wie geliefert, diese Punkte darin sind inzwischen entschieden:
- Garantie bei 48 Monaten: E-103, siehe `contracts/VARIANTEN.md`.
- Nutzung der Microsoft-Medien: E-104.
- `DESIGN.md`: mit dieser Fassung umgestellt.
- Sand auf der Startseite bleibt (E-146). Der Kontaktblock im Fuß zeigt nur Telefon und E-Mail, Anschrift im Impressum (F14, E-146).

## lenovo.online

Eigenständige Storefront im selben Code, nicht Teil von Beta 1. Alles ist Entwurf bis zur Markenfreigabe (E-017), die Freischaltung bleibt bis dahin gesperrt. Kennzeichnung im Entwurf: „Platzhalter“ (E-099). Im Hub stehen nur Regeln, keine Logos und keine Motive (E-092). Das Token-Paket wird beim Bau von lenovo.online neu eingeordnet, `brand/tokens.lenovo.css` ist bis dahin nicht gegen das Designsystem vom 05.11.2026 geprüft.

- Vollständig getrennt von Surface.Love: kein Herz, kein Claim, kein Open Sans, kein Markenblau, keine Microsoft-Medien, auch nicht als Platzhalter.
- Eigenständig gegenüber dem Hersteller: nie dessen Schriftzug, nie Kasten mit weißem Schriftzug oder vollflächiges Rot mit weißer Schrift, nur eigene Motive.
- Seite neutral, die Farbe kommt aus Logo und Motiven. `sf-accent` sparsam für Rate, primären Button und aktiven Schritt, `sf-action` höchstens einmal je Ansicht.
- Schrift: Bricolage Grotesque 700 für Wortmarke, `display`, `h1`, `h2`, Inter für alles andere, beide SIL OFL.
- Runde Karten und Bilder, zwei Schattentiefen, keine farbigen Schatten. Dieselben drei Dauern und dieselbe Kurve, kein Marken-Puls.

Solange Lenovo nicht gebaut ist, zeigt die Storefront im Shop nur eine neutrale Fassung.

## Gemeinsam für beide

- Klickziele mindestens 44 px, sichtbarer Fokusring, reduzierte Bewegung, Kontrast nach den Tokens.
- Rote Linien (E-065): nichts vorausgewählt, was kostet, kein Confirmshaming, keine künstliche Verknappung, kein erfundener Social Proof, Abwahl nie schwerer als Zuwahl.
- Je Shop nur die eigenen Schriften laden. `tokens.css` setzt ihre Werte auf `:root`, im Shop deshalb unter `[data-sf]` einbinden.
- Abnahme durch Sascha auf beta.surface.love, nicht im Prototyp (E-098).
