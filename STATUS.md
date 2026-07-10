# Projektstatus Surface as a Service Shop (slshopv2)

Zusammenführung der drei parallelen Arbeitsstränge nach einer Pause. Stand: 10.07.2026.
Stränge: Shop-App (Google AI Studio), Preis-Pipeline (Azure), Bild-Chat (images.json und Bilder).

## Kurzfassung
- Shop-App: Phasen 1 bis 3 in AI Studio gebaut. Phase 1 und 2 abgenommen und per Checkpoint gesichert.
  Phase 3 (Produktdetail) gebaut, die abschließende Regressionsprüfung und der Checkpoint stehen noch aus.
- Preis-Pipeline: rechnet aus der echten Microsoft-Liste 358 Surface-Artikel, nur Raten, plus Verfügbarkeit
  und Specs. Läuft aber noch nicht in den GCS-Bucket, die Brücke Azure Blob nach GCS fehlt, der
  Function-Deploy ist nicht bestätigt.
- Bild-Chat: Bildkonzept deutlich weiterentwickelt zu images.json v2 (Modelle plus Mapping, Galerien).
  Rund 25 Fotosets identifiziert, vier offene Fragen, noch keine Bilder verarbeitet oder im Bucket.
- Wichtig: Bildansatz und Datenvertrag haben sich seit dem ursprünglichen Konzept verändert. Das Repo
  (images.json, Abschnitt Bildkonzept) muss angepasst werden, bevor die Bild-Phase im Shop gebaut wird.

## 1. Shop-App (Google AI Studio, Frontend)
Architektur unverändert: React, TypeScript, Tailwind als statisch baubare SPA, später von FastAPI in
europe-west1 ausgeliefert, Daten aus dem Bucket (Variante A).
- Phase 0: FastAPI-Grundgerüst in west1 steht.
- Phase 1, abgenommen und Checkpoint: Grundgerüst, Navigation, Designsystem (cyanes schlagendes Herz,
  Slogan work love balance klein, Segoe-Stapel, Tokens, Cyan nur für Rate, primären Button, aktives Navi
  und Pille), deutsche i18n-Schicht, Geräteübersicht gegen products.sample.json mit Suche und Sortierung,
  marketingstarker zweispaltiger Hero, 0800-SURFACE als Vanity mit Ziffern bei Mouseover, sentence-case-Labels.
- Phase 2, abgenommen und Checkpoint: Markt-Registry mit DE aktiv und US definiert, deaktiviert und
  ausgeblendet. Zentraler Währungs- und Steuer-Formatter (locale, currency, taxModel des aktiven Marktes).
  Datenquelle über markt.dataBase plus markt.productsFile. en-Wörterbuch als Stub mit Rückfall auf de.
  Kontaktdaten aus dem Markt.
- Phase 3, gebaut, Abnahme offen: Produktdetailseite je Gerät unter /geraete/{msku}, Umschalter
  Vertragsart und Laufzeit mit Live-Rate, Vorauswahl der rate_from-Kombination, Verfügbarkeitsanzeige,
  Hervorhebungen aus product-overrides.json (badge, marketing), ruhige nicht-gefunden-Ansicht, primärer
  Button Zur Anfrage hinzufügen noch ohne Logik (TODO für die Korb-Phase).
- Offen: 5-Punkte-Regressionsprüfung (Detailseite Rate 67,11 und 79,86, Umschalten, nur reale Laufzeiten,
  Verfügbarkeit und Badge, Direktaufruf und nicht-gefunden, alte Seiten unverändert), dann push und
  Checkpoint Phase 3.
- Läuft aktuell gegen die Beispieldaten products.sample.json und product-overrides.json aus dem Repo,
  noch nicht gegen Live-Daten aus dem Bucket.

## 2. Preis-Pipeline (Azure Functions, Produktdaten)
- Provisionierung abgeschlossen (Shell-Escaping über Temp-Dateien gelöst, Key Vault RBAC deaktiviert).
- Title-zu-Specs-Parser gebaut, aus der echten 1031-Zeilen-Microsoft-CSV entstehen 358 Surface-Artikel,
  ohne EK, VK oder Faktoren im öffentlichen File.
- Datenvertrag erweitert: availability {status, stock} plus optional display_name und specs {cpu, ram_gb,
  storage_gb, color, screen_inch, generation} aus einer MSKU-Mapping-Tabelle.
- Kanonischer Dateiname products.json. Stand committet in Azure DevOps (f50478d).
- Offen und teils blockierend für den Shop:
  - Brücke Azure Blob nach GCS-Bucket slshopv2-media noch nicht gebaut. Bis dahin fließen keine Live-Daten
    in den Shop.
  - Function-Deploy nicht als laufend und blob-schreibend bestätigt.
  - Specs-Entwurf für alle 358 Artikel erzeugt, aber noch nicht geprüft, nach data/product_specs.json
    übernommen und neu exportiert. Daher noch keine display_name und specs im Live-Output.
  - Statuswert unknown ist nicht im veröffentlichten Vertrag. Entscheidung: entweder unknown in den Vertrag
    aufnehmen, oder die Pipeline lässt das Feld weg, wenn unbekannt. Der Shop behandelt fehlende
    Verfügbarkeit sicher als auf Anfrage (grau).

## 3. Bild-Chat (images.json und Bilder)
- Rolle: ausschließlich Bilder und die Datei images.json, keine Preise.
- Bildkonzept weiterentwickelt: von einem Bild je Produkt zu Mehrwinkel-Galerien je Bildmodell mit
  sprechenden Suffixen.
- Neues Schema images.json version 2: ein Block models mit slug, family, Hauptbild, Vorschaubild und
  gallery, sowie ein flaches map, das jede Varianten-MSKU auf einen Bildmodell-slug zeigt. Ein Fotoset je
  einzigartiger Kombination aus Familie, Generation, Bildschirmgröße und Farbe, unabhängig von CPU, RAM,
  Speicher, OS oder Konnektivität.
- Rund 25 Fotosets identifiziert (etwa 9 Geräte- und 16 Zubehör-Bildmodelle) plus ein generisches
  Service-Fallback.
- Vier offene Fragen: Pro 12 Zoll Snapdragon gegen Pro 13 Zoll Intel wirklich andere Bildschirmgröße,
  Laptop 13 Zoll in Schwarz vorhanden, Generation des Laptop 5G und ob er Fotos mit Laptop 8 teilt,
  Slim-Pen-Bundles eigene Fotos oder Tastaturbild.
- Workflow: Quellbilder über das GitHub-Repo oder als ZIP, Upload in den Bucket über Cloud Shell durch Sascha.
- Stand: Schema steht, aber noch keine Bilder verarbeitet oder im Bucket.

## Reconciliation, vor der Bild-Phase im Shop zu erledigen
Der Bildansatz ist über das ursprüngliche Konzept hinausgewachsen. Anzupassen:
- KONZEPT.md Abschnitt 9 (Bildkonzept): von {MSKU}.webp plus Fallback auf das images.json-v2-Modell
  umstellen, also MSKU auf Bildmodell-slug, je Modell Hauptbild, Vorschau und Galerie.
- data/images.json im Repo: vom leeren Platzhalter auf das v2-Schema (models plus map) bringen, sobald der
  Bild-Chat die Matrix und die vier offenen Fragen final hat.
- DATA-CONTRACT.md und DETAILS.md: den Verweis auf images.json als einfache Zuordnung auf die neue Rolle
  als maßgebliche Bildschicht mit Galerien schärfen.
- Der Shop-Bild-Resolver liest dann images.json v2, löst MSKU auf slug auf und zeigt Hauptbild, Vorschau
  und optional Galerie, mit Fallback über die Familie. Dateinamen kommen aus images.json, nicht mehr starr
  aus der MSKU.

## Empfohlene nächste Schritte
1. Phase 3 sauber abschließen: 5-Punkte-Regressionsprüfung, dann push und Checkpoint Phase 3.
2. Repo an den neuen Stand angleichen (Bildkonzept v2, Datenvertrag um availability, display_name und specs
   geschärft), damit alle Beteiligten dieselbe Grundlage haben.
3. Zwei unabhängige Zulieferstränge vorantreiben:
   a. Preis-Pipeline: Brücke Blob nach GCS bauen und Function-Deploy bestätigen, damit products.json live im
      Bucket landet. Specs prüfen und exportieren.
   b. Bild-Chat: vier offene Fragen klären, Matrix und images.json v2 finalisieren, erste Bilder in den Bucket.
4. Dann im Shop die Bild-Phase gegen images.json v2 bauen (mit Platzhaltern lauffähig, echte Bilder greifen
   automatisch), danach Anfragekorb und Checkout, Backend-Anfrage, Vorteilsseite, i18n-Umschaltung, Domain.
