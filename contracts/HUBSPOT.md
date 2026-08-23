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
Eine gemeinsame SL-Pipeline für beide Marken, keine eigene Lenovo-Pipeline. Die Marke wird über ein
Deal-Feld unterschieden, siehe Abschnitt 9.

Je Stufe der sichtbare Name und der interne Name. Folgt aus dem Portal.

| Stufe, sichtbar | interner Name | Bedeutung |
|---|---|---|
| noch einzutragen | noch einzutragen | noch einzutragen |

## 4. Pflichtfelder je Deal
Welche Felder beim Anlegen eines Deals aus dem Shop immer gesetzt werden, mit internem Namen und Herkunft.
Folgt. Grundsatz aus der Arbeitsweise: ein Deal je Vertragsende, kein Bündeln verschiedener Enddaten.

Immer gesetzt werden mindestens Marke und Deal-Quelle aus dem Storefront, siehe Abschnitt 9, dazu Markt
und Lane. Die internen Feldnamen folgen aus dem Portal.

## 5. Firmenfelder
Standard- und eigene Felder, die wir pflegen, mit internem Namen. Folgt.

## 6. Kontaktfelder
Standard- und eigene Felder, die wir pflegen, mit internem Namen. Folgt.

## 7. Abo-Felder
Felder für refurbished Abos, Stripe-Bezug, Status, Laufzeit, Rechnung. Folgt, Abgleich mit
[DB-SCHEMA.md](DB-SCHEMA.md) Abschnitt 2.3.

Auch am Abo werden Marke und Storefront mitgeführt, gleiche Werte wie am Deal.

## 8. Grundsatz
HubSpot ist der kaufmännische Master. Bei Widerspruch zwischen Shop-Datenbank und HubSpot gilt HubSpot
für alles Kaufmännische, die Datenbank für Bestand und Katalog.

## 9. Marken im gemeinsamen Portal, getroffene Entscheidung
Entschieden: **eine gemeinsame SL-Pipeline für beide Marken**, keine eigene Lenovo-Pipeline.

- **Deal-Feld Marke**, Werte Surface und Lenovo. Pflichtfeld an jedem Deal aus dem Shop. Interner Feldname
  und interne Optionswerte noch einzutragen.
- **Deal-Quelle je Storefront**, der Quellenwert wird aus der Storefront-Config gesetzt und sagt, über
  welchen Auftritt der Vorgang hereinkam. Werte je Storefront stehen in
  [STOREFRONTS.md](STOREFRONTS.md) Abschnitt 4.
- Zuordnung Storefront zu Markenwert: surface ergibt Surface, lenovo ergibt Lenovo. Kommt eine weitere
  Marke dazu, kommt ein Optionswert dazu, keine neue Pipeline.

Warum so: eine Pipeline heißt ein Trichter, eine Stufenlogik, eine Auswertung, und Filter und Berichte je
Marke über das Feld. Zwei Pipelines würden Stufen doppelt pflegen und die Zahlen zerschneiden.

Auswertung je Marke läuft über Filter und Ansichten auf dem Feld Marke, nicht über getrennte Pipelines.
