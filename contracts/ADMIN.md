# ADMIN, das Steuer-Backend des Shops

## Zweck
Sascha steuert den Shop ohne Deployment und ohne Code. Das Admin-Backend ist die
Oberflaeche ueber Konfigurationsdaten, nie deren einziger Speicherort.

## Grundprinzip: Konfiguration ist Daten
Jede Stellschraube liegt als Datum in der Datenbank oder als Datei im Bucket,
nie hart im Code. Eine Funktion ins Backend rausziehen heisst: Wert wird zu
Daten, Maske bekommt ein Feld. Der Shop liest Konfiguration zur Laufzeit.

## Scope in zwei Stufen
- Stufe 1, Vorfilter in der Preis-Pipeline: Hersteller und grobe Kategorien.
  Haelt die oeffentliche products.json klein. Konfiguration liegt zunaechst
  versioniert im privaten Pricing-Repo, perspektivisch als config/scope.json im
  Bucket, vom Admin-Backend geschrieben, von der Pipeline je Lauf gelesen.
  Heute: Surface komplett.
- Stufe 2, Feinkuration im Shop: je Artikel sichtbar oder nicht, sofort wirksam,
  ohne Pipeline-Lauf. Kein Warten auf 04:00 UTC.

## Eiserne Trennung der Datenarten
- Feed-Daten: Produkte, Raten, Namen. Der Sync ueberschreibt sie bei jedem Lauf.
- Kurations-Daten: Sichtbarkeit, Notizen, spaeter Anzeigenamen und Zuordnungen.
  Schreibt nur das Admin-Backend. Der Sync fasst sie NIE an.
- Verknuepfung ueber die MSKU. Fehlt zu einem Artikel ein Kurationseintrag,
  gilt die Erstauftauchen-Politik seines Herstellers.

## Erstauftauchen-Politik
Je Hersteller ein Standard fuer neu auftauchende Artikel:
- microsoft: sichtbar
- alle anderen (kuenftig lenovo): unsichtbar bis kuratiert
Damit erscheint bei einer Scope-Erweiterung kein Artikel ungefragt im Shop.

## Was der Admin nie kann
- Preise oder Raten aendern. Raten kommen ausschliesslich aus der Pipeline.
- EK, VK oder Faktoren sehen. Diese Werte existieren im Shop-System nicht.
- Die Kommerzwelt ersetzen. Kontakte, Deals, Angebote bleiben in HubSpot.

## Ausbaustufe 1, die erste Maske
- Zugang: ein Admin-Konto, Zugangsdaten als Umgebungsvariablen, Session-Cookie,
  kein oeffentlicher Link, noindex. Spaeter echte Benutzerverwaltung.
- Katalog-Steuerung: Liste aus dem Leseabbild mit Suche und Filtern nach
  Hersteller und Familie, Sichtbarkeit je Artikel und als Massenaktion.
- Sync-Karte: Datenstand source_date, letzter Sync, Zaehler, Knopf fuer
  Trockenlauf und echten Lauf ueber die geschuetzte Sync-Route.
- Datenstand-Karte: Artikel gesamt, sichtbar, je Hersteller und Familie.

## Ausbaustufen, benannt und offen
Promotions-Pflege, Anzeigenamen und MSKU-Zuordnung, Bildzuordnungs-Uebersicht,
Anfragen-Uebersicht sobald der Anfrage-Endpunkt existiert, Verlagerung der
Scope-Stufe 1 in den Bucket, Lenovo-Onboarding als erster Ernstfall der Kuration.
Die Kategorie-Substanz (wg1, lwg1, wg2, articleType) pflegt der Preislisten-Chat
nach dem Sortiments-Abruf in diesen Kontrakt ein.

## Nicht-Ziele
Kein CMS, kein zweites HubSpot, keine Preispflege, keine Bildbearbeitung.
