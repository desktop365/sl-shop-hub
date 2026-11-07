# Bausteine und Zustände, surface.love

Stand `slshopv18-arbeit.html`, Artifact-Version 24, Designsystem Surface.Love V2-2026. Verläufe auf Bild und Film kommen aus dem Token `schleier` (`blue-950`), die Stopps sind feste Werte und als Ausnahme angenommen (A1 bis A4, B1).

Diese Datei trägt die Übersetzung nach React. Der Prototyp wird nicht kopiert. Beschrieben ist die berechnete Wirkung für `data-sf="surface"`, der Block ab Zeile 742 überschreibt die allgemeinen Regeln davor. V18 enthält keinen Lenovo-Zweig mehr. Raten stehen als Daten im Prototyp, es gibt keine Faktoren (E-099). Texte in Anführungszeichen stehen so im Code.

„Gemessen“ heißt: im Prototyp in Chrome ausgeführt, Schirmbreite 1398 px und 372 px, Werte aus `getComputedStyle` und `getAnimations`.

## Token-Brücke

Alle Bausteine laufen über diese Variablen aus dem Block `[data-sf="surface"]` (Zeile 11 bis 36). Die rechte Spalte löst über `ds/surfacelove/tokens.css` auf.

| Variable | Wert im Block | Aufgelöst, hell |
|---|---|---|
| `--sf-accent` | `var(--brand)` | `#00A3E0` |
| `--sf-accent-strong` | `var(--accent-text)` | `#0076A8` |
| `--sf-accent-weak` | `var(--chip-cool)` | `#DFF0F8` |
| `--sf-action` | `var(--action)` | `#FFB23E` |
| `--sf-action-hover` | `var(--action-hover)` | `#CB891A` |
| `--sf-action-ink` | `var(--on-action)` | `#000000` |
| `--sf-focus` | `var(--focus)` | `#000000` |
| `--sf-ink` | `var(--ink)` | `#000000` |
| `--sf-text-2` | `var(--ink-muted)` | `#42494D` |
| `--sf-surface` | `var(--surface)` | `#FFFFFF` |
| `--sf-surface-2` | `var(--surface-raised)` | `#F6F9FA` |
| `--sf-border` | `var(--line)` | `#DFE3E5` |
| `--sf-border-strong` | `var(--control-border)` | `#747C7F` |
| `--sf-logo-ink` | `var(--brand)` | `#00A3E0` |
| `--sf-success` | `var(--success)` | `#007066` |
| `--sf-incoming` | `var(--warning)` | `#734C0F` |
| `--sf-onrequest` | `var(--ink-subtle)` | `#5A6265` |
| `--sf-badge-new-bg` | `var(--surface-raised)` | `#F6F9FA` |
| `--sf-badge-new-ink` | `var(--ink)` | `#000000` |
| `--sf-badge-ref-bg` | `var(--chip-cool)` | `#DFF0F8` |
| `--sf-badge-ref-ink` | `var(--on-chip-cool)` | `#124163` |
| `--sf-font` | `var(--font-sans)` | `"Open Sans", "Segoe UI", Arial, sans-serif` |
| `--sf-w-display` | `300` | gleich |
| `--sf-w-body` | `400` | gleich |
| `--sf-w-strong` | `600` | gleich |
| `--sf-text-display` | `clamp(2.75rem, 1.9rem + 3.6cqw, 4rem)` | gleich |
| `--sf-text-h1` | `clamp(2rem, 1.55rem + 1.9cqw, 2.75rem)` | gleich |
| `--sf-text-h2` | `clamp(1.5rem, 1.3rem + 0.9cqw, 2rem)` | gleich |
| `--sf-text-h3` | `1.125rem` | gleich |
| `--sf-text-body` | `1rem` | gleich |
| `--sf-text-small` | `0.875rem` | gleich |
| `--sf-text-micro` | `0.75rem` | gleich |
| `--sf-w-h2` | `300` | gleich |
| `--sf-tracking-display` | `0` | gleich |
| `--sf-leading-tight` | `1.094` | gleich |
| `--sf-leading-body` | `1.5` | gleich |
| `--sf-radius` | `var(--radius-none)` | `0px` |
| `--sf-radius-sm` | `var(--radius-none)` | `0px` |
| `--sf-radius-btn` | `var(--radius-s)` | `4px` |
| `--sf-shadow-card` | `none` | gleich |
| `--sf-shadow-float` | `none` | gleich |
| `--sf-ease` | `cubic-bezier(.2,.7,.3,1)` | gleich |
| `--sf-dur-1` | `150ms` | gleich |
| `--sf-dur-2` | `260ms` | gleich |
| `--sf-dur-3` | `550ms` | gleich |
| `--sf-pulse` | `0s` | gleich |
| `--sf-tint` | `0%` | gleich |
| `--sf-space-1` | `var(--space-1)` | `4px` |
| `--sf-space-2` | `var(--space-2)` | `8px` |
| `--sf-space-3` | `var(--space-3)` | `12px` |
| `--sf-space-4` | `var(--space-4)` | `16px` |
| `--sf-space-5` | `var(--space-6)` | `24px` |
| `--sf-space-6` | `var(--space-8)` | `32px` |
| `--sf-space-7` | `var(--space-12)` | `48px` |
| `--sf-space-8` | `var(--space-16)` | `64px` |
| `--sf-space-9` | `var(--space-24)` | `96px` |
| `--sf-container` | `1240px` | gleich |
| `--sf-gutter` | `clamp(20px, 4cqw, 40px)` | gleich |

Ergänzungen:

| Punkt | Wert |
|---|---|
| Lokale Überschreibung | `[data-screen-label="Vorteile"]` und `[data-screen-label="Inspiration"]` setzen `--sf-accent-strong` auf `--accent-text-sand` (`#06557F`) |
| Abstand | `--sf-space-5` ist `--space-6` (24 px), `--space-5` im Designsystem ist 20 px. Beide kommen im Code vor, je Baustein steht der tatsächlich benutzte Name |
| Dunkler Modus | `tokens.css` enthält `[data-theme="dark"]`, der Prototyp setzt `data-theme` nie |
| Lokale Variablen je Element | `--d` (Verzögerung, wirkt nur zusammen mit `data-rev`), `--devc` (Gerätefarbe, im Surface-Zweig durch flache Flächen ohne sichtbare Wirkung), `--c` (Farbkreis, Hexwert aus den Daten) |

## Bewegung, Grundregeln

#### Dauern und Kurven

| Name | Wert | Glossar | Einsatz |
|---|---|---|---|
| `--sf-dur-1` | 150 ms | Duration | Hover an Knöpfen und Pfeilen |
| `--sf-dur-2` | 260 ms | Duration | Listenzeilen, Marker, kleine Zustandswechsel |
| `--sf-dur-3` | 550 ms | Duration | Reglerfüllung, Schalter, Tinte, Gerätebild |
| `--sf-ease` | `cubic-bezier(.2,.7,.3,1)` | Ease-out, als Cubic-bezier | Standardkurve überall |
| `--sf-pulse` | `0s` | Duration | Herzschlag, damit im Surface-Zweig ohne sichtbare Wirkung |
| Überschwingkurve | `cubic-bezier(.34,1.56,.64,1)`, fester Wert, kein Token | Bounce, Näherung (Kurve statt Feder) | `ratepulse`, `chkIn`, Rückfedern des Griffs |
| Zähler im JS | `1 - (1 - p)^3`, 420 ms, fester Wert, kein Token | Ease-out | `animateRate()` |
| Weitere feste Dauern, kein Token | .3s, .35s, .4s, .42s, .45s, .55s, .6s, .7s, .9s, 220 ms | Duration | je Baustein genannt |

#### Keyframes

| Keyframes | Eigenschaft | Dauer, Kurve, Verzögerung | Glossar | Wirkung im Surface-Zweig |
|---|---|---|---|---|
| `revUp` | `transform`, translateY(18px) nach none | .7s, `--sf-ease`, `var(--d,0s)` | Enter, mit Translate. Mit gesetztem `--d`: Stagger | Läuft auf jedem `[data-rev]`, bei jedem Einfügen ins DOM |
| `chkIn` | `transform`, scale(.6) nach scale(1) | 220 ms, Überschwingkurve | Pop in | Auf `.bst.on .chk svg` |
| `ratepulse` | `transform`, scale 1, 1.045, 1 | .42s, Überschwingkurve | Pulse, Näherung (läuft einmal) | Auf `.rate-live.pulse` |
| `slBandFlash` | `border-top-color`, `--brand` nach `--line` | .6s, `--sf-ease` | Pulse, Näherung (einmal, nur Randfarbe) | Auf `.band.flash`, ersetzt `ring` |
| `dlgIn` | `transform`, translateY(12px) nach none | .3s, `--sf-ease` | Enter, mit Translate | Auf `.dlg-in` |
| `sheetUp` | `transform`, translateY(40px) nach none | .35s, `--sf-ease` | Enter, mit Translate | Auf `.dlg.bottom .dlg-in` und `.dlg.zub .dlg-in` unter 760 px |
| `zubSide` | `transform`, translateX(60px) nach none | .4s, `--sf-ease` | Enter, mit Translate | Auf `.dlg.zub .dlg-in` ab 760 px |
| `beat` | `transform`, scale 1, 1.12, 1, 1.08, 1 | `var(--sf-pulse,0s)`, 3 Durchläufe | Pulse | Keine: Dauer 0s auf `.heart.go`, `.logo .heart` hat `animation:none` (gemessen) |
| `ring` | `box-shadow` | .6s | Pulse, Näherung | Keine: von `slBandFlash` überschrieben |
| `kb` | `transform`, scale und translate, `forwards` | 7s | Scale mit Fill mode, Näherung | Keine: `.scene-art` ist `display:none` |
| `fadeUp` | `transform`, translateY(20px) nach none | .9s | Enter, mit Translate | Keine: `.fx` wird nicht gerendert |
| `morph` | `opacity`, `transform` | .4s | Fade in mit Translate | Keine: `.morph` wird nicht gerendert |

#### Reduced Motion (Glossar: Reduced motion)

| Stelle | Regel |
|---|---|
| CSS, Zeile 61 bis 64 | `@media (prefers-reduced-motion: reduce)`: `*, *::before, *::after {animation:none!important; transition:none!important}`, `[data-rev]{opacity:1!important; transform:none!important}` |
| `REDUCE` im JS | Einmal beim Laden aus `matchMedia` gelesen |
| Medien | `slVideo()` liefert nur Poster, `slVctl()` nichts, `vslot()` im Akkordeon die Szene plus `.tag` „Videoslot: eigenes Material folgt“, `observeMedia()` läuft nicht (gemessen: 0 Videos, 0 `.vctl`) |
| Neigung | `[data-stage]` bindet keine Zeigerereignisse |
| Zahlen | `animateRate()` setzt den Endwert ohne Zählen |
| Rechenhinweis | `updateAus()` zeigt „Rate wird neu berechnet“ nicht |
| Griff | Schließen ohne Bewegung, Rückfedern ohne Transition |
| Punktnavigation | `scrollTo` mit `behavior:"auto"` |

## Breakpoints

Alle Schwellen sind `@container screen`, bezogen auf die Inline-Breite von `.screen`, nicht auf das Fenster. Handy heißt unter der jeweiligen Schwelle, Desktop darüber. Bei `max-width` gilt die Regel unter und bis zur Schwelle.

| Schwelle | Regel | Betroffen |
|---|---|---|
| `max-width:560px` | Kurzzeile statt Langzeile | `.b2 .hl-l`, `.b2 .hl-s` |
| `min-width:560px` | 2 Spalten | `.frow` |
| `min-width:620px` | 2 Spalten | `.uc` |
| `max-width:699px` | Umbruch erlaubt | `.railhead` |
| `min-width:700px` | 2 Spalten | `.typegrid`, `.ref-promise` |
| `max-width:760px` | `min-height:0`, Kampagne mit `padding-top:200px` und eigenem Verlauf | `.b2-in`, `.mood-in`, `.b2 .sl-veil` |
| `min-width:760px` | 3 Spalten, Seitenblatt statt Unterblatt | `.insp`, `.sl-imp-g`, `.dlg.zub` |
| `min-width:800px` | Navigation und Telefon an, Menüknopf aus, 3 Spalten im Fuß | `.nav`, `.phone-l`, `.only-m`, `.ftr-grid` |
| `min-width:820px` | 4 Spalten | `.cyc` |
| `min-width:840px` | 2 Spalten, Punktnavigation an | `.leaf`, `.dots` |
| `min-width:860px` | 2 Spalten, Bahn ohne Scrollen, Bühne klebt | `.vlist`, `.acc`, `.split`, `.kfg`, `.kstage-wrap`, `.bahn` |
| `max-width:899px` | Verlauf für Handy | `.sl-hf-a .sl-veil` |
| `min-width:900px` | 4 Spalten, 3 Spalten, Summenleiste statt Unterleiste | `.uc`, `.sl-rateband-in`, `.aus`, `.aus-sum`, `.aus-bar` |
| `min-width:1000px` | 3 und 4 Spalten | `.typegrid`, `.ref-promise` |

Außerhalb von Container-Regeln:

| Stelle | Bedingung | Wirkung |
|---|---|---|
| `screenStartSurface()` | `state.view === "mobile"` oder `window.innerWidth < 700` | Hero-Video und Poster in der Mobilfassung |
| `SZ` in `pimg()` | Media-Angaben in `sizes`, nur wenn `IMAGES.live` wahr ist | `card`, `leaf`, `stage`, `thumb` |
| `initScreen()` | `(pointer:fine)` | 3D-Neigung der Bühne |

Abgeleitete Größen über `cqw`, ohne feste Schwelle: `--sf-text-display`, `--sf-text-h1`, `--sf-text-h2`, `--sf-gutter`, `.sect`, `.sect-tight`.

## Global

### Seitenraster (`.screen`, `.wrap`, `.sect`, `.sect-tight`, `renderScreen()`, alle Seiten)
Trägt Container-Breite, Seitenrand und vertikale Abschnittsabstände.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | Seite gerendert | `.screen` scrollt vertikal, `overflow-x:hidden`, `container-name:screen`, `isolation:isolate` |
| Blatt offen | `state.sheet` wahr, Klasse `.sheetopen` | `.screen` mit `overflow:hidden` |
| Abschnitt | Markup | `.wrap.sect` und `.wrap.sect-tight` tragen Seitenrand plus vertikalen Abstand |

Tokens: `--sf-surface`, `--sf-ink`, `--sf-font`, `--sf-text-body`, `--sf-leading-body`, `--sf-container`, `--sf-gutter`, `--sf-border-strong` (Scrollleiste). `.sect` `clamp(48px,7cqw,96px)`, `.sect-tight` `clamp(32px,5cqw,64px)`, beide fester Wert, kein Token.

Handy: gemessen bei 372 px Seitenrand 20 px, `.sect` 48 px, `.sect-tight` 32 px.

Desktop: gemessen bei 1398 px Seitenrand 40 px, `.sect` 96 px, `.sect-tight` 64 px, `.wrap` bis 1240 px.

Bewegung: keine.

### Fokusring (`:focus-visible`, kein JS, alle Seiten)
Einzige erlaubte Schattenform, Regel gilt für alles Fokussierbare, Abweichungen stehen in der Tabelle.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Fokus, Standard | Tastaturfokus | `outline:0`, `box-shadow:var(--focus-ring)`, 2 px Weiß, 2 px Schwarz (gemessen) |
| Fokus an `.sw`, `.sw.on` | Tastaturfokus | `[data-sf] .sw{box-shadow:none}` steht später bei gleicher Spezifität, kein sichtbarer Fokus (gemessen) |
| Fokus an `.stop.on` | Tastaturfokus, auch nach Pfeiltaste per `again.focus()` | `.stop.on{box-shadow:none}`, kein sichtbarer Fokus (gemessen) |
| Fokus an `.stop` ohne `.on` | Tastaturfokus | Ring, blendet über die Transition von `box-shadow` ein |
| Fokus an `.zgal-dots button` | Tastaturfokus | Ring plus `outline:2px solid`, `outline-offset:6px` (gemessen) |
| Fokus an `.zgal-thumbs button` | Tastaturfokus | Ring plus `outline:2px solid`, `outline-offset:2px` |
| Fokus an `.fld input` | `:focus`, auch per Maus | Ring plus `border-color:var(--focus)` |
| Fokus an `.nav span`, `.ftr-col span` | nicht fokussierbar | im Prototyp nicht gezeichnet |

Tokens: `--focus-ring`, `--focus`, `--sf-focus`.

Handy: gleich.

Desktop: gleich.

Bewegung: keine, außer `.stop` (Interpolation / Tween, `box-shadow`, 260 ms, `--sf-ease`, Verzögerung 0).

### Typografie (`.display`, `.h1`, `.h2`, `.lead`, `.small`, `.micro`, `.num`, Markup, alle Seiten)
Die Schriftstufen des Shops, jede Stufe als Zeile.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| `.display` | Klasse | `--sf-text-display`, Gewicht 300, Zeilenhöhe 1.094, `text-wrap:balance`. Gemessen 44 px bei 372, 64 px bei 1398 |
| `.h1` | Klasse | `--sf-text-h1`, Gewicht 300, Zeilenhöhe 1.18, `balance`. Gemessen 32 px bei 372, 44 px bei 1398 |
| `.h2` | Klasse | `--sf-text-h2`, Gewicht 300, Zeilenhöhe 1.25, `balance` |
| `.lead` | Klasse | 18/28 px, Gewicht 300, `--ink-muted`, `max-width:52ch`, `text-wrap:pretty` |
| `.small` | Klasse | `--sf-text-small`, Zeilenhöhe 20 px, `--sf-text-2` |
| `.micro` | Klasse | `--sf-text-micro`, Zeilenhöhe 16 px, `--ink-subtle` |
| `.num` | Klasse | `font-variant-numeric:tabular-nums` |

Tokens: `--sf-text-display`, `--sf-text-h1`, `--sf-text-h2`, `--sf-text-small`, `--sf-text-micro`, `--sf-w-display`, `--sf-w-h2`, `--sf-tracking-display`, `--ink-muted`, `--ink-subtle`, `--sf-text-2`. `.lead` 18/28 px und die Zeilenhöhen 1.18, 1.25 fester Wert, kein Token.

Handy: Größe über `cqw`, siehe Tabelle.

Desktop: Größe über `cqw`, siehe Tabelle.

Bewegung: keine. Tabular numbers über `.num`.

### Etikett Zeile (`.lbl`, `.kick`, `.sl-eyebrow`, Markup, alle Seiten)
Kleine Kopfzeile über Überschriften und Gruppen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Standard `.lbl`, `.kick` | Klasse | 12/16 px, Gewicht 600, Sperrung .14em, Versalien, `--sf-accent-strong` |
| In `.grp-h`, `.bkat-h`, `.kstage-wrap` | Eltern | Keine Sperrung, keine Versalien, `--ink-muted` |
| `.cmp-c.lbl` | Vergleichstabelle | 14/20 px, Gewicht 400, keine Versalien, `--ink-muted` |
| Auf Sand | `[data-screen-label="Vorteile"]`, `"Inspiration"` | Farbe `--accent-text-sand` |
| Auf tiefer Fläche | `.dark .lbl` | `--on-deep-accent` |
| `.sl-eyebrow` | Hero | 12/16 px, 600, .14em, Versalien, `--on-deep-accent` |

Tokens: `--sf-accent-strong`, `--ink-muted`, `--accent-text-sand`, `--on-deep-accent`, `--accent-text` (Grundwert `.sl-eyebrow`). 12/16 px und .14em fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Abschnittskopf (`.railhead`, Markup, Startseite, Geräte)
Setzt Etikett und Überschrift links, Link oder Lead rechts.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | Markup | `flex`, `align-items:flex-end`, `space-between`, `gap:20px`, `margin-bottom:clamp(28px,4cqw,52px)` |
| Breitenbegrenzung | Inline `max-width` am Kind | `max-width:38rem!important`, der Inline-Wert in `ch` wirkt nicht |

Tokens: keine, alle Maße fester Wert, kein Token.

Handy: bis 699 px `flex-wrap:wrap`.

Desktop: ab 700 px einzeilig.

Bewegung: keine.

### Kopf (`.hdr`, `.hdr-in`, `.hdr-cta`, `header()`, alle Seiten)
Klebende Kopfzeile mit Navigation, Telefon, Anfragekorb und Herz rechts.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | immer, Klassen `.solid .onlight` | `--surface`, 1 px Linie unten, kein Blur, `position:sticky`, `z-index:20` |
| Über dem Hero | `.overhero` | im Prototyp nicht gezeichnet, `hdr.dataset.hero` wird nie gesetzt |

Tokens: `--surface`, `--line`, `--border-hair`. `.hdr-in` `height:74px`, `gap:20px`, fester Wert, kein Token.

Handy: unter 800 px Reihenfolge Menüknopf, Korb, Herz. Navigation und Telefon aus.

Desktop: ab 800 px Reihenfolge Navigation, Telefon, Korb, Herz.

Bewegung: `transition` auf `background` und `border-color` 260 ms, `--sf-ease`, Verzögerung 0 ist definiert. Die Klassen wechseln nicht, also keine sichtbare Bewegung.

### Hauptnavigation (`.nav`, `header()`, alle Seiten)
Vier Textziele im Kopf.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 14 px, `--ink-muted`, `gap:26px` |
| Hover | Zeiger | Farbe `--ink`, Unterstrich 1 px in `currentColor` wächst von links |
| Aktiv, aktuelle Seite | | im Prototyp nicht gezeichnet |
| Ohne Ziel | „So funktioniert es“ hat kein `data-go` | Kein Klickziel, Hover wie alle |
| Fokus | `span`, nicht fokussierbar | im Prototyp nicht gezeichnet |

Tokens: `--ink-muted`, `--ink`, `--sf-text-small`, `--sf-dur-2`, `--sf-ease`. `gap:26px` fester Wert, kein Token.

Handy: unter 800 px `display:none`.

Desktop: ab 800 px `display:flex`.

Bewegung: Hover effect mit Scale und Transform origin links, `::after`, `transform` scaleX(0) nach scaleX(1), 260 ms, `--sf-ease`, Verzögerung 0 (gemessen). Farbe springt.

### Menüknopf (`.only-m`, `header()`, alle Seiten)
Öffnet im Prototyp nichts.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe, Hover, Fokus | wie Symbolknopf | siehe `.iconbtn` |
| Menü offen | | im Prototyp nicht gezeichnet, kein Klick-Handler |

Tokens: wie `.iconbtn`.

Handy: unter 800 px sichtbar, ganz links.

Desktop: ab 800 px `display:none`.

Bewegung: wie `.iconbtn`.

### Telefonlink (`.phone-l`, `.ph-r`, `header()` und `screenStartSurface()`, alle Seiten)
Zeigt die Vanity-Nummer, die Rufnummer klappt bei Hover aus.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 14 px, Gewicht 600, Icon in `--icon`. Im Kopf `--ink-muted`, in `.contactline` `--sf-ink` |
| Hover | Zeiger, nur im Kopf | `.ph-r` wächst auf `max-width:130px`, `margin-left:6px` |
| Fokus | Tastatur | Ring |
| Klick | `a[href^="tel:"]` | Im Prototyp `preventDefault` |

Tokens: `--icon`, `--ink-muted`, `--sf-ink`, `--sf-text-2`, `--sf-text-small`, `--sf-ease`. `.35s`, `130px`, `gap:8px` fester Wert, kein Token.

Handy: unter 800 px im Kopf aus. In `.contactline` per Inline-Stil immer sichtbar, dort ohne `.ph-r`.

Desktop: ab 800 px im Kopf sichtbar.

Bewegung: Reveal, Näherung (über `max-width` statt Clip-path), `max-width` und `margin-left`, .35s, `--sf-ease`, Verzögerung 0 (gemessen).

### Symbolknopf (`.iconbtn`, `header()`, `sheetHTML()`, `zubSheet()`, `screenAusstattung()`, alle Seiten)
Quadratischer Knopf für Korb, Menü und Schließen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 42 x 42 px, `--radius-s`, ohne Rand, Icon in `--sf-ink` |
| Hover | Zeiger | Fläche `--surface-raised` |
| Aktiv | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |

Tokens: `--radius-s`, `--surface-raised`, `--sf-ink`, `--sf-dur-1`, `--sf-ease`. 42 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Hover effect, `background`, 150 ms, `--sf-ease`, Verzögerung 0 (gemessen).

### Korbzähler (`.count`, `header()`, alle Seiten)
Zeigt die Gerätemenge im Anfragekorb am Korbsymbol.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Mit Inhalt | `cartCount()` größer 0 | 17 px hohe Pille oben rechts, `--marker`, Schrift `--on-action`, 11 px, 600 |
| Leer | `cartCount()` ist 0 | Inline `display:none` |
| Platzhalter | Korb startet aus `BRANDS.surface.cart` mit Menge 5, danach `localStorage` | Zahl 5 |

Tokens: `--marker`, `--on-action`, `--radius-pill`. 17 px, 11 px, `top:4px`, `right:2px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Herz und Logo (`.logo`, `.heart`, `markSurface`, `header()`, alle Seiten)
Einziges Logo, rechts außen im Kopf, führt zur Startseite.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | SVG 43 x 38 px, Füllung `--sf-accent`, `margin-left:var(--space-3)`, `flex:none` |
| Hover | Zeiger | Keine Änderung: `[data-sf] .logo .heart{animation:none}` (gemessen) |
| Nach Seitenwechsel | `render()` setzt `.go` | Keine Änderung, gleicher Grund |
| Fokus | Tastatur | Ring |

Tokens: `--sf-accent`, `--space-3`, `--sf-pulse`.

Handy: gleich.

Desktop: gleich.

Bewegung: keine. `beat` ist definiert und wirkt nicht, siehe Keyframes.

### Band Versprechen (`.ftr-band`, `.sl-band`, `.sl-band-title`, `.sl-band-text`, `footer()`, alle Seiten)
Blaues Band vor dem Fuß mit Satz und weißem Herz.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Fläche `--surface-brand`, Titel 28/34 px 300 in `--on-brand-display`, Text 14/20 px in `--on-brand`, Herz in `--on-brand-display`, `padding-top` und `padding-bottom` `--space-6` |

Tokens: `--surface-brand`, `--on-brand-display`, `--on-brand`, `--space-4`, `--space-6`. 28/34 px und 14/20 px fester Wert, kein Token.

Handy: keine eigene Regel, `flex`, `space-between`, Herz 43 x 38 px.

Desktop: wie Handy.

Bewegung: keine.

### Fuß (`.ftr`, `.ftr-grid`, `.ftr-note`, `.ftr-col`, `.ftr-base`, `.sl-claim`, `.sl-contact`, `footer()`, alle Seiten)
Claim, Firmenangaben aus `BRANDS.surface.firma`, Reseller-Logo, zwei Linkspalten, Grundzeile.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Kein Rand oben, `--ink-muted`, 14 px. Claim 30/35 px 300 in `--heading`, dreizeilig |
| Link Hover | Zeiger auf `.ftr-col span` | Farbe `--sf-ink`, Unterstrich mit Abstand 3 px |
| Link ohne Ziel | „So funktioniert es“, „AGB“, „Widerruf“, „Markenhinweise“ ohne `data-go` | Kein Klickziel, Hover wie alle |
| Link mit Ziel | `data-go` auf `geraete`, `konfigurator`, `refkat`, `impressum`, `datenschutz` | Seitenwechsel |
| Fokus | `span`, nicht fokussierbar | im Prototyp nicht gezeichnet |

Tokens: `--ink-muted`, `--heading`, `--ink`, `--ink-subtle` (`.ftr-base`), `--sf-text-small`, `--sf-ink`, `--sf-space-4`, `--sf-space-6`, `--sf-space-7`, `--space-4`, `--space-6`. `.ftr` oben `clamp(48px,6cqw,80px)`, `.ftr-note` `max-width:28rem`, `.ftr-base` 11/16 px fester Wert, kein Token.

Handy: unter 800 px 1 Spalte, `gap` 32 px.

Desktop: ab 800 px 3 Spalten `1.3fr 1fr 1fr`.

Bewegung: keine.

### Reseller-Logo (`.sl-reseller`, `footer()`, `screenStartSurface()`, alle Seiten)
Unverändertes Logo aus dem Designsystem.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Höhe 48 px, Breite automatisch. Im Fuß `margin-top:var(--space-6)` |

Tokens: `--space-6`. 48 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich, in `.sl-rateband-in` ab 900 px als dritte Spalte.

Bewegung: keine.

### Knopf (`.btn`, `.primary`, `.ghost`, `.ghostw`, `.block`, `.loading`, Markup, alle Seiten)
Einziger Aktionsknopf, drei Varianten.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe `.primary` | | `--action`, Schrift `--on-action`, 14/20 px, 600, `padding:12px 16px`, `min-height:44px`, `--radius-s` (gemessen) |
| Hover `.primary` | Zeiger | `--action-hover` |
| Aktiv `.primary` | `:active` | `--action-active`, keine Verschiebung, `transform:none` |
| Ruhe `.ghost` | | Transparent, Schrift `--heading`, Rand 1 px `--line-strong` |
| Hover `.ghost` | Zeiger | `--surface-raised` |
| Ruhe `.ghostw` | Auf tiefer Fläche | Transparent, Schrift und Rand `--on-deep` |
| Hover `.ghostw` | Zeiger | Fläche `--on-deep`, Schrift `--heading` |
| Aktiv `.ghost`, `.ghostw` | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Laden | `.loading`, gesetzt von `data-send` und `data-pay`, Text wird ersetzt | `opacity:.7`, `pointer-events:none` (gemessen). 900 ms |
| Gesperrt | | im Prototyp nicht gezeichnet |
| Volle Breite | `.block` | `width:100%` |

Tokens: `--action`, `--action-hover`, `--action-active`, `--on-action`, `--heading`, `--line-strong`, `--surface-raised`, `--on-deep`, `--radius-s`, `--sf-w-strong`, `--sf-dur-1`, `--sf-ease`. 14/20 px, 12/16 px Innenabstand, 44 px, `gap:9px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Hover effect, `background`, 150 ms, `--sf-ease`, Verzögerung 0 (gemessen). Farbwechsel bei `.ghostw` springt. Press / Tap feedback gibt es nicht.

### Textlink (`.lnk`, `.onw`, Markup, Startseite, Geräte, Konfigurator, Ausstattung, Anfrage-Blatt, Geprüftes Gerät, Kasse)
Unterstrichener Link mit Pfeil.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 14 px, 600, `--sf-accent-strong`, unterstrichen, Abstand 3 px, Pfeil rechts, `gap:7px` |
| Hover | Zeiger | Pfeil rückt 4 px nach rechts |
| Auf Bild | `.onw` | `--on-deep` |
| Rücklink | Inline `color:var(--sf-text-2)` | Pfeil links vor dem Text, um 180 Grad gedreht, auch bei Hover, keine Verschiebung |
| Klein | Inline `font-size:var(--sf-text-micro)`, „Positionen ändern“, „Bestellung ändern“ | 12 px |
| Fokus | Tastatur | Ring |

Tokens: `--sf-accent-strong`, `--on-deep`, `--sf-text-small`, `--sf-text-2`, `--sf-text-micro`, `--sf-dur-1`, `--sf-ease`.

Handy: gleich.

Desktop: gleich.

Bewegung: Hover effect mit Translate, `transform` translateX(4px) am `svg`, 150 ms, `--sf-ease`, Verzögerung 0 (gemessen).

### Ink-Link (`.lnk-ink`, `refBand()`, `recompute()`, `bstRowHTML()`, `altDlg()`, `screenRefProd()`, Startseite, Geräte, Konfigurator, Ausstattung, Anfrage-Blatt, Geprüftes Gerät)
Schwarzer Link für Hinweise auf geprüfte Geräte und Stufenwechsel.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 14 px, 600, `--ink`, ohne Unterstrich |
| Hover | Zeiger | Unterstrich mit Abstand 3 px, Pfeil rückt 4 px |
| In `.bst-cond` | Eltern | 12 px |
| Fokus | Tastatur | Ring |

Tokens: `--ink`, `--sf-text-small`, `--sf-text-micro`, `--sf-dur-1`, `--sf-ease`.

Handy: gleich.

Desktop: gleich.

Bewegung: Hover effect mit Translate, `transform` translateX(4px) am `svg`, 150 ms, `--sf-ease`, Verzögerung 0 (gemessen).

### Platzhalter-Kennzeichen (`.platzhalter`, Markup, alle Seiten)
Kennzeichnet Platzhalter sichtbar. Die Kennzeichnung heißt immer „Platzhalter“, das Wort „Demo“ meint nur Demo-Geräte, und die gibt es im Shop nicht (E-099).

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 11/16 px, 400, Pille, Rand 1 px `--line`, Schrift `--ink-subtle`, `padding:0 8px`, `margin-left:8px` |
| Auf Bild | `.b2-in .platzhalter`, `.mood-in .platzhalter` | Schrift und Rand `--on-deep` |
| Platzhalter, Texte | Daten oder Markup | „Platzhalter“, „Link-Ziel Platzhalter“, „Platzhalter-Motive“, „Platzhalter: Motive und Link-Ziele“, „Platzhalter-Bestand“, „Platzhalter-Bausteine“ |
| Platzhalter, Texte | Markup | „Platzhalter“, „Gerüst, Text folgt vom Master“ |

Tokens: `--line`, `--ink-subtle`, `--radius-pill`, `--on-deep`. 11/16 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Medien-Etikett (`.tag`, `.dark`, `pimg()`, `slMotiv()`, `scene()`, `vslot()`, Startseite, Geräte, Konfigurator, Anfrage-Blatt, Geprüfte Geräte Katalog, Geprüftes Gerät, Kasse)
Sagt auf Bildern an, dass das Motiv Platzhalter oder Referenz ist.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `top:14px`, `left:14px`, `--surface`, `--ink-muted`, 11/16 px, Pille, `padding:4px 12px`, `z-index:3` |
| In Geräte- und Typfeld, Bühne | `.dev-field`, `.type-field`, `.kstage` | `top:auto`, `bottom:14px` |
| Dunkel | `.tag.dark` | `--scrim`, `--on-deep` |
| Im Thumb | `pimg()` in `.line-thumb` | `.line-thumb` ist `position:static`, Bezug ist `.sheet` oder `.screen`. Das Etikett liegt außerhalb des Thumbs oben links am Blatt (gemessen) |
| Platzhalter, Texte | Render-Funktion | „Kampagnenmotiv, Platzhalter“, „Redaktionsmotiv, Platzhalter“, „Referenz Microsoft, Feed-Bild folgt“, „Kampagnenmotiv, Platzhalter, Slot leer“, Bildname plus „, Platzhalter“ |
| Ersatz, Texte | Reduced Motion oder Bildfehler | „Videoslot: eigenes Material folgt“, „Bildslot: eigenes Material folgt“ |

Tokens: `--surface`, `--ink-muted`, `--scrim`, `--on-deep`, `--radius-pill`. Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Etikett Geprüft (`.type-badge`, `refCard()`, `screenRefProd()`, Geprüfte Geräte Katalog, Geprüftes Gerät)
Markiert Geräte der geprüften Spur auf dem Bild.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | „Geprüft“, `top:14px`, `left:14px`, 12/16 px, 600, Pille, `--chip-cool`, `--on-chip-cool`, `padding:4px 12px` |

Tokens: `--chip-cool`, `--on-chip-cool`, `--radius-pill`. Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Etikett Zustand und Farbe (`.pill-ink`, `.type-meta`, `refCard()`, `screenRefProd()`, Geprüfte Geräte Katalog, Geprüftes Gerät)
Zeigt „Zustand gut“, „Zustand sehr gut“ und „Farbe ...“ neben dem Status.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `t.zustand`, `t.farbe` | 12/16 px, 600, Pille, `--chip-cool`, `--on-chip-cool`, `padding:4px 12px`, ohne Rand (gemessen) |
| Ohne Farbe | `t.farbe` fehlt | Keine Farb-Pille |

Tokens: `--chip-cool`, `--on-chip-cool`, `--radius-pill`. `.type-meta` `gap:12px`, `margin-top:12px` fester Wert, kein Token.

Handy: gleich, `flex-wrap:wrap`.

Desktop: gleich.

Bewegung: keine.

### Etikett warm (`.bst-etikett`, `bstRowHTML()`, `recompute()`, Konfigurator, Ausstattung)
Warmes Etikett neben Titeln, Text „Empfohlen“, kuratiert (E-065).

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Empfohlen | `bstEmpList()` aus `KUR.empfohlen` | 12/16 px, 600, Pille, `--chip-warm`, `--accent-warm-text`, `padding:4px 12px`, `margin-left:8px` (gemessen) |
| Stufe | `KUR.empfohlene_stufe`, sonst `t.empfohlen` | Gleiches Aussehen |

Tokens: `--chip-warm`, `--accent-warm-text`, `--radius-pill`. Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Verfügbarkeit (`.stat`, `statHTML()`, `stockState()`, `refBand()`, Startseite, Geräte, Geprüfte Geräte Katalog, Geprüftes Gerät)
Punkt plus Text aus dem Bestand.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Sofort verfügbar | Bestand über `CFG.knappSchwelle` (5), `.ok` | Punkt `--sf-success`, Text `--sf-text-2`, „sofort verfügbar“ |
| Im Band | `refBand()`, fest `.ok` | Text „Sofort verfügbar“, unabhängig von der Menge |
| Knapp | Bestand 2 bis 5, `.low` | Punkt und Text `--warning`, „nur noch n verfügbar“ |
| Einzelstück | Bestand 1, `.low` | Punkt und Text `--warning`, „Einzelstück“ |
| Vergriffen | Bestand 0, `.out` | Punkt `--sf-onrequest`, Text `--sf-text-2`, „derzeit vergriffen“. Nur auf der Produktseite, der Katalog filtert auf Bestand |

Tokens: `--sf-success`, `--sf-incoming`, `--warning`, `--sf-onrequest`, `--sf-text-2`, `--sf-text-small`. Punkt 8 x 8 px rund (50 %), `gap:8px`, fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Eingabefeld (`.fld`, `sheetHTML()`, `screenRefKasse()`, Anfrage-Blatt, Kasse)
Beschriftetes Textfeld.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Label 12/16 px, 600, `--ink-muted`. Feld Rand 1 px `--control-border`, `--radius-s`, `--surface-raised`, `padding:var(--space-3)`, `min-height:44px` (gemessen) |
| Platzhalter | leer | `--ink-subtle` |
| Hover | | im Prototyp nicht gezeichnet |
| Fokus | `:focus` | Ring plus Rand `--focus` |
| Fehler | | im Prototyp nicht gezeichnet, keine Prüfung, kein `required` |
| Gesperrt | | im Prototyp nicht gezeichnet |

Tokens: `--ink-muted`, `--control-border`, `--radius-s`, `--surface-raised`, `--space-3`, `--ink-subtle`, `--focus`, `--focus-ring`, `--sf-ink`, `--sf-space-5` (Abstand nach unten). 12/16 px, 44 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Feldzeile (`.frow`, `sheetHTML()`, `screenRefKasse()`, Anfrage-Blatt, Kasse)
Setzt Name und E-Mail nebeneinander.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `grid`, `gap:0 20px` |

Tokens: keine, `gap` fester Wert, kein Token.

Handy: unter 560 px 1 Spalte.

Desktop: ab 560 px `1fr 1fr`.

Bewegung: keine.

### Zustimmung (`.chk-line`, `sheetHTML()`, `screenRefKasse()`, Anfrage-Blatt, Kasse)
Natives Kontrollkästchen mit Text.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 12 px, `--sf-text-2`, Zeilenhöhe 1.55, `gap:12px` |
| Gewählt | Nutzer | `accent-color:var(--accent-text)` |
| Fokus | Tastatur | Ring (gemessen) |
| Fehler, nicht gesetzt | | im Prototyp nicht gezeichnet, Weitergehen ist ohne Haken möglich |

Tokens: `--sf-text-micro`, `--sf-text-2`, `--accent-text`, `--sf-space-4`.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Menge (`.qty`, `.qv`, `data-q`, `data-lq`, `data-bq`, `data-rq`, Konfigurator, Ausstattung, Anfrage-Blatt, Geprüftes Gerät)
Plus-Minus-Zähler in drei Größen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe, Standard | `.qty` | 44 x 44 px, `--radius-s`, Rand 1 px `--control-border`, Zahl `.qv` 1.5rem, 600, tabellarisch, `min-width:56px` |
| Ruhe, in `.line-ctl` | Anfrage-Blatt | 32 x 32 px, Zeichen 15 px, `.qv` `min-width:34px`, `--sf-text-body` |
| Ruhe, in `.bst-qty` | Ausstattung | 30 x 30 px, Zeichen 14 px, `.qv` `min-width:26px`, `--sf-text-small` |
| Hover | Zeiger | `--sf-surface-2` |
| Aktiv | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Minimum | Menge 1 | Minus bleibt aktiv, Wert bleibt 1 |
| Maximum, gesperrt | Nur Geprüftes Gerät, Menge gleich Bestand | Plus `disabled`, Inline `opacity:.4`, `cursor:default`, darunter `.small` „maximal n verfügbar“ (gemessen) |

Tokens: `--control-border`, `--radius-s`, `--sf-surface-2`, `--sf-text-body`, `--sf-text-small`, `--sf-dur-1`, `--sf-ease`. Maße fester Wert, kein Token. Trefferfläche `::after`, `inset:-8px`.

Handy: gleich.

Desktop: gleich.

Bewegung: Hover effect, `background`, 150 ms, `--sf-ease`, Verzögerung 0 (gemessen). Tabular numbers.

### Haken (`.chk`, `recompute()`, `bstRowHTML()`, Konfigurator, Ausstattung)
Quadrat mit Häkchen als Auswahlanzeige.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 26 x 26 px, `--radius-s`, Rand 1.5 px `--control-border`, Häkchen `color:transparent` |
| Gewählt in `.tierrow.on` | Stufe gewählt | Fläche und Rand `--sf-ink`, Häkchen `#fff`, fester Wert, kein Token |
| Gewählt in `.bst.on` | Baustein gewählt | Fläche und Rand `--sf-accent-strong`, Häkchen `#fff`, fester Wert, kein Token |

Tokens: `--control-border`, `--radius-s`, `--sf-ink`, `--sf-accent-strong`, `--sf-dur-2`, `--sf-ease`.

Handy: gleich.

Desktop: gleich.

Bewegung: Pop in nur in `.bst.on`: `chkIn`, `transform` am `svg`, 220 ms, Überschwingkurve, Verzögerung 0. `updateAus()` schreibt die Karten neu, deshalb startet die Bewegung bei jedem Klick an allen gewählten Bausteinen (gemessen). `transition` auf `background`, `border-color`, `color` 260 ms ist definiert, läuft nicht, weil `.tierrow` und `.bst` neu geschrieben werden (gemessen).

### Entfernen (`.line-x`, `sheetHTML()`, `ausRowsHTML()`, `screenRefKasse()`, Anfrage-Blatt, Ausstattung, Kasse)
Kreuz zum Entfernen einer Position.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 30 x 30 px, `--radius-s`, Icon `--sf-ink` (gemessen): `.line-x{color:var(--sf-text-2)}` verliert gegen `.screen button` |
| In `.arow` | Ausstattung | 26 x 26 px, `margin-top:-2px` |
| Hover | Zeiger | `--sf-surface-2`, Icon `--sf-ink` |
| Fokus | Tastatur | Ring |

Tokens: `--radius-s`, `--sf-surface-2`, `--sf-ink`. Maße fester Wert, kein Token. Trefferfläche `::after`, `inset:-8px`.

Handy: gleich.

Desktop: gleich.

Bewegung: keine, Hover springt.

### Summe (`.sum`, `sheetHTML()`, `screenRefKasse()`, Anfrage-Blatt, Kasse)
Summenzeile mit großer Rate, darunter meist die Bruttozeile als `.micro`.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Linie oben, `padding-top:var(--sf-space-4)`, Betrag 28/32 px, 300, `--sf-accent-strong`, tabellarisch |
| Ohne Linie | Kasse Schritt 3, Inline `border-top:0` | Keine Linie |

Tokens: `--sf-border`, `--sf-space-2`, `--sf-space-4`, `--sf-accent-strong`, `--sf-text-small`. 28/32 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine. Tabular numbers.

### Positionsbild (`.line-thumb`, `sheetHTML()`, `screenRefKasse()`, Anfrage-Blatt, Kasse)
Kleines Quadrat mit Gerätebild in Positionszeilen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 64 px, 1:1, `--sf-surface-2`, `--sf-radius-sm`, Bild 86 % |
| Ohne Bild | `fam` fehlt, etwa Baustein-Position in der Anfrage | `.mock` |

Tokens: `--sf-surface-2`, `--sf-radius-sm`. 64 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Positionszeile (`.aus-rows`, `.arow`, `.rt`, `ausRowsHTML()`, Ausstattung, Anfrage-Blatt, Kasse)
Kompakte Liste aus Gerät und Bausteinen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 14 px, `padding:11px 0`, Linie oben außer erste Zeile, Titel 600, Unterzeile 12 px `--sf-text-2`, Betrag tabellarisch |
| Entfernbar | `removable` wahr, Summenleiste und Positionsblatt | Mit `.line-x` |
| Nur Anzeige | Abschluss Anfrage und Kasse | Ohne `.line-x` |
| Mit Paketinhalt | `ctx.zub` | Je Teil eine Zeile „inkl. ...“ |
| Mit Menge | Menge größer 1 | „Menge n“ in der Unterzeile |

Tokens: `--sf-border`, `--sf-text-small`, `--sf-text-micro`, `--sf-text-2`. `padding`, `gap:10px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine. Tabular numbers.

### Leerzustand (`.empty`, `sheetHTML()`, `screenRefKat()`, Anfrage-Blatt, Geprüfte Geräte Katalog)
Mittiger Hinweis mit einem Knopf.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Leer, Anfrage | Korb ohne Positionen | „Noch nichts drin“, Text, `.btn.ghost` „Geräte ansehen“, kein Blattfuß |
| Leer, Katalog | Bestand „alles vergriffen“ | „Gerade sind alle Geräte im Einsatz“, Text mit Rate ab `abFrom()`, `.btn.primary` „Neugerät konfigurieren“ |

Tokens: keine eigenen. `padding:clamp(40px,8cqw,80px) 0` fester Wert, kein Token.

Handy: gleich, Abstand über `cqw`.

Desktop: gleich, Abstand über `cqw`.

Bewegung: keine.

### Abschluss (`.done`, `.done-heart`, `.done-id`, `sheetHTML()`, `screenRefKasse()`, Anfrage-Blatt, Kasse)
Bestätigung nach Anfrage oder Zahlung.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Anfrage gesendet | `state.aqStep` 3 | Herz, „Anfrage gesendet“, „Ihre Anfrage-ID“, feste Platzhalter-ID, Text, Positionen aus `state.lastOrder` |
| Abo aktiv | `state.kaStep` 4 | Herz, „Abo aktiv, vielen Dank“, „Ihre Abo-Nummer“, feste Platzhalter-ID, Text, Positionen |
| Zahlung abgebrochen | `state.kaStep` 5 | Ohne Herz, „Zahlung abgebrochen“, siehe Kasse |

Tokens: `--sf-space-5`, `--sf-ink` (Inline an `.done-id`). Herz 64 x 57 px, `padding:clamp(30px,6cqw,60px) 0` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Enter mit Translate über `data-rev`: `revUp`, .7s, `--sf-ease`, Verzögerung 0. Das Herz trägt `.go`, `beat` läuft mit Dauer 0s, also ohne sichtbare Wirkung.

### Inklusivliste (`.incl`, `inclList()`, Konfigurator, Geprüftes Gerät)
Vier Leistungen plus Schlusszeile.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Punkt 9 x 9 px in `--marker` statt Haken (`svg` aus), `--ink`, 14 px, `padding:13px 0`, Linie oben `--line` |
| Schlusszeile | `.last` | Ohne Punkt, 600, `--heading` |

Tokens: `--marker`, `--radius-pill`, `--ink`, `--line`, `--heading`, `--sf-text-small`. 9 px, 13 px, `gap:12px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Konditionszeile (`.cond`, `screenRefProd()`, `screenAusstattung()`, Ausstattung, Geprüftes Gerät)
Eingerahmte Textzeile für Mindestlaufzeit, Vergriffen-Text und Rückrichtung.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Linie oben und unten, `padding:16px 0`, 14 px, `--sf-text-2`, `b` 600 `--sf-ink` |
| Variante | Inline `border-bottom:0` oder `border-top:0;padding-bottom:0` | Eine Linie weniger |

Tokens: `--sf-border`, `--sf-text-small`, `--sf-text-2`, `--sf-ink`. 16 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Gruppe (`.grp`, `.grp-h`, `.now`, `screenKonfig()`, `screenRefProd()`, Konfigurator, Geprüftes Gerät)
Auswahlblock mit Kopfzeile links und aktuellem Wert rechts.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `padding:var(--sf-space-5) 0`, Linie oben, erstes Vorkommen ohne Linie. `.now` 14 px, 600 |
| Wert | `recompute()` schreibt `[data-now]` | Text wechselt ohne Bewegung |

Tokens: `--sf-space-5`, `--sf-space-4`, `--sf-border`, `--sf-text-small`. `gap:14px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Bühne (`.kfg`, `.kstage-wrap`, `.kstage`, `.tilt`, `.kstage-cap`, `initScreen()`, Konfigurator, Geprüftes Gerät)
Zweispalter mit Gerätebild links, das auf den Zeiger reagiert.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `.kstage` 1:1, `--surface-raised`, kein Verlauf, `--sf-radius` (gemessen `background-image:none`) |
| Neigung | Zeiger über `[data-stage]`, nur `(pointer:fine)` und ohne `REDUCE` | `.tilt` `rotateY(x*7deg) rotateX(-y*5deg)`, `x` und `y` von -.5 bis .5 |
| Verlassen | `pointerleave` | Inline-`transform` leer, Rückkehr über die Transition |
| Farbe gewechselt | `recompute()`, `data-stageimg` | `pimg()` schreibt das Bild neu. Beide Farben zeigen dasselbe Referenzbild, solange `IMAGES.live` falsch ist |
| Laden, Fehler | Bildfehler | `src` wechselt auf `surface-pro-freisteller.png`, ohne Zwischenzustand |

Tokens: `--surface-raised`, `--sf-radius`, `--sf-text-small`, `--sf-text-2`, `--sf-ink`, `--sf-space-5`, `--sf-space-6`, `--sf-ease`. `perspective:1100px`, `top:96px`, Spaltenmaße fester Wert, kein Token.

Handy: unter 860 px 1 Spalte, `gap:var(--sf-space-6)`, `.kstage-wrap` statisch.

Desktop: ab 860 px `1.02fr .98fr`, `gap:clamp(32px,5cqw,80px)`, `.kstage-wrap` `position:sticky`, `top:96px` (gemessen).

Bewegung: 3D tilt / Flip mit Perspective, `transform` an `.tilt`, .35s, `--sf-ease`, Verzögerung 0 (gemessen). `.kstage` hat `transition:background .6s`, `.kstage img` `transform .5s`, `opacity .4s`, beide ohne Auslöser im Surface-Zweig.

### Ratenband (`.band`, `.band-in`, `.band-break`, `screenKonfig()`, `screenRefProd()`, Konfigurator, Geprüftes Gerät)
Klebende Leiste unten mit Rate, Aufschlüsselung und Hauptknopf.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `--surface`, Linie oben, kein Blur, `position:sticky`, `bottom:0`, `z-index:15` |
| Geändert | `pushRate(..., true)` setzt `.flash`, nur Konfigurator | Linie oben wechselt von `--brand` zurück auf `--line` |
| Geprüftes Gerät | `screenRefProd()` | Statische Summe, kein `.rate-live`, kein `.flash`, „Abo starten“, Hinweis „Zubehör und Lizenzen wählen Sie im nächsten Schritt“ |
| Vergriffen | Bestand 0 auf der Produktseite | Band entfällt |
| Aufschlüsselung | `[data-brk-dev]`, `[data-brk-add]`, `[data-brk-gross]` | „Gerät x €“, leer für Zubehör (keine `data-ad`-Zeile im Render), Brutto |

Tokens: `--surface`, `--sf-border`, `--brand`, `--line`, `--sf-gutter`, `--sf-container`, `--sf-text-micro`, `--sf-text-2`, `--sf-ink`, `--sf-ease`. `padding:14px` plus `env(safe-area-inset-bottom)`, `gap:18px` fester Wert, kein Token.

Handy: `.band-in` mit `flex-wrap:wrap`, Knopf per `margin-left:auto`. Rate gemessen 28 px.

Desktop: Rate gemessen 44 px, `.band-in` bis `calc(var(--sf-container) - 2*var(--sf-gutter))`.

Bewegung: Pulse, Näherung: `slBandFlash`, `border-top-color`, .6s, `--sf-ease`, Verzögerung 0 (gemessen).

### Rate im Band (`.band-num`, `.rate-live`, `pushRate()`, `animateRate()`, Konfigurator, Ausstattung, Geprüftes Gerät)
Große Monatsrate mit Einheit.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Betrag `clamp(28px,3.4cqw,44px)!important`, 300, `--sf-accent-strong`, tabellarisch, Einheit 14 px `--sf-text-2` |
| Zählt | Wert ändert sich, auch beim Laden des Konfigurators von 0 an | Zahlen laufen zum Zielwert |
| Pulst | `pushRate()` mit `flash` wahr und geändertem Wert | Betrag skaliert kurz |
| Inline-Größe | `.aus-bar` setzt `font-size:1.55rem` | Wirkt nicht, `!important` gewinnt, gemessen 28 px |

Tokens: `--sf-accent-strong`, `--sf-text-small`, `--sf-text-2`. `clamp` fester Wert, kein Token.

Handy: gemessen 28 px.

Desktop: gemessen 44 px.

Bewegung: Number ticker mit Tabular numbers, Text per `requestAnimationFrame`, 420 ms, Ease-out `1-(1-p)^3`, Verzögerung 0. Pulse, Näherung: `ratepulse`, `transform`, .42s, Überschwingkurve, Verzögerung 0 (gemessen).

### Dialog (`.dlg`, `.dlg-in`, `altDlg()`, `screenRefKasse()`, `screenAusstattung()`, `zubSheet()`, `placeSheet()`, Anfrage-Blatt, Kasse, Ausstattung, Geprüftes Gerät)
Modale Ebene mit Scrim, Inhalt je Seite als eigener Baustein.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Offen | Zustand wahr, `data-dlgpos` | `absolute`, `top` und `height` aus `scrollTop` und `clientHeight`, `--scrim`, `z-index:44`, `.dlg-in` `--sf-surface`, ohne Schatten, `max-width:520px` |
| Fokus | | Knöpfe mit Ring, Fokussteuerung im Prototyp nicht gezeichnet |
| Escape | | im Prototyp nicht gezeichnet |
| Seite dahinter | | Bleibt scrollbar, nur `.sheetopen` sperrt |

Tokens: `--scrim`, `--sf-surface`, `--sf-radius`. `padding:24px`, `clamp(24px,4cqw,36px)`, `max-width:520px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Enter mit Translate: `dlgIn`, `transform`, .3s, `--sf-ease`, Verzögerung 0 (gemessen).

### Griff (`.grip`, `data-grip`, `shDragEnd()`, Ausstattung, Geprüftes Gerät)
Ziehleiste oben am Unterblatt.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Balken 44 x 5 px, `--sf-border-strong`, `--radius-none`, `cursor:grab`, `touch-action:none`, `aria-hidden` |
| Ziehen | `pointerdown` am Griff | Blatt folgt dem Zeiger nach unten, nach oben begrenzt auf 0. `.dlg` Inline `rgba(12,14,17, .42*(1-dy/h))`, fester Wert, kein Token (gemessen) |
| Loslassen, weit | Weg über 30 % der Höhe oder Tempo über .6 px/ms | Blatt fährt um Höhe plus 24 px raus, Scrim auf 0, nach 260 ms geschlossen (gemessen) |
| Loslassen, kurz | sonst | Blatt federt auf 0, Scrim wieder `--scrim` (gemessen) |
| Fassen während Rückfedern | `pointerdown` | Aktueller Versatz wird aus `DOMMatrixReadOnly` übernommen |
| Ab 760 px im Zubehörblatt | Container-Regel | `display:none` |

Tokens: `--sf-border-strong`, `--radius-none`, `--sf-dur-2`, `--sf-ease`, `--scrim`. Balkenmaße und Schwellen fester Wert, kein Token.

Handy: sichtbar.

Desktop: im Positionsblatt sichtbar, dieses öffnet nur unter 900 px. Im Zubehörblatt ab 760 px aus.

Bewegung: Drag, `transform`, ohne Transition, will-change nur während des Ziehens. Swipe to dismiss, `transform`, 260 ms, `--sf-ease`, Verzögerung 0. Rückfedern Bounce, Näherung, `transform`, .45s, Überschwingkurve, Verzögerung 0. Interruptible animation beim erneuten Fassen.

### Medienslot (`.vslot`, `.vposter`, `vslot()`, `slVideo()`, `slMotiv()`, `observeMedia()`, Startseite, Geräte)
Einheitlicher Rahmen für Film, Poster oder Motiv.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Video läuft | Sichtbar ab 15 %, `IntersectionObserver`, im Akkordeon nur `.acc-layer.on` | `video` `muted loop playsinline`, `object-fit:cover` |
| Video pausiert | Außerhalb des Bildes, oder `data-up` durch den Nutzer | Standbild |
| Poster | `REDUCE` oder `OFFLINE` | `img.vposter` |
| Motiv | `slMotiv()` | `img.vposter` plus `.tag` |
| Fehler | `error` an `video` oder `img` im Slot, `initScreen()` | Inhalt wird `.slot-leer` plus `.tag` „Bildslot: eigenes Material folgt“ |
| Laden | `preload="metadata"` | im Prototyp nicht gezeichnet |

Tokens: `--surface-deep` (in `.sl-hf`). Sonst `background:#0E1116`, fester Wert, kein Token.

Handy: Hero mit eigener Video-Datei, siehe Breakpoints.

Desktop: gleich.

Bewegung: Loop des Videos, keine CSS-Bewegung.

### Videoknopf (`.vctl`, `slVctl()`, Startseite)
Hält das Hero-Video an und startet es wieder.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Spielt | Standard | 44 x 44 px, `--radius-s`, Rand `--on-deep`, `--scrim`, Pause-Icon `.ic-pause` |
| Pausiert | Klick, `.paused`, setzt `data-up` am Video | Play-Icon `.ic-play`, `aria-label` bleibt „Video anhalten“ |
| Hover | Zeiger | `--surface-deep` |
| Fokus | Tastatur | Ring |
| Reduced Motion | `REDUCE` oder `OFFLINE` | Knopf entfällt |

Tokens: `--radius-s`, `--on-deep`, `--scrim`, `--surface-deep`. 44 px, `top:18px`, `right:18px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine, Hover springt.

### Produktbild (`.dev-field img`, `.type-field img`, `.kstage img`, `.line-thumb img`, `pimg()`, `imgModel()`, `IMAGES`, Fehler-Listener am `document`, Startseite, Geräte, Konfigurator, Anfrage-Blatt, Geprüfte Geräte Katalog, Geprüftes Gerät, Kasse)
Bildslot mit `srcset` aus dem Manifest.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Platzhalter, Referenz | `IMAGES.live` falsch, heutiger Stand | `img` mit `m.ref` plus `.tag` „Referenz Microsoft, Feed-Bild folgt“ |
| Live | `IMAGES.live` wahr | `srcset` aus `IMG_W`, `sizes` aus `SZ`, WebP |
| Ohne Modell | `OFFLINE` oder keine MSKU | `.mock` |
| Laden | `fetchpriority="high"` oder `loading="lazy"`, `decoding="async"` | im Prototyp nicht gezeichnet |
| Fehler | `error` in `.dev-field`, `.type-field`, `.kstage`, `.line-thumb` | `src` wird `surface-pro-freisteller.png`, einmalig über `data-lokal` |
| Randlos | `src` enthält `Produkt/` in `.dev-field`, `.type-field`, `.kstage` | 100 % x 100 %, `object-fit:cover` |

Tokens: keine, Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine eigene, siehe Träger.

### Bildersatz (`.scene`, `.sc-team`, `.sc-focus`, `.sc-detail`, `.mock`, `.slot-leer`, `scene()`, `mock()`, `slotArt()`, Geräte, Startseite, Geprüftes Gerät)
Motive aus der Bildwelt, wo kein eigenes Material vorliegt. Fehlt ein Medium, steht eine ruhige Fläche mit Etikett. Es gibt keine gezeichnete Szene und keine Verläufe mehr (B2).

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| `.scene` | Standard | `--surface-sand` plus `Bildwelt/surface-go-kontext.jpg`, `28% 40%/cover` |
| `.sc-team` | `scene("team")` | Position `88% 22%`, Größe 190 % |
| `.sc-focus` | `scene("focus")` | Position `52% 62%`, Größe 150 % |
| `.sc-detail` | `scene("detail")` | `--surface-raised` plus `surface-pro-freisteller.png`, zentriert, `contain` |
| Drittes Use-Case-Motiv | `.ucard:nth-child(3) .scene`, auch `.mood .scene` | `surface-stift-dunkel.jpg`, `60% 50%`, `cover` |
| `.mock` | `mock()` | 88 % breit, 16:9, `surface-pro-freisteller.png`, `contain` |
| Slot ohne Kurationsmotiv | `slotArt()`, Quelle immer `null` | `.scene` plus `.tag` „..., Slot leer“ |
| Medium fehlt oder lädt nicht | `error` an `video` oder `img`, Film bei reduzierter Bewegung ohne Standbild | `.slot-leer`, flach `--surface-raised`, `.tag` „Bildslot: eigenes Material folgt“ oder „Videoslot: eigenes Material folgt“ |

Tokens: `--surface-sand`, `--surface-raised`. Bildpositionen fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Refurbished-Band (`.refslot`, `.refband`, `refBand()`, Startseite, Geräte)
Einziger Hinweis auf geprüfte Geräte auf diesen Seiten.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe, Bestand vorhanden | `refAvail()` nicht leer | `--surface-sand`, `padding:20px 24px`, `.stat.ok` „Sofort verfügbar“, Text mit kleinster Rate aus `refMin()`, `.platzhalter`, `.lnk-ink` |
| Ohne Bestand | Schalter „alles vergriffen“ | Funktion liefert leer. Auf der Geräteseite bleibt `section.sect-tight` als Abstand |
| Bestand knapp, Einzelstücke, ein Typ vergriffen | Schalter | Rate neu aus den verfügbaren Typen, Aussehen gleich |
| `.refslot.off` | | Klasse wird nie gesetzt |

Tokens: `--surface-sand`, `--sf-radius`, `--sf-ink`, `--sf-text-small`. `padding`, `margin-top:clamp(20px,3cqw,34px)`, `min-width:15rem` fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: einzeilig.

Bewegung: keine. Accordion / Collapse über `grid-template-rows` 550 ms ist definiert und hat keinen Auslöser.

### Use-Case-Kachel (`.uc`, `.slim`, `.ucard`, `.ucard-in`, `.ucard-go`, `screenStartSurface()`, `useCases()`, Startseite, Geräte)
Situation als Bildkarte, führt mit Vorbelegung in den Konfigurator.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe, Startseite | `.uc` | 4:5, `slMotiv()` plus `.tag`, Plakette `linear-gradient` nach oben, Titel 18/26 px, 600, `--on-deep` |
| Ruhe, Geräte | `.uc.slim` | 3:2 (gemessen), `slotArt()` mit Bildersatz |
| Hover | Zeiger | Pfeil in „Passendes Gerät“ rückt 4 px |
| Aktiv | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Klick | `data-uc` | `state.fami`, `state.presetSize`, Seite Konfigurator |
| Platzhalter | Motive | `.tag`, Abschnitt mit `.platzhalter` „Platzhalter-Motive“ |

Tokens: `--on-deep`, `--sf-radius`, `--sf-text-micro`, `--space-12`, `--sf-dur-1`, `--sf-ease`. Verlauf `Token `schleier``, `b` 18/26 px, Sperrung -.01em, `padding:48px 20px 22px` fester Wert, kein Token. `.ucard:first-child .vposter` `scale(1.02)` fest.

Handy: unter 620 px 1 Spalte, ab 620 px 2 Spalten.

Desktop: ab 900 px 4 Spalten, `gap:clamp(12px,1.8cqw,20px)`.

Bewegung: Hover effect mit Translate, `transform` translateX(4px) am `svg`, 150 ms, `--sf-ease`, Verzögerung 0 (gemessen). `--d` ist gesetzt und wirkt nicht, das Element trägt kein `data-rev`.

## Startseite

Reihenfolge in `screenStartSurface()`: Kopf, Hero, Ratenband, Kampagne, Geräte, Use Cases, Vorteile, Können, Mood, Modern Workplace, Community, Inspiration, Zitat, Band Versprechen, Fuß.

### Hero (`.sl-hf`, `.sl-hf-hero`, `.sl-hf-a`, `.sl-hf-in`, `.sl-veil`, `.hero-cta`, `screenStartSurface()`, Startseite)
Film über die ganze Breite mit blauem Verlauf, Kernsatz und zwei Knöpfen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `display:flex`, `align-items:flex-end`, Grund `--surface-deep`, Film absolut, `.sl-veil` darüber, Text `--on-deep`, Eyebrow `--on-deep-accent` |
| Video pausiert | `.vctl` | Standbild, siehe Videoknopf |
| Reduced Motion | `REDUCE` | Nur Poster, kein `.vctl` |
| Bildfehler | `error` | `scene()` plus `.tag`, siehe Medienslot |
| Knöpfe | „Gerät wählen“, `.btn.primary`. „So funktioniert es“, `.btn.ghostw` | Beide führen auf `geraete` |

Tokens: `--surface-deep`, `--on-deep`, `--on-deep-accent`, `--space-3`, `--space-4`, `--space-6`, `--space-12`, `--sf-text-display`. `min-height:clamp(520px,47cqw,800px)`, `.lead` `max-width:50ch`, `.hero-cta` `gap:12px`, Verlauf `Token `schleier`` fester Wert, kein Token.

Handy: gemessen `min-height:520px`, Display 44 px. Verlauf `180deg, schleier 10 % 0%, schleier 60 % 28%, schleier 92 % 100%`. Video `surface-business-hero-mobil.mp4`, wenn `state.view` mobil oder Fenster unter 700 px.

Desktop: gemessen `min-height:657px` bei 1398 px, Display 64 px. Verlauf `180deg, schleier 0 % 18%, schleier 55 % 52%, schleier 90 % 100%`.

Bewegung: Loop des Videos, `autoplay`. Sonst keine, `.display`, `.lead` tragen kein `.fx` und kein `data-rev`.

### Hero-Ratenband (`.sl-rateband`, `.sl-rateband-in`, `.sl-rb-rate`, `.sl-rb-fig`, `.sl-rb-u`, `.sl-rb-facts`, `screenStartSurface()`, Startseite)
Blaues Band direkt unter dem Hero mit kleinster Rate, drei Fakten und Reseller-Logo.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `abFrom(b.fams[1])` | Fläche `--surface-brand`, Zahl 44/48 px, 300, `--on-brand-display`, Einheit und Fakten 14/20 px `--on-brand`, Punkt 6 x 6 px `--on-brand` |

Tokens: `--surface-brand`, `--on-brand`, `--on-brand-display`, `--radius-pill`, `--space-1`, `--space-2`, `--space-3`, `--space-4`, `--space-5`, `--space-6`, `--space-12`. 44/48 px, 14/20 px, 6 px fester Wert, kein Token.

Handy: unter 900 px 1 Spalte, Blöcke untereinander.

Desktop: ab 900 px `auto 1fr auto`, `align-items:baseline`, Logo `align-self:center` (gemessen 3 Spalten).

Bewegung: keine.

### Kampagne (`.b2`, `.b2-in`, `.hl-l`, `.hl-s`, `screenStartSurface()`, Startseite)
Großes Motiv mit englischer Kopfzeile, deutscher Subzeile und Link.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `b.slots.buehne2` | Motiv `Motive/buehne.jpg`, `.sl-veil` z 2, Text z 3 in `--on-deep`, `.h1` `max-width:24ch`, `.lead` `max-width:50ch` |
| Link Hover | `.lnk.onw` | Pfeil rückt 4 px |
| Platzhalter | Motiv und Link-Ziel | `.tag` „Kampagnenmotiv, Platzhalter“, `.platzhalter` „Link-Ziel Platzhalter“. Link führt im Prototyp auf `geraete` |

Tokens: `--on-deep`, `--sf-radius`, `--space-2`, `--space-8`. `min-height:clamp(320px,38cqw,500px)`, Verlauf `Token `schleier``, `object-position:50% 22%` fester Wert, kein Token.

Handy: bis 760 px `padding-top:200px` und Verlauf `180deg, schleier 0 % 12%, schleier 78 % 40%, schleier 94 % 100%`. Bis 560 px Kurzzeile `.hl-s` statt `.hl-l`. Gemessen `min-height:320px`.

Desktop: Verlauf `180deg, schleier 0 % 18%, schleier 72 % 50%, schleier 94 % 100%`. Gemessen `min-height:500px`, `padding:32px`.

Bewegung: keine.

### Gerätebahn (`.bahn`, `screenStartSurface()`, Startseite)
Drei Gerätekarten nebeneinander, auf dem Handy als Snap-Karussell.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `grid`, `gap:clamp(14px,2cqw,28px)` |
| Wischen | Handy, nativ | `scroll-snap-type:x mandatory`, Scrollleiste aus |

Tokens: keine, Maße fester Wert, kein Token.

Handy: unter 860 px `grid-auto-columns:min(78%,420px)`, `overflow-x:auto` (gemessen 259 px je Karte bei 372).

Desktop: ab 860 px `grid-auto-columns:1fr`, `overflow:visible` (gemessen 3 Spalten je 368 px).

Bewegung: keine, Snap ist nativ.

### Gerätekarte (`.dev`, `.dev-field`, `.dev-name`, `.dev-claim`, `.dev-meta`, `.dev-rate`, `.dev-go`, `devCard()`, Startseite)
Karte je Gerätereihe, führt in den Konfigurator.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Feld 4:3.4, `--surface-raised`. Name 24/32 px, 400. Rate 28/32 px, 300, `--sf-accent-strong`, `small` `--ink-muted`. Pfeilfeld 38 x 38 px, `--radius-s`, Rand `--control-border` |
| Hover | Zeiger | Bild `translateY(-8px) scale(1.03)`. `.dev-go` Fläche und Rand `--sf-ink`, Pfeil `--sf-surface`, `translateX(3px)` |
| Aktiv | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Klick | `data-fam` | `state.fami`, Seite Konfigurator |
| Platzhalter | `pimg()` | `.tag` unten links |

Tokens: `--surface-raised`, `--sf-radius`, `--sf-text-small`, `--sf-text-2`, `--sf-text-micro`, `--ink-muted`, `--sf-accent-strong`, `--radius-s`, `--control-border`, `--sf-ink`, `--sf-surface`, `--sf-border`, `--sf-dur-1`, `--sf-dur-3`, `--sf-ease`. 24/32 px, 28/32 px, 38 px fester Wert, kein Token.

Handy: Breite aus `.bahn`.

Desktop: Breite aus `.bahn`.

Bewegung: Hover effect mit Translate und Scale, `transform` am Bild, 550 ms, `--sf-ease`, Verzögerung 0. Hover effect, `.dev-go` `background`, `border-color`, `transform`, 150 ms, `--sf-ease`, Verzögerung 0 (gemessen). Pfeilfarbe springt. `--d` ist gesetzt und wirkt nicht.

### Vorteile (`.vlist`, `.vrow`, `[data-screen-label="Vorteile"]`, `screenStartSurface()`, Startseite)
Vier nummerierte Vorteile auf Sand über die volle Breite.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Sand über `::before` mit `width:100cqw`, `z-index:-1`. Zeile Linie oben `--sand-300`, Marker 32 x 2 px `--marker`, Nummer `--ink-subtle`, `h3` 18 px, 600, `p` 14 px `--ink-muted` |
| Hover | Zeiger auf Zeile | Kinder rücken 8 px, Marker bleibt |

Tokens: `--surface-sand`, `--accent-text-sand`, `--sand-300`, `--marker`, `--border-rule`, `--ink-subtle`, `--ink-muted`, `--sf-text-h3`, `--sf-text-small`, `--sf-text-micro`, `--sf-dur-2`, `--sf-ease`. `padding:26px 0`, `gap:20px`, `max-width:44ch` fester Wert, kein Token.

Handy: unter 860 px 1 Spalte.

Desktop: ab 860 px `1fr 1fr`, `column-gap:clamp(32px,5cqw,72px)`.

Bewegung: Hover effect mit Translate, `transform` translateX(8px) an `.vrow>*`, 260 ms, `--sf-ease`, Verzögerung 0 (gemessen). `--d` ist gesetzt und wirkt nicht.

### Kontaktzeile (`.contactline`, `screenStartSurface()`, Startseite)
Satz plus Telefonlink am Ende der Vorteile.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Linie oben `--sand-300`, `padding-top:24px`, Text 14 px `--sf-ink`, `.phone-l` immer sichtbar |

Tokens: `--sand-300`, `--sf-ink`, `--sf-text-small`. `margin-top:clamp(20px,3cqw,32px)`, `min-width:15rem` fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: einzeilig.

Bewegung: keine, Telefonlink hier ohne `.ph-r`.

### Können-Akkordeon (`.acc`, `.acc-stage`, `.acc-layer`, `.acc-item`, `.acc-tx`, Klick-Handler `.acc-item`, Startseite)
Vier Fähigkeiten, je eine offen, Film wechselt mit.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `.acc-item` Linie oben, `padding:20px 0 20px 22px`, `b` 18 px, 600, Strich links 2 px `--sf-border` bei scaleY(.85) |
| Gewählt | `.on`, Standard Index 0 | Strich `--marker`, scaleY(1), Text 14 px in `--sf-ink` offen (gemessen, `.acc-item{color:var(--sf-text-2)}` verliert gegen `.screen button`), Schicht `.acc-layer.on` sichtbar, Video spielt |
| Hover | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Reduced Motion | `REDUCE` | Szene plus `.tag` „Videoslot: eigenes Material folgt“ in jeder Schicht (gemessen) |
| Schließen aller | | Nicht vorgesehen, Klick auf die offene Zeile ändert nichts |

Tokens: `--sf-border`, `--marker`, `--sf-ink`, `--sf-text-2`, `--sf-text-h3`, `--sf-text-small`, `--sf-radius`, `--sf-space-6`, `--sf-dur-2`, `--sf-ease`. `.acc-stage` 5:4, Maße fester Wert, kein Token.

Handy: unter 860 px 1 Spalte, `gap:var(--sf-space-6)`, Bühne über der Liste.

Desktop: ab 860 px `1.1fr .9fr`, `align-items:center`, `gap:clamp(40px,5cqw,80px)`.

Bewegung (alle gemessen, Quelle `.acc-item` Klick): Crossfade, `.acc-layer` `opacity`, .55s, `--sf-ease`, Verzögerung 0. Scale, `.acc-layer` `transform` scale(1.015) nach none, .9s, `--sf-ease`, Verzögerung 0. Accordion / Collapse, `.acc-tx` `grid-template-rows`, .45s, `--sf-ease`, Verzögerung 0. Fade in, Text `opacity`, .35s, `--sf-ease`, Verzögerung .1s, dazu `padding-top`, .45s, Verzögerung 0. Scale, Strich `transform` und `background`, 260 ms, `--sf-ease`, Verzögerung 0.

### Mood (`.mood`, `.mood-in`, `screenStartSurface()`, Startseite)
Film mit kurzem Satz, unten links.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `b.slots.mood` | Video `tastatur.mp4` ohne `.vctl`, spielt bei Sichtbarkeit. `.h1` und `.lead` in `--on-deep`, `.sl-veil` z 2 |
| Reduced Motion | `REDUCE` | Poster |
| Platzhalter | Text | `.platzhalter` „Platzhalter“ in der Subzeile |

Tokens: `--on-deep`, `--sf-text-h1`, `--space-2`, `--space-8`, `--sf-radius`. `min-height:clamp(320px,34cqw,460px)`, `.lead` 18/28 px. Verlauf aus `schleier`, `180deg, 0 % bei 30 %, 85 % bei 100 %`.

Handy: gemessen `min-height:320px`. Bis 760 px Verlauf `180deg, 0 % bei 0 %, 88 % bei 30 %, 96 % bei 100 %`, weil der Titel dort oben liegt. Kontrast Titel 11,71, Text 13,29.

Desktop: gemessen `min-height:460px`.

Bewegung: Loop des Videos.

### Modern Workplace (`.dark`, `.cyc`, `.cyc-step`, `.cyc-ic`, `screenStartSurface()`, Startseite)
Tiefe Fläche mit vier weißen Karten zum Lebenszyklus.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Fläche `--surface-deep`, Text `--on-deep`, `.lead` `--on-deep-muted`. Karte `--surface`, `padding:var(--space-6)`, `b` 18/26 px `--heading`, `p` 14/20 px `--ink-muted`, Icon 32 px hoch |

Tokens: `--surface-deep`, `--on-deep`, `--on-deep-muted`, `--on-deep-accent`, `--surface`, `--ink`, `--heading`, `--ink-muted`, `--space-4`, `--space-5`, `--space-6`. 18/26 px, 14/20 px, 32 px, `margin-top:clamp(32px,5cqw,64px)` fester Wert, kein Token.

Handy: unter 820 px 1 Spalte, `gap:var(--space-5)`.

Desktop: ab 820 px 4 Spalten.

Bewegung: keine.

### Community (`.thread`, `.thread-ico`, `screenStartSurface()`, Startseite)
Sonderfall: Community und Zitat auf der Startseite sind Platzhalter ohne Inhalt. Regel: im Shop nur ausspielen, wenn echte Daten vorliegen, sonst Abschnitt ausblenden (E-065).

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Platzhalter | `b.community`, heutiger Stand | `.platzhalter` „Platzhalter“, eckige Klammern in Überschrift, Beiträgen und `.micro` „[Link zur Community]“ |
| Ruhe, Zeile | | Linie oben, `padding:20px 4px`, Icon `--icon`, Titel 16 px, 600 und per Vererbung `--sf-text-2` (gemessen), Metazeile 12 px |
| Hover | Zeiger auf Zeile | Alle Kinder rücken 12 px |
| Fokus | Tastatur | Ring |
| Klick | | Kein Handler |
| Leer, keine Beiträge | | im Prototyp nicht gezeichnet |

Tokens: `--sf-border`, `--icon`, `--sf-text-body`, `--sf-text-micro`, `--sf-text-2`, `--sf-dur-2`, `--sf-ease`. Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Hover effect mit Translate, `transform` translateX(12px) an `.thread>*`, 260 ms, `--sf-ease`, Verzögerung 0 (gemessen).

### Inspiration (`.insp`, `.icard`, `.icard-media`, `[data-screen-label="Inspiration"]`, `screenStartSurface()`, Startseite)
Drei Redaktionskarten auf Sand.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Bild 3:2, `.kick` in `--accent-text-sand` (gemessen), Titel 18 px, 600, Text 14 px |
| Hover | Zeiger | Titel unterstrichen, Abstand 3 px |
| Fokus | Tastatur | Ring |
| Klick | `data-ziel` | Kein Handler |
| Platzhalter | Motive und Ziele | `.tag` „Redaktionsmotiv, Platzhalter“, `.platzhalter` „Platzhalter: Motive und Link-Ziele“ |

Tokens: `--surface-sand`, `--accent-text-sand`, `--sf-radius`, `--sf-text-h3`, `--sf-text-small`, `--sf-text-2`. `gap:clamp(14px,2cqw,22px)` fester Wert, kein Token.

Handy: unter 760 px 1 Spalte.

Desktop: ab 760 px 3 Spalten.

Bewegung: keine, Unterstreichung springt. `--d` ist gesetzt und wirkt nicht.

### Zitat (`.sl-zitat`, `screenStartSurface()`, Startseite)
Sonderfall: Community und Zitat auf der Startseite sind Platzhalter ohne Inhalt. Regel: im Shop nur ausspielen, wenn echte Daten vorliegen, sonst Abschnitt ausblenden (E-065).

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Platzhalter | `b.stories[0]`, heutiger Stand | `.h1` mit Text in eckigen Klammern, `.small` mit Angaben in eckigen Klammern, `.platzhalter` „Platzhalter“ |
| Leer | | im Prototyp nicht gezeichnet |

Tokens: `--sf-text-h1`, `--sf-text-small`, `--sf-text-2`. `max-width:760px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

## Geräte

Reihenfolge in `screenGeraete()`: Kopf, Seitenkopf, Punktnavigation und drei Blätter, Vergleich, Use-Case-Kachel `.uc.slim`, Service, Refurbished-Band, Band Versprechen, Fuß.

### Seitenkopf Geräte (`.sheets`, `screenGeraete()`, Geräte)
Einleitung über den Blättern.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `.lbl`, `h1.display` mit Inline `font-size:var(--sf-text-h1)`, `.lead` |
| Scroll Snap | `.sheets{scroll-snap-type:y proximity}`, `.leaf{scroll-snap-align:start}` | Keine Wirkung: `.sheets` scrollt nicht, `.screen` hat keinen Snap (gemessen) |

Tokens: `--sf-text-h1`. `padding:clamp(32px,5cqw,64px) 0 8px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Enter mit Translate, `revUp` über `data-rev` an der `h1`, `transform`, .7s, `--sf-ease`, Verzögerung 0 (gemessen).

### Geräteblatt (`.leaf`, `.leaf-facts`, `.leaf-fact`, `screenGeraete()`, Geräte)
Ein Blatt je Gerätereihe mit Bild, Fakten und Knopf.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `data-leaf` | Linie oben, Bild im `.dev-field`, `.lbl` „0n, Claim“, Faktenzeilen 14 px, Rate inline in `--sf-accent-strong` |
| Knopf | Index 0 `.btn.primary`, sonst `.btn.ghost` | „Konfigurieren“, `data-fam` |
| Platzhalter | `pimg()` Ansicht `three-quarter` | `.tag` unten links |

Tokens: `--sf-border`, `--sf-space-5`, `--sf-space-6`, `--sf-text-h1`, `--sf-text-small`, `--sf-text-2`, `--sf-accent-strong`. `min-height:clamp(560px,74cqw,760px)`, `padding:clamp(40px,6cqw,72px) 0` fester Wert, kein Token.

Handy: unter 840 px 1 Spalte, gemessen `min-height:560px`.

Desktop: ab 840 px `1.06fr .94fr`, `gap:clamp(36px,6cqw,90px)`, gemessen `min-height:760px`.

Bewegung: keine, `--d` ist gesetzt und wirkt nicht. Die Hover-Regel für das Bild hängt an `.dev:hover`, hier nicht aktiv.

### Punktnavigation (`.dots`, `pass()`, `data-dot`, Geräte)
Zeigt und wählt das sichtbare Blatt.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 9 x 9 px, `--radius-s`, Rand `--sf-border-strong` |
| Gewählt | `pass()` beim Scrollen, Oberkante über Schirmmitte | `--sf-ink`, `scale(1.3)` |
| Hover | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Klick | `data-dot` | `scrollTo` auf das Blatt minus 60 px |
| Trefferfläche | `::after`, `inset:-18px` bei 19 px Raster | Die Flächen überlappen, der spätere Punkt liegt oben. Klick auf die Mitte von Punkt 2 trifft Punkt 3 (gemessen) |

Tokens: `--radius-s`, `--sf-border-strong`, `--sf-ink`, `--sf-dur-1`, `--sf-ease`. Maße fester Wert, kein Token.

Handy: unter 840 px `display:none`.

Desktop: ab 840 px `display:flex`, `position:sticky`, `top:50%`, `float:right`, `gap:10px`.

Bewegung: Scale, `transform` und `background`, 150 ms, `--sf-ease`, Verzögerung 0. Scrollen: Translate, Näherung, natives `behavior:"smooth"`, Dauer und Kurve vom Browser.

### Vergleich (`.cmpwrap`, `.cmp`, `.cmp-c`, `.hd`, `.rate`, `screenGeraete()`, Geräte)
Drei Geräte nebeneinander in vier Zeilen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Kopfzelle 18/26 px, 600, `--heading`, unten 2 px `--line-strong`. Zelle 14 px, `padding:16px 14px`, Linie oben. `.lbl` 14/20 px, 400 |
| Rate | `.rate` | `--sf-accent-strong`, 400, tabellarisch |
| Überlauf | Schirm schmaler als `.cmp` | `.cmpwrap` scrollt horizontal, schmale Scrollleiste |

Tokens: `--heading`, `--line-strong`, `--border-rule`, `--sf-border`, `--sf-accent-strong`, `--sf-text-small`, `--ink-muted`. Spalten `minmax(96px,150px) repeat(3,minmax(130px,1fr))`, `min-width:600px` fester Wert, kein Token.

Handy: gemessen 4 Spalten je 150 px, 600 px breit, scrollbar.

Desktop: gemessen 150 px plus 3 x 337 px.

Bewegung: keine.

### Service (`.split`, `.split-media`, `screenGeraete()`, Geräte)
Bild und Text nebeneinander.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Bild 4:3, `.lbl`, `.h1`, `.lead`, `.lnk` „Gerät konfigurieren“ |
| Platzhalter | `slotArt()` | `.scene.sc-team` plus `.tag` „Kampagnenmotiv, Platzhalter, Slot leer“ |

Tokens: `--sf-radius`, `--sf-space-6`. `gap:clamp(40px,6cqw,88px)` fester Wert, kein Token.

Handy: unter 860 px 1 Spalte.

Desktop: ab 860 px `1fr 1fr`.

Bewegung: keine, `--d` ist gesetzt und wirkt nicht.

## Konfigurator

Reihenfolge in `screenKonfig()`: Kopf, Rücklink, Familienschalter, Bühne, Größe, Farbe, Leistung, Laufzeit, Menge, Inklusivliste mit Hinweis geprüfte Geräte, Ratenband, Band Versprechen, Fuß. Zustand liegt in den `data-*` von `.cfg`, `recompute()` schreibt Texte und Klassen.

### Familienschalter (`.famswitch`, `.ink`, `syncInk()`, `screenKonfig()`, Konfigurator)
Wechselt zwischen den drei Gerätereihen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 16 px, 600, `--sf-text-2`, `padding:16px 0 18px`, `gap:26px`, Linie unten |
| Gewählt | `.on` | `--sf-ink`, Tinte 2 px `--sf-ink` |
| Hover | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Überlauf | Schmaler Schirm | `overflow-x:auto`, Scrollleiste aus |
| Vorbelegt | `state.presetSize` aus Use Case oder Rückrichtung | Größe vorgewählt |

Tokens: `--sf-text-body`, `--sf-text-2`, `--sf-ink`, `--sf-border`, `--sf-space-5`, `--sf-dur-1`, `--sf-dur-3`, `--sf-ease`. Maße fester Wert, kein Token.

Handy: gleich, scrollt bei Bedarf.

Desktop: gleich.

Bewegung: Layout animation, `.ink` `transform`, 550 ms, `--sf-ease`, Verzögerung 0. Klick schreibt die Seite neu (`render()`), die Tinte läuft daher bei jedem Rendern von links ein, die Breite springt (gemessen).

### Größe (`.rail`, `.rail-item`, `recompute()`, `screenKonfig()`, Konfigurator)
Größenwahl mit Preisdelta.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `b` `clamp(1.1rem,1.6cqw,1.375rem)`, 600, `--sf-text-2`. Unterzeile `.s` und Delta `.d` 12 px in `--sf-ink` (gemessen): `.rail-item{color:var(--sf-text-2)}` verliert gegen `.screen button` |
| Gewählt | `.on`, `data-opt="size"` | `b` `--sf-ink`, `.d` 600 „gewählt“, Tinte darunter |
| Delta | `dfmt()` | „plus 10,00 €“, „minus ...“, „inklusive“ |
| Größe in dieser Stufe nicht lieferbar | `f.rates[size][tier]` leer | Statt Delta „in dieser Stufe nicht lieferbar“, die Größe bleibt wählbar, die Stufe springt auf die nächste lieferbare |
| Hover | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring |
| Eine Größe | `f.sizes.length` ist 1 | Keine Leiste, `.small` „Dieses Gerät gibt es in einer Größe.“, `.now` fest |
| „Empfohlen“ | `s.sub` in `.s`, kuratiert | Text, nur aus Kurationsdaten (E-065) |

Tokens: `--sf-text-2`, `--sf-ink`, `--sf-text-micro`, `--sf-border`, `--sf-dur-1`, `--sf-dur-3`, `--sf-ease`. `gap:clamp(16px,3cqw,40px)` fester Wert, kein Token.

Handy: gemessen `gap:16px`.

Desktop: gemessen `gap:40px`.

Bewegung (gemessen): Layout animation, `.ink` `transform` und `width`, 550 ms, `--sf-ease`, Verzögerung 0. Beim Laden läuft nur `transform` von links ein. Interpolation / Tween, `b` `color`, 150 ms, `--sf-ease`, Verzögerung 0.

### Farbe (`.swrow`, `.sw`, `recompute()`, `screenKonfig()`, Konfigurator)
Farbfelder aus dem Bildfeed.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | 40 x 40 px, `--radius-s`, Rand 1 px `--control-border`, Fläche `var(--c)` aus den Daten |
| Hover | Zeiger | `scale(1.06)` |
| Gewählt | `.on` | `::after`, Rahmen 1.5 px `--sf-ink`, `inset:-6px`, `--radius-s` |
| Fokus | Tastatur | Kein sichtbarer Fokus, siehe Fokusring (gemessen) |
| Leer | `imgModel()` liefert nichts, `OFFLINE` | `.small` „Ausführungen werden geladen, sobald Artikel im Feed geführt werden.“ |
| Hinweis | Immer bei Farben | `.small` „inklusive“, `.micro` „Weitere Ausführungen erscheinen hier, sobald sie im Feed geführt werden.“ |

Tokens: `--radius-s`, `--control-border`, `--border-hair`, `--sf-ink`, `--sf-dur-2`, `--sf-ease`. Hexwerte `#C9CCD1`, `#26262A` aus den Daten, 40 px, 1.5 px fester Wert, kein Token.

Handy: gleich, `flex-wrap:wrap`, `gap:14px`.

Desktop: gleich.

Bewegung (gemessen): Hover effect mit Scale, `.sw` `transform`, 260 ms, `--sf-ease`, Verzögerung 0. Scale in, `::after` `opacity` und `transform` scale(.86) nach scale(1), 260 ms, `--sf-ease`, Verzögerung 0.

### Leistung (`.tierrow`, `.shelf-tx`, `.shelf-rate`, `recompute()`, `data-tierlist`, Konfigurator)
Radiogruppe der Stufen mit Mehrwert-Satz, Spezifikation und Delta.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Linie oben, `padding:15px 2px`, `.chk` leer, Titel 14 px, 600, Text und `.micro` 12 px, Delta 14 px `--sf-text-2`, „plus x € im Monat“ |
| Gewählt | `.on`, `aria-checked` | `.chk` `--sf-ink`, Delta `--sf-ink`, 600, Text „gewählt“ |
| Vorauswahl | `KUR.empfohlene_stufe`, sonst `f.def.tier` | Gewählt beim Laden |
| Nicht lieferbar | `.aus`, `disabled`, Rate fehlt in dieser Größe | Text `--sf-text-2`, `.chk` 40 % Deckkraft, `cursor:not-allowed`, statt Delta „in dieser Größe nicht lieferbar“, kein Preis |
| „Empfohlen“ | `KUR.empfohlene_stufe`, sonst `t.empfohlen` | `.bst-etikett`, nur aus Kurationsdaten (E-065) |
| Hover | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur | Ring (gemessen) |

Tokens: `--sf-border`, `--sf-ink`, `--sf-text-small`, `--sf-text-micro`, `--sf-text-2`. Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Liste wird bei jedem `recompute()` neu geschrieben, keine Transition läuft (gemessen).

### Laufzeit-Regler (`.trk`, `.trk-in`, `.trk-line`, `.trk-fill`, `.stop`, `.stop-lbl`, `trackHTML()`, `setTrack()`, `nearestStop()`, Konfigurator)
Regler mit festen Stufen, zieh- und per Pfeiltaste bedienbar. Es gibt nur Leasing, keine Vertragsart zur Wahl (E-099).

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Linie 2 px `--sf-border`, Füllung 2 px `--sf-ink`, Stop 16 x 16 px, `--radius-s`, Rand 2 px `--control-border`, Fläche `--sf-surface`, Beschriftung 12 px |
| Hover | Zeiger auf Stop | Rand `--sf-ink` |
| Gewählt | `.on` | `--ink`, `scale(1.15)`, kein Halo, Beschriftung `--sf-ink` (gemessen) |
| Ziehen | `pointerdown` auf `.trk` | Nächster Stop rastet, `recompute(host,false)`, beim Loslassen `recompute(host,true)` |
| Tastatur | Pfeil links, rechts auf `.stop` | Wechsel plus `focus()`, Fokus unsichtbar an `.stop.on`, siehe Fokusring |
| Stufen | `TERMS` | 24, 36, 48 Monate, Voreinstellung 48. Die beworbene ab-Rate ist die 48-Monats-Rate. Die Pipeline liefert auch 60 und 72, der Shop blendet sie aus |
| Überschrift | `.now` | „Leasing, 48 Monate“ |
| Satz darunter | `[data-saving]` | „Bei n Monaten zahlen Sie x € weniger im Monat.“ oder „Längste Laufzeit, x € günstiger als bei n Monaten.“ |
| Rand | `.first`, `.last` | Beschriftung links- und rechtsbündig |

Raten: Nur aus `products.json`, Feld `rates.leasing`, je Größe, Stufe und Laufzeit. Der Prototyp hält dieselben Werte als Tabelle `f.rates`, Stand HubSpot 06.11.2026.

Tokens: `--sf-border`, `--sf-ink`, `--ink`, `--control-border`, `--sf-surface`, `--radius-s`, `--radius-none`, `--sf-text-micro`, `--sf-text-2`, `--sf-dur-2`, `--sf-dur-3`, `--sf-ease`. `.trk` `height:74px`, Stop 16 px fester Wert, kein Token. Trefferfläche `::after`, `inset:-14px`.

Handy: gleich, `touch-action:pan-y`.

Desktop: gleich.

Bewegung (gemessen): Layout animation, `.trk-fill` `width`, 550 ms, `--sf-ease`, Verzögerung 0. Scale, `.stop` `transform`, `background`, `border-color`, 260 ms, `--sf-ease`, Verzögerung 0. Interpolation / Tween, `.stop-lbl b` `color`, 260 ms. Drag ohne Momentum.

### Hinweis geprüfte Geräte (`.amz`, `.in`, `recompute()`, `refMatch()`, Konfigurator)
Zeile unter der Inklusivliste, nur bei Bestand gleicher Reihe und Größenklasse.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Sichtbar | `refMatch()` findet Typ | „Auch als geprüftes Gerät ab x € im Monat, sofort verfügbar“, `.platzhalter`, `.lnk-ink` „Ansehen“ mit `data-rt` |
| Ohne Treffer | Kein Typ, etwa Schalter „alles vergriffen“ | `.off`, Höhe 0, Inhalt nach 280 ms geleert |

Tokens: `--sf-text-small`, `--sf-text-2`, `--sf-ink`, `--sf-dur-2`, `--sf-ease`. `margin-top:18px` fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: gleich.

Bewegung: Accordion / Collapse, `grid-template-rows`, 260 ms, `--sf-ease`, Verzögerung 0.

## Ausstattung

Reihenfolge in `screenAusstattung()`: Kopf, Rücklink, Seitenkopf, Auswahlzeile, Komplett ausstatten, Kategorien, Summenleiste, Unterleiste, Band Versprechen, Fuß. Daten kommen aus dem Block `platzhalter-bausteine`, nichts ist vorausgewählt. Der Kontext ist `ausContext()`, Welt `neu` oder `refurb`.

### Seitenkopf Ausstattung (`.aus`, `screenAusstattung()`, Ausstattung)
Zweispalter aus Karten und Summenleiste, darüber Einleitung.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `.lbl` „Ausstattung“, `.platzhalter` „Platzhalter-Bausteine“, `.h1`, `.lead`, Rücklink auf `konfigurator` oder `refprod` |

Tokens: `--sf-space-4`, `--sf-space-5`. `padding-bottom:clamp(32px,5cqw,56px)` fester Wert, kein Token.

Handy: unter 900 px 1 Spalte. Gemessen bei 372 px wird die Spalte 365 px breit statt 332 px, weil `.bst` 327 px Mindestinhalt hat, rechts werden 13 px durch `overflow-x:hidden` abgeschnitten.

Desktop: ab 900 px `1fr minmax(320px,384px)`, `gap:clamp(28px,4cqw,72px)` (gemessen 720 px und 384 px).

Bewegung: Enter mit Translate, `revUp` über `data-rev` am Kopfblock, `transform`, .7s, `--sf-ease`, Verzögerung 0.

### Auswahlzeile (`.stufe1`, `screenAusstattung()`, Ausstattung)
Zeigt das gewählte Gerät mit Link zum Ändern.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Neugerät | `ctx.welt` „neu“ | Rahmen 1 px `--sf-border`, `padding:14px 18px`, 14 px, `.lnk` „Ändern“ |
| Geprüftes Gerät | `ctx.welt` „refurb“ | Dazu `.cond` „Mindestlaufzeit 12 Monate ...“ ohne Linie oben |
| Mit Menge | Menge größer 1 | „, Menge n“ |

Tokens: `--sf-border`, `--sf-radius-sm`, `--sf-text-small`. Maße fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: gleich.

Bewegung: keine.

### Komplett ausstatten (`.komplett`, `komplettHTML()`, `bstKomplett()`, Ausstattung)
Wählt mit einem Klick alle empfohlenen Bausteine.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | Mindestens ein Empfohlener wählbar und nicht gewählt | `--surface-sand`, `padding:14px 18px`, `.small`, `.btn.ghost` mit Inline `padding:12px 22px` (gemessen) |
| Alles gewählt | Nichts mehr hinzuzufügen | Block entfällt |
| Nach Klick | `data-komplett` | `.bst-note` „Hinzugekommen: ...“, darunter Karten neu |

Tokens: `--surface-sand`, `--sf-radius-sm`. Maße fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: gleich.

Bewegung: keine eigene, Karten siehe Bausteinzeile.

### Kategorie (`.bkats`, `.bkat`, `.bkat-h`, `bkatsHTML()`, `bstKatItems()`, Ausstattung)
Karte je Kategorie in der Reihenfolge `KUR.reihenfolge`.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Rahmen 1 px `--sf-border`, `padding:18px 18px 8px` (gemessen), `.lbl` plus `.platzhalter` „Platzhalter“, `.micro` „je Nutzer, monatlich“ oder „je Gerät, in der Rate“ |
| Leere Kategorie | Kein Baustein sichtbar | Keine Karte |
| Gar keine Karte | Alle ausgeblendet | `.small` „Für diese Auswahl gibt es derzeit keine Bausteine. Sie können direkt fortfahren.“ |
| Sortierung | `bstEmpList()` | Empfohlene zuerst |

Tokens: `--sf-border`, `--sf-radius`. Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Bausteinzeile (`.bst`, `.bst-main`, `.bst-tx`, `.nutz`, `.neben`, `.bst-delta`, `bstRowHTML()`, `bstState()`, `bstSelect()`, Ausstattung)
Ein Schalter je Baustein mit Nutzen und Monatsdelta.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `bstState` „ok“ | Rand 1 px `--sf-border`, `.chk` leer, Titel 14 px, 600, `.nutz` 14 px, `.neben` 12 px, Delta 14 px `--sf-text-2`, „plus x € im Monat“ |
| Empfohlen, nicht gewählt | `.emp` | Rand `--sf-border-strong`, `.bst-etikett` „Empfohlen“ |
| Gewählt | `.on`, `role="switch"`, `aria-checked` | Rand `--sf-accent-strong`, `outline` 1 px `--accent-text`, Versatz -2 px, ohne Schatten, `.chk` `--sf-accent-strong`, Delta `--sf-ink`, 600 |
| Gewählt, Menge größer 1 | `state.bstSel` | Dazu `.micro` „n × x €“ |
| Gesperrt | `bstState` „bedingt“, `.locked` | `--sf-surface-2`, `.bst-main` `disabled`, `cursor:default`, Hinweis `.bst-cond` |
| Ausgeblendet | `bstState` „hidden“ | Nicht gerendert |
| Hover | | im Prototyp nicht gezeichnet |
| Fokus | Tastatur auf `.bst-main` | Ring |
| Platzhalter | Schalter Bausteine „alles verfügbar“ | Standard |
| Platzhalter | Schalter „Copilot bedingt“ | Copilot gesperrt, in Welt neu |
| Platzhalter | Schalter „Dock ohne Preis“ | Dock ausgeblendet |
| Platzhalter | Schalter „Zubehör geprüfte Geräte nicht verfügbar“ | Kategorie Zubehör in Welt refurb ausgeblendet |
| Abhängigkeiten | `benoetigt`, `benoetigt_oder`, `schliesst_aus` | Automatisch mit- oder abgewählt, Rückmeldung über `.bst-note` |

Tokens: `--sf-border`, `--sf-border-strong`, `--sf-accent-strong`, `--accent-text`, `--border-hair`, `--sf-surface-2`, `--sf-ink`, `--sf-text-small`, `--sf-text-micro`, `--sf-text-2`, `--sf-radius-sm`, `--sf-dur-1`, `--sf-ease`. Maße fester Wert, kein Token.

Handy: Delta rechts mit `white-space:nowrap`, siehe Seitenkopf zur Mindestbreite.

Desktop: gleich.

Bewegung: Pop in, siehe Haken. `transition` auf `border-color`, `box-shadow` 150 ms ist definiert, läuft nicht, weil `updateAus()` die Karten neu schreibt (gemessen). Tabular numbers am Delta.

### Bedingungszeile (`.bst-cond`, `bstRowHTML()`, Ausstattung)
Text unter einer Zeile, wenn eine Voraussetzung gilt.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Gesperrt | `bstState` „bedingt“ | „verfügbar ab Stufe“, `.lnk-ink` „Stufe wechseln“, führt in den Konfigurator |
| Voraussetzung | Nicht gewählt, `x.hinweis_voraus` | Text aus den Daten |

Tokens: `--sf-text-micro`, `--sf-text-2`. `padding:0 16px 12px 54px` fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: gleich.

Bewegung: keine.

### Bausteinmenge (`.bst-qty`, `bstRowHTML()`, `data-bq`, Ausstattung)
Mengenzeile unter gewählten, mengenfähigen Bausteinen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Sichtbar | `.on` und `x.mengenfaehig` | `.qty` 30 x 30 px, Text „Menge, Startwert folgt der Gerätemenge“ |
| Ausgeblendet | Nicht gewählt oder nicht mengenfähig | Nicht gerendert |
| Minimum | Menge 1 | Minus bleibt aktiv, Wert bleibt 1 |

Tokens: `--sf-text-micro`, `--sf-text-2`, `--sf-text-small`. `padding:0 16px 12px 54px` fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: gleich.

Bewegung: siehe Menge.

### Hinweiszeile (`.bst-note`, `bkatsHTML()`, `komplettHTML()`, `bstSelect()`, Ausstattung)
Sagt nach einem Klick, was automatisch mitgewählt oder abgewählt wurde.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Sichtbar | `state.bstNotes`, `role="status"` | `--info-surface`, `--info`, 14/20 px, `padding:var(--space-3) var(--space-4)`, eckig |
| Leer | Mengenänderung oder Schalter Bausteine | `state.bstNotes` leer, keine Zeile |

Tokens: `--info-surface`, `--info`, `--radius-none`, `--space-3`, `--space-4`. 14/20 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Weitere Optionen (`.exp`, `.exp-h`, `.exp-b`, `.ch`, `bkatsHTML()`, `data-bstexp`, Ausstattung)
Klappt Bausteine ab dem vierten in einer Kategorie auf.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Geschlossen | Mehr als 3 Bausteine | „Weitere Optionen (n)“, 14 px, 600, Pfeil `--sf-text-2` |
| Offen | `.on`, `state.bstOpen` | Pfeil 90 Grad, Inhalt sichtbar |
| Fokus | Tastatur | Ring |
| Platzhalter | Daten haben höchstens 3 je Kategorie | Wird mit den heutigen Daten nicht gerendert |

Tokens: `--sf-border`, `--sf-text-small`, `--sf-ink`, `--sf-text-2`, `--sf-space-5`, `--sf-dur-2`, `--sf-ease`. `padding:18px 0` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Accordion / Collapse, `grid-template-rows`, 260 ms, `--sf-ease`, und Rotate, `transform` rotate(90deg) an `.ch`, 260 ms, sind definiert. Beide laufen nicht, `updateAus(false)` schreibt den Inhalt neu.

### Summenleiste (`.aus-sum`, `screenAusstattung()`, `updateAus()`, `ausStatus()`, Ausstattung)
Klebende Spalte mit Rate, Positionen und Weiter-Knopf.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Rahmen 1 px `--sf-border`, `padding:24px`, `.lbl` „Ihre Rate“, `.platzhalter`, Rate, Brutto und Positionszahl als `.micro`, `.aus-rows`, `.btn.primary.block` |
| Laden | Klick mit Änderung, `ausStatus()` | `.micro` „Rate wird neu berechnet“ für 200 ms |
| Serverrate weicht ab | `KUR.mengenstaffel` | Zählt nach 420 ms nach. Der Datenblock hat keine `mengenstaffel`, also nicht erreichbar |
| Neugerät | `ctx.cta` | „Weiter zur Anfrage“, Satz „Unverbindlich, das Angebot kommt per E-Mail.“ |
| Geprüftes Gerät | `ctx.cta` | „Weiter zur Kasse“, Satz „Zahlung erst im nächsten Schritt.“ |
| Fehler | | im Prototyp nicht gezeichnet |

Tokens: `--sf-border`, `--sf-radius`, `--sf-surface`. `padding:24px`, `top:90px` fester Wert, kein Token.

Handy: unter 900 px `display:none`.

Desktop: ab 900 px `display:block`, `position:sticky`, `top:90px` (gemessen).

Bewegung: siehe Rate im Band. Der Klick setzt `.flash` auf das erste `[data-band]`, das ist `.aus-bar`, dafür gibt es keine Regel, also keine Bewegung (gemessen).

### Unterleiste (`.aus-bar`, `screenAusstattung()`, `data-ausbar`, Ausstattung)
Klebende Leiste unten auf dem Handy, öffnet die Positionsliste.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `--surface`, Linie oben, kein Blur, Rate 28 px (Inline 1.55rem wirkt nicht), Brutto, Positionszahl, `.btn.primary` mit Inline `padding:13px 22px` (gemessen) |
| Klick auf Leiste | `data-ausbar` | Öffnet Positionsblatt |
| Klick auf Knopf | `data-aus-go` | Weiter zu Anfrage oder Kasse, ohne Blatt |
| Fokus | `tabindex="0"`, `role="button"` | Ring, Enter und Leertaste ohne Handler |
| Laden | wie Summenleiste | `.micro` „Rate wird neu berechnet“ |

Tokens: `--surface`, `--sf-border`, `--sf-gutter`. `padding:12px` plus `env(safe-area-inset-bottom)`, `gap:14px` fester Wert, kein Token.

Handy: unter 900 px `display:flex`, `position:sticky`, `bottom:0`, `z-index:15`.

Desktop: ab 900 px `display:none`.

Bewegung: Number ticker und Pulse, siehe Rate im Band. Kein Band-Blinken.

### Positionsblatt (`.dlg.bottom`, `screenAusstattung()`, `state.ausSheet`, Ausstattung)
Unterblatt mit allen Positionen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Offen | `state.ausSheet` | `.dlg-in` volle Breite, `max-height:82%`, `overflow-y:auto`, `.grip`, `h2` „Ihre Positionen“, `.iconbtn`, `.aus-rows`, `.btn.primary.block` |
| Schließen | `.iconbtn`, Klick auf Scrim, Griff | Blatt weg |
| Fokus | Tastatur | Ring |
| Entfernen | `.line-x`, `updateAus()` | Zeile weg, Blatt bleibt offen, keine Einblendung |

Tokens: `--sf-radius`, `--sf-surface`, `--scrim`. `max-height:82%` fester Wert, kein Token.

Handy: Öffnet nur unter 900 px, Auslöser ist die Unterleiste.

Desktop: Kein Auslöser ab 900 px.

Bewegung: Enter mit Translate, `sheetUp`, `transform`, .35s, `--sf-ease`, Verzögerung 0 (gemessen). Ziehen siehe Griff.

## Anfrage-Blatt

Wird in `renderScreen()` auf jeder Seite ins DOM gesetzt, sichtbar nur mit `.sheetopen`. Tab „Anfrage“ legt Ausstattung als Hintergrund.

### Blatt (`.sheet`, `.scrim2`, `.sheetopen`, `.sheet-top`, `.sheet-body`, `.sheet-foot`, `sheetHTML()`, `placeSheet()`, alle Seiten)
Seitliches Blatt für Korb, Kontakt und Bestätigung.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Geschlossen | `state.sheet` falsch | `translateX(101%)`, `.scrim2` `opacity:0`, `pointer-events:none` |
| Offen | `data-sheet="open"`, `.sheetopen` | `transform:none`, `.scrim2` `--scrim`, `.screen` ohne Scrollen, Rand links 1 px `--line`, ohne Schatten |
| Schritt 1 | `state.aqStep` 1 | Titel „Ihre Anfrage“, Positionen, Summe, Knopf „Weiter zum Kontakt“ |
| Schritt 2 | `state.aqStep` 2 | Titel „Kontakt“, Formular, Knopf „Anfrage senden“ |
| Schritt 3 | `state.aqStep` 3 | Titel „Fertig“, `.done`, `.btn.ghost.block` „Weiter stöbern“ |
| Leer | Korb leer, nicht Schritt 3 | Titel „Ihre Anfrage“, `.empty`, kein `.sheet-foot` |
| Fokus | Tastatur | Ring an `.iconbtn`, Fokussteuerung im Prototyp nicht gezeichnet |
| Escape | | im Prototyp nicht gezeichnet |
| Speicher | `saveCart()`, `localStorage` `slshop-cart-surface` | Korb überlebt Neuladen |

Tokens: `--sf-surface`, `--line`, `--border-hair`, `--scrim`, `--sf-border`, `--sf-space-5`, `--sf-dur-3`, `--sf-ease`. `width:min(560px,100%)`, `.45s`, `z-index:41` fester Wert, kein Token.

Handy: gemessen 372 px, also volle Breite.

Desktop: gemessen 560 px, rechts.

Bewegung: CSS definiert Slide in, `.sheet` `transform`, .45s, `--sf-ease`, Verzögerung 0, und Fade in, `.scrim2` `opacity`, 550 ms, `--sf-ease`, Verzögerung 0. Beides läuft im Prototyp nicht, Öffnen und Schließen gehen über `render()`, die Elemente entstehen im Endzustand (gemessen). Im Hintergrund startet dabei `revUp` neu.

### Blatt-Fortschritt (`.sheet-prog`, `sheetHTML()`, Anfrage-Blatt)
Drei Striche für die drei Schritte.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Offen | | 2 px, `--sf-border`, eckig |
| Erreicht | `.on` | `--sf-accent` |

Tokens: `--sf-border`, `--sf-accent`, `--radius-none`, `--sf-space-5`, `--sf-dur-2`, `--sf-ease`. 2 px, `gap:6px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: `transition` auf `background` 260 ms definiert, läuft nicht, jeder Schritt rendert neu.

### Anfrageposition (`.line`, `.line-tx`, `.line-ctl`, `.line-rate`, `.lr`, `.cart-total`, `sheetHTML()`, `data-lq`, `data-rm`, Anfrage-Blatt)
Eine Korbzeile mit Menge und Betrag.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `.line-thumb`, Titel 14 px, 600, Unterzeile 12 px, `.qty` 32 x 32 px, `.qv` 16 px `--sf-text-2`, Betrag `b.lr` 14 px, 600, als Block, „mtl.“ darunter 12 px, beide `--sf-text-2` und tabellarisch (gemessen, `.line-tx span` gewinnt gegen `.line-rate`), `.line-x` rechts |
| Menge geändert | `data-lq` | Zahl, Betrag, `.cart-total` und `.count` sofort neu, ohne Rendern |
| Entfernt | `data-rm` | `render()`, letzte Position führt zum Leerzustand |
| Baustein-Position | Aus Ausstattung, ohne `fam` | `.mock` als Bild, Unterzeile „Baustein · Kategorie“ |
| Platzhalter | Startkorb `BRANDS.surface.cart` | Eine Position mit Menge 5 |

Tokens: `--sf-border`, `--sf-text-small`, `--sf-text-micro`, `--sf-text-2`. `padding:18px 0`, `gap:16px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine. Tabular numbers.

### Kontaktformular (`.fldwrap`, `sheetHTML()`, `data-send`, Anfrage-Blatt)
Schritt 2, Felder Firma, Name, E-Mail, Telefon optional, Nachricht optional, eine Zustimmung.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `.fld`, `.frow`, `.chk-line`, `.sum`, `.lnk` „Positionen ändern“ |
| Laden | `data-send` | `.btn.loading`, Text „Wird gesendet…“, 900 ms, dann Schritt 3 |
| Fehler | | im Prototyp nicht gezeichnet, Senden geht auch leer |

Tokens: keine eigenen, über `.fld`, `.chk-line`, `.sum`, `.lnk`: `--control-border`, `--surface-raised`, `--focus-ring`, `--ink-muted`, `--accent-text`, `--sf-border`, `--sf-accent-strong`, `--sf-text-micro`.

Handy: `.frow` 1 Spalte unter 560 px.

Desktop: `.frow` 2 Spalten ab 560 px, gemessen wird der Schirm, nicht das Blatt.

Bewegung: keine.

### Alternativen-Dialog (`.alt`, `.alt-tx`, `.alt-take`, `.altref`, `altDlg()`, Anfrage-Blatt)
Später Verfügbarkeits-Check beim Schritt von 1 nach 2, einmal je Sitzung.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Offen | `data-step="2"` und `state.altDone` falsch | `h2` „Ihre Variante ist gerade nicht lieferbar“, `.lead` plus `.platzhalter`, bis 3 Zeilen, `.btn.ghost.block` „Bei meiner Auswahl bleiben“, `.micro` |
| Zeile Ruhe | | Linie oben, `padding:16px 2px`, Titel 14 px, 600, Unterzeile 12 px, „Übernehmen“ 12 px, 600, `--sf-accent-strong` |
| Zeile Hover | Zeiger | Kinder rücken 8 px |
| Fokus | Tastatur | Ring |
| Mit geprüftem Gerät | `refMatch()` findet Typ | `.altref`, Linie `--sf-border-strong`, `.lbl`, `.lnk-ink` „Geprüfte Geräte ansehen“, `.platzhalter` |
| Ohne geprüftes Gerät | Kein Typ, Schalter „alles vergriffen“ | Block entfällt |
| Auswahl | `data-altok`, `data-altkeep` | `state.altDone` wahr, Schritt 2 |
| Schließen über Scrim | | im Prototyp nicht gezeichnet |

Tokens: `--sf-border`, `--sf-border-strong`, `--sf-accent-strong`, `--sf-text-small`, `--sf-text-micro`, `--sf-text-2`, `--sf-space-4`, `--sf-space-5`, `--sf-dur-2`, `--sf-ease`. Maße fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Enter mit Translate und Stagger über `data-rev`, `revUp`, .7s, `--sf-ease`, Verzögerung 0, 60, 120 ms je Zeile, `.altref` 220 ms. Hover effect mit Translate, `transform` translateX(8px) an `.alt>*`, 260 ms, `--sf-ease`, Verzögerung 0. Dialog siehe Dialog.

## Geprüfte Geräte Katalog

Reihenfolge in `screenRefKat()`: Kopf, Seitenkopf, Versprechen, je Reihe Gruppenkopf und Raster, Zubehörzeile oder Leerzustand, Band Versprechen, Fuß.

### Versprechen (`.sl-feat`, `.sl-feat-sand`, `.ref-promise`, `.sl-feat-dot`, `.sl-feat-s`, `screenRefKat()`, Geprüfte Geräte Katalog)
Vier feste Aussagen auf Sand unter der Überschrift.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `--surface-sand`, `padding:var(--space-5) var(--space-6)`, Punkt 9 x 9 px `--marker`, Text 14/20 px `--ink` (gemessen) |
| Kopf | `.lbl` plus `.platzhalter` „Platzhalter-Bestand“ | `h1.display` in `--sf-text-h1`, `.lead` |

Tokens: `--surface-sand`, `--space-3`, `--space-5`, `--space-6`, `--marker`, `--radius-pill`, `--ink`, `--sf-text-h1`. 9 px, 14/20 px fester Wert, kein Token.

Handy: unter 700 px 1 Spalte.

Desktop: ab 700 px 2 Spalten, ab 1000 px 4 Spalten.

Bewegung: Enter mit Translate, `revUp` an der `h1`, `transform`, .7s, `--sf-ease`, Verzögerung 0.

### Gruppenkopf (`.grouphead`, `screenRefKat()`, Geprüfte Geräte Katalog)
Reihenname und Anzahl der Varianten.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Linie oben, `padding-top:18px`, `h3` 18 px, 600, `.small` „n Varianten auf Lager“ |
| Eine Variante | Liste Länge 1 | „1 Variante auf Lager“ |
| Reihe ohne Bestand | Schalter | Gruppe entfällt |

Tokens: `--sf-border`, `--sf-text-h3`. `margin:clamp(28px,4cqw,44px) 0 18px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Typkarte (`.typegrid`, `.type`, `.type-field`, `.type-sym`, `.type-name`, `.type-spec`, `.type-foot`, `.type-rate`, `.type-go`, `refCard()`, Geprüfte Geräte Katalog)
Karte je Lagertyp, nach Rate sortiert, führt zur Produktseite.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | Feld 4:3, `--surface-raised`, `.type-badge`, `.tag`, „Symbolbild der Reihe“ 12 px, Name 18 px, 600, Spezifikation 14 px, `.pill-ink`, `.stat`, Rate 28/32 px, 300, `.platzhalter`, Pfeilfeld 36 x 36 px `--radius-s` |
| Mit Zubehör | `t.enthalten_zubehoer` | Zeile „inkl. ...“ |
| Hover | Zeiger | `.type-go` Fläche und Rand `--sf-ink`, Pfeil `--sf-surface`, `translateX(3px)`. Bild bleibt ruhig |
| Fokus | Tastatur | Ring |
| Bestand knapp | Schalter „knapp“ | `.stat.low` „nur noch n verfügbar“ |
| Einzelstück | Schalter „Einzelstücke“ | `.stat.low` „Einzelstück“ |
| Ein Typ vergriffen | Schalter „ein Typ vergriffen“ | Typ `weg1` fehlt im Raster, Zähler im Gruppenkopf sinkt |
| Alles vergriffen | Schalter | Keine Karte, `.empty` |

Tokens: `--surface-raised`, `--sf-radius`, `--sf-text-micro`, `--sf-text-h3`, `--sf-text-small`, `--sf-text-2`, `--sf-accent-strong`, `--ink-muted`, `--radius-s`, `--control-border`, `--sf-ink`, `--sf-surface`, `--sf-border`, `--sf-dur-1`, `--sf-ease`. 28/32 px, 36 px fester Wert, kein Token.

Handy: unter 700 px 1 Spalte, `gap:clamp(14px,2cqw,22px)`.

Desktop: ab 700 px 2 Spalten, ab 1000 px 3 Spalten.

Bewegung: Hover effect mit Translate, `.type-go` `background`, `border-color`, `transform`, 150 ms, `--sf-ease`, Verzögerung 0. Pfeilfarbe springt.

### Zubehörzeile (`.accline`, `screenRefKat()`, Geprüfte Geräte Katalog)
Nennt buchbares Zubehör aus `b.refAdd`.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | Mindestens eine Gruppe | `--surface-sand`, `padding:18px 22px`, 14 px, `--sf-text-2`, rechter Text per `margin-left:auto` |
| Alles vergriffen | Keine Gruppe | Entfällt |

Tokens: `--surface-sand`, `--sf-radius-sm`, `--sf-text-small`, `--sf-text-2`. Maße fester Wert, kein Token.

Handy: `flex-wrap:wrap`.

Desktop: einzeilig.

Bewegung: keine.

## Geprüftes Gerät

Reihenfolge in `screenRefProd()`: Kopf, Rücklink, Bühne mit `.type-badge`, Im Paket enthalten, Produktspalte, Ratenband, Band Versprechen, Fuß.

### Produktspalte (`.kfg > div`, `.type-meta`, `.cond`, `.grp`, `screenRefProd()`, `stockOf()`, `stockState()`, Geprüftes Gerät)
Rechte Spalte, zwei Grundzustände aus dem Bestand.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Verfügbar | Bestand größer 0 | `.h1`, `.lead`, `.pill-ink`, `.stat`, `.cond` „Mindestlaufzeit 12 Monate“, Menge, Inklusivliste, Rückrichtung, Ratenband |
| Bestand knapp, Einzelstück | Schalter | `.stat.low`, Plus-Knopf sperrt bei Bestand |
| Vergriffen | Bestand 0 | `.cond` mit `.stat.out` und Text, `.btn.primary` „Andere Geräte ansehen“, `.btn.ghost` „Als Neugerät konfigurieren“. Kein Band, kein Paketinhalt |
| Tab im Schalter „ein Typ vergriffen“ | `t.weg1` setzt `state.rt` | Zeigt genau den vergriffenen Typ |
| Bildzeile | `.kstage-cap` | „Symbolbild der Reihe. Geprüft, gereinigt und mit Windows 11 Pro neu aufgesetzt, mit Gewährleistung.“ |

Tokens: keine eigenen, über `.pill-ink`, `.stat`, `.cond`, `.grp`: `--chip-cool`, `--on-chip-cool`, `--sf-success`, `--warning`, `--sf-onrequest`, `--sf-border`, `--sf-text-2`, `--sf-ink`, `--sf-text-small`, `--sf-space-5`.

Handy: Bühne über der Spalte, unter 860 px.

Desktop: Zweispalter ab 860 px, Bühne klebt.

Bewegung: keine eigene.

### Im Paket enthalten (`.zubrow`, `.zk`, `.zthumb`, `.zchip`, `zubIncludedHTML()`, Geprüftes Gerät)
Zeigt mitgeliefertes Zubehör ohne Preis und ohne Schalter.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Kachel Ruhe | Bildmodell in `ZUBBILD` | Rahmen 1 px `--sf-border`, `--radius-s`, Bild 80 x 60 px eckig, Titel 14 px, 600 |
| Kachel Hover | Zeiger | `--sf-surface-2` |
| Kachel Fokus | Tastatur | Ring, die eigene `outline`-Regel verliert (gemessen) |
| Chip ohne Bilder | Kein Bildmodell | `.zchip`, Pille, Rahmen, `padding:11px 18px`, nicht klickbar |
| Leer | `enthalten_zubehoer` fehlt | Block entfällt |
| Vergriffen | Bestand 0 | Block entfällt |
| Mehrzahl | `menge` größer 1 | „2× Titel“ |

Tokens: `--sf-border`, `--radius-s`, `--radius-none`, `--radius-pill`, `--sf-surface-2`, `--sf-text-small`, `--sf-ink`, `--sf-dur-1`, `--sf-ease`. Maße fester Wert, kein Token. Trefferfläche `::after`, `inset:-4px`.

Handy: `flex-wrap:wrap`, `gap:10px`.

Desktop: gleich.

Bewegung: Hover effect, `background`, `border-color`, 150 ms, `--sf-ease`, Verzögerung 0.

### Zubehörblatt (`.dlg.zub`, `.zgal`, `.zgal-dots`, `.zgal-thumbs`, `zubSheet()`, Geprüftes Gerät)
Eigene Galerie je Zubehörteil, ohne Preis, nur Schließen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Offen | `data-zub` | `.grip`, `h2`, `.iconbtn`, `.small` „Geprüft und gereinigt“, `.zgal` 4:3 mit `.scene.sc-detail` plus `.tag` |
| Ein Bild | `gallery` leer | Keine Punkte |
| 2 bis 3 Bilder | `bilder.length` ab 2 | `.zgal-dots`, Punkt 9 x 9 px `--radius-s` |
| Ab 4 Bildern | `bilder.length` ab 4 | Zusätzlich `.zgal-thumbs` 64 x 48 px. Die Daten erreichen das heute nicht |
| Gewählt | `.on` | Punkt `--sf-ink`. Thumb Rand plus `inset` 1 px `--sf-ink` |
| Fokus | Tastatur | Siehe Fokusring |
| Schließen | `.iconbtn`, Scrim, Griff | `state.zubKeep` hält die Scrollposition |
| Platzhalter | Keine echten Bilder | `.tag` „Hauptansicht, Platzhalter“ |

Tokens: `--sf-radius`, `--sf-radius-sm`, `--sf-surface-2`, `--sf-border`, `--sf-border-strong`, `--sf-ink`, `--sf-focus`, `--radius-s`, `--radius-none`, `--scrim`. Maße fester Wert, kein Token.

Handy: unter 760 px Unterblatt, volle Breite, `max-height:88%`, Griff sichtbar (gemessen).

Desktop: ab 760 px Seitenblatt rechts, `width:min(460px,94%)`, volle Höhe, Griff aus (gemessen 460 px).

Bewegung: Handy Enter mit Translate, `sheetUp`, .35s, `--sf-ease`, Verzögerung 0. Desktop Enter mit Translate, `zubSide`, `transform`, .4s, `--sf-ease`, Verzögerung 0. Klick auf einen Punkt rendert neu und startet die Bewegung erneut (gemessen). Ziehen siehe Griff.

### Ausklapper Einmalig kaufen (`.exp`, `.exp-h`, `.exp-in`, `.buyprice`, `data-buytoggle`, `data-cash="kauf"`, `screenRefProd()`, Geprüftes Gerät)
Stille Kauf-Option nach E-099, nur auf der Produktseite. Kaufpreis aus dem HubSpot-Feld Kaufpreis netto. Nie in Teasern, Querverweisen, Kampagnen oder Vergleichen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Kein Kaufpreis | `t.kauf` leer, im Prototyp Surface Pro 9 | Der Ausklapper fehlt ganz, das Gerät ist nicht kaufbar |
| Geschlossen | `state.buy` falsch | „Einmalig kaufen statt monatlicher Service“ |
| Offen | `state.buy` wahr, `.on` | `.buyprice` 28/32 px, 300, `.platzhalter`, `.small`, `.btn.ghost` „Zur Kasse mit Kaufpreis“ |

Tokens: `--sf-border`, `--sf-text-small`, `--sf-ink`, `--sf-text-2`, `--sf-space-5`. 28/32 px, `.exp-in` `padding-bottom:22px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: Accordion / Collapse und Rotate sind definiert, laufen nicht, `render()` schreibt neu (gemessen).

### Rückrichtung (`.cond`, `.lnk-ink`, `newMin()`, `data-newfam`, `screenRefProd()`, Geprüftes Gerät)
Verweist auf das günstigste Neugerät gleicher Reihe und Größenklasse.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Sichtbar | `newMin()` findet Gerät | `.cond` ohne untere Linie, „Als Neugerät mit Vollgarantie ab x € im Monat.“, `.lnk-ink` „Zum Konfigurator“ |
| Vergriffen | Bestand 0 | Entfällt |
| Klick | `data-newfam` | Konfigurator mit vorbelegter Reihe und Größe |

Tokens: `--sf-border`, `--sf-text-small`, `--sf-text-2`, `--sf-ink`, `--ink`.

Handy: gleich.

Desktop: gleich.

Bewegung: siehe Ink-Link.

## Kasse

`screenRefKasse()`, drei Schritte plus zwei Endzustände, nur für geprüfte Geräte.

### Kassenrahmen (`.cash`, `screenRefKasse()`, Kasse)
Schmale Spalte für alle Schritte.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | | `max-width:640px`, zentriert, Fußknopf mit `margin-top:30px` |

Tokens: keine, `padding:clamp(26px,4cqw,48px) 0 clamp(40px,6cqw,72px)` fester Wert, kein Token.

Handy: gemessen `padding-top:26px`.

Desktop: gemessen `padding-top:48px`.

Bewegung: Enter mit Translate, `revUp` auf `[data-rev]` bei jedem Schritt, `transform`, .7s, `--sf-ease`, Verzögerung 0 (gemessen).

### Kassen-Fortschritt (`.cash-prog`, `screenRefKasse()`, Kasse)
Drei Striche für die Schritte 1 bis 3.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Offen | | 2 px, `--sf-border`, eckig, `gap:6px` |
| Erreicht | `.on` | `--sf-accent` |
| Endzustand | `state.kaStep` 4 oder 5 | Nicht gerendert |

Tokens: `--sf-border`, `--sf-accent`, `--radius-none`, `--sf-space-6`. 2 px fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Schritt 1, Bestellung (`.crow`, `.crow-tx`, `.crow-rate`, `screenRefKasse()`, Kasse)
Gerätezeile, gewählte Bausteine, Summe.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `state.cashMode` „abo“ | Gerät mit `.line-thumb`, „Service, Mindestlaufzeit 12 Monate · Menge n“, „inkl. ...“. Bausteine mit `margin-left:80px` und `.line-x`. `.sum` „Monatliche Rate gesamt“, `.micro` Brutto plus `.platzhalter` |
| Baustein entfernt | `data-bst-rm` | `render()` |
| Knopf | `data-kastep="2"` | „Weiter zu den Firmendaten“ |
| Kaufmodus | `state.cashMode` „kauf“ | „Einmalkauf“, Kaufpreis statt Rate, „Einmalsumme netto“. Kaufweg nach E-099, nur von der Produktseite und nur mit Kaufpreis (`t.kauf`). |

Tokens: `--sf-border`, `--sf-text-small`, `--sf-text-micro`, `--sf-text-2`. `padding:18px 0`, `gap:16px` fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine eigene, siehe Kassenrahmen. Tabular numbers an `.num`.

### Schritt 2, Firmendaten (`.fld`, `.frow`, `.chk-line`, `screenRefKasse()`, `data-kastep`, Kasse)
Felder Firma, Name, E-Mail, Telefon optional, Lieferadresse, „USt-IdNr, optional“, drei Zustimmungen.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `state.kaStep` 2 | `.h1` „Firmendaten“, Felder, Knopf „Weiter zur Übergabe“, `.lnk` „Bestellung ändern“ |
| Fehler | | im Prototyp nicht gezeichnet, Weitergehen ohne Prüfung |

Tokens: keine eigenen, über `.fld`, `.chk-line`, `.lnk`: `--control-border`, `--surface-raised`, `--focus-ring`, `--ink-muted`, `--accent-text`, `--sf-accent-strong`, `--sf-text-micro`.

Handy: `.frow` 1 Spalte unter 560 px.

Desktop: `.frow` 2 Spalten (gemessen 310 px je Spalte).

Bewegung: siehe Kassenrahmen.

### Schritt 3, Übergabe (`.sum`, `.btn.loading`, `screenRefKasse()`, `data-pay`, Kasse)
Letzter Schritt vor Stripe.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `state.kaStep` 3 | `.h1` „Übergabe“, `.lead`, `.sum` ohne Linie, `.btn.primary.block` „Weiter zur sicheren Zahlung“, `.micro` „Sichere Zahlung über Stripe, monatliche Rechnung.“ |
| Laden | `data-pay` | `.btn.loading`, „Wird an Stripe übergeben…“, 900 ms (gemessen) |
| Konflikt | Menge größer als Bestand minus 1 | Konflikt-Dialog. Standardtyp hat Bestand 1, ohne vorherige Typwahl tritt er also immer ein (gemessen) |
| Zahlung gelingt | Schalter Stripe „Zahlung gelingt“ | Abo aktiv |
| Abbruch | Schalter Stripe „Abbruch“ | Stripe-Abbruch |
| Kaufmodus | `kauf` wahr | „Einmalsumme netto“, „einmalige Abbuchung“. Kaufweg nach E-099, nur von der Produktseite und nur mit Kaufpreis (`t.kauf`). |

Tokens: keine eigenen, über `.sum`, `.btn`: `--sf-accent-strong`, `--sf-text-small`, `--action`, `--on-action`.

Handy: gleich.

Desktop: gleich.

Bewegung: siehe Kassenrahmen.

### Abo aktiv (`.done`, `.aus-rows`, `screenRefKasse()`, `state.kaStep` 4, Kasse)
Erfolgsende nach Stripe.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Ruhe | `state.stripeFail` falsch | Siehe Abschluss, Positionen `max-width:440px`, `.btn.ghost` „Weitere Geräte ansehen“ |

Tokens: keine eigenen, über `.done`: `--sf-space-5`, `--sf-ink`, `--sf-text-small`, `--sf-text-2`.

Handy: gleich.

Desktop: gleich.

Bewegung: siehe Abschluss.

### Stripe-Abbruch (`.done`, `screenRefKasse()`, `state.kaStep` 5, Kasse)
Ende, wenn die Zahlung abbricht.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Stripe-Abbruch | `state.stripeFail` wahr | Ohne Herz, `h2` „Zahlung abgebrochen“, `.lead` „Es wurde nichts abgebucht und nichts reserviert. Sie können jederzeit weitermachen, wo Sie waren.“, `.btn.primary` „Zurück zur Kasse“, `.btn.ghost` „Zum Gerät“ |

Tokens: keine eigenen, über `.done`: `--sf-space-5`, `--sf-ink`, `--sf-text-small`, `--sf-text-2`.

Handy: gleich.

Desktop: gleich.

Bewegung: siehe Abschluss.

### Konflikt-Dialog (`.dlg`, `.btn`, `screenRefKasse()`, `state.conflict`, `data-fix`, Kasse)
Bestand hat sich zwischen Auswahl und Zahlung geändert.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Rest vorhanden | Bestand minus 1 größer 0 | „Von diesem Gerät sind noch n verfügbar, Sie hatten m gewählt. ...“, `.btn.primary` „Menge auf n anpassen“, `.btn.ghost` „Anderes geprüftes Gerät wählen“, `.btn.ghost` „Als Neugerät anfragen“ |
| Kein Rest | Bestand minus 1 ist 0 | „Dieses Gerät ist inzwischen vergeben. Es wurde nichts abgebucht und nichts reserviert.“ (gemessen), `.btn.primary` „Anderes geprüftes Gerät wählen“, `.btn.ghost` „Als Neugerät anfragen“ |
| Auswahl | `data-fix` `qty`, `kat`, `neu` | Menge plus Schritt 1, Katalog, Konfigurator |
| Schalter Bestand | Klick im Prototyp | Setzt `state.conflict` zurück |

Tokens: keine eigenen, über `.dlg`, `.btn`: `--scrim`, `--sf-surface`, `--action`, `--on-action`, `--heading`, `--line-strong`.

Handy: gleich.

Desktop: gleich.

Bewegung: siehe Dialog.

## Rechtsseiten

Sonderfall: Impressum und Datenschutz sind Gerüste, die Texte liefert der Master.

### Rechtskopf (`.lbl`, `.platzhalter`, `.h1`, `.lead`, `rechtKopf()`, Rechtsseiten)
Kopf beider Seiten mit Kennzeichnung.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Gerüst | Heutiger Stand | `.lbl` „Rechtliches“, `.platzhalter` „Gerüst, Text folgt vom Master“, `.h1`, `.lead` mit Platzhalter |

Tokens: `--sf-accent-strong`, `--sf-text-h1`, `--ink-muted`, `--line`, `--ink-subtle`, `--radius-pill`, `--space-2` (`.sl-imp .lead`).

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

### Impressum (`.sl-imp`, `.sl-imp-g`, `.sl-imp-b`, `screenImpressum()`, Rechtsseiten)
Fünf Blöcke mit Überschrift, Inhalt liefert der Master.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Gerüst | Heutiger Stand | `h2` „Anbieter“, „Vertretung“, „Kontakt“, „Register“, „Umsatzsteuer“, je `[Text vom Master]` |

Tokens: `--ink`, `--heading`, `--space-2`, `--space-8`, `--space-12`. `h2` 18/26 px, 600, Text 16/24 px fester Wert, kein Token.

Handy: unter 760 px 1 Spalte.

Desktop: ab 760 px 3 Spalten (gemessen).

Bewegung: keine.

### Datenschutz (`.sl-recht`, `.sl-recht-a`, `screenDatenschutz()`, Rechtsseiten)
Drei Abschnitte als Gerüst, Inhalt liefert der Master.

Zustände:

| Zustand | Auslöser | Aussehen |
|---|---|---|
| Gerüst | Heutiger Stand | `.lead` „Stand [Datum]“, je `h2` `[Überschrift Abschnitt n]` und `[Text vom Master]`, `max-width:72ch` |

Tokens: `--ink`, `--heading`, `--space-2`, `--space-8`. `h2` 18/26 px, 600, Text 16/24 px, 72ch fester Wert, kein Token.

Handy: gleich.

Desktop: gleich.

Bewegung: keine.

## Sammelzeilen

Prototyp-Hülle, kein Baustein: `.bar`, `.bar-title`, `.barlbl`, `.tabs`, `.tab`, `#stage`, `.devlabel`, `.phone`, `.frame`, `.desk`, `.browserbar`, `.wdots`, `.url`.

Reine Hilfsklassen und Zustandsträger ohne eigene Gestalt, jeweils beim Träger beschrieben: `.cfg`, `.solid`, `.onlight`, `.n`, `.tx`, `.s`, `.d`, `.first`, `.last`, `.on`, `.off`, `.go`, `.emp`, `.locked`, `.low`, `.ok`, `.out`, `.ic-pause`, `.ic-play`, `.paused`, `.pulse`, `.flash`, `.hide`, `.hr`.

Innenteile von `.scene`, im Surface-Zweig `display:none`: `.scene-art`, `.kb`, `.sc-grain`, `.sc-light`, `.sc-desk`, `.sc-window`, `.sc-person`, `.body`, `.lap`, `.lap2`, `.p1`, `.p2`, `.sc-table`, `.sc-cup`, `.sc-note`, `.sc-mockwrap`, `.mock-screen`, `.mock-base`.

Im CSS oder JS vorhanden, im Surface-Zweig nicht gerendert: `.hero`, `.scrim`, `.hero-in`, `.hero-sl`, `.hero-sl-in`, `.hero-sl-media`, `.hero-anchor`, `.u`, `.hero-facts`, `.fx`, `.fx2`, `.fx3`, `.fx4`, `.morph`, `.story`, `.stories`, `.story-in`, `.story-q`, `.story-a`, `.story-dev`, `.shelf-row`, `.sw-note`, `.badge`, `.bigrate`, `.ftr-contact`, `.slogan`, `.done-ico`, `.sc-hero`, `.overhero`, `.ondark`, `.tier-detail`, `.rcfg`, `.dd`. Funktionen ohne Aufruf im Surface-Zweig: `heroSurface()`, `stageB2()`, `moodBand()`, `inspTeaser()`, `islot()`, `recomputeRef()` ohne Wirkung. Attribute `data-ad`, `data-radd`, `data-ru`: kein Element im Render. `data-mess`, `data-mess-*`: am Markup vorhanden, kein Handler im Prototyp.

#### Prototyp-Schalter und ihre Zustände

| Schalter | Wert | Wirkung | Beschrieben bei |
|---|---|---|---|
| Bestand | normal | `t.bestand` | Verfügbarkeit, Typkarte |
| Bestand | knapp | `min(bestand, 3)` | Verfügbarkeit, Typkarte, Menge |
| Bestand | Einzelstücke | 1 je Typ mit Bestand | Verfügbarkeit, Typkarte, Konflikt-Dialog |
| Bestand | ein Typ vergriffen | Typ `weg1` ist 0, Produkt-Tab zeigt ihn | Typkarte, Produktspalte |
| Bestand | alles vergriffen | Alle 0 | Refurbished-Band, Hinweis geprüfte Geräte, Leerzustand, Produktspalte, Alternativen-Dialog |
| Stripe | Zahlung gelingt | `state.stripeFail` falsch | Abo aktiv |
| Stripe | Abbruch | `state.stripeFail` wahr | Stripe-Abbruch |
| Bausteine | alles verfügbar, Copilot bedingt, Dock ohne Preis, Zubehör geprüfte Geräte nicht verfügbar | `state.bstMode` | Bausteinzeile |
| Ansicht | Desktop, Mobil | `.desk` oder `.phone`, Schirmbreite gemessen 1398 und 372 px | Breakpoints, Hero |

