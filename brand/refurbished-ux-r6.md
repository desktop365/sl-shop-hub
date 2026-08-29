# Refurbished-UX r6, Konzept und Design-Auftrag

Strom 50, Stand 2026-08-29 (angepasst an contracts/REFURBISHED.md vom
28.08., der Kontrakt schlägt dieses Dokument). Grundlage: Auftrag des
Masters vom 28.08. (sechs
Bausteine, entschieden von Sascha), 90-REFURBISHED_v3 (HubSpot ist
Bestands-Master, Leseabbild je Typ, Rückschreiben der Statuswechsel),
UX-VARIANTEN-KONZEPT.md, contracts/VARIANTEN.md, contracts/SICHTBARKEIT.md,
E-014, E-015, E-016, E-019, E-032, E-034, E-037. Teil A ist das UX-Konzept,
Teil B der Umsetzungsauftrag an Claude Design. Ergebnisdatei laut E-032:
brand/slshopv6-prototyp.html.

Alle Zahlen in diesem Dokument (Raten, Kaufpreise, Schwellen) sind
Demo-Annahmen und im Prototyp sichtbar als Demo zu kennzeichnen. Echte Raten
kommen aus dem HubSpot-Leseabbild (r8), nie aus dem Markup (E-016 sinngemäß).

---

## Teil A, das UX-Konzept

### 1. Grundhaltung

Refurbished ist die zweite Spur des Shops: sofort verfügbar, online
abschließbar, ehrlich gebraucht. Sie ergänzt die Neugeräte-Spur, sie
konkurriert nicht mit ihr. Deshalb gilt überall: Refurbished spricht leise
(typografisch sekundär, nie Akzentfarbe, maximal ein Berührungspunkt je
Bildschirm) und hält, was es sagt (jede Zeile erscheint nur, wenn das
Leseabbild echten Bestand kennt).

### 2. Der Bestand als UX-Gegenstand

Sieben Lagervarianten ("Typen"), Bestand vom 28.08., Quelle
SL_Geraetebestand_Shop:

| Typ | Reihe | Größenklasse | Bestand |
|---|---|---|---|
| Surface Laptop 5, 15" | laptop | gross | 125 |
| Surface Laptop 5, 13,5" | laptop | kompakt | 7 |
| Surface Laptop 4, 15", 256 GB | laptop | gross | 31 |
| Surface Laptop 4, 15", 512 GB | laptop | gross | 4 |
| Surface Pro 9 | pro | kompakt | 33 |
| Surface Pro 8 | pro | kompakt | 17 |
| Surface Pro 8, 32 GB | pro | kompakt | 1 |

Dazu Zubehör-Bundles (einstufig laut VARIANTEN.md): Dock 2, Surface Pen,
Netzteil, ausschließlich als Zumietposition auf der Refurb-Produktseite.

Die Größenklasse (kompakt, gross) ist ein Kurations-Datum je Typ und je
Neugeräte-Familie. Sie ist der Matching-Schlüssel zwischen den Spuren:
Surface Laptop 13,8" neu matcht Laptop 13,5" refurbished, 15" matcht 15",
jede Pro-Größe matcht die Pro-Typen (es gibt nur kompakte Pros), das Ultra
matcht nichts. Nie exakte Zollwerte vergleichen, die Klassen entscheiden.

Verfügbarkeit je Typ kommt aggregiert aus dem HubSpot-Leseabbild
(bestand_verfuegbar = Anzahl Geräte im Status verfügbar). Vier
Anzeigezustände, Schwelle als Konfigwert (Vorschlag knapp bei 5 oder
weniger), nie im Code:

- **verfügbar** (Bestand über Schwelle): grüner Statuspunkt, "sofort
  verfügbar". Keine Zahl, keine Dringlichkeit.
- **knapp** (1 < Bestand <= Schwelle): bernsteinfarbener Punkt, "nur noch
  n verfügbar". Ehrliche Information, kein Countdown, kein Drängeln.
- **Einzelstück** (Bestand 1): bernstein, "Einzelstück". Betrifft real den
  Pro 8 mit 32 GB.
- **vergriffen** (Bestand 0): der Typ erscheint nicht mehr im Katalog
  (Entscheidung Sascha, Sketch-Review 28.08.). Refurbished ist eine eigene
  Spur mit endlichem physischem Bestand, SICHTBARKEIT.md bindet nur die
  Neugeräte-Spur. Zwei Schutzdetails: das Ausblenden greift gedämpft, der
  Bestand muss eine konfigurierbare Zeit stabil null sein (Vorschlag 60
  Minuten), nie Verschwinden live vor den Augen des Nutzers. Und die
  Produktseite bleibt per Direktlink erreichbar, zeigt dann grauen Punkt
  und "derzeit vergriffen" mit den Wegen zurück zum Katalog und "Als
  Neugerät konfigurieren", Deep-Links und Race-Fälle aus dem Amazon-Moment
  laufen nie ins Leere.

Kategorie ganz leer: Katalog zeigt einen ruhigen Leerzustand ("Gerade ist
alles vermietet. Neue Geräte konfigurieren Sie ab X € im Monat.") mit Weg in
den Konfigurator. Startseiten-Band, Amazon-Moment und Alternativen-Ergänzung
verschwinden dann automatisch, weil ihre Anzeigebedingung (Bestand > 0)
nicht mehr erfüllt ist. Es gibt keinen Zustand, in dem der Shop Refurbished
verspricht und nichts liefern kann.

### 3. Die sechs Bausteine

**Baustein 1, Refurbished-Katalog.** Eigene Seite, Navigationspunkt
"Refurbished" im Header zeigt hierher. Kopf: "Refurbished, sofort
verfügbar" mit Subzeile (geprüfte Geräte aus Rückläufern, monatlich mietbar,
Versand inklusive). Zwei Gruppen, Surface Laptop und Surface Pro, darin
Typkarten: Microsoft-Standardbild des Bildmodells (E-019) mit grünem
Refurbished-Badge und kleiner Kennzeichnung "Symbolbild der Reihe,
Lieferung als geprüftes Gebrauchtgerät", Name in Kundensprache, Spec-Zeile,
Zustandsklasse als Ink-Pille ("Zustand sehr gut" oder "Zustand gut", finale
Klassen folgen mit REFURBISHED.md), Verfügbarkeitszeile nach dem
Zustandsmodell oben, Monatsrate "X € mtl. netto" (eine Rate je Typ, die
kleinste echte Monatsrate aus dem Leseabbild, REFURBISHED.md),
Weg zur Produktseite. Sortierung: Rate aufsteigend; vergriffene Typen
erscheinen nicht im Katalog (siehe Zustandsmodell, gedämpftes Ausblenden). Unter den Geräten eine schmale Zubehör-Zeile (Dock 2,
Pen, Netzteil, "im Abo dazu buchbar, Auswahl auf der Geräteseite"), ohne
eigene Karten-Bühne.

**Baustein 2, der Amazon-Moment im Konfigurator.** Unterhalb des
Ratenfelds, nach der "Im Preis enthalten"-Liste, eine einzelne Textzeile:
"Auch refurbished ab X € im Monat, sofort verfügbar". Anzeigebedingung:
das Leseabbild kennt mindestens einen Typ gleicher Reihe und Größenklasse
mit Bestand größer null. X ist die günstigste Monatsrate über alle
passenden Typen. Ein Klick führt zur Produktseite des günstigsten passenden
Typs. Typografie: sekundäre Textfarbe, Link in Ink mit Pfeil, ausdrücklich
NICHT die Akzentfarbe und nicht die Standard-Linkfarbe accent-strong. Diese
Zeile ersetzt den bisherigen pauschalen Refurb-Querverweis des Konfigurators
und ist dessen einziger Refurb-Berührungspunkt. Wechselt der Nutzer Familie
oder Größe, wird die Bedingung neu ausgewertet, die Zeile erscheint und
verschwindet ohne Layoutsprung (fester Platz, leere Höhe kollabiert weich).

**Baustein 3, Refurbished im Alternativen-Moment.** Der späte Check der
Anfrage-Strecke (SICHTBARKEIT.md, E-014, E-037) bleibt unverändert: bis zu
drei Neu-Alternativen derselben Reihe, Rangfolge Farbe (bedingt), Speicher
aufwärts, zuletzt Prozessor und Größe. NEU als vierte, klar abgesetzte
Ebene darunter: genau EIN lagernder Refurb-Typ gleicher Reihe und
Größenklasse, unter einer Trennlinie mit dem Label "Sofort verfügbar,
refurbished", mit Zustand, Rate und dem Weg "Refurbished ansehen".
Wichtige Mechanik-Wahrheit: die Neu-Alternativen sind per Klick in die
Anfrage übernehmbar, das Refurb-Angebot ist es NICHT, denn es lebt in einer
anderen Vertragswelt (Stripe-Abo statt unverbindlicher Anfrage). Der Klick
öffnet die Refurb-Produktseite, der Anfragekorb bleibt vollständig erhalten,
der Rückweg in die Anfrage bleibt offen. Das wird dem Nutzer nicht erklärt,
es verhält sich einfach so. Diese Ergänzung erweitert SICHTBARKEIT.md um
eine Stufe, die Kontraktänderung formuliert der Master (Vorschlag im
EINGANG-50 vom 28.08.).

**Baustein 4, die Rückrichtung.** Jede Refurb-Produktseite trägt am Ende
des Konfigurationsbereichs eine ruhige Zeile: "Als Neugerät mit Vollgarantie
ab Y € im Monat", Y ist die günstigste Neugeräte-Rate derselben Reihe und
Größenklasse aus products.json (Leasing 36, dynamisch, E-016). Der Klick
öffnet den Konfigurator der Familie mit passender Größen-Vorauswahl. Auch
diese Zeile ist sekundär gesetzt, der Aufstiegspfad ist sichtbar, er
schreit nicht.

**Baustein 5, die Startseiten-Fläche.** Direkt unterhalb der drei
Familienkarten ein schmales, ruhiges Band auf Flächenfarbe: grüner
Statuspunkt, "Sofort verfügbar: Refurbished ab 29,90 € im Monat", rechts
der Weg "Refurbished entdecken". Kein Kartenformat, keine Bildbühne, keine
Konkurrenz zu den drei Hauptkarten. Die 29,90 sind die von Sascha gesetzte
Zielrate des günstigsten Geräts und kommen produktiv als kleinste Rate aus
dem Leseabbild, im Prototyp als Demo gekennzeichnet. Anzeigebedingung:
Gesamtbestand größer null. KONSEQUENZ der Ein-Berührungspunkt-Regel: die
bisherige große Refurbished-Split-Sektion weiter unten auf der Startseite
entfällt ersatzlos, ihre Bildfläche (Higgsfield ICE) wird zur neutralen
Service-Sektion ohne Refurb-Bezug umgewidmet oder gestrichen. Auf der
Geräte-Seite bleibt die bestehende Refurbished-Lane als deren einziger
Berührungspunkt bestehen.

**Baustein 6, die Kasse.** Eigenständige Refurb-Kasse in drei Schritten,
getrennt vom Anfrage-Wizard der Neugeräte.

1. Übersicht: Positionszeilen (Gerät mit Zustand und Abo-Modell, Menge,
   Zubehör-Zeilen), Summe mtl. netto groß, brutto klein. Bei gewählter
   Kauf-Option stattdessen die Einmalsumme netto plus brutto.
2. Firmendaten: Firma, Name, E-Mail, Telefon optional, Lieferadresse,
   USt-IdNr optional, Bestätigung "Ich handle als Unternehmer im Sinne des
   § 14 BGB", AGB und Datenschutz, optionaler Consent für Herkunfts-Tracking
   (90_v3, DSGVO).
3. Übergabe: eine Hauptaktion "Weiter zur sicheren Zahlung", Mikrozeile
   "Sichere Zahlung über Stripe, monatliche Rechnung". Ladezustand "Wird an
   Stripe übergeben".

Reservierungslogik (REFURBISHED.md Abschnitt 4): erst der Klick auf die
Übergabe reserviert die Stückzahl im Bestands-Master, nicht schon das
Betreten der Kasse, damit Bummler nichts blockieren. Das ist unsere
Lesart von "Checkout-Start" im Kontrakt; legt der Master den Begriff
anders aus, gilt der Kontrakt. Die Reservierung verfällt nach einer
Frist (Konfigwert, Kontrakt-Startwert 30 Minuten), Zahlung setzt
vermietet, Abbruch oder Fristablauf gibt frei. Unmittelbar vor der
Reservierung läuft der späte Bestands-Check: reicht der Bestand für die
gewählte Menge nicht mehr, erscheint ein ehrlicher Dialog ("Gerade wurden
Geräte vermietet, verfügbar sind noch n") mit drei Wegen: Menge anpassen,
anderen Refurb-Typ wählen (Katalog), als Neugerät anfragen. Nach Stripe:
Erfolgsseite mit Abo-Bestätigung, Versandausblick und dem Hinweis, dass die
Rechnung monatlich kommt; Abbruchseite mit ruhigem Wiedereinstieg, ohne
Druck. Die Kasse ist in beide Richtungen werbefrei: kein Refurb-Hinweis im
Neugeräte-Checkout (Schutzregel), kein Neugeräte-Hinweis in der
Refurb-Kasse, dort zählt nur der Abschluss.

Kauf als stille Option: ausschließlich auf der Refurb-Produktseite, als
zugeklappter Ausklapper "Einmalig kaufen statt mieten" unterhalb des
Ratenfelds. Zugeklappt ist kein Preis sichtbar. Aufgeklappt: Kaufpreis
netto (Angebotsdatum, erlaubt laut 90_v3), Gewährleistungshinweis,
sekundäre Aktion "Zur Kasse mit Kaufpreis". In Teasern, Querverweisen,
Katalogkarten, Startseite und Konfigurator erscheint niemals ein Kaufpreis,
und es gibt keine Gegenüberstellung von Miete und Kauf als Tabelle.

### 4. Fokus-Schutz, operationalisiert

1. Refurb-Hinweise auf Neugeräte-Flächen (Startseiten-Band, Amazon-Moment,
   Alternativen-Ergänzung, Geräte-Lane) nutzen ausschließlich Ink und
   sekundäre Textfarben. Die Akzentfarbe behält ihre drei Träger (aktiver
   Schritt, Rate, Hauptaktion) und färbt nie einen Refurb-Hinweis, auch
   nicht als Linkfarbe. Das grüne Refurbished-Badge und die Statuspunkte
   sind Statusfarben und bleiben erlaubt.
2. Je Bildschirm höchstens ein Refurb-Berührungspunkt: Startseite das Band
   (der alte Split entfällt), Geräte-Seite die Lane, Konfigurator die
   Amazon-Zeile, Alternativen-Dialog der eine Refurb-Block. Auf
   Refurb-eigenen Seiten zählt die Rückrichtung als Neu-Hinweis und ist
   dort ebenfalls genau einmal vorhanden.
3. Der Neugeräte-Anfrage-Wizard (Schritte Übersicht und Kontakt) ist
   vollständig refurb-frei.
4. Keine Preisvergleiche neu gegen refurbished, nirgends, auch nicht
   implizit durch nebeneinandergestellte Raten.
5. Alle Raten dynamisch aus dem Leseabbild beziehungsweise products.json,
   Demo-Daten im Prototyp sichtbar gekennzeichnet (Runde-2-Auflage 4).

### 5. Datenanforderung an r8 und r9 (zur Übergabe an Strom 10 und 20)

Das Leseabbild muss je Typ liefern: typ_id, reihe, groessenklasse,
anzeige_name, spec_zeile, zustandsklasse, bestand_verfuegbar, monatsrate
(eine je Typ, die kleinste echte Monatsrate, gesetzt von Sascha als
Konfigurationsdatum), optional
kauf_vk_netto, bildmodell_ref (Brücke zur Bildmatrix aus Strom 40). Dazu
zwei Steuerwerte: knappheits_schwelle, reservierungs_frist_minuten. Für den
Amazon-Moment und die Rückrichtung braucht der Shop zusätzlich die
Größenklassen-Zuordnung der Neugeräte-Familien als Kurations-Datum (E-015,
Zuordnungsschicht aus VARIANTEN.md).

---

## Teil B, Umsetzungsauftrag an Claude Design (Runde r6)

Grundlage: brand/slshopv5-prototyp.html als Basis, dieses Dokument als
verbindliches UX-Gerüst, CLAUDE-DESIGN-BRIEF.md für Tokens und Invarianten.
Ergebnis: brand/slshopv6-prototyp.html (Versionsschema E-032), beide Marken
aus demselben Markup, Desktop und 390px.

Zu bauen oder zu ändern:

1. NEU Refurbished-Katalogseite nach Teil A Baustein 1, mit den sieben
   echten Typen und den echten Beständen (125, 7, 31, 4, 33, 17, 1) als
   Demo-Datensatz, Raten als Demo gekennzeichnet.
2. ÜBERARBEITET Refurbished-Produktseite: KEINE Abo-Modell-Wahl mehr,
   stattdessen eine Konditionszeile nach REFURBISHED.md ("Mindestlaufzeit
   6 Monate, danach monatlich kündbar, Kündigungsfrist 1 Monat zum
   Monatsende") und eine Monatsrate je Typ. Dazu Verfügbarkeitszeile nach
   dem Vier-Zustands-Modell, Mengen-Stepper mit Bestandsgrenze und Hinweis
   "maximal n verfügbar", Zubehör-Zeilen (Dock 2 + 4,90, Pen + 1,90,
   Netzteil + 0,90, Demo), Kauf-Ausklapper nach Baustein 6, Rückrichtungs-
   Zeile nach Baustein 4.
3. NEU Refurb-Kasse, drei Schritte plus Stripe-Übergabe-Mock, Erfolgs- und
   Abbruchseite, später Bestands-Check als Dialog mit den drei Wegen.
4. GEÄNDERT Konfigurator: Amazon-Moment-Zeile nach Baustein 2, bedingt
   sichtbar je Familie und Größe, eigene Linkklasse in Ink ohne Akzent.
5. GEÄNDERT Alternativen-Moment: Refurb-Block als vierte Ebene nach
   Baustein 3, mit Trennlinie und Label.
6. GEÄNDERT Startseite: Band unter den drei Familienkarten nach Baustein 5,
   der bisherige Refurbished-Split wird entfernt, die Bildsektion neutral
   umgewidmet.
7. NEU ein Demo-Schalter in der Werkzeugleiste des Prototyps, der die
   Bestandslage umschaltet (normal, knapp, Einzelstück-Fokus, ein Typ
   vergriffen, alles vergriffen), damit alle Zustände abnehmbar sind. Im
   Zustand "ein Typ vergriffen" fehlt dessen Karte im Katalog, seine
   Produktseite ist über den Schalter direkt aufrufbar und zeigt den
   Vergriffen-Zustand. Der Amazon-Moment bleibt in allen Zuständen eine
   reine Textzeile ohne Bild (bestätigt im Sketch-Review 28.08.).

Abnahmekriterien, zusätzlich zu den bestehenden aus Brief und Runde 2:

1. Kein Refurb-Hinweis trägt die Akzentfarbe, maschinell prüfbar: keine
   Refurb-Hinweis-Klasse verwendet --sf-accent oder --sf-accent-strong.
2. Je Bildschirm höchstens ein Refurb-Berührungspunkt, der Anfrage-Wizard
   und die Refurb-Kasse sind querverweisfrei.
3. Kaufpreise erscheinen ausschließlich im aufgeklappten Ausklapper der
   Produktseite.
4. Alle Zustände (verfügbar, knapp, Einzelstück, vergriffen, Kategorie
   leer) sind über den Demo-Schalter erreichbar und gestaltet. Vergriffene
   Typen fehlen im Katalog, ihre Produktseite zeigt den Vergriffen-Zustand,
   und nichts verschwindet mit Layoutsprung oder live vor den Augen des
   Nutzers.
5. Alle Demo-Zahlen tragen die Demo-Kennzeichnung, das Startseiten-Band
   zeigt 29,90 als Demo der Zielrate.
6. Beide Marken rendern fehlerfrei, die Lenovo-Storefront nutzt analoge
   Demo-Typen ohne Microsoft-Medien.
