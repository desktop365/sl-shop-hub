# Surface.Love, Arbeitsweise und Repo-Struktur

Betriebshandbuch für den Aufbau. Dieses Dokument legt fest, welche Oberfläche was tut, was sie liefert, in welcher Form, und wo alles abgelegt wird. Es gehört ins Hub-Repo, alle Oberflächen richten sich danach.

## 1. Prinzip
- Die Brücke ist das Hub-Repo, nicht Copy-Paste. Entscheidungen und Vorgaben werden dort abgelegt, Claude Code und die Agenten lesen sie von dort.
- Ein Master je Domäne, keine zwei Wahrheiten. HubSpot ist Master der kaufmännischen Welt, unser System ist Master der Produktwelt, die Datenbank ist das Leseabbild für den Shop.
- Wenige, klar getrennte Oberflächen. Denken im Strategie-Strang, Bauen in Claude Code, Betreiben in Cowork.

## 2. Die Oberflächen, wer was liefert

| Oberfläche | Rolle | liest | liefert | Ablage | Modell |
|---|---|---|---|---|---|
| Strategie und Architektur, Projekt-Chat | Entscheidungen, Landkarte, Vorgaben | dieses Handbuch, Landkarte | Specs und Kontrakte | Hub-Repo | Opus 4.8 |
| Bau, Claude Code, ein Workspace | Shop, Infra, Pricing, Bild-Tooling bauen | Hub-Repo, Kontrakte | Code, Deploys, Migrationen | Shop-Repo, Pipeline-Repos, Hostinger | Sonnet 5 Standard, Opus für harte Architektur, Haiku für Triviales |
| Betrieb, Cowork | Kundenkommunikation, Deals, Abos, Lifecycle | HubSpot, Mail | gepflegte kaufmännische Daten | HubSpot | Sonnet 5, Opus für große Kunden |
| Content und SEO, Cowork | Artikel, Blog, technisches SEO begleiten | Quellen, Hub | Beiträge, Metadaten | Blog, Shop-Repo | Sonnet 5, Opus für Flaggschiff-Artikel |

Kern sind zwei chatartige Stränge, Strategie hier und der Code-Workspace, plus ein bis zwei Cowork-Stränge für den Betrieb. Content darf anfangs im Betriebs-Cowork mitlaufen.

## 3. Die Repos

### 3.1 Übersicht
- **sl-shop-hub**, die Brücke und Quelle der Wahrheit für Specs und Kontrakte. GitHub desktop365/sl-shop-hub, lokal C:\Dev\sl-shop-hub. Kein Code, keine Secrets.
- **surface-love-shop**, die neue App. GitHub desktop365/surface-love-shop, lokal C:\Dev\surface-love-shop. Next.js plus MySQL, hier baut Claude Code.
- **surface-love-pricing**, die Preis-Pipeline für Neu-Raten. Azure DevOps desktop365/Surface.Love/surface-love-pricing, lokal C:\Dev\surface-love-pricing.
- **sl-bilder**, das Bild-Tooling. Neu als Repo desktop365/sl-bilder, lokal C:\Dev\sl-bilder.
- **SLSHOPAISTUDIO**, alter AI-Studio-Shop, nur Archiv und Nachschlagewerk, bleibt live bis zum Umschalten.

Alle vier liegen im selben VS-Code-Workspace C:\Admin\VSCode-Configs\_workspaces\Surface-Love.code-workspace, Claude Code sieht alles.

### 3.2 sl-shop-hub, Ordnerbaum
```
sl-shop-hub/
  README.md
  ARBEITSWEISE.md          dieses Handbuch
  LANDKARTE.md             Architektur-Landkarte
  PROJECT.md DESIGN.md UX.md KONZEPT.md DETAILS.md
  contracts/
    DATA-CONTRACT.md       products.json Schema
    IMAGES.md              images.json Schema
    DB-SCHEMA.md           MySQL Leseabbild, Bestand, Abo
    HUBSPOT.md             Felder, Pipeline-Stufen, kaufmännischer Master
    MARKETS.md             Sprachen, Währungen, Vertragsarten je Markt
    PROMOS.md              Aktionsregeln
    STOREFRONTS.md         Marken-Auftritte je Domain
  data/
    products.sample.json
    images.sample.json
  brand/
    SL_Heart_RGB.svg colors.md tokens.css
  prompts/
    00-context.md
    claude-code-kickoff.md
  CHANGELOG.md
```

### 3.3 surface-love-shop, Ordnerbaum
```
surface-love-shop/
  CLAUDE.md                Arbeitsanweisung, liegt bei
  README.md
  .env.example             ohne echte Werte
  package.json next.config.js
  app/
    [locale]/
      (shop)/              Katalog, Produktdetail, Anfrage, Refurbished, Checkout
      api/                 Anfrage, Stripe-Webhooks, HubSpot-Sync, Sync-Jobs
  components/              UI und Designsystem
  lib/                     HubSpot, Stripe, Graph-Mail, Formatter, Markt-Logik
  db/                      Schema, Migrationen, Sync
  content/                 i18n-Texte de, en
  config/                  markets, contract-types, storefronts
  public/
  docs/                    Verweis aufs Hub, lokale Notizen
```

### 3.4 Pipelines
- **surface-love-pricing** liest den Distributor-Feed, Surface und künftig Lenovo, und erzeugt products.json.
- **sl-bilder** verarbeitet Quellbilder mit Pillow, WebP, erzeugt Größen, nummeriert und lädt hoch, und schreibt images.json.

## 4. Die Verträge, in welcher Form

| Vertrag | Zweck | Form | Master | erzeugt von | gelesen von | Ablage |
|---|---|---|---|---|---|---|
| products.json | Neu-Katalog und Raten | JSON nach DATA-CONTRACT.md | Pricing-Pipeline | pricing-Repo | Shop, Sync nach MySQL | Datenstore, Schema und Sample im Hub |
| images.json | MSKU zu Fotoset | JSON nach IMAGES.md | Bild-Pipeline | sl-bilder | Shop | Datenstore oder Hub, Medien im Objektspeicher |
| DB-Schema | Leseabbild, Bestand, Abo-Status | SQL-Migrationen plus DB-SCHEMA.md | Shop-App | shop-Repo | Shop | MySQL, Doku im Hub |
| HubSpot-Map | Felder, Stufen, Deal, Firma, Kontakt, Abo | HUBSPOT.md | HubSpot | Agent über MCP | Shop und Agenten | HubSpot, Map im Hub |
| Markt-Config | Sprachen, Währungen, Vertragsarten je Markt | Config plus MARKETS.md | App-Config | shop-Repo | Shop und Pipeline | shop/config, Doku im Hub |
| Promotions | Preisaktionen | DB-Tabelle plus PROMOS.md | Datenbank, agent-gepflegt | Agent oder Admin | Shop und Checkout | MySQL, Doku im Hub |
| Storefronts | Marke, Domain, Hersteller-Filter, Recht, Absender | Config plus STOREFRONTS.md | App-Config | shop-Repo | Shop und Agenten | shop/config, Doku im Hub |
| Brand-Tokens | Farben, Typo, Radius | tokens.css | Hub | Strategie | Shop | Hub/brand |

## 5. Speicher-Plan, wo was liegt
- Specs, Verträge, Marke, Prompts liegen im **Hub-Repo**.
- App-Code liegt in **surface-love-shop**, dort auch die Storefront- und Markt-Config.
- Pipeline-Code liegt in **surface-love-pricing** und **sl-bilder**.
- Live-Katalog products.json und images.json gehen in den **Objektspeicher** und werden von dort nach MySQL synchronisiert.
- Medien, die Bilder als WebP, liegen im **Objektspeicher**, Ablageort noch offen, GCS oder Hostinger.
- Leseabbild, refurbished Bestand, Abo-Status und Promos liegen in **MySQL**.
- Kaufmännische Daten, Kontakte, Deals, Angebote, Abos, Rechnung, liegen in **HubSpot**.
- Abo und Zahlung laufen über **Stripe** und werden nach HubSpot gespiegelt.
- Secrets liegen nur als **Umgebungsvariable** der jeweiligen Oberfläche, nie im Repo.

## 6. Die Verbindungen, Flüsse
1. **Entscheidung zu Bau.** Strategie-Chat schreibt die Vorgabe ins Hub, Claude Code liest das Hub und baut im Shop-Repo, deployt zu Hostinger. Kein Kopieren.
2. **Neu-Katalog.** Distributor-Feed, Surface und Lenovo, zur Pricing-Pipeline, dann products.json in den Datenstore, Shop-Sync, MySQL, Shop. Der Katalog ist herstellerneutral, der Hersteller-Filter des Storefronts schneidet ihn beim Ausliefern zu.
3. **Bilder.** Quellbilder zur Bild-Pipeline, der Agent schneidet, konvertiert nach WebP, nummeriert und lädt hoch, in den Objektspeicher plus images.json, der Shop liest.
4. **Refurbished.** Rücklauf, Erfassung und Zustand, MySQL-Bestand, Shop, Kunde abonniert, Stripe, HubSpot-Abo und Rechnung, Versand, Bestand aktualisiert.
5. **Anfrage neu.** Shop zum Anfrage-Endpunkt, HubSpot-Deal und Graph-Mail, Agent bearbeitet kleine Fälle, eskaliert große. Marke, Storefront und Deal-Quelle gehen aus der erkannten Domain mit an den Deal.
6. **Kaufmännisch.** Shop und Agenten schreiben Geschäftsereignisse über API und MCP nach HubSpot, HubSpot bleibt Master.
7. **Storefront.** Der Aufruf trifft eine Domain, die App erkennt daraus den Storefront, lädt Marke, Optik, rechtliche Texte, Kontaktdaten und Absender, und wendet den Hersteller-Filter auf Katalog, Bestand, Suche und Empfehlungen an. Kein markenübergreifender Querverkauf. Alles Kaufmännische geht mit Marke und Deal-Quelle nach HubSpot, in die gemeinsame Pipeline.

## 7. Konventionen und Leitplanken
- Kundentext deutsch, echte Umlaute ä ö ü ß, keine langen Bindestriche, Komma statt.
- Nie Einkauf, Verkauf oder Leasingfaktoren öffentlich, nur Monatsraten.
- Preise nie schätzen, Eingabe über Widget.
- Ein HubSpot-Deal je Vertragsende, kein Bündeln verschiedener Enddaten.
- Ein Storefront ist ein Einmarken-Auftritt, kein markenübergreifender Querverkauf, kein Hinweis auf die andere Marke.
- Wir-Form in Kundenmails, Entwurf immer erst zeigen und bestätigen lassen, Allen antworten.
- Secrets nur als Umgebungsvariable, nie im Repo, im öffentlichen Hub keine internen Preise.
- Windows ARM, PowerShell, Terminalbefehle in wenige kopierbare Boxen.
- In jedem Code-Repo liegt ein Root-CLAUDE.md, damit Claude Code Konventionen und Hub-Pfade automatisch lädt, liegt als eigene Datei bei.

## 8. Startreihenfolge
1. Repo surface-love-shop anlegen, in den Workspace aufnehmen, CLAUDE.md ins Root legen.
2. Dieses Handbuch und die Landkarte ins Hub committen, die Kontrakte unter contracts anlegen.
3. sl-bilder als Repo initialisieren, in den Workspace aufnehmen.
4. MCPs einrichten, HubSpot und Mail im Betriebs-Cowork, Hostinger und GitHub in Claude Code.
5. Offenen Punkt Objektspeicher entscheiden, GCS behalten oder zu Hostinger.
6. Phase 0 in Claude Code starten, Next.js plus MySQL bei Hostinger, mehrsprachig, Designtokens aus dem Hub. Der Kickoff-Prompt liegt im Hub unter prompts.
