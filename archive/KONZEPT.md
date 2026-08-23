> Abgeloest und archiviert. Beschreibt den ersten Anlauf mit FastAPI auf Google Cloud Run aus der AI-Studio-Zeit, keine Vorgabe mehr. Gueltig sind LANDKARTE.md, ARBEITSWEISE.md, STATUS.md und die Kontrakte unter contracts. Die wertvollen Teile, Rechenlogik und Anfrage-Logik, stehen jetzt in contracts/PRICING.md und contracts/ANFRAGE.md.

# Konzeptpapier: Surface as a Service Shop (slshopv2)

Zentrales Referenz- und Arbeitsdokument. Lebt im Repo `desktop365/sl-shop-hub`.
Stand: 18.06.2026. Status: in Umsetzung, Bau noch nicht begonnen (Fundament steht).

---

## 0. Wie dieses Dokument zu nutzen ist

Dieses Papier beschreibt verbindlich, was wir bauen, wie wir es bauen und warum. Es ist die
gemeinsame Grundlage für alle Beteiligten: den Chat, der die App in Google AI Studio baut, die
VS-Code-Chats für die Preis-Pipeline und die Bildaufbereitung, sowie Claude für Planung und Prompts.

Es ist ein lebendes Dokument. Wir erweitern und korrigieren es, statt Wissen über einzelne Chats zu
verstreuen. Konkrete Detail-Dateien (Datenvertrag, Designtokens, Beispieldaten, Prompts) liegen
ebenfalls im Repo und werden hier referenziert, nicht dupliziert.

Wichtiger Sicherheitshinweis vorab: dieses Repo ist öffentlich. In diesem Papier stehen deshalb
keine Geheimnisse und keine konkreten Tenant-, App- oder Konto-IDs. Alle Schlüssel und IDs liegen im
Secret Manager bzw. in einer privaten Ablage. Öffentlich sind ausschließlich fertige Verkaufsraten,
nie EK oder VK.

---

## 1. Vision und Ziel

Wir bauen eine moderne B2B-Anfrageplattform für Microsoft Surface as a Service, keinen klassischen
Kaufshop. Geschäftskunden konfigurieren Geräte, Zubehör, Microsoft 365 und Services, sehen planbare
Monatsraten für Leasing und Finanzierung, legen alles in einen Anfragekorb und senden eine
unverbindliche Anfrage. Diese Anfrage wird zu einer E-Mail an den Vertrieb und zu einem Deal in
HubSpot. Es gibt keinen Warenkorb-Kauf, keine Zahlung, kein Kundenkonto.

Das Ziel der Seite ist die qualifizierte Anfrage. Alles, Design, Inhalte, Navigation, dient diesem
einen Zweck, mit so wenig Klicks wie möglich und ohne dass der Nutzer unterwegs abspringt.

---

## 2. Zielgruppe und Positionierung

Zielgruppe sind deutschsprachige kleine und mittlere Unternehmen und ihre Entscheider. Sie denken in
Budget, Liquidität, Aufwand und Verlässlichkeit, nicht in Endkundenpreisen.

Kernbotschaft: mit Surface as a Service fährt ein Unternehmen deutlich günstiger und sorgenfreier als
mit dem Einmalkauf. Diese vier Vorteile ziehen sich durch die gesamte Seite und werden klar
herausgestellt:

1. Liquidität und Planbarkeit. Keine hohe Anfangsinvestition, eine feste Rate pro Gerät und Monat,
   budget- und bilanzschonend. Den steuerlichen Aspekt formulieren wir vorsichtig als möglichen
   Betriebsausgaben-Vorteil, ohne verbindliche Steuerberatung.
2. Rundum-sorglos, das eigentliche Unterscheidungsmerkmal zum Kauf. Volles Management durch uns:
   Beschaffung, Einrichtung und Provisionierung, Rollout und Logistik, Support, Reparatur und
   Austausch, optional Versicherung, am Laufzeitende Rückgabe oder Tausch auf die neue Generation.
   Ein Ansprechpartner, ein Vertrag, eine Rate.
3. KI und Copilot, klar getrennt dargestellt. Copilot+ PC als KI-fähige Hardware auf der einen Seite,
   Microsoft 365 Copilot als Software auf der anderen. Botschaft: mit Service immer auf aktueller,
   KI-fähiger Hardware, ohne alle paar Jahre neu kaufen zu müssen.
4. Skalierbarkeit und Nachhaltigkeit. Einfach hoch- und runterskalieren, neue Mitarbeiter schnell
   ausgestattet, Geräte im Kreislauf statt im Schrank.

Diese Vorteile bekommen eine eigene, conversion-kritische Vorteilsseite mit Designelementen, nicht
nur Text. Dort: ein klarer Hero mit dem Versprechen in einem Satz, ein visueller Kostenvergleich Kauf
gegen Service, der die versteckten Zusatzkosten des Kaufs sichtbar macht und Platz für einen späteren
ROI-Rechner lässt, das Sorglos-Paket als Leistungskacheln, ein KI-Block zu Copilot, ein Abschnitt zu
Skalierbarkeit und Nachhaltigkeit, und durchgehend genau eine Hauptaktion, der Sprung in die Anfrage.
Der ROI-Rechner ist eine eigene, spätere Interaktionsphase und bekommt vorerst nur einen Platzhalter.

---

## 3. Markenführung (Branding)

- Das Logo ist allein das Herz. Kein Wortbild daneben.
- Das Herz schlägt im Doppeltakt, ein sanfter Herzschlag-Puls. Es kann zugleich als Ladeindikator
  dienen.
- Das Wort "surface.love" erscheint nirgends sichtbar auf der Seite. Einzige Ausnahmen sind die
  Domain selbst und das Impressum, wo rechtlich der Firmenname stehen muss.
- Falls überhaupt etwas neben dem Herz steht, dann höchstens der leise Claim "work love balance",
  klein geschrieben.
- Telefon prominent und immer erreichbar im Kopfbereich: 0800 7873223 bzw. +49 800 7873223.

Logo-Asset und Farben liegen in `brand/`. Das Herz nutzt in der SVG minimal abweichend `#00A3DE`,
verbindlich ist `#00A3E0`, im App-Einsatz färben wir das Herz über `currentColor`.

---

## 4. Designsprache und Tokens

Anmutung: ruhig, premium, minimalistisch, großzügige Weißräume. Tokens liegen in `brand/tokens.css`.

Farben und ihre Rollen, das ist wichtiger als die Werte:
- Cyan `#00A3E0` ist der einzige Akzent. Nur drei Dinge dürfen cyan sein: der aktive Schritt im
  Wizard, die Rate "ab X pro Monat", der primäre Button. Dadurch sticht das Wesentliche immer heraus.
- Text in Tinten-Schwarz `#1A1A1A`, Sekundärtext Grau `#6B6B70`.
- Reines Schwarz `#000000` nur für Logo und Wortbild-Ersatz.
- Flächen Weiß, Sektionen sehr helles Grau `#F5F6F7`, Linien `#E6E7E9`.
- Verfügbarkeit als kleiner Statuspunkt, nie cyan: grün für verfügbar, bernstein für im Zulauf, grau
  für auf Anfrage.

Typografie:
- Hausschrift laut Farbwelt ist Segoe Pro in den Schnitten Light und Semibold.
- Web-Stapel: `"Segoe UI Variable", "Segoe UI", system-ui, -apple-system, BlinkMacSystemFont, Roboto,
  "Helvetica Neue", Arial, sans-serif`. Auf den Windows-Geräten der Zielgruppe rendert das echtes
  Segoe, markennah und kostenlos, auf anderen Systemen greift ein sauberer Ersatz. Segoe Pro selbst
  ist lizenzpflichtig und fürs Web nicht nötig.
- Gewichte: 300 Light für große Überschriften, 400 für Fließtext, 600 Semibold für Buttons und
  Hervorhebung. Schriftgrößen großzügig.

Form und Bewegung: 8er-Raster, weiche Ecken um 14 Pixel, sehr sparsame Schatten nur an schwebenden
Elementen. Genau ein primärer Button pro Bildschirm, cyan gefüllt, daneben höchstens ein dezenter
sekundärer als Outline. Bewegung zurückhaltend, der Herzschlag alle rund 3,5 Sekunden, kurze
Übergänge, die Rate zählt beim Umschalten sanft hoch.

---

## 5. UX-Konzept und Anfrage-Wizard

Leitgedanke: die ganze Seite ist ein Trichter zur unverbindlichen Anfrage. So wenig Klicks wie
möglich, keine Sackgasse, der Nutzer darf nie absterben.

Einstieg: Wizard und Katalog laufen parallel, der Wizard ist der sichtbare Hauptweg. Beide enden im
selben Anfragekorb.

Vier sichtbare Schritte, mehr nicht:
1. Gerät
2. Konfiguration (Vertragsart und Laufzeit, optional Zubehör, Software, Services)
3. Übersicht (Anfragekorb)
4. Kontakt und Absenden, dann Bestätigung

Durchgehender Schritt-Indikator oben, der aktuelle cyan, erledigte mit Haken, anklickbar zum
Zurückspringen. Der Anfragekorb ist immer präsent, am Desktop als mitlaufende Karte rechts, am Handy
als fixe Leiste unten mit Anzahl, Summe und primärem Button.

Gegen das Absterben:
- Genau eine offensichtliche Hauptaktion plus ein Zurück-Weg je Bildschirm.
- Sinnvolle Vorauswahl bei Vertragsart und Laufzeit, damit sofort eine Rate dasteht.
- Optionale Schritte klar überspringbar.
- Eingabeprüfung direkt am Feld, keine Fehlerwände.
- Der Korb merkt sich alles, auch nach einem Reload.
- Kurzes Formular, Pflicht sind nur Firma, Name und E-Mail. Telefon und Nachricht optional.
  DSGVO-Checkbox, Turnstile. Kein Konto, keine Zahlung. Geschäftskunden-Hinweis dezent.
- Bestätigung mit Anfrage-ID im Format SL-JJJJMMTT-XXXXXX und einer kurzen Erklärung, was als
  Nächstes passiert.

Preise und Verfügbarkeit: netto prominent, brutto sekundär, Formulierung "unverbindlich".
Verfügbarkeit nur als weiche Stufe (verfügbar, im Zulauf, auf Anfrage), keine exakte Stückzahl.
Leasingfaktoren werden nie angezeigt, damit sich der VK nicht zurückrechnen lässt.

Schnellster Pfad: Gerät, "In Anfrage übernehmen", "Übersicht", "Anfrage senden", kurzes Formular,
fertig.

Details und Tokens: siehe `UX.md` und `DESIGN.md` im Repo.

---

## 6. Informationsarchitektur und Seiten

- Startseite: Positionierung Surface as a Service in einem Satz, Einstieg in Wizard und Katalog, die
  vier Vorteile angerissen, klare Hauptaktion. Unterscheidung Copilot+ PC (Hardware) gegen Microsoft
  365 Copilot (Software) sauber dargestellt.
- Katalog und Produktdetail: Geräteübersicht mit Filtern und Sortierung, Detailseite mit Umschalter
  Vertragsart und Laufzeit, Rate, Verfügbarkeit, Hervorhebungen.
- Konfigurator-Wizard: der geführte Hauptweg zur Anfrage.
- Vorteilsseite Surface as a Service: eigene, conversion-kritische Seite (siehe Abschnitt 2).
- Microsoft 365 und Services: datengetriebene Bereiche.
- Inhaltsseiten: So funktioniert es, FAQ, Kontakt, Über uns.
- Rechtsseiten: Impressum, Datenschutz, AGB, Markenhinweise, Cookie-Consent. Rechtsrahmen nach
  aktuellem Stand, also DDG statt TMG.
- SEO: Title-Tags, Meta-Descriptions, strukturierte Daten, Sitemap, robots.txt.

---

## 7. Technische Architektur

Grundprinzip: App und Daten strikt getrennt. Die App ist Code und Design, die Daten und Medien liegen
zentral in der Cloud und werden zur Laufzeit geladen. So bricht ein Datenwechsel nie die App, und ein
App-Update fasst nie die Daten an.

Laufzeit und Hosting:
- Projekt `slshopv2` in Google Cloud, Region `europe-west1` (Belgien). Begründung in Abschnitt 10.
- Anwendung in Python mit FastAPI, als Google Cloud Run Dienst, zustandslos. Keine persistenten Daten
  lokal im Container.
- Die App liefert zweierlei aus: die gebaute Single-Page-Oberfläche als statische Dateien, und die
  API unter `/api` (Produktdaten und Anfrage). Der interaktive Wizard mit Live-Raten und mitlaufendem
  Korb läuft clientseitig in dieser Oberfläche, FastAPI liefert Daten und nimmt die Anfrage entgegen.
- Deployment aus einem GitHub-Repo über Cloud Build nach Cloud Run. Die AI-Studio-Vorschau in
  europe-west2 gilt nur als Vorschau, nicht als Produktion.

Medien und Daten:
- Ein Google Cloud Storage Bucket `slshopv2-media` hält Produktdaten und Bilder. Zugriff über die
  offizielle Bibliothek `google-cloud-storage`.
- Produktdaten als `products.json` im Bucket, von der Pipeline erzeugt (siehe Abschnitt 8, Variante
  A). Beim Bauen entwickeln wir gegen die lokale Beispieldatei `data/products.sample.json` in der
  Form aus dem Datenvertrag, später wird nur die Quelle auf den Bucket umgestellt.

Sicherheit im Code: keine Geheimnisse im Quellcode. Graph, HubSpot und Turnstile beziehen ihre
Schlüssel aus Secret Manager bzw. Umgebungsvariablen.

Warum dieser Aufbau trägt: alles liegt in einer Cloud, der Container ist zustandslos und beliebig
skalierbar, der Code lebt versioniert im Repo und wird reproduzierbar deployt, und die teuren oder
fragilen Teile, Preisberechnung und Bildaufbereitung, sind sauber ausgelagert.

---

## 8. Datenkonzept

### 8.1 Preis-Pipeline (Quelle der Wahrheit für Preise)
Eine Azure Function in Python 3.12 auf Flex Consumption, Region Germany West Central, läuft per Timer
täglich um 05:00 Europe/Berlin. Sie holt die Echtzeit-Preisliste des Distributors Continue per Basic
Auth, serverseitig bereits auf Microsoft gefiltert, Antwort als semikolongetrennte CSV. Der
Distributor erlaubt nur drei Abrufe je 15 Minuten, deshalb läuft das streng zeitgesteuert, die App
ruft nie direkt beim Distributor ab.

Verarbeitung: auf Surface für den deutschen Markt filtern (Software und Fremdmärkte raus, rund 358
Artikel), Aufschlag Faktor 1,25 auf den EK netto, daraus VK netto, daraus die Monatsraten je
Vertragsart und Wertstaffel über die DLL-Faktortabelle. Gerundet wird kaufmännisch (ROUND_HALF_UP)
auf exakt zwei Stellen, identisch zur DLL-Bank, weil die Rate so im Vertrag steht. Die Faktortabelle
ist nach Gerätewert gestaffelt, praktisch alle Geräte liegen in der Stufe bis 5.000 Euro, eine
bekannte Ausnahme ist der Surface Pro 12 5G in der Stufe bis 10.000.

Ausgabe: zwei getrennte Blob-Container. `pricelist-public` mit der öffentlichen Datei, nur Raten, für
den Shop. `pricelist-internal` mit EK und VK, ausschließlich intern, nie öffentlich. Vor jedem
Überschreiben sichert die Pipeline die letzte gute Version und prüft Plausibilität (genug Artikel,
gültige Raten, kein Einbruch), bei Fehlschlag bleibt die alte Datei live.

### 8.2 Datenvertrag der öffentlichen Datei
Verbindliche Form in `contracts/DATA-CONTRACT.md`, Beispiel in `data/products.sample.json`. Kurz:
- Öffentlich sind nur fertige Monatsraten, keine EK-, VK- oder Faktorwerte.
- Je Produkt: sku, msku, manufacturer, name, title_raw, rates.leasing und rates.finanzierung mit je
  {term, net, gross}, rate_from als günstigste Kombination für die Anzeige "ab X pro Monat". net ist
  Standard, gross (mal 1,19) liegt als Komfortfeld dabei.
- Optionale Felder, defensiv behandeln: size_inch, os, is_5g, without_charger.
- Vorwärtskompatibel, kommen später aus der Pipeline: availability {status, stock} mit status in
  in_stock, incoming, out_of_stock, sowie display_name und specs {cpu, ram_gb, storage_gb, color,
  screen_inch, generation}. Die App baut bereits jetzt dagegen und zeigt sie, sobald sie da sind.
- Vertragsarten und Laufzeiten: Leasing 15, 24, 32, 36. Finanzierung 15, 24, 36.

### 8.3 Datenfluss in die App (Variante A)
Die Pipeline lädt ihre fertige öffentliche Datei am Ende des Laufs zusätzlich als `products.json` in
den Bucket `slshopv2-media`. Die App liest immer aus dem Bucket, eine Quelle, kein Cloud-übergreifender
Laufzeit-Aufruf. Einmaliger Aufwand: die Pipeline braucht einen GCS-Dienstkonto-Schlüssel, abgelegt
im Azure Key Vault.

### 8.4 Handgepflegte Begleitdateien
- `data/product-overrides.json`: Hervorhebungen je MSKU, also featured, badge, priority, marketing.
  So lassen sich Geräte bewerben und hervorheben, ohne die App anzufassen.
- `data/images.json`: optionales Mapping MSKU auf Bilddatei, nur nötig bei abweichenden Namen.
Beide werden im Repo gepflegt und danach in den Bucket synchronisiert.

### 8.5 Lizenzen und Services
`licenses.json` (Microsoft 365, Copilot) und `services.json` gibt es noch nicht. Sie entstehen im
selben Schema (meta, items, rates). Offen ist die Quelle der Lizenzpreise, das klärt Sascha.

---

## 9. Bildkonzept

Maßgeblich ist contracts/IMAGES.md, dort steht die vollständige Spezifikation. Diese Kurzfassung ersetzt das
frühere Modell mit starrer MSKU-Benennung.
- Bilder liegen im Bucket unter `images/`. Dateien sind je Bildmodell benannt (slug) mit sprechenden
  Suffixen, nicht mehr starr nach MSKU.
- Die Datei `data/images.json` (version 2) ist die maßgebliche Bildschicht: ein Block `models` mit
  slug, family, Hauptbild, Vorschau und gallery, plus ein flaches `map`, das jede MSKU auf einen
  Bildmodell-slug abbildet. Ein Fotoset je einzigartiger Kombination aus Familie, Generation,
  Bildschirmgröße und Farbe, unabhängig von CPU, RAM, Speicher, OS oder Konnektivität.
- Der Shop-Resolver liest `images.json`, löst die MSKU über `map` auf den slug auf und zeigt Hauptbild,
  Vorschau und optional die Galerie. Fallback: `_fallback-{familySlug}.webp`, dann `_fallback.webp`.
- Format WebP, Qualität etwa 80. Hauptbild bis 1200 x 1200, Gerät eingepasst, nicht beschnitten, weißer
  oder transparenter Hintergrund. Vorschaubild bis 400 x 400, gleiches Framing.
- Öffentlicher Aufruf: `https://storage.googleapis.com/slshopv2-media/images/{name}`.
- Die Bildaufbereitung läuft im eigenen Bild-Chat, der `images.json` pflegt. Bilder blockieren den Start
  nicht, der Shop baut gegen Platzhalter, echte Bilder greifen automatisch über die Zuordnung.
- Später optional ein eigener Hostname wie cdn.surface.love über Cloudflare vor dem Bucket, ohne
  Codeänderung.

---

## 10. Hosting und Domains

- Produktion in europe-west1, aus drei Gründen: die Region kann die Cloud-Run-Domainzuordnung,
  europe-west2 (Standard der AI-Studio-Veröffentlichung) kann das nicht. Sie liegt in der EU, sauber
  für deutsche Geschäftskundendaten. Und sie ist nah am Kernmarkt.
- USA nicht als Standort. Die USA ist in unserer Architektur ein Daten- und Marktthema, kein
  Hosting-Umzug. Ein EU-Dienst kann später denselben US-Datensatz ausliefern. Erst bei echtem
  US-Traffic ist der saubere Ausbau ein globaler Lastverteiler mit mehreren Regionen.
- Domainzuordnung: Cloud Run bietet drei Wege. Der globale externe Application Load Balancer ist von
  Google als produktiv empfohlen. Die Cloud-Run-Domainzuordnung ist Vorschau und nur in bestimmten
  Regionen verfügbar, darunter europe-west1. Firebase Hosting ist die dritte Option. Da Cloudflare
  bei uns die Kante ist (DNS, CDN, WAF, Turnstile), genügt zum Start die Domainzuordnung in
  europe-west1 mit Cloudflare als DNS only. Der Umstieg auf den Load Balancer ist später ohne
  App-Änderung möglich.
- Cloudflare-Einträge: CNAME `www` auf `ghs.googlehosted.com`, DNS only (graue Wolke), Apex per
  Weiterleitung auf www. Domainbestätigung bei Google per TXT. Wichtige Falle: wenn Cloudflare als CDN
  davor proxyt, muss unter SSL/TLS, Edge-Zertifikate die Option "Always use https" aus sein, sonst
  scheitert die Validierung oder die Zertifikatserneuerung.
- surface.love ist Phase 10. Bis dahin ist die Seite unter der run.app-Adresse erreichbar.

---

## 11. Integrationen und Anfrage-Endpoint

Konkrete IDs, Tenant und Schlüssel liegen nicht hier, sondern in Secret Manager und einer privaten
Ablage. Hier nur das Konzept.

### 11.1 E-Mail über Microsoft Graph
- App-only Versand über Microsoft Graph sendMail. Absender ist das geteilte Postfach
  `shop@surface.love`. Antwortadresse (Reply-To) ist `sales@surface.love`, gesetzt im Backend.
- Berechtigung Mail.Send als Anwendung, Administratorzustimmung erteilt. Eingegrenzt über RBAC for
  Applications, also der moderne Weg, nicht die alte Application Access Policy: ein Exchange-Service-
  Principal-Zeiger, ein Management Scope auf das Attribut CustomAttribute1 gleich SLWebMailer, und
  eine Rollenzuweisung Application Mail.Send auf genau diesen Scope. Die App kann dadurch
  ausschließlich als `shop@surface.love` senden.
- Hinweis: der RBAC-Cache greift erst nach bis zu zwei Stunden, der allererste echte Sendeversuch kann
  daher verzögert sein.
- Warum nicht die Sales-Gruppe als Absender: `sales.de@surface.love` und `sales@surface.love` gehören
  einer Microsoft-365-Gruppe, app-only kann nicht als Gruppe senden. Deshalb das eigene geteilte
  Postfach shop@ als technischer Absender, Reply-To zurück auf sales@.

### 11.2 HubSpot
- HubSpot-Konto vorhanden. Zugriff über einen Service-Schlüssel, den modernen Weg, der die alten
  Private Apps ablöst. Scopes je lesen und schreiben für contacts, companies, deals.
- Eine Pipeline, daher Pipeline-Kennung "default", erste Deal-Stufe "appointmentscheduled".
- Ablauf bei einer Anfrage: Kontakt per E-Mail upserten (erst suchen, dann aktualisieren oder neu
  anlegen), dann einen Deal anlegen und mit dem Kontakt verknüpfen.

### 11.3 Cloudflare Turnstile
- Widget in Cloudflare angelegt, Modus Managed, Hostnamen umfassen surface.love und die run.app-
  Adresse. Öffentlicher Sitekey im Frontend, geheimer Key serverseitig zur Prüfung.

### 11.4 Endpoint /api/anfrage
Ablauf, jeder externe Aufruf in eigenem try/catch, nie ein Geheimnis loggen:
1. Einfaches Rate-Limit je IP, etwa fünf Anfragen je 60 Sekunden, sonst 429.
2. Pflichtfelder firma, name, email prüfen, sonst 400.
3. Turnstile serverseitig prüfen, bei Fehlschlag 400.
4. HubSpot, nur wenn aktiviert, Kontakt upserten und Deal anlegen, Fehler nur loggen.
5. E-Mail über Graph, nur wenn aktiviert, Token holen, sendMail an das interne Ziel mit
   übersichtlicher HTML-Darstellung samt Artikeltabelle, Reply-To auf die Kundenadresse.
6. Sobald Validierung und Turnstile in Ordnung sind, immer mit 200 und der Anfrage-ID antworten, auch
   wenn HubSpot oder Mail intern scheitern. Diese beiden dürfen die Browser-Antwort nie kippen.
Der Endpoint wird in FastAPI mit httpx umgesetzt, inhaltlich identisch zum früheren Node-Entwurf.

### 11.5 Umgebungsvariablen (Werte im Secret Manager)
GRAPH_TENANT_ID, GRAPH_CLIENT_ID, GRAPH_CLIENT_SECRET, MAIL_SENDER (shop@surface.love), MAIL_ENABLED,
MAIL_TO (Default sales@surface.love), HUBSPOT_ACCESS_TOKEN, HUBSPOT_ENABLED, HUBSPOT_PIPELINE_ID
(default), HUBSPOT_DEAL_STAGE_ID (appointmentscheduled), TURNSTILE_SECRET, und öffentlich der
Turnstile-Sitekey. Diese Variablen müssen am neuen slshopv2-Dienst gesetzt werden, der bisherige
Vorschau-Dienst in west2 kennt sie nicht.

---

## 12. Sicherheit und Datenschutz

- Keine Geheimnisse im öffentlichen Repo, keine EK- oder VK-Werte, keine Leasingfaktoren im Frontend.
- Schlüssel im Secret Manager, der interne Preis-Container nie öffentlich.
- EU-Hosting für deutsche Geschäftskundendaten. Turnstile gegen Spam, Rate-Limit am Endpoint.
- Datenschutz, Impressum, AGB nach aktuellem Rechtsstand, DDG statt TMG.

---

## 13. Repos, Tooling, Rollen, Zusammenarbeit

Repos:
- `desktop365/sl-shop-hub` (öffentlich): zentrale Ablage. Datenvertrag, Design- und UX-Vorgabe,
  dieses Konzeptpapier, Phasenplan, Beispieldaten, Brand-Tokens, der Kontext-Block für AI-Studio-
  Prompts, und die handgepflegten Dateien product-overrides.json und images.json. Roh-Zugriff über
  raw.githubusercontent.com, damit kein Kopieren über den PC nötig ist.
- App-Repo für den FastAPI-Code von slshopv2, aus dem Cloud Build deployt. Genauer Name wird
  bestätigt (offener Punkt).
- `Surface.Love` in Azure DevOps, Repo `surface-love-pricing`: die Preis-Pipeline. Getrennt von der
  Shop-App, der echte Stand liegt auf dem Branch master.

Rollen der Beteiligten:
- Google AI Studio: baut die App slshopv2, Phase für Phase, jeder Prompt mit vorangestelltem
  Kontext-Block.
- VS-Code-Chat Preis-Pipeline: die Azure-Function, Berechnung und Bereitstellung der products.json.
- Bild-Chat: Aufbereitung und Benennung der Produktbilder für den Bucket.
- Claude: Planung, Konzept, Prompts, Architekturentscheidungen.

Konventionen: Kommunikation auf Deutsch, keine langen Bindestriche, echte Umlaute, Befehle möglichst
gebündelt. Vor jedem Azure-, CLI- oder Graph-Befehl die Syntax über Microsoft Learn prüfen. Für die
VS-Code-Umgebung gelten zusätzlich die bestehenden Hausregeln (Tab-Modell, Auth-Dualität in DevOps).

---

## 14. Bauplan in Phasen mit Abnahmekriterien

Regel für jede Phase: eine Sorge pro Prompt, danach testen, in GitHub pushen, benannten Checkpoint
setzen. Bricht etwas, zurück auf den letzten guten Stand statt weiterzureparieren.

- Phase 0, Fundament. Erledigt: minimale FastAPI-Landingpage in europe-west1, Repos verbunden,
  zentrale Ablage steht. Abnahme: Dienst antwortet, Repos erreichbar.
- Phase 1, Grundgerüst, Designsystem, dünne i18n-Schicht (de), Geräteübersicht gegen
  products.sample.json. Abnahme: deutsche Startseite und Katalog laden aus der Beispieldatei, keine
  erfundenen Produkte, Designtokens und Herz sitzen, DE einzige sichtbare Sprache.
- Phase 2, Datenschicht und Markt-Config (DE aktiv, US definiert und deaktiviert), Währungs- und
  Steuer-Formatter. Abnahme: Markt- und Sprachgerüst steht, Preise und Steuer kommen aus der Config,
  DE-Seite unverändert.
- Phase 3, Produktdetail mit Vertragsart und Laufzeit, Rate, Verfügbarkeitsanzeige, Hervorhebungen aus
  den Overrides. Abnahme: Umschalter aktualisiert die Rate sofort, Verfügbarkeit und Badges erscheinen.
- Phase 4, Bildauflösung gegen den Bucket. Abnahme: echte Bilder greifen über die Namenskonvention,
  Fallback sauber, kein Flackern.
- Phase 5, Anfragekorb und Checkout mit Anfrage-ID, ohne echten Versand. Abnahme: Korb summiert,
  Pflichtfelder und DSGVO greifen, ID wird erzeugt, Bestätigung erscheint.
- Phase 6, Zubehör, Microsoft 365, Services, datengetrieben. Abnahme: Bereiche laden aus ihren Dateien.
- Phase 7, Backend /api/anfrage in FastAPI mit Turnstile, HubSpot, Graph-Mail. Abnahme: Testanfrage
  erzeugt einen Deal in HubSpot und eine Mail an Sales (RBAC-Cache bis zwei Stunden beachten).
- Phase 8, Vorteilsseite Surface as a Service (conversion-kritisch, direkt nach dem Anfrage-Kern),
  dann übrige Inhalts- und Rechtsseiten, SEO. Abnahme: Vorteile und Sorglos-Paket klar herausgestellt,
  Rechtsseiten vorhanden.
- Phase 9, zweite i18n-Scheibe, Marktumschaltung und en-Wörterbuch, erst wenn alles stabil läuft.
- Phase 10, Domain surface.love, west1-Dienst aus GitHub, Domainzuordnung, Cloudflare, Zertifikat.
- Später, eigene Interaktionsphase: ROI-Rechner auf der Vorteilsseite.

---

## 15. Lehren aus dem ersten Anlauf und Arbeitsregeln

Der erste Anlauf scheiterte an einem einzigen i18n-Mega-Prompt, der Datenladeschicht, Steuerlogik,
Zustand und Routing gleichzeitig umbaute. Eine Inkonsistenz reichte für den Totalausfall, die
folgenden Reparatur-Prompts auf bereits kaputtem Stand eskalierten zum Totalschaden. Daraus die
verbindlichen Regeln:

1. Eine Sorge pro Prompt. Nie ein großer Mehrzweck-Umbau.
2. i18n und andere strukturelle Themen nur in dünnen, isolierten Scheiben.
3. Nach jeder Phase testen, in GitHub pushen, benannten Checkpoint setzen. Externe Sicherung ist
   Pflicht, nicht Kür.
4. Bricht etwas, sofort auf den letzten guten Stand zurück, nicht auf kaputtem Stand weiterreparieren.
5. Erst den Datenvertrag festzurren, dann bauen, sonst erfindet das Modell Produkte.
6. Produktion gehört nach europe-west1, die AI-Studio-Vorschau in west2 ist nur Vorschau.

---

## 16. Offene Entscheidungen und Risiken

- Frontend-Aufbau: gebaute Single-Page-Oberfläche, ausgeliefert von FastAPI, ist die Empfehlung. Der
  genaue Schnitt zwischen Server und Client wird beim ersten Frontend-Prompt festgezurrt.
- App-Repo für slshopv2 und die Cloud-Build-Anbindung: Name und Verbindung bestätigen.
- Anreicherung der Daten um Verfügbarkeit, display_name und specs: kleine Pipeline-Änderung plus eine
  MSKU-Mapping-Tabelle und ein erneuter Listenzug. Vorwärtskompatibel, blockiert den Start nicht.
- Quelle der Lizenz- und Servicepreise: offen, klärt Sascha.
- Bildbenennung nach MSKU: läuft im eigenen Bild-Chat.
- Namensvereinheitlichung: kanonisch heißt die Datei im Bucket products.json, die Pipeline-Ausgabe
  wird unter diesem Namen abgelegt.
- Firmen- und Rechtsdaten für Impressum, Datenschutz, AGB: liefert Sascha für Phase 8.
- Optionaler eigener Bild-Hostname cdn.surface.love: später, ohne Codeänderung.

---

## 17. Referenzen im Repo

- README.md, Überblick und Datenfluss
- PROJECT.md, Zielbild, Positionierung, Branding
- DESIGN.md und brand/tokens.css, Designsprache und Tokens
- UX.md, Wizard und Bedienregeln
- contracts/DATA-CONTRACT.md und data/products.sample.json, Datenform
- PLAN.md, Phasenplan
- prompts/00-context.md, Kontext-Block für AI-Studio-Prompts
- brand/SL_Heart_RGB.svg und brand/colors.md, Logo und Farben
