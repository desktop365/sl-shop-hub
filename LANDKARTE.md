# Surface.Love, Architektur-Landkarte

Working-Stand als Grundlage für den Umbau von der AI-Studio-App zur eigenen Plattform. Getroffene Annahmen sind als Empfehlung markiert und in Abschnitt 17 zur Bestätigung gesammelt.

**Übersicht auf einem Blatt:** [SYSTEMKARTE-A0.svg](SYSTEMKARTE-A0.svg), der
Wertstrom vom Distributor-Feed bis zur Anfrage im CRM, dazu Stränge,
Zeitband und Kontraktleiste. Druckbar auf A0 quer, Stand 25.08.2026.

## 0. Zielbild
Eine eigene, aus Claude Code gebaute Plattform, die zweigleisig verkauft: Neugeräte zur Rate über die DLL-Bank, und refurbished Geräte aus eigenem Bestand im Abo mit Zahlung über Stripe. Betrieb weitgehend durch Agenten über Mail und HubSpot, Mensch nur für Spezialfälle und Großkunden. Von Anfang an mehrsprachig und mehrmarktfähig, mit eingebautem SEO und einer Marketing-Brücke zu LinkedIn. Version zwei bringt ein Kundenportal mit Login.

## 1. Die Teilbereiche, das System in Modulen
1. Katalog und Produktdaten, mehrere Hersteller (Surface, Lenovo), zwei Zustände (neu, refurbished)
2. Preis-Engine, getrennt für neu und refurbished
3. Promotions, datengetriebene Preisaktionen
4. Shop-Frontend, Konfigurator, zwei Kassenwege, mehrsprachig
5. Anfrage und Checkout, neu = Anfrage zur Bank, refurbished = Abo-Kauf mit Stripe
6. Bestandsverwaltung refurbished, Seriennummern, Zustand, Verfügbarkeit
7. Zahlung und Abo, Stripe, SEPA-Lastschrift, Rechnungen
8. CRM und Automatisierung, HubSpot plus Mail-MCP plus Agenten
9. Marketing und Leads, HubSpot zu LinkedIn-Anzeigen, Messung, Besucherbezug
10. SEO und Inhalte, agentengetrieben, Blog
11. Bilder-Pipeline, Quelle, Zuschnitt, Optimierung, Einspielung
12. Kundenportal, Login, Kommunikation, Auf- und Querverkauf (Version zwei)
13. DLL-Bank-Anbindung, Bonität, Vertrag, Unterschrift (später)
14. Infrastruktur, Hosting bei Hostinger, MySQL, Domain, Media
15. Storefronts, Einmarken-Auftritte je Domain, Marke, Sortiment, Recht und Absender je Domain

## 2. Zwei Geschäftsmodelle, zwei Kassenwege
- Neu: Kunde konfiguriert, stellt eine Anfrage, Bonitätsprüfung und Vertrag über die DLL-Bank. Kein Sofortkauf. Umsatz über Leasing und Finanzierung.
- Refurbished: Kunde wählt ein geprüftes Gerät aus eigenem Bestand, schließt direkt ein Abo ab, zahlt über Stripe. Keine Bank. Volle Marge, wiederkehrender Umsatz.
Beide Wege leben in einer App, mit einem gemeinsamen Katalog, der den Zustand unterscheidet.

## 2a. Storefronts, Einmarken-Auftritte je Domain
Die zweite Achse neben dem Geschäftsmodell. Ein Storefront ist eine Konfiguration je Domain, sie legt
Marke, Optik, Hersteller-Filter, rechtliche Texte, Kontaktdaten, Mail-Absender und die HubSpot-Parameter
fest. Die App erkennt die Domain und rendert den passenden Auftritt.

Eine Codebasis, ein HubSpot, ein Bestand. Nach außen getrennte Marken-Shops:
- **surface** auf surface.love, Microsoft Surface, Herz und Cyan, aktiv.
- **lenovo** auf lenovo.online, Lenovo, eigene Marke, vorbereitet.

Drei Achsen, die sich kombinieren: Storefront (Marke und Domain), Markt (Land, Währung, Recht), Lane (neu,
refurbished). Ein Aufruf ist immer ein Tripel daraus.

Regel: kein markenübergreifender Querverkauf. Die Verbindung neu zu refurbished aus Abschnitt 6 bleibt
innerhalb einer Marke, ein Surface-Besucher sieht nie ein Lenovo-Angebot und umgekehrt.

Name lenovo.online und Lenovo-Logo unterliegen Lenovos Partner- und Markenregeln, vor Livegang gegen den
Partnervertrag zu prüfen, siehe Abschnitt 17.

Verbindlich in contracts/STOREFRONTS.md.

## 3. Wie die Produkte in den Shop kommen
Zwei Quellen, klar getrennt:
- Neu, vom Distributor: Der Distributor-Feed, Surface und künftig Lenovo, wird von der Preis-Pipeline eingelesen, normalisiert, mit Spezifikationen angereichert und mit Raten versehen. Ergebnis ist der Datenvertrag (products.json), den der Shop liest. Neue Hersteller sind eine Erweiterung der Pipeline, das Datenmodell ist herstellerneutral. Welcher Hersteller in welchem Auftritt erscheint, entscheidet der Hersteller-Filter des Storefronts, nicht der Katalog.
- Refurbished, aus eigenem Bestand: Rückläufer kommen herein, stetiger Strom, werden erfasst, geprüft und mit Zustand bewertet, und landen als konkrete Einheiten mit Seriennummer in der Bestandsverwaltung (MySQL). Von dort werden sie im Shop gelistet, gefiltert nach dem Hersteller des jeweiligen Storefronts. Kein Distributor.

## 4. Preis-Engine, wer, wo, wie
Grundsatz: keine manuelle Preisschätzung, Preise entstehen automatisiert.
- Neu: Kosten vom Distributor, Aufschlag, Leasing- bzw. Finanzierungsfaktor, ergibt die Monatsrate. Das läuft in der bestehenden Preis-Pipeline (heute Azure-Funktion, täglich), entkoppelt vom Shop. Der Host ist flexibel, die Pipeline kann bleiben oder später als Cron-Worker zu Hostinger ziehen.
- Refurbished: der Preis ist ein selbst gesetzter Abo-Preis, weil das Gerät uns gehört. Regelbasiert, zum Beispiel abgeleitet aus der Neu-Rate abzüglich eines Refurbished-Faktors oder aus dem Restwert über die Laufzeit, je Modell, mit optionaler Übersteuerung je Einheit. Das läuft im Backend der App, weil es am Bestand hängt. Ein Agent oder du setzt die Regel und die Ausnahmen.
Nur Raten sind öffentlich, nie Faktoren, Einkauf oder interne Werte.

## 5. Promotions
Eine Aktionsschicht über den Grundpreisen, datengetrieben, ohne neues Deployment:
- Regel je Aktion: Prozent oder fester Abschlag, Geltung auf Hersteller, Modell, Zustand oder Markt, Zeitraum, optional Code, optional Banner.
- Anzeige im Shop als statt-jetzt.
- Übergabe in den Checkout: bei refurbished als Stripe-Gutschein, bei neu als berücksichtigter Angebotspreis.
- Pflege über Admin oder Agent, nicht im Code.

## 6. Kundenansprache, neu gegen refurbished
Zwei Linien, verbunden statt getrennt:
- Neu: neueste Technik, volle Garantie, sorgenfrei zur Rate.
- Refurbished: clever sparen, geprüfte Geräte aus eigenem Bestand, nachhaltiger, sofort verfügbar, im flexiblen Abo.
Sichtbar wird der Unterschied über einen Zustands-Umschalter im Katalog, klare Kennzeichnung je Produktkarte, und die Preisrahmung. Der Hebel für Umsatz ist die Querverbindung: auf der Neu-Seite ein Hinweis, dasselbe Modell refurbished, ab Y sparen, und umgekehrt der Aufstieg vom gebrauchten zum neuen Gerät. Das ist der eingebaute Ab- und Aufverkauf.

## 7. Bilder-Pipeline, Quelle, Zuschnitt, Optimierung, Einspielung
- Quelle: Neu = Herstellerfotos von Microsoft und Lenovo, als Reseller nutzbar, aber nicht ins öffentliche Repo. Refurbished = zunächst repräsentative Modellfotos plus Zustandsangabe, keine Einzelfotografie je Gerät, das skaliert bei laufendem Rücklauf nicht. Echte Einzelfotos nur, wenn ein Gerät stark abweicht.
- Zuschnitt und Optimierung: die bestehende Pillow-Pipeline, WebP in Qualität 80, Hauptbild bis 1200 mal 1200 eingepasst, Vorschau bis 400 mal 400, Fallbacks.
- Automatisierung: die Pipeline wird zum Agenten-Ablauf. Quelle ablegen, der Agent schneidet zu, konvertiert, erzeugt die Größen, benennt nach der Konvention, lädt hoch und trägt die Zuordnung in images.json ein.
- Einspielung: über den Media-Speicher plus die Zuordnung MSKU zu Fotoset in images.json, die der Shop liest. Media liegt im GCS-Bucket slshopv2-media, entschieden, siehe contracts/INFRA.md.

## 8. Internationalisierung
Von Tag eins strukturell, nicht nachgerüstet:
- Mehrsprachig, Deutsch und Englisch zuerst, Texte über ein i18n-System.
- Mehrmarktfähig: Währung, rechtliche Texte, Vertragsarten und Kontaktdaten je Markt, aufbauend auf dem Markt-Konzept, das wir schon haben (Deutschland aktiv, USA vorbereitet).
- Preise und Verfügbarkeit je Markt.

## 9. CRM und Automatisierung
- HubSpot bleibt das Rückgrat für Kontakte, Firmen, Deals, Abos.
- Ein Portal und eine gemeinsame SL-Pipeline für beide Marken, keine eigene Lenovo-Pipeline. Die Marke
  steckt in einem Deal-Feld mit den Werten Surface und Lenovo, dazu die Deal-Quelle je Storefront.
  Auswertung je Marke über Filter auf dem Feld, siehe contracts/HUBSPOT.md.
- Dein Mail-MCP bindet das Postfach an, Kundenmails auslesen und beantworten, alles nach HubSpot gespiegelt.
- Agenten übernehmen den Lebenszyklus für kleine Fälle: Anfrage aufnehmen, antworten, Status pflegen, Versand anstoßen. Eskalation an dich bei Spezialfällen und Großkunden.

## 10. Marketing und Leads
- HubSpot zu LinkedIn: Anzeigen aus HubSpot heraus schalten, Lead-Formulare synchron, Kampagnen messen.
- Attribution: welcher Lead und welcher Deal kam aus welcher Kampagne.
- Besucher auf der Seite: HubSpot-Tracking auf der Seite für Verhalten und Zuordnung. Echte Enttarnung einzelner Besucher ist nur eingeschränkt und unter DSGVO-Vorbehalt möglich, hier gehen wir bewusst sauber und datenschutzkonform vor.

## 11. SEO und Inhalte
- Technisches SEO ist eingebaut: serverseitiges Rendern, saubere Metadaten, Sitemaps, strukturierte Daten, schnelle Seiten. Das liefert der moderne Stack von Haus aus.
- Je Storefront eine eigene SEO-Identität: kanonische Domain, eigene Sitemap und robots, eigene
  Metadaten. Kein Inhalt erscheint unter zwei Domains ohne Kanonik. Rechtliche Texte und Kontaktdaten
  ebenso je Storefront, nicht geteilt.
- Inhalte agentengetrieben: der Content-Agent, den wir entworfen haben, zweisprachig, wöchentliche Artikel aus LinkedIn, YouTube, Surface-Quellen und Herstellerseiten, veröffentlicht über den Blog. Du gibst nur Richtung, der Agent macht.

## 12. Kundenportal, Version zwei
- Login für Bestandskunden.
- Kommunikation über das Portal, Standardfälle beantworten Agenten.
- Abo-Selbstverwaltung über das Stripe-Kundenportal.
- Schneller Auf- und Querverkauf, passende Angebote je Kunde.

## 13. DLL-Bank-Anbindung, später
- Bonitätsprüfung, Vertragsgenerierung, Versand zur Unterschrift, am Neu-Zweig.
- Kontrollierter Auslöser, Zugangsdaten serverseitig als Secret.
- Kommt, wenn der Kern steht, die HubSpot-Stufe Vertrag gesendet ist vorbereitet.

## 14. Infrastruktur und Hosting
- Hosting bei Hostinger über das gemanagte Node-Hosting, verwaltet aus Claude Code über das Hostinger-Plugin, GitHub-Repo verbunden.
- Datenbank: MySQL für Bestand, Abos, Zuordnungen, Portal.
- Zahlung: Stripe, hostunabhängig in die App integriert.
- Eine App, zwei Domains. Dieselbe Anwendung liefert beide Storefronts aus und unterscheidet sie an der
  Domain, kein zweiter Deploy, keine Kopie der Codebasis.
- Domain und DNS: surface.love liegt bei Cloudflare und zeigt bis zum Umschalten auf den alten Shop, die neue App läuft unter worklove.shop bei Hostinger, lenovo.online kommt später dazu. Details in contracts/INFRA.md.
- Media: Bilder und Live-Dateien liegen im GCS-Bucket slshopv2-media, entschieden, siehe contracts/INFRA.md.
- Der alte AI-Studio-Shop bleibt live, bis der neue steht.

## 15. Was 1 zu 1 übernommen wird, was neu entsteht
Übernommen: Design und Designsystem, UX und Ablauf, der Datenvertrag, die Preis-Pipeline für neu, das Bildkonzept, die Anfrage-Logik mit Turnstile, HubSpot und Graph-Mail, das Markt-Konzept.
Neu: eigener App-Rahmen mit Next.js und MySQL, die Bestandsverwaltung refurbished, Stripe-Abos und Rechnung, die Promotions-Schicht, die Marketing- und Attributionsbrücke, der agentengetriebene Betrieb, das Kundenportal.

## 16. Reihenfolge, Phasen
0. Fundament: neuer App-Rahmen (Next.js, MySQL), mehrsprachig und mehrmarktfähig von Anfang an, Hosting bei Hostinger, Domain, Designsystem portiert.
1. Neu-Shop portieren: Katalog aus der Preis-Pipeline, Konfigurator, Anfrage zur Bank, HubSpot und Mail.
2. Refurbished-Zweig: Bestandsverwaltung, refurbished Preise, Stripe-Abo, Rechnung, HubSpot-Abgleich, Ansprache und Querverkauf.
3. Marketing und SEO: HubSpot zu LinkedIn, Tracking und Attribution, technisches SEO, Content-Agent.
4. Agenten für den Lebenszyklus: kleine Anfragen automatisiert, Eskalation an dich.
5. Kundenportal, Version zwei: Login, Kommunikation, Selbstverwaltung, Auf- und Querverkauf.
6. DLL-Bank-Anbindung: Bonität, Vertrag, Unterschrift.
Querschnitt, immer dabei: mehrere Hersteller (Surface, Lenovo), i18n, die Bilder-Pipeline.

## 17. Offene Entscheidungen
1. Hosting bei Hostinger fix, oder soll ich es kurz gegen eine Alternative stellen. Empfehlung: Hostinger, gut geeignet.
2. Stripe für die Refurbished-Abos, bestätigt, oder Hostingers eigenen Subscriptions-Baustein prüfen. Empfehlung: Stripe.
3. Reihenfolge recht, erst neu portieren, dann refurbished, dann Agenten. Empfehlung: ja.
4. Media-Ablage, entschieden, bleibt im GCS-Bucket slshopv2-media, siehe contracts/INFRA.md.
5. Refurbished-Bilder: repräsentative Modellfotos plus Zustandsangabe als Standard, bestätigt.
6. Lenovo-Storefront: Domainname lenovo.online, Logo und Wortmarke gegen Lenovos Partner- und
   Markenregeln prüfen, dazu der Sortimentsschnitt. Offen bis zur Prüfung des Partnervertrags.
