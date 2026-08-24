# UX-Konzept: Produkt und Variante statt SKU-Katalog

Stand 24.08.2026, Grundlage für Prototyp V4 (`slshopv4-prototyp.html`) und für Runde 2 mit
Claude Design. Ergänzt CLAUDE-DESIGN-BRIEF.md, bei Widerspruch gilt dieses Dokument.

## 1. Diagnose

Bisher (V3 und die erste Claude-Design-Runde) war der Shop SKU-zentriert: ein Katalog mit
Einzelgeräten (Surface Laptop 5, Surface Pro 9, Surface Go 4, ...), jede Karte eine fertige
Kombination, das Produktdetail mit einer einzelnen "Ausstattung"-Pillenreihe. Mit dem echten
Sortiment explodiert das: drei Produkte mal Displaygröße mal Farbe mal Prozessor mal RAM mal
SSD ergeben Dutzende Karten, und der Kunde soll die richtige erraten. Das überfrachtet und
verlagert die Denkarbeit zum Kunden.

Tatsächlich gibt es im Surface-Sortiment nur **drei Produkte**:

1. **Surface Pro**, das flexible 2 in 1
2. **Surface Laptop**, der Allrounder
3. **Surface Laptop Ultra**, maximale Leistung

Alles andere sind Varianten dieser drei. Genau so denken auch Microsoft und Apple: erst das
Produkt (eine Entscheidung nach Nutzungstyp), dann die Variante (wenige geführte Klicks).

## 2. Leitprinzipien

1. **Zwei Entscheidungen, klar getrennt.** Ebene 1: Welches Produkt passt zu mir? (drei
   Karten, positioniert nach Einsatz, nicht nach Technik.) Ebene 2: Welche Variante? (ein
   Konfigurator pro Produkt, alle Wahlen flach sichtbar, keine Dropdowns.)
2. **Kuratierte Ausstattungen statt Spec-Matrix.** RAM, SSD und Prozessor werden nicht
   einzeln abgefragt, sondern zu zwei bis drei benannten Stufen gebündelt (Essential,
   Advanced, Performance), jede mit einem Empfehlungssatz in Kundensprache ("Für E-Mail,
   Office und Microsoft 365" statt "16/256"). B2B-Entscheider denken in Mitarbeiterprofilen,
   nicht in RAM-Riegeln. Die volle Spezifikation steht als Nebenzeile dabei.
3. **Sinnvolle Vorauswahl überall.** Beim Öffnen des Konfigurators ist die beliebteste
   Variante bereits gewählt ("Beliebt"-Badge), die Rate sofort sichtbar. Der schnellste Weg
   ist null Klicks: öffnen, "In Anfrage übernehmen". Jede Änderung ist optional.
4. **Delta-Preise, der HaaS-Vorteil.** An jeder nicht gewählten Option steht die Differenz
   zur aktuellen Monatsrate ("+ 8,00 €", "− 5,50 €"), nie ein absoluter Preis. Bei
   Monatsraten sind Aufpreise psychologisch winzig, das ist unser stärkstes Argument und
   gehört in die Oberfläche.
5. **Adaptive Schritte.** Hat ein Produkt nur eine Displaygröße, erscheint der Schritt
   nicht. Das Layout fragt nur, was es fragen muss.
6. **Reihenfolge vom Sichtbaren zum Vertraglichen.** Größe, Farbe, Ausstattung, dann
   Vertragsart und Laufzeit, Menge, Zubehör, Rate. Erst das Gerät fühlen, dann rechnen.

## 3. Die Journey

**Ebene 1, Produktwahl ("Geräte", ersetzt den Katalog).** Drei große Karten mit Bild,
Einsatz-Claim und ab-Rate, dazu ein kompakter Vergleichsstreifen (Für wen, Display,
Ausstattung bis, ab-Rate) für die, die kurz abwägen wollen. Kein Karten-Grid aus SKUs mehr.
Startseite zeigt dieselben drei Karten als Sektion "Drei Geräte, alle Möglichkeiten".

**Ebene 2, Konfigurator (ersetzt das Produktdetail neu).** Links das Gerät (Bild wechselt
mit Farbe und Größe), rechts die Wahlen in fester Reihenfolge:
Größe (Kacheln mit Delta) → Farbe (Swatches, "inklusive") → Ausstattung (Stufenkarten mit
Empfehlungssatz, Spec-Zeile, Delta, "Beliebt") → Vertragsart (Leasing/Finanzierung) →
Laufzeit (15/24/32/36 bzw. 15/24/36) → Menge → "Dazu passend" (zwei, drei Add-ons mit
"+ X € mtl.") → Ratenfeld mit Aufschlüsselung (Gerät, Add-ons, mal n Geräte), netto groß,
brutto klein, Hauptaktion, darunter "Im Preis enthalten" mit der Schlusszeile "Ein
Ansprechpartner, ein Vertrag, eine Rate." (Signatur aus der Claude-Design-Runde, bleibt.)
Querverweis "Auch refurbished ab X €" ans Ende, nie markenübergreifend.

**Ebene 3, Anfrage.** Unverändert der Wizard; Positionen heißen jetzt Produkt plus
Variantenzeile ("Surface Laptop, 13,8", Advanced, Leasing, 36 Monate").

**Refurbished bleibt eine eigene, noch einfachere Strecke.** Refurbished hat keine freie
Konfiguration: was auf Lager ist, ist konfiguriert. Also Wahl aus konkreten verfügbaren
Geräten (Karte mit Spezifikation und Zustand), dann Abo-Modell (Flexibel/12/24), Menge,
Abo starten. Querverweis "Als Neugerät konfigurieren".

## 4. Was das für Daten und Systeme heißt

- **Kein neues Pricing.** Die Azure-Pipeline liefert weiter Raten je MSKU und
  Vertragsart/Laufzeit in products.json. Neu ist nur eine kuratierte Zuordnungsebene im
  Katalog-Read-Model (App-Postgres): MSKU → Produktfamilie, Größe, Farbe, Stufe
  (essential/advanced/performance) plus Empfehlungstext und "Beliebt"-Flag. Pflegbar als
  Overrides, agent-tauglich.
- **Die Bildmodell-Architektur passt exakt.** Bilder sind bereits nach Familie, Generation,
  Größe und Farbe organisiert (nicht pro SKU), also genau entlang der Konfigurator-Achsen.
  Farbwechsel im Konfigurator = Bildmodellwechsel aus images.json.
- **Stufen sind kuratiert, nicht berechnet.** Nicht jede lieferbare RAM/SSD-Kombination
  muss angeboten werden. Zwei bis drei Stufen pro Produkt und Größe reichen; Exoten bleiben
  "auf Anfrage" über Vertrieb. Das ist eine Sortimentsentscheidung, die der Shop sichtbar
  macht, nicht versteckt.
- **HubSpot unberührt.** Anfragen tragen die aufgelöste MSKU plus lesbare Variantenzeile.

## 5. Was der V4-Prototyp zeigt

Tabs: Start, Geräte, Konfigurator, Refurbished Abo, Anfrage. Beide Marken, Desktop und
Mobil. Startseite bleibt die V3-Videoseite (Microsoft-Referenzen, gekennzeichnet), die
Sektion "Finden Sie Ihr Gerät" wird zu den drei Produktkarten. Der Konfigurator rechnet
live: Deltas an Größe und Stufe beziehen sich immer auf die aktuelle Auswahl samt
Vertragsart und Laufzeit, die Rate zählt beim Wechsel, das Feld pulst einmal. Lenovo läuft
mit denselben Komponenten und eigenen Familien (Business Notebook, Convertible,
Workstation). Zwei Higgsfield-Motive aus Runde 2 (Lounge, ICE) sind als eigenes Material
eingebunden und so beschriftet, als erster Schritt weg von den Microsoft-Referenzen.

Demo-Annahmen im Prototyp, vor Übernahme zu ersetzen: Stufen-Specs, Größen- und
Stufen-Aufpreise, Farbpaletten sowie die Laufzeitfaktoren (aus der bekannten
74,90er-Reihe abgeleitet). Echte Werte kommen aus products.json.

## 6. Auftrag Runde 2 an Claude Design

Grundlage: CLAUDE-DESIGN-BRIEF.md (Invarianten und Medien gelten unverändert) plus dieses
Dokument plus `slshopv4-prototyp.html` als verbindliches UX-Gerüst.

1. Nicht mehr gestalten: SKU-Katalog, Produktdetail mit Ausstattungs-Pillen. Diese
   Screens entfallen ersatzlos zugunsten von Geräte-Übersicht und Konfigurator.
2. Gestalterisch anheben: die drei Produktkarten (Ebene 1) als markanter Moment der Seite,
   der Konfigurator als ruhige, geführte Strecke (Wahlgruppen klar getaktet, Gerät links
   präsent und farblich live), das Ratenfeld als typografischer Held.
3. Beibehalten aus eurer Runde 1: Add-on-Zeilen, "Im Preis enthalten" mit Schlusszeile,
   Korb-Persistenz, Wizard-Feinheiten, leerer Korb als Einladung.
4. Abnahme zusätzlich zu den bisherigen Kriterien: von "Geräte" bis zur sichtbaren
   Wunschrate sind es höchstens vier Klicks (Produkt, Größe, Stufe, Laufzeit), und null
   Klicks führen zu einer gültigen, beliebten Vorauswahl.
