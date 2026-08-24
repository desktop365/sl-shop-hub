# Design-Auftrag: Startseite SL Shop (surface.love und lenovo.online)

Du bist Claude Design. Dein Auftrag: gestalte die Startseite unseres B2B-Shops auf dem Niveau von
microsoft.com/de-de/surface, mit echten Videos und Bildern (URLs unten), als interaktiven
HTML-Prototyp. Ein bestehender Prototyp (slshopv2-prototyp.html, angehängt) liefert Struktur,
Logik und Token-System. Er ist funktional korrekt, aber gestalterisch noch nicht auf
Microsoft-Niveau. Geh gestalterisch drüber und heb ihn auf Premium-Qualität.

---

## 1. Kontext: wer wir sind und was verkauft wird

SL Deutschland GmbH aus Dresden vermietet und verleast Microsoft-Surface-Hardware an deutsche
Geschäftskunden (B2B, "Surface as a Service"). Es gibt zwei Vertriebswege ("Lanes"):

1. **Neugeräte**: der Kunde konfiguriert ein Gerät und stellt eine unverbindliche Anfrage.
   Kein Online-Kauf, kein Warenkorb-Checkout mit Zahlung. Das Angebot kommt per E-Mail
   (Leasing oder Finanzierung über eine Bank).
2. **Refurbished-Geräte**: geprüfte Rückläufer, sofort online als Abo abschließbar
   (Stripe, monatlich kündbar oder mit Laufzeit).

Eine Plattform, zwei Einmarken-Storefronts, umgeschaltet ausschließlich über ein
`data-sf`-Attribut und CSS-Tokens:

- **surface.love**: die Hauptmarke, Microsoft-Surface-Sortiment
- **lenovo.online**: Platzhalter-Identität (Markenfreigabe offen), gleiche Komponenten,
  eigener Token-Satz, keinerlei Microsoft-Medien und keine echten Lenovo-Markenzeichen

Zielgruppe: Geschäftsführer und IT-Verantwortliche kleiner und mittlerer Unternehmen.
Tonalität: ruhig, premium, vertrauensbildend, deutsch, per Sie.

## 2. Was du anheben sollst (der eigentliche Design-Auftrag)

Der angehängte Prototyp setzt die Struktur bereits um. Dein Mehrwert:

- **Komposition und Rhythmus**: großzügigerer Weißraum, klarere vertikale Taktung der
  Sektionen, souveräne Typo-Hierarchie wie bei Microsoft (große, leichte Headlines,
  viel Luft, wenige Gewichte)
- **Hero-Bühne**: kinoreifer Auftritt mit dem echten Video, sauberem Scrim, präziser
  Textplatzierung, elegantem Einstiegs-Stagger
- **Video-Akkordeon**: das Herzstück. Weiche Crossfades, klare aktive Markierung,
  angenehme Aufklapp-Animation, mobil als sauberes Akkordeon
- **Mikro-Bewegung**: Scroll-Reveals, Hover-Zustände, Ratenzähler, alles orchestriert
  statt zufällig, nie verspielt
- **Mobile Exzellenz**: die Seite muss auf 390px genauso überzeugen wie auf 1300px
- **Zwei Marken, ein Code**: alles nur über die Tokens; ein Screenshot-Vergleich beider
  Marken muss identische Layouts bei komplett eigenem Charakter zeigen

Du darfst Abstände, Sektionsübergänge, Typografie-Feinheiten, Kartenproportionen und
Animationsdetails frei verbessern. Nicht verhandelbar sind die Invarianten in Abschnitt 5,
die Inhalte in Abschnitt 6 und die Medienregeln in Abschnitt 7.

## 3. Liefergegenstand

Ein einziger interaktiver HTML-Prototyp (eine Datei, kein Build-Schritt), der enthält:

- die komplette Startseite, scrollbar, mit allen Sektionen aus Abschnitt 6
- einen Umschalter Desktop/Mobil sowie einen Markenumschalter surface/lenovo
  (gern wie im angehängten Prototyp als schmale dunkle Werkzeugleiste außerhalb des Shops)
- beide Token-Sätze inline (Quelle: tokens.surface.css und tokens.lenovo.css, angehängt)
- die echten Microsoft-Medien (Abschnitt 7) in der Surface-Storefront, Szenen- oder
  Poster-Fallbacks in der Lenovo-Storefront

Optional als zweiter Schritt, falls Zeit bleibt: Katalog und Produktdetail im selben Stil.

## 4. Design-System (Kurzfassung, Details in DESIGN-V2.md im Anhang)

**Token-Namensraum `--sf-*`**, Komponenten kennen ausschließlich Variablen, nie Hex-Werte
oder Markennamen.

surface.love:
- Akzent gestuft: `--sf-accent` #00A3E0 (Marke, aktiver Schritt, Tints),
  `--sf-accent-strong` #007DB8 (Links, Raten, 4,5:1 auf Weiß),
  `--sf-action` #007DB8, Hover #006CA0 (Hauptaktion)
- Schrift: Segoe-UI-Stapel, Gewichte 300 (Display), 400 (Text), 600 (Betonung)
- Radien: 18px Karten, 12px klein, Pille für Buttons
- Eigenheit: das Herz-Logo (Herz mit Doppel-Herzschlag-Linie) pulst alle 3,5s dezent

lenovo.online (Platzhalter "Carbon und Karmin"):
- `--sf-accent` #D0342C, strong #A82519, warme Greige-Neutrale
- Schrift: Inter, Display 600 statt 300
- Radien: 12/8/10px, kein Logo-Puls (`--sf-pulse: 0s`)

Bewegung: eine Kurve `cubic-bezier(.2,.7,.3,1)`, drei Dauern 150/260/550ms,
`prefers-reduced-motion` schaltet alles ab (auch Video-Autoplay).

## 5. Unverrückbare Regeln (Invarianten)

1. Der Akzent hat genau drei Träger: aktiver Schritt, Monatsrate, Hauptaktion.
   Statuspunkte sind grün/bernstein/grau, nie Akzentfarbe.
2. Genau eine Hauptaktion (Primärbutton) pro Screen. Alle weiteren Aktionen sekundär
   (Outline, Glas-Button auf Video, Textlink mit Pfeil).
3. Preise: nur Monatsraten. Niemals Einkaufspreise, Verkaufspreise, Faktoren oder Margen.
   Netto prominent, Brutto als kleine Komfortzeile (netto mal 1,19). Format "74,90 €",
   Komma als Dezimaltrenner, "mtl. netto".
4. Laufzeiten verbindlich: Leasing 15/24/32/36 Monate, Finanzierung 15/24/36 Monate,
   Vorauswahl Leasing 36. Refurbished-Abo: flexibel (monatlich kündbar), 12, 24 Monate.
5. Surface-Logo ist ausschließlich das Herz mit Herzschlag-Linie. Der Schriftzug
   "Surface.Love" erscheint nur als Domain im Footer. Slogan "work love balance" klein.
6. Lenovo-Storefront: keine echten Lenovo-Logos oder -Schriftzüge, neutraler
   Platzhalter (Quadrat mit Strich genügt), und keinerlei Microsoft-Videos oder -Bilder.
7. Telefon: sichtbar als "0800-SURFACE", die echten Ziffern 0800 7873223 gleiten erst
   bei Hover auf, der Link wählt tel:+498007873223. Lenovo: "0800 000 0000" als Dummy.
8. Mobil (unter 760px) gibt es eine feststehende Bottom-Bar: Telefon, "Gerät anfragen"
   (Hauptaktion), Anfragekorb.
9. Sprache: Deutsch, echte Umlaute, sentence case (keine Versalien-Headlines), keine
   langen Gedankenstriche im UI-Text (Kommas oder kurze Bindestriche verwenden).
10. Footerpflicht: Hinweis "Angebot richtet sich an Unternehmer im Sinne des § 14 BGB",
    Links Impressum, Datenschutz, AGB, Widerruf, Markenhinweise, Kontakt sales@surface.love.
11. Barrierefreiheit: Fokusringe, aria-Labels an Icon-Buttons und der Video-Steuerung,
    Kontrast mindestens 4,5:1 für Text, Video nie als einziger Informationsträger.

## 6. Aufbau der Startseite (Reihenfolge fest, Gestaltung frei)

1. **Header**, sticky, leichtes Blur: Logo (Herz), Navigation (Katalog, Refurbished,
   So funktioniert es, Kontakt), Telefon-Vanity, ab 900px Primärbutton "Gerät anfragen",
   Anfragekorb-Icon mit Zähler.
2. **Hero mit Vollbild-Video** (Medium 7.1): Scrim von links und unten, darauf
   Eyebrow-Pille "Surface as a Service", Headline "Surface für Ihr Team, zur Monatsrate.",
   Subline "Neue Geräte konfigurieren und unverbindlich anfragen, geprüfte refurbished
   Geräte sofort im Abo. Planbare Kosten statt Investition.", Buttons "Gerät auswählen"
   (primär) und "So funktioniert es" (Glas), Vertrauenszeile (Für Geschäftskunden,
   Monatsrate statt Investition, Austausch bei Defekt), Pause/Play-Knopf unten rechts.
   Lenovo-Texte: "Business-Notebooks zur Monatsrate." und sinngemäße Subline.
3. **"Gemacht für Ihren Arbeitstag"**: vier Hochformat-Videokarten 4:5 (Medien 7.2),
   darunter Titel und Kurztext:
   - Von Anfang an sicher: Geräte kommen vorkonfiguriert, Sicherheit läuft im Hintergrund mit.
   - Den ganzen Tag mobil: leicht, leise, mit Akku für den ganzen Arbeitstag.
   - Schnell bei jeder Aufgabe: Tabs, Calls und KI laufen flüssig nebeneinander.
   - Immer kamerafertig: Meetings mit automatischem Licht, ohne Störgeräusche.
4. **"Finden Sie Ihr Gerät"**: vier Familienkarten mit ab-Rate und Link "Ansehen":
   Laptops (ab 74,90 €), 2 in 1 (ab 79,90 €), Zubehör (ab 4,90 €), Refurbished im Abo
   (ab 27,90 €, grünes Refurbished-Badge). Lenovo: 66,90 / 76,90 / 4,90 / 23,90.
5. **Video-Akkordeon "Ein Gerät, alles drin"** (Medien 7.3): Bühne 5:4 mit Crossfade,
   daneben vier Punkte, aktiver Punkt mit Ink-Markierung links und aufklappendem Text,
   nur das aktive Video läuft:
   - Dateien schneller finden: beschreiben statt suchen, die Suche findet Dokumente und Bilder per KI.
   - Alle Apps Ihres Teams: Microsoft 365, Branchensoftware und mehr, sofort startklar.
   - Inhalte mit KI erstellen: Entwürfe, Bilder und Texte direkt auf dem Gerät.
   - Auch nach Feierabend: ein Gerät für Arbeit und Zuhause, vom Meeting bis zum Spiel.
6. **"Das Sorglos-Paket"**: vier Vorteilskacheln mit Icon:
   Liquidität geschont / Rundum sorglos / Immer KI-fähig / Skalierbar
   (Texte im angehängten Prototyp, unverändert übernehmen).
7. **Geräte-Spotlight** auf grauer Fläche: großes Gerät, "Surface Laptop 5",
   "ab 74,90 € mtl. netto, unverbindlich", Sekundärbutton "Zum Gerät".
   Lenovo: "Business Notebook 14", ab 66,90 €.
8. **Refurbished-Split**: Bild links (Medium 7.4 oder Szene), rechts Badge Refurbished,
   "Sofort im Abo", Beschreibung, "ab 29,90 € mtl. netto im Abo", Link "Abo entdecken".
9. **Kundenzitat**, zentriert: "Ausgerollt in einer Woche, seitdem einfach Ruhe im
   Betrieb." Geschäftsführung, Agentur aus Dresden.
10. **Footer**: Logo, Kurzbeschreibung, Kontakt (Vanity-Nummer, sales@surface.love),
    Spalten Shop und Rechtliches, Basiszeile mit Domain und § 14 BGB-Hinweis.
11. **Mobile Bottom-Bar** (nur unter 760px), siehe Invariante 8.

## 7. Medien: echte Microsoft-Videos und -Bilder (Referenz, vor Livegang ersetzen)

Alle folgenden Assets stammen von microsoft.com/de-de/surface (Contentful-CDN, öffentlich
erreichbar) und werden im Prototyp direkt per URL eingebunden. Sie sind Microsoft-Material
und dienen nur der internen Designabnahme. Jeder Slot trägt eine kleine sichtbare
Beschriftung "Referenz Microsoft, vor Livegang ersetzen". In der Lenovo-Storefront dürfen
sie nicht erscheinen, dort greifen die gestalteten Szenen-Platzhalter aus dem Prototyp
oder neutrale Flächen.

Wiedergaberegeln: muted, loop, playsinline, preload metadata, object-fit cover. Autoplay
nur im Hero. Alle anderen Videos starten und pausieren per IntersectionObserver bei
Sichtbarkeit, im Akkordeon läuft nur die aktive Ebene. prefers-reduced-motion: kein
Autoplay, Poster zeigen. Bei Ladefehler tauscht der Slot automatisch auf den Fallback.

### 7.1 Hero (16:9)
Video:
https://videos.ctfassets.net/jy9s7k22hbg4/55HlSYKd6rt82zVC87JShZ/28866452787f1c73420c3638c64e4997/MSFT-Surface_Hero_Desktop_Multi_1920x1080-17.mp4
Poster:
https://images.ctfassets.net/jy9s7k22hbg4/bPyR4d56RSSOiaVbkcwg3/a9a5b18703f0cf9433588f1c02d11c50/MSFT-Surface_Hero_Desktop_Multi_3840x2160_Poster_17.jpg

### 7.2 Videokarten (4:5, Reihenfolge wie Abschnitt 6.3)
1. Sicher:
https://videos.ctfassets.net/jy9s7k22hbg4/3uJ8YTmOFRWmLIDxLM4c2D/cafe4dd1328055bab59f7646a7698841/COM_303_Always_protected_Emerald-1080x1350.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/4KFwSBHBVD7iWD4cbM65Zo/37b7ad8825e890b9d102cfe3d00a15d9/COM_303_Always_protected_Emerald_Poster-1080x1350.jpg
2. Mobil:
https://videos.ctfassets.net/jy9s7k22hbg4/6vaShuDdPFvBKulmHMA6Bw/ad16f13cc34f351d3266531aab79bd6e/COM_302_Stay_Unplugged_Black-1080x1350.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/2tMNF3EhSZ7HP0ybPQArpZ/a5889c500fed15f28bbf34f50beed6d5/COM_302_Stay_Unplugged_Black_Poster-1080x1350.jpg
3. Schnell:
https://videos.ctfassets.net/jy9s7k22hbg4/6MunHX2roathEaKZaVxkZ9/2d4683f1a2c58622ffeaa0ae33712971/COM_301_Multitasking_Emerald-1080x1350.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/22kqtXWEE2840Sd2CmGxaX/d3ad03e30d93ac12b38be42ef6c7cab6/COM_301_Multitasking_Emerald_Poster-1080x1350.jpg
4. Kamera:
https://videos.ctfassets.net/jy9s7k22hbg4/2F3Sw8jjhmFfcGVJQ6wemY/fa1a820a1a0e234bf4a74c8de57dc419/COM_304_Camera_Desktop-1080x1350.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/1213RO4ZOBgJgPeiZPn2YY/53d0691d3061c1828ef07945460db6be/COM_304_Camera_Desktop_Poster-1080x1350.jpg

### 7.3 Video-Akkordeon (5:4, Reihenfolge wie Abschnitt 6.5)
1. Suche:
https://videos.ctfassets.net/jy9s7k22hbg4/HzF11t6MQfREHq3UDGjNU/ad57b3b11b226f9bd5e13d2c398efa0d/MSFT-Accordian-Search-Desktop-1680x1344.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/6gZboUm7gvFitbD42cXywe/7bccc502a2713fe7edb3e2b460c9cbd6/MSFT-Accordian-Search-Mobile-Poster-996x1660.jpg
2. Apps:
https://videos.ctfassets.net/jy9s7k22hbg4/7601rcAH1zGpIsU73QgsGz/8baff2e00b4d3bd2fde9bff973e2db0a/msft_Accordian_All_Your_Apps_Desktop-1680x1344.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/2dTuhsNOXx6j7iaBP1jpub/a6f8f2b9b904154912680d6ff069a848/msft_Accordian_All_Your_Apps_Mobile_Poster-996x1344.jpg
3. KI/Cocreator:
https://videos.ctfassets.net/jy9s7k22hbg4/1LNcACGi94NkpiWyjjBeZt/88023630b294c3c64b00086faa5d2ec7/COM_401_Accordian_Cocreator_Desktop-1680x1344.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/3UXOnu5cB83mu2v0WBYiZc/ce11f8bd1e727f1db71c229c7f96223f/COM_403_Accordian_Cocreator_Mobile_Poster-996x1660.jpg
4. Feierabend/Gaming:
https://videos.ctfassets.net/jy9s7k22hbg4/2ZgkXxy4kkVBWlh6JAXydV/ca04cbdb60858260dc0fe6b951d1f7cf/msft-COM_404_Gaming_Dune_Desktop-1680x1344.mp4
Poster: https://images.ctfassets.net/jy9s7k22hbg4/3J0pvd7Mmdtp0feKICoSAa/a4cba025b03f744c06377152619ef564/COM_404_Gaming_Dune_Mobile_Poster-996x1660-14.jpg

### 7.4 Weitere Bildflächen
Für Refurbished-Split und sonstige Bildflächen entweder die Poster aus 7.2 wiederverwenden
oder die Szenen-Platzhalter aus dem angehängten Prototyp übernehmen. Keine weiteren
Fremdquellen einbinden.

## 8. Abnahmekriterien

1. Beide Marken rendern fehlerfrei aus demselben Markup, Umschalten nur über `data-sf`.
2. Genau ein Primärbutton pro Ansicht, Akzent nur auf den drei erlaubten Trägern.
3. Hero-Video läuft automatisch (stumm), Pause-Knopf funktioniert, Akkordeon wechselt
   Video und Text, Karten-Videos spielen nur im Sichtbereich.
4. prefers-reduced-motion: keine Bewegung, keine Autoplay-Videos, Poster sichtbar.
5. 390px und 1300px sind beide gestalterisch überzeugend, Bottom-Bar nur mobil.
6. Alle Microsoft-Slots tragen die Referenz-Beschriftung.
7. Texte exakt wie in Abschnitt 6, deutsch, sentence case, ohne lange Gedankenstriche.

## 9. Anhänge zu diesem Auftrag

- slshopv2-prototyp.html (funktionierender V3-Prototyp als Ausgangsbasis)
- tokens.surface.css und tokens.lenovo.css (verbindliche Token-Sätze)
- DESIGN-V2.md (vollständige Designspezifikation mit Komponenten und Zuständen)

Wenn etwas im Widerspruch steht: dieses Briefing schlägt DESIGN-V2.md, DESIGN-V2.md
schlägt den Prototyp.
