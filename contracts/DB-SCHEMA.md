# DB-Schema, Postgres

Status: Gerüst. Überschriften stehen, der Feininhalt folgt beim Bau von Phase 0 und Phase 2.

Maßgeblich für das Leseabbild des Katalogs, den refurbished Bestand, die Abos, die Promotions und das
Anfragen-Log. Master der Struktur ist das Shop-Repo, dort liegen die SQL-Migrationen. Dieses Dokument
beschreibt sie, es ersetzt sie nicht.

## 1. Zweck
- Wofür die Datenbank da ist und wofür ausdrücklich nicht.
- Abgrenzung zu den anderen Mastern: HubSpot ist kaufmännischer Master, die Preis-Pipeline ist Master
  des Neu-Katalogs, die Bild-Pipeline ist Master der Bildschicht.
- Grundsatz: keine internen Preise, keine Einkaufs- oder Faktorwerte in Feldern, die der Shop ausliefert.

## 2. Tabellen

### 2.1 Katalog, Leseabbild
- Zweck: der aus products.json synchronisierte Neu-Katalog, lesend für den Shop.
- Felder: noch offen, orientiert sich an [DATA-CONTRACT.md](DATA-CONTRACT.md).
- Sync-Quelle: products.json aus der Preis-Pipeline über den Objektspeicher, geplant täglich.

### 2.2 Refurbished Bestand
- Zweck: konkrete Einheiten aus eigenem Bestand, je Gerät eine Zeile.
- Felder: Seriennummer, Modellbezug, Zustand, Verfügbarkeit, Abo-Preis, optionale Übersteuerung je Einheit.
- Zustandsstufen und Verfügbarkeitsstufen: noch festzulegen.
- Sync-Quelle: eigene Erfassung im Shop-Backend, kein Distributor. Master ist diese Tabelle.

### 2.3 Abos, Stripe-Status
- Zweck: laufende Abos zu refurbished Geräten, Laufzeit, Zahlungsstatus.
- Felder: Stripe-Kennungen für Kunde, Abonnement und Preis, Status, Beginn, Ende, Bezug zur Bestandseinheit.
- Zusätzlich Marke und Storefront, siehe Abschnitt 5. Sie sagen, über welchen Auftritt das Abo entstand,
  und werden bei der Spiegelung nach HubSpot mitgegeben.
- Sync-Quelle: Stripe über Webhooks, Spiegelung nach HubSpot, siehe [HUBSPOT.md](HUBSPOT.md).

### 2.4 Promotions
- Zweck: Preisaktionen als Daten, ohne neues Deployment.
- Felder: Typ, Wert, Geltung, Zeitraum, Code, Banner, siehe [PROMOS.md](PROMOS.md).
- Sync-Quelle: Pflege über Admin oder Agent, Master ist diese Tabelle.

### 2.5 Anfragen-Log
- Zweck: Nachweis der eingegangenen Anfragen aus dem Neu-Zweig, technisch, nicht kaufmännisch.
- Felder: Anfrage-Kennung, Zeitpunkt, Warenkorb, Marke, Storefront, Markt, Sprache, Ergebnis der Übergabe
  an HubSpot und Mail. Marke und Storefront siehe Abschnitt 5.
- Sync-Quelle: der Anfrage-Endpunkt des Shops. Kaufmännischer Master des Vorgangs bleibt HubSpot.

## 3. Sync-Quellen in der Übersicht
Je Tabelle eine Zeile: Quelle, Richtung, Takt, wer schreibt, wer nur liest. Folgt beim Bau.

## 4. Migrationen und Versionierung
Ablage, Benennung und Reihenfolge der SQL-Migrationen im Shop-Repo. Folgt beim Bau.

## 5. Marke und Storefront als Querschnittsfelder
Jeder kundenbezogene Vorgang trägt, woher er kam. Zwei Felder, gemeinsam gesetzt:

- **Marke**, Werte Surface und Lenovo, gleicher Wertevorrat wie das Deal-Feld Marke in
  [HUBSPOT.md](HUBSPOT.md) Abschnitt 9.
- **Storefront**, die id aus [STOREFRONTS.md](STOREFRONTS.md) Abschnitt 3, zum Beispiel surface, lenovo.

Gesetzt werden sie beim Eingang aus der erkannten Domain, nicht aus einer Nutzereingabe. Sie stehen im
Anfragen-Log (Abschnitt 2.5) und in der Abo-Tabelle (Abschnitt 2.3) und gehen in die Deal- und
Abo-Spiegelung nach HubSpot mit.

Katalog und refurbished Bestand tragen die Felder nicht. Der Bestand ist markenübergreifend, welcher
Storefront ein Gerät zeigt, ergibt sich aus dem Hersteller-Filter, nicht aus einem Feld an der Einheit.
