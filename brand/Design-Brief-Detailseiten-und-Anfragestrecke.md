# Design-Brief, Detailseiten und Anfragestrecke

Für den Design-Chat. Das grundlegende Design steht bei dir bereits, Farben, Tokens, Herz, Typografie, die ruhige Premium-Anmutung. Dieser Brief liefert das, was dir fehlt, die Erfahrung aus dem Konfigurator und der Anfragestrecke, die wir im ersten Anlauf erarbeitet haben. Er beschreibt die funktionalen Module der Detailseiten und des Checkouts, die du jetzt fertig gestalten sollst. Nicht das große Ganze, sondern die Bausteine, Abläufe und Zustände darin.

## 0. Was steht, was dieser Brief ergänzt
Steht und bleibt unverändert: Designsprache, Cyan als einziger Akzent, Herz-Logo, Segoe-Stapel, die Tokens, das ruhige Premium-Gefühl.
Neu von dir zu gestalten: die Produktdetailseite mit Konfigurator, die Wahl von Vertragsart und Laufzeit, das Hinzufügen und Konfigurieren von Bundles, Zubehör, Software-Lizenzen und Services, die Darstellung des voll gemanagten Service, der mitlaufende Anfragekorb, und die Anfragestrecke bis zur Bestätigung.

## 1. Technischer Rahmen, damit dein Design baubar ist
Die App ist Next.js mit dem App Router, React in funktionalen Komponenten, TypeScript, Tailwind. Deine Designtokens leben als CSS-Variablen in brand/tokens.css, das Theming je Storefront, surface und lenovo, läuft über diese Variablen. Gestalte also mit Tokens, nicht mit festen Hex-Werten. Mehrsprachig über [locale], Deutsch aktiv, Englisch vorbereitet, alle Texte als Platzhalter für i18n. Katalog und Detailseite werden serverseitig gerendert, wegen SEO. Der Konfigurator und der Anfragekorb sind interaktiv im Browser, mit Live-Rate und mitlaufendem Korb, der auch nach einem Reload erhalten bleibt.

Wichtig zur Rate: der Browser rechnet keine Preise. Alle Raten kommen fertig aus products.json, je Vertragsart und Laufzeit. Der Konfigurator wählt nur aus und zeigt die passende gespeicherte Rate, und summiert die Add-ons zu einem unverbindlichen Monatswert. Es gibt keinen Rechner, der aus Einkauf oder Faktoren ableitet, das ist bewusst so.

Liefere so, dass Claude Code daraus React-Komponenten mit Tailwind bauen kann, komponentenweise, mit klaren Zuständen.

## 2. Die Leitidee, in einem Satz
Die ganze Seite ist ein Trichter zur unverbindlichen Anfrage, mit so wenig Klicks wie möglich und ohne Sackgasse, der Nutzer darf nie absterben. Verkauft wird nichts, es entsteht eine Anfrage. Über allem steht ein Versprechen, ein Ansprechpartner, ein Vertrag, eine Rate, alles voll verwaltet. Das ist der emotionale Kern, den deine Detailseiten und der Checkout tragen müssen.

Zwei Wege teilen sich die Strecke, halte beide im Blick. Neu, Konfiguration und dann Anfrage zur Bank, kein Sofortkauf, das ist der Hauptweg. Refurbished, geprüftes Gerät aus eigenem Bestand, direktes Abo über Stripe, Phase zwei, aber der Checkout muss diesen zweiten Ausgang kennen.

## 3. Die Module im Detail

### 3.1 Produktdetailseite
Der Ort, an dem aus Interesse eine Konfiguration wird.
- Bildgalerie, Hauptbild groß, darunter Vorschaubilder, weitere Ansichten je nach Gerät, offen, geschlossen, Rückseite, Anschlüsse, Stift. Die Bilder kommen aus images.json, ein Fotoset je Bildmodell, mit Fallback, falls ein Set fehlt. Gestalte auch den Fallback-Zustand würdig, nicht als Lücke.
- Kopf, der Anzeigename, der Hersteller, optionale Auszeichnungen wie Badge oder featured, ein kleiner Verfügbarkeitspunkt, grün verfügbar, bernstein im Zulauf, grau auf Anfrage, nie cyan. Prominent die Rate, ab X pro Monat, cyan, netto groß, brutto klein daneben, mit dem Wort unverbindlich.
- Spezifikationen kompakt, CPU, RAM, Speicher, Farbe, Bildschirmgröße, Generation, dazu dezente Kennzeichnungen wie 5G oder ohne Ladegerät, wo zutreffend.
- Der Konfigurator-Block, das Herz der Seite, siehe 3.2.
- Der Rundum-sorglos-Block kompakt eingebettet, siehe 3.7, damit der Kunde sofort begreift, dass die Rate alles trägt.
- Ein klarer Einstieg zu Add-ons, Zubehör, Software und Services hinzufügen, siehe 3.3 bis 3.6.
- Genau eine Hauptaktion, In Anfrage übernehmen, cyan gefüllt. Daneben höchstens ein dezenter zweiter Weg, weiter stöbern.
- Querverweis innerhalb der Marke, dasselbe Modell refurbished, ab Y sparen, oder umgekehrt der Aufstieg zum neuen Gerät. Nie markenübergreifend.
- Aktion, falls aktiv, als statt-jetzt, der Grundpreis bleibt sichtbar.

### 3.2 Konfigurator, Vertragsart und Laufzeit
Das zentrale Steuermodul. Es erscheint auf der Detailseite und im Wizard-Schritt Konfiguration, gleiches Verhalten.
- Vertragsart wählen, Leasing oder Finanzierung, als klarer Umschalter.
- Laufzeit wählen, bei Leasing 15, 24, 32, 36 Monate, bei Finanzierung 15, 24, 36 Monate. Nur die zur Vertragsart passenden Laufzeiten zeigen.
- Sinnvolle Vorauswahl, damit sofort eine Rate dasteht, der Nutzer muss nichts tun, um einen Preis zu sehen.
- Die Rate reagiert live auf jede Änderung, netto prominent, brutto sekundär, und zählt beim Umschalten sanft hoch, ruhig, nicht verspielt.
- Menge, falls mehrere Geräte, mit Auswirkung auf die Summe.
- Leasingfaktoren, Einkauf oder Verkauf erscheinen nirgends, damit sich der Verkaufspreis nicht zurückrechnen lässt. Nur fertige Monatsraten.
- Hauptaktion, In Anfrage übernehmen.

### 3.3 Bundles, das Konfigurieren
Ein Bundle ist das Gerät plus passende Ergänzungen, als geführtes Zusammenstellen. Zwei Spielarten, gestalte beide oder eine klare, die beide abdeckt.
- Vorgeschnürte Bundles, fertige Pakete, Gerät mit Tastatur, Stift, einer Lizenz, als auswählbare Option mit eigener Gesamtrate.
- Selbst zusammenstellen, das Gerät als Basis, dann Zubehör, Software und Services einzeln dazu.
Jede Ergänzung ist eine eigene Position mit eigener Monatsrate. Beim Hinzufügen aktualisiert sich der Anfragekorb und die unverbindliche Monatssumme. Optional und klar überspringbar, wer nur das Gerät will, kommt in einem Klick weiter.

### 3.4 Zubehör
Eine datengetriebene Liste passender Zubehörartikel, Tastaturen, Stifte, Docks, Mäuse. Je Artikel ein Bild, ein Name, eine Monatsrate, hinzufügen und entfernen, Menge. Dezente Kennzeichnung, was zum Gerät passt. Kein Warenkorb-Kauf, alles fließt in die Anfrage.

### 3.5 Software und Lizenzen
Microsoft-365-Lizenzen und weitere Software, datengetrieben, gleiches Ratenschema. Je Lizenz Name, kurze Erklärung, Rate je Platz, Anzahl der Plätze wählbar, hinzufügen und entfernen. Klar getrennt, Copilot+ PC ist die KI-fähige Hardware, Microsoft 365 Copilot ist die Software, verwechsle das im Text nie. Die Laufzeit sinnvoll an die Geräterate angelehnt.

### 3.6 Services
Verwaltete Zusatzleistungen als Positionen, etwa erweiterte Einrichtung, Versicherung, besonderer Support. Gleiche Darstellung, Name, kurze Erklärung, Rate, hinzufügen und entfernen. Der Grundservice ist immer enthalten, siehe 3.7, diese hier sind das Mehr obendrauf.

### 3.7 Gemanagter Service, die Rundum-sorglos-Darstellung
Das Alleinstellungsmerkmal, es muss überall spürbar sein, ohne zu erschlagen. Im Preis enthalten, kompakt als Leistungskacheln oder Häkchenliste, Beschaffung, Einrichtung, Rollout, Support, Reparatur und Austausch, optional Versicherung, am Laufzeitende Rückgabe oder Tausch auf die neue Generation. Die Botschaft, ein Ansprechpartner, ein Vertrag, eine Rate.
Auf der Detailseite kompakt, auf der eigenen Vorteilsseite ausführlich mit den vier Vorteilen, Liquidität und Planbarkeit, Rundum-sorglos, KI und Copilot, Skalierbarkeit und Nachhaltigkeit. Auf der Vorteilsseite Platz für einen späteren ROI-Rechner vorsehen, aber nicht bauen.

### 3.8 Anfragekorb
Immer präsent, nie versteckt. Am Desktop eine mitlaufende Karte rechts, am Handy eine fixe Leiste unten mit Anzahl, Summe und primärem Button. Inhalt, die Geräte mit Vertragsart, Laufzeit und Rate, die Add-ons mit Raten, Mengen änderbar, Positionen entfernbar. Die Summe als unverbindliche Monatsrate, netto prominent, brutto sekundär. Der Korb merkt sich alles, auch nach einem Reload. Aus dem Korb führt genau ein Weg weiter, zur Übersicht und zum Absenden.

### 3.9 Checkout, die Anfragestrecke
Vier sichtbare Schritte, mehr nicht, mit durchgehendem Indikator oben, der aktuelle cyan, erledigte mit Haken, anklickbar zum Zurück.
1. Gerät, aus Katalog oder Wizard.
2. Konfiguration, Vertragsart und Laufzeit, optional Zubehör, Software, Services.
3. Übersicht, der Anfragekorb als Seite.
4. Kontakt und Absenden, dann Bestätigung.
Der Kontaktschritt ist ein kurzes Formular, Pflicht nur Firma, Name und E-Mail, Telefon und Nachricht optional, DSGVO-Checkbox, das Turnstile-Widget, ein dezenter Geschäftskunden-Hinweis. Kein Konto, keine Zahlung im Neu-Weg. Eingabeprüfung direkt am Feld, keine Fehlerwände. Genau eine Hauptaktion, Anfrage senden.
Die Bestätigung zeigt die Anfrage-ID im Format SL-JJJJMMTT-XXXXXX und erklärt kurz, was als Nächstes passiert, dazu ein sanfter Weiterweg, weiter stöbern oder Kontakt. Der schnellste Pfad muss möglich bleiben, Gerät, In Anfrage übernehmen, Übersicht, Anfrage senden, kurzes Formular, fertig.

### 3.10 Refurbished-Weg, das Abo, Phase zwei mitdenken
Statt einer Anfrage schließt der Kunde hier direkt ein Abo ab, gezahlt über Stripe. Der Checkout muss diesen zweiten Ausgang kennen, auch wenn er erst in Phase zwei gebaut wird. Gestalte die Weiche mit, ein refurbished Gerät führt zu jetzt abonnieren und in die Stripe-Kasse, ein neues Gerät führt zur Anfrage. Zustand und Verfügbarkeit des einzelnen Geräts klar gekennzeichnet, geprüft, Zustandsstufe.

### 3.11 Zustände, das Unaufgeregte richtig machen
- Laden, der Herzschlag als ruhiger Ladeindikator.
- Leerer Korb, kein trauriger Zustand, sondern eine Einladung zu handeln, mit einem Weg hinein.
- Preis unbekannt, dann auf Anfrage statt einer Zahl, der Weg bleibt offen.
- Verfügbarkeit als weicher Punkt, nie exakte Stückzahl.
- Fehler, in der Stimme der Oberfläche, was ist passiert und wie es weitergeht, keine Entschuldigung, nie vage.

## 4. Welche Daten die Bausteine zeigen
Damit dein Design an die echten Felder passt, die Datenlage aus dem Datenvertrag.
- Je Gerät, Anzeigename, Hersteller, Spezifikationen mit CPU, RAM, Speicher, Farbe, Bildschirmgröße, Generation, Kennzeichen wie 5G oder ohne Ladegerät.
- Raten, je Vertragsart und Laufzeit ein Wert mit netto und brutto, dazu die günstigste Rate für die Anzeige ab X pro Monat.
- Verfügbarkeit als Status, verfügbar, im Zulauf, auf Anfrage.
- Auszeichnungen, featured und Badge aus einer handgepflegten Datei, für Startseite und Hervorhebungen.
- Bilder, ein Fotoset je Bildmodell aus images.json, Hauptbild, Vorschau, Galerie, mit Fallback.
- Zubehör, Software und Services kommen aus eigenen Dateien im gleichen Ratenschema, gestalte sie als Positionen mit Name, kurzer Erklärung und Rate.

## 5. Leitplanken, nicht verhandelbar
- Öffentlich nur fertige Monatsraten, nie Einkauf, Verkauf oder Leasingfaktoren.
- Netto prominent, brutto sekundär, immer unverbindlich.
- Cyan nur für drei Dinge, aktiver Schritt, die Rate, der primäre Button. Sonst nichts cyan.
- Genau eine Hauptaktion je Bildschirm, plus ein Zurück-Weg. Nie eine Sackgasse.
- Durchgehend normale Schreibweise, keine Großbuchstaben-Labels, kein breites Sperren.
- Logo nur das Herz, das Wort surface.love nirgends sichtbar. Telefon als 0800-SURFACE, echte Ziffern nur bei Fokus.
- Deutsch, echte Umlaute, keine langen Bindestriche, Komma statt.
- Texte sind Designmaterial, aktive Verben, benenne Dinge danach, was der Nutzer tut, nicht wie das System gebaut ist. Der Button, der Anfrage senden heißt, führt zur Bestätigung, die von gesendet spricht.
- Barrierefreiheit als Boden, bis zum Handy responsiv, sichtbarer Tastaturfokus, reduzierte Bewegung respektiert.

## 6. Was wir von dir erwarten, die Deliverables
Damit wir es mit Claude Code umsetzen können.
- Gestaltete Bildschirme für jedes Modul oben, Detailseite, Konfigurator, Bundles, Zubehör, Software, Services, Anfragekorb, die vier Wizard-Schritte, die Bestätigung.
- Ein interaktiver Prototyp mindestens für die Detailseite mit Konfigurator und für die Wizard-Strecke, damit wir den Fluss fühlen, das Umschalten der Rate, den mitlaufenden Korb.
- Ein Baustein-Verzeichnis, welche Komponenten es gibt, Umschalter, Laufzeit-Auswahl, Ratenanzeige, Add-on-Zeile, Korb-Karte, Schritt-Indikator, Formularfeld, mit ihren Zuständen, normal, aktiv, deaktiviert, Fehler, laden.
- Zu jeder Komponente, welche Daten sie zeigt, angelehnt an Abschnitt 4, damit Claude Code weiß, was hineinfließt.
- Responsives Verhalten je Baustein, Desktop und Handy, besonders der Korb, rechts gegen fixe Leiste unten.
- Bewegungsnotizen, wo etwas animiert, Herzschlag, hochzählende Rate, sanfte Übergänge, zurückhaltend.
- Alles auf deinen Tokens, als CSS-Variablen, nicht als feste Werte, damit das Theming je Storefront trägt.
- Eine kurze Designbegründung, warum die Signatur so sitzt und wie die Steuermodule ruhig bleiben.

Halte deine Kühnheit an einer Stelle, der Signatur und dem Rundum-sorglos-Gefühl. Die Steuermodule selbst, Umschalter, Laufzeit, Korb, bleiben ruhig, präzise und diszipliniert.

## 7. Was jetzt NICHT zu gestalten ist
Nicht bauen, Platz höchstens vorsehen, der ROI-Rechner auf der Vorteilsseite, eine Vergleichsfunktion, ein Beratungsassistent welches Surface passt zu mir, ein FAQ-Chatbot, die Versicherungs- und Schutzlogik im Detail. Konzentrier dich auf die Strecke vom Gerät bis zur gesendeten Anfrage und auf das voll verwaltete Gefühl.
