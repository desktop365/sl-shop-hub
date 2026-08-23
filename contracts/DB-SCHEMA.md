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
- Sync-Quelle: Stripe über Webhooks, Spiegelung nach HubSpot, siehe [HUBSPOT.md](HUBSPOT.md).

### 2.4 Promotions
- Zweck: Preisaktionen als Daten, ohne neues Deployment.
- Felder: Typ, Wert, Geltung, Zeitraum, Code, Banner, siehe [PROMOS.md](PROMOS.md).
- Sync-Quelle: Pflege über Admin oder Agent, Master ist diese Tabelle.

### 2.5 Anfragen-Log
- Zweck: Nachweis der eingegangenen Anfragen aus dem Neu-Zweig, technisch, nicht kaufmännisch.
- Felder: Anfrage-Kennung, Zeitpunkt, Warenkorb, Markt, Sprache, Ergebnis der Übergabe an HubSpot und Mail.
- Sync-Quelle: der Anfrage-Endpunkt des Shops. Kaufmännischer Master des Vorgangs bleibt HubSpot.

## 3. Sync-Quellen in der Übersicht
Je Tabelle eine Zeile: Quelle, Richtung, Takt, wer schreibt, wer nur liest. Folgt beim Bau.

## 4. Migrationen und Versionierung
Ablage, Benennung und Reihenfolge der SQL-Migrationen im Shop-Repo. Folgt beim Bau.
