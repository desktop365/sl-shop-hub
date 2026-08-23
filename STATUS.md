# Surface.Love, Übergabe nach Phase 0

Übergabe an den nächsten Strategie-Chat, den Master-Prompter. Dieses Dokument orientiert und verweist auf das Hub-Repo, das die vollständigen Vorgaben trägt. Es ersetzt die bisherige STATUS.md.

## 1. Was Surface.Love ist
Zweigleisige B2B-Hardwarevermietung zur Monatsrate. Neugeräte über DLL-Leasing als Anfrage, refurbished aus eigenem Bestand im Abo über Stripe. Zwei Einmarken-Auftritte aus einer Codebasis, Surface unter surface.love, Lenovo unter lenovo.online, kein gemischter Shop. Mehrsprachig und mehrmarktfähig von Anfang an, Deutschland aktiv, USA vorbereitet.

## 2. Master-Modell, eine Wahrheit je Domäne
- HubSpot, kaufmännischer Master, Kontakte, Deals, Angebote, Abos, Rechnung, Kommunikation, Marketing. Portal 145452563, Professional.
- Preis-Pipeline, Master der Neu-Raten, erzeugt products.json.
- Bild-Pipeline, erzeugt images.json und die Bilder.
- Objektspeicher, GCS-Bucket slshopv2-media in europe-west2, hält die Medien und die Live-Dateien products.json und images.json.
- App-Datenbank MySQL, Leseabbild des Katalogs plus refurbished Bestand, Abo-Status, Promotionen, Anfragen-Log. Der Shop liest nur hieraus, nicht aus zwei Quellen.
- HubSpot Professional kann keine Custom Objects, keine Ratenmatrix, keine Bildergalerien. Produkte liegen dort nur als Positionen am Deal, nicht als Katalog.

## 3. Wo alles liegt
Ein VS-Code-Workspace, C:\Admin\VSCode-Configs\_workspaces\Surface-Love.code-workspace, bindet vier Repos ein:
- Hub, Quelle der Wahrheit, github.com/desktop365/sl-shop-hub, C:\Dev\sl-shop-hub. Öffentlich, Roh-Zugriff über raw.githubusercontent.com.
- Shop-App, github.com/desktop365/surface-love-shop, C:\Dev\surface-love-shop. Next.js plus MySQL.
- Preis-Pipeline, Azure DevOps surface-love-pricing, C:\Dev\surface-love-pricing.
- Bild-Pipeline, sl-bilder, C:\Dev\sl-bilder.
- Alter AI-Studio-Shop, SLSHOPAISTUDIO, nur Archiv, lokal als surface-love-shop-aistudio-archiv beiseitegelegt.

Hosting bei Hostinger, Business-Tarif, gemanagtes Node-Hosting, Server in Frankfurt, verwaltet aus Claude Code über das Hostinger-Plugin.

Domains: surface.love liegt bei Cloudflare und zeigt weiter auf den alten Shop, bleibt unberührt bis zum Umschalten. worklove.shop ist die vorläufige Arbeits- und Testadresse, komplett bei Hostinger, live mit Zertifikat. surface-service.com ist registriert, aber noch im Review wegen des Worts Surface.

## 4. Was in Phase 0 fertig ist
Die Shop-App steht als lebendiges Fundament, öffentlich erreichbar unter https://worklove.shop.
- Next.js App Router, TypeScript, Tailwind, mehrsprachig über [locale], Deutsch aktiv, Englisch vorbereitet.
- Storefronts, Surface aktiv mit Herz und Cyan, Lenovo vorbereitet als neutraler Platzhalter. Erkennung über den Hostnamen, in Produktion nur Hostname. worklove.shop als Testdomain des Surface-Storefronts hinterlegt, testHosts, mit noindex und ohne Kanonik, damit die Testseite nicht in den Index gerät.
- Designsystem aus brand/tokens.css, thembar je Storefront.
- MySQL-Datenbank u704706543_shop2, auf demselben Server wie die App, verbunden über 127.0.0.1. Die acht Tabellen aus DB-SCHEMA.md sind angelegt.
- Migration läuft automatisch bei jedem Deploy, das build-Skript ist prisma migrate deploy und danach next build.
- Umgebungsvariablen in Hostinger gesetzt, DATABASE_URL mit 127.0.0.1 und shop2, GCS_BASE_URL, NODE_ENV production, CATALOG_ALLOW_SEED false.
- Zustandsendpunkt /de/api/health liefert Storefront, Markt, Datenbankzustand und Katalogzahlen.
- Deploy automatisch bei jedem Push auf main über die GitHub-Anbindung.

## 5. Wichtige Learnings aus Phase 0
Damit der neue Chat nicht in dieselben Fallen läuft:
- Datenbankhost, localhost scheitert im Passenger-Kontext über einen Unix-Socket, 127.0.0.1 erzwingt TCP und funktioniert. Immer 127.0.0.1.
- App und Datenbank liegen bei diesem Tarif auf demselben Server, kein Fernzugriff nötig, keine Remote-Freischaltung.
- Ein Passwortwechsel im hPanel kann die Datenbank neu anlegen und auf einen anderen Server schieben. An der Datenbank nichts unbedacht ändern, für Phase 2 regelmäßige Backups vorsehen.
- Build-Abhängigkeiten, Pakete, die der Build braucht, etwa @tailwindcss/postcss, müssen in dependencies stehen, nicht nur devDependencies, weil der Hostinger-Build den Produktionsbaum nutzt. Dasselbe gilt bald für tsx, das der Sync braucht.
- Deploy-Weg, Web App über Deploy Web App, nicht der Git-Weg nach public_html und nicht Custom PHP/HTML. Die Node-App verwandelt die bestehende Website an Ort und Stelle, ohne Löschen.
- Website nie löschen, um neu anzulegen, das Löschen nimmt zugeordnete Datenbanken mit.

## 6. Was offen ist, der nächste Block
Der Katalog. Der Bucket ist leer, deshalb zeigt der Shop ehrlich null Geraete. Der Blocker liegt in den Pipelines, nicht mehr in der App. Wichtig, die Preis-Pipeline ist gebaut, aber nie End-zu-End bewiesen, sie hat noch nie in den Bucket geschrieben, und der Anfrage-Endpunkt ist im neuen Stack noch nicht gebaut. Deshalb gilt, erst pruefen, dann bauen.
Aufgaben des nächsten Blocks:
- Zuerst rein lesend pruefen, laeuft die Preis-Pipeline, ist der Distributor erreichbar, stimmen die Raten, siehe contracts/PRICING.md Abschnitt 5. Erst dann den Schreibweg in den Bucket bauen.
- Bild-Pipeline dazu bringen, images.json und die Bilder in den Bucket zu schreiben. Vorher die vier offenen Bildfragen klären, Pro 12 Zoll gegen 13 Zoll gleiche physische Größe, Laptop 13 Zoll in Schwarz, Laptop 5G welche Generation visuell, Slim-Pen-Bundles eigene Fotos.
- Sync auf dem Server lauffähig machen, tsx nach dependencies, dann läuft Bucket zu Datenbank.
- Danach erscheinen zum ersten Mal echte Geräte im Shop.

Weiter hinten in der Landkarte, in dieser Reihenfolge: Refurbished-Zweig mit eigenem Bestand und Stripe, Marketing und LinkedIn mit Attribution, Content-Agent für den Blog, Kundenportal in Version zwei, DLL-Bank-Anbindung, und der Domain-Umzug surface.love auf Hostinger.

Kleine Nacharbeit, vorgemerkt: die irreführende Meldung „Datenbank war nicht erreichbar" im Zustandsendpunkt schärfen. Die Umlaute in LANDKARTE.md sind bereits normalisiert.

## 7. Arbeitsweise und Oberflächen
- Die Brücke ist das Hub-Repo, nicht Copy-Paste. Strategie schreibt Vorgaben ins Hub, Claude Code liest sie dort und baut. Der neue Chat liest zuerst das Hub.
- Oberflächen, Strategie-Chat auf Opus 4.8, Bau in Claude Code auf Sonnet 5 mit Opus für harte Architektur und Haiku für Triviales, Design als normaler Chat, Betrieb und Content als Cowork erst später.
- Bei jeder kopierbaren Box angeben, in welchem Workspace und, bei Terminalbefehlen, in welchem Terminalprofil sie läuft. Claude Code öffnet einmal pro Workspace und wird über den Repo-Namen im Prompt gesteuert. Die Terminals sind davon unabhängig, nur für manuelle Git- und Shell-Befehle. Terminalprofile, Shop Hub, Shop App, Pricing Pipeline, Bilder.
- Deutsch, echte Umlaute, keine langen Bindestriche, Komma statt. Nie Einkauf, Verkauf oder Leasingfaktoren im Frontend, nur Monatsraten, Preise nie schätzen.

## 8. Zuerst lesen im Hub
Roh-URL-Muster, https://raw.githubusercontent.com/desktop365/sl-shop-hub/main/<pfad>
- ARBEITSWEISE.md, Rollen, Verträge, Flüsse, Repo-Struktur
- LANDKARTE.md, Architektur und Phasen
- contracts/, DATA-CONTRACT, PRICING, ANFRAGE, INFRA, IMAGES, DB-SCHEMA, HUBSPOT, MARKETS, PROMOS, STOREFRONTS
- brand/tokens.css, die Designtokens
