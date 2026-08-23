# HubSpot-Map

Status: Gerüst. Überschriften stehen, die konkreten internen Feldnamen und Stufen werden über den
HubSpot-MCP ausgelesen und hier eingetragen.

HubSpot ist der kaufmännische Master. Kontakte, Firmen, Deals und Abos werden dort geführt, der Shop und
die Agenten schreiben hinein, sie halten keine zweite Wahrheit.

## 1. Portal
- Portal-ID: noch einzutragen.
- Zugriff: über MCP im Betriebs-Cowork und über API aus dem Shop, Zugangsdaten nur als Umgebungsvariable.

## 2. Objekte
- Kontakt
- Firma
- Deal
- Abo, Abbildung noch festzulegen, eigenes Objekt oder Deal mit Kennzeichen.
- Verknüpfungen zwischen den Objekten.

## 3. Deal-Pipeline, Stufen
Je Stufe der sichtbare Name und der interne Name. Folgt aus dem Portal.

| Stufe, sichtbar | interner Name | Bedeutung |
|---|---|---|
| noch einzutragen | noch einzutragen | noch einzutragen |

## 4. Pflichtfelder je Deal
Welche Felder beim Anlegen eines Deals aus dem Shop immer gesetzt werden, mit internem Namen und Herkunft.
Folgt. Grundsatz aus der Arbeitsweise: ein Deal je Vertragsende, kein Bündeln verschiedener Enddaten.

## 5. Firmenfelder
Standard- und eigene Felder, die wir pflegen, mit internem Namen. Folgt.

## 6. Kontaktfelder
Standard- und eigene Felder, die wir pflegen, mit internem Namen. Folgt.

## 7. Abo-Felder
Felder für refurbished Abos, Stripe-Bezug, Status, Laufzeit, Rechnung. Folgt, Abgleich mit
[DB-SCHEMA.md](DB-SCHEMA.md) Abschnitt 2.3.

## 8. Grundsatz
HubSpot ist der kaufmännische Master. Bei Widerspruch zwischen Shop-Datenbank und HubSpot gilt HubSpot
für alles Kaufmännische, die Datenbank für Bestand und Katalog.
