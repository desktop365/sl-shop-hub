# Phasenplan und Lehren

## Lehren aus dem ersten Anlauf
- Ein einziger i18n-Mega-Prompt hat Datenladeschicht, Steuerlogik, Zustand und Routing zugleich
  umgebaut, eine Inkonsistenz reichte fuer den Totalausfall. Daher: i18n nur in duennen Scheiben.
- Keine externe Sicherung. Daher: GitHub-Sync und Checkpoint nach jeder Phase.
- Reparatur-Prompts auf kaputtem Stand eskalierten zum Totalschaden. Daher: bei Bruch zurueck, nicht weiter.
- Region-Falle: AI-Studio-Deploy in west2 kann keine eigene Domain. Produktion daher west1.
- Erst Datenvertrag festzurren, dann bauen, sonst erfindet das Modell Produkte.

## Phasen
0  Fundament: FastAPI in west1 steht, Repo verbunden, Checkpoint- und Sync-Disziplin. (erledigt)
1  Grundgeruest, Designsystem, duenne i18n-Schicht (de), DE einzige sichtbare Sprache, Geraeteuebersicht
   gegen products.sample.json.
2  Datenschicht und Markt-Config (DE aktiv, US definiert und deaktiviert), Waehrungs- und Steuer-Formatter.
3  Produktdetail mit Vertragsart und Laufzeit, Rate, Verfuegbarkeitsanzeige, Hervorhebungen aus Overrides.
4  Bildaufloesung gegen den Bucket.
5  Anfragekorb und Checkout mit Anfrage-ID, ohne echten Versand.
6  Zubehoer, Microsoft 365, Services, datengetrieben.
7  Backend /api/anfrage in FastAPI: Turnstile, HubSpot, Graph-Mail ueber shop@surface.love.
8  Vorteilsseite Surface as a Service (conversion-kritisch, frueh nach dem Anfrage-Kern), dann uebrige
   Inhalts- und Rechtsseiten, SEO.
9  Zweite i18n-Scheibe: Marktumschaltung und en-Woerterbuch, erst wenn alles stabil.
10 Domain surface.love: west1-Dienst aus GitHub, Domainzuordnung, Cloudflare, Zertifikat.
   ROI-Rechner als eigene spaetere Interaktionsphase.
