# Surface.Love, Architektur-Landkarte

Working-Stand als Grundlage fuer den Umbau von der AI-Studio-App zur eigenen Plattform. Getroffene Annahmen sind als Empfehlung markiert und in Abschnitt 17 zur Bestaetigung gesammelt.

## 0. Zielbild
Eine eigene, aus Claude Code gebaute Plattform, die zweigleisig verkauft: Neugeraete zur Rate ueber die DLL-Bank, und refurbished Geraete aus eigenem Bestand im Abo mit Zahlung ueber Stripe. Betrieb weitgehend durch Agenten ueber Mail und HubSpot, Mensch nur fuer Spezialfaelle und Grosskunden. Von Anfang an mehrsprachig und mehrmarktfaehig, mit eingebautem SEO und einer Marketing-Bruecke zu LinkedIn. Version zwei bringt ein Kundenportal mit Login.

## 1. Die Teilbereiche, das System in Modulen
1. Katalog und Produktdaten, mehrere Hersteller (Surface, Lenovo), zwei Zustaende (neu, refurbished)
2. Preis-Engine, getrennt fuer neu und refurbished
3. Promotions, datengetriebene Preisaktionen
4. Shop-Frontend, Konfigurator, zwei Kassenwege, mehrsprachig
5. Anfrage und Checkout, neu = Anfrage zur Bank, refurbished = Abo-Kauf mit Stripe
6. Bestandsverwaltung refurbished, Seriennummern, Zustand, Verfuegbarkeit
7. Zahlung und Abo, Stripe, SEPA-Lastschrift, Rechnungen
8. CRM und Automatisierung, HubSpot plus Mail-MCP plus Agenten
9. Marketing und Leads, HubSpot zu LinkedIn-Anzeigen, Messung, Besucherbezug
10. SEO und Inhalte, agentengetrieben, Blog
11. Bilder-Pipeline, Quelle, Zuschnitt, Optimierung, Einspielung
12. Kundenportal, Login, Kommunikation, Auf- und Querverkauf (Version zwei)
13. DLL-Bank-Anbindung, Bonitaet, Vertrag, Unterschrift (spaeter)
14. Infrastruktur, Hosting bei Hostinger, Postgres, Domain, Media

## 2. Zwei Geschaeftsmodelle, zwei Kassenwege
- Neu: Kunde konfiguriert, stellt eine Anfrage, Bonitaetspruefung und Vertrag ueber die DLL-Bank. Kein Sofortkauf. Umsatz ueber Leasing und Finanzierung.
- Refurbished: Kunde waehlt ein geprueftes Geraet aus eigenem Bestand, schliesst direkt ein Abo ab, zahlt ueber Stripe. Keine Bank. Volle Marge, wiederkehrender Umsatz.
Beide Wege leben in einer App, mit einem gemeinsamen Katalog, der den Zustand unterscheidet.

## 3. Wie die Produkte in den Shop kommen
Zwei Quellen, klar getrennt:
- Neu, vom Distributor: Der Distributor-Feed, Surface und kuenftig Lenovo, wird von der Preis-Pipeline eingelesen, normalisiert, mit Spezifikationen angereichert und mit Raten versehen. Ergebnis ist der Datenvertrag (products.json), den der Shop liest. Neue Hersteller sind eine Erweiterung der Pipeline, das Datenmodell ist herstellerneutral.
- Refurbished, aus eigenem Bestand: Ruecklaeufer kommen herein, stetiger Strom, werden erfasst, geprueft und mit Zustand bewertet, und landen als konkrete Einheiten mit Seriennummer in der Bestandsverwaltung (Postgres). Von dort werden sie im Shop gelistet. Kein Distributor.

## 4. Preis-Engine, wer, wo, wie
Grundsatz: keine manuelle Preisschaetzung, Preise entstehen automatisiert.
- Neu: Kosten vom Distributor, Aufschlag, Leasing- bzw. Finanzierungsfaktor, ergibt die Monatsrate. Das laeuft in der bestehenden Preis-Pipeline (heute Azure-Funktion, taeglich), entkoppelt vom Shop. Der Host ist flexibel, die Pipeline kann bleiben oder spaeter als Cron-Worker zu Hostinger ziehen.
- Refurbished: der Preis ist ein selbst gesetzter Abo-Preis, weil das Geraet uns gehoert. Regelbasiert, zum Beispiel abgeleitet aus der Neu-Rate abzueglich eines Refurbished-Faktors oder aus dem Restwert ueber die Laufzeit, je Modell, mit optionaler Uebersteuerung je Einheit. Das laeuft im Backend der App, weil es am Bestand haengt. Ein Agent oder du setzt die Regel und die Ausnahmen.
Nur Raten sind oeffentlich, nie Faktoren, Einkauf oder interne Werte.

## 5. Promotions
Eine Aktionsschicht ueber den Grundpreisen, datengetrieben, ohne neues Deployment:
- Regel je Aktion: Prozent oder fester Abschlag, Geltung auf Hersteller, Modell, Zustand oder Markt, Zeitraum, optional Code, optional Banner.
- Anzeige im Shop als statt-jetzt.
- Uebergabe in den Checkout: bei refurbished als Stripe-Gutschein, bei neu als beruecksichtigter Angebotspreis.
- Pflege ueber Admin oder Agent, nicht im Code.

## 6. Kundenansprache, neu gegen refurbished
Zwei Linien, verbunden statt getrennt:
- Neu: neueste Technik, volle Garantie, sorgenfrei zur Rate.
- Refurbished: clever sparen, gepruefte Geraete aus eigenem Bestand, nachhaltiger, sofort verfuegbar, im flexiblen Abo.
Sichtbar wird der Unterschied ueber einen Zustands-Umschalter im Katalog, klare Kennzeichnung je Produktkarte, und die Preisrahmung. Der Hebel fuer Umsatz ist die Querverbindung: auf der Neu-Seite ein Hinweis, dasselbe Modell refurbished, ab Y sparen, und umgekehrt der Aufstieg vom gebrauchten zum neuen Geraet. Das ist der eingebaute Ab- und Aufverkauf.

## 7. Bilder-Pipeline, Quelle, Zuschnitt, Optimierung, Einspielung
- Quelle: Neu = Herstellerfotos von Microsoft und Lenovo, als Reseller nutzbar, aber nicht ins oeffentliche Repo. Refurbished = zunaechst repraesentative Modellfotos plus Zustandsangabe, keine Einzelfotografie je Geraet, das skaliert bei laufendem Ruecklauf nicht. Echte Einzelfotos nur, wenn ein Geraet stark abweicht.
- Zuschnitt und Optimierung: die bestehende Pillow-Pipeline, WebP in Qualitaet 80, Hauptbild bis 1200 mal 1200 eingepasst, Vorschau bis 400 mal 400, Fallbacks.
- Automatisierung: die Pipeline wird zum Agenten-Ablauf. Quelle ablegen, der Agent schneidet zu, konvertiert, erzeugt die Groessen, benennt nach der Konvention, laedt hoch und traegt die Zuordnung in images.json ein.
- Einspielung: ueber den Media-Speicher plus die Zuordnung MSKU zu Fotoset in images.json, die der Shop liest. Offene Frage: Media beim GCS-Bucket lassen oder zu Hostinger ziehen, siehe Abschnitt 17.

## 8. Internationalisierung
Von Tag eins strukturell, nicht nachgeruestet:
- Mehrsprachig, Deutsch und Englisch zuerst, Texte ueber ein i18n-System.
- Mehrmarktfaehig: Waehrung, rechtliche Texte, Vertragsarten und Kontaktdaten je Markt, aufbauend auf dem Markt-Konzept, das wir schon haben (Deutschland aktiv, USA vorbereitet).
- Preise und Verfuegbarkeit je Markt.

## 9. CRM und Automatisierung
- HubSpot bleibt das Rueckgrat fuer Kontakte, Firmen, Deals, Abos.
- Dein Mail-MCP bindet das Postfach an, Kundenmails auslesen und beantworten, alles nach HubSpot gespiegelt.
- Agenten uebernehmen den Lebenszyklus fuer kleine Faelle: Anfrage aufnehmen, antworten, Status pflegen, Versand anstossen. Eskalation an dich bei Spezialfaellen und Grosskunden.

## 10. Marketing und Leads
- HubSpot zu LinkedIn: Anzeigen aus HubSpot heraus schalten, Lead-Formulare synchron, Kampagnen messen.
- Attribution: welcher Lead und welcher Deal kam aus welcher Kampagne.
- Besucher auf der Seite: HubSpot-Tracking auf der Seite fuer Verhalten und Zuordnung. Echte Enttarnung einzelner Besucher ist nur eingeschraenkt und unter DSGVO-Vorbehalt moeglich, hier gehen wir bewusst sauber und datenschutzkonform vor.

## 11. SEO und Inhalte
- Technisches SEO ist eingebaut: serverseitiges Rendern, saubere Metadaten, Sitemaps, strukturierte Daten, schnelle Seiten. Das liefert der moderne Stack von Haus aus.
- Inhalte agentengetrieben: der Content-Agent, den wir entworfen haben, zweisprachig, woechentliche Artikel aus LinkedIn, YouTube, Surface-Quellen und Herstellerseiten, veroeffentlicht ueber den Blog. Du gibst nur Richtung, der Agent macht.

## 12. Kundenportal, Version zwei
- Login fuer Bestandskunden.
- Kommunikation ueber das Portal, Standardfaelle beantworten Agenten.
- Abo-Selbstverwaltung ueber das Stripe-Kundenportal.
- Schneller Auf- und Querverkauf, passende Angebote je Kunde.

## 13. DLL-Bank-Anbindung, spaeter
- Bonitaetspruefung, Vertragsgenerierung, Versand zur Unterschrift, am Neu-Zweig.
- Kontrollierter Ausloeser, Zugangsdaten serverseitig als Secret.
- Kommt, wenn der Kern steht, die HubSpot-Stufe Vertrag gesendet ist vorbereitet.

## 14. Infrastruktur und Hosting
- Hosting bei Hostinger ueber das gemanagte Node-Hosting, verwaltet aus Claude Code ueber das Hostinger-Plugin, GitHub-Repo verbunden.
- Datenbank: Postgres fuer Bestand, Abos, Zuordnungen, Portal.
- Zahlung: Stripe, hostunabhaengig in die App integriert.
- Domain und DNS: surface.love ueber Hostinger.
- Media: Bilder im Objektspeicher, Ablageort noch zu entscheiden.
- Der alte AI-Studio-Shop bleibt live, bis der neue steht.

## 15. Was 1 zu 1 uebernommen wird, was neu entsteht
Uebernommen: Design und Designsystem, UX und Ablauf, der Datenvertrag, die Preis-Pipeline fuer neu, das Bildkonzept, die Anfrage-Logik mit Turnstile, HubSpot und Graph-Mail, das Markt-Konzept.
Neu: eigener App-Rahmen mit Next.js und Postgres, die Bestandsverwaltung refurbished, Stripe-Abos und Rechnung, die Promotions-Schicht, die Marketing- und Attributionsbruecke, der agentengetriebene Betrieb, das Kundenportal.

## 16. Reihenfolge, Phasen
0. Fundament: neuer App-Rahmen (Next.js, Postgres), mehrsprachig und mehrmarktfaehig von Anfang an, Hosting bei Hostinger, Domain, Designsystem portiert.
1. Neu-Shop portieren: Katalog aus der Preis-Pipeline, Konfigurator, Anfrage zur Bank, HubSpot und Mail.
2. Refurbished-Zweig: Bestandsverwaltung, refurbished Preise, Stripe-Abo, Rechnung, HubSpot-Abgleich, Ansprache und Querverkauf.
3. Marketing und SEO: HubSpot zu LinkedIn, Tracking und Attribution, technisches SEO, Content-Agent.
4. Agenten fuer den Lebenszyklus: kleine Anfragen automatisiert, Eskalation an dich.
5. Kundenportal, Version zwei: Login, Kommunikation, Selbstverwaltung, Auf- und Querverkauf.
6. DLL-Bank-Anbindung: Bonitaet, Vertrag, Unterschrift.
Querschnitt, immer dabei: mehrere Hersteller (Surface, Lenovo), i18n, die Bilder-Pipeline.

## 17. Offene Entscheidungen
1. Hosting bei Hostinger fix, oder soll ich es kurz gegen eine Alternative stellen. Empfehlung: Hostinger, gut geeignet.
2. Stripe fuer die Refurbished-Abos, bestaetigt, oder Hostingers eigenen Subscriptions-Baustein pruefen. Empfehlung: Stripe.
3. Reihenfolge recht, erst neu portieren, dann refurbished, dann Agenten. Empfehlung: ja.
4. Media-Ablage: Bilder beim bestehenden GCS-Bucket lassen, oder zu Hostinger ziehen, damit alles unter einem Dach liegt.
5. Refurbished-Bilder: repraesentative Modellfotos plus Zustandsangabe als Standard, bestaetigt.
