# HubSpot-Map

HubSpot ist der kaufmännische Master. Kontakte, Firmen, Deals und Abos werden dort geführt, der Shop und die Agenten schreiben hinein, sie halten keine zweite Wahrheit.

## 1. Portal
- Portal-ID, 145452563, app-eu1, Tarif Professional.
- Zugriff, über den MCP im Betriebs-Cowork und über einen Private-App-Token als API-Zugang aus dem Shop, Zugangsdaten nur als Umgebungsvariable, siehe ANFRAGE.md.
- Professional kann keine Custom Objects. Produkte werden nicht als Katalog in HubSpot geführt, nur als Positionen am Deal.

## 2. Objekte
- Kontakt, Firma, Deal.
- Abo, Abbildung noch festzulegen, eigenes Objekt oder Deal mit Kennzeichen, Abgleich mit DB-SCHEMA.md Abschnitt 2.3.
- Verknüpfungen zwischen den Objekten.

## 3. Deal-Pipeline, Stufen
Eine gemeinsame SL-Pipeline für beide Marken, keine eigene Lenovo-Pipeline. Die Pipeline-ID wird über den MCP ausgelesen und hier ergänzt.

| Stufe, sichtbar | interner Wert |
|---|---|
| Kontakt aufgenommen | appointmentscheduled |
| Vertrag ausgelaufen, Übernahme anstreben | 3114765528 |
| Konkret über ein Produkt gesprochen | qualifiedtobuy |
| Deal zurückgestellt, Check Notes | 3378162891 |
| DLL Freigabe eingeholt | presentationscheduled |
| Shop Anfrage | 5550972114 |
| Vertrag oder Angebot zugesendet | decisionmakerboughtin |
| Nachverhandlung | contractsent |
| Wartet auf Rücksendung Geräte | 3114765529 |
| Geräte bestellen und versenden | 3657598138 |
| Versendet, wartet auf Abrechnung | 4611711170 |
| Abgeschlossen und gewonnen | closedwon |
| Abgeschlossen und verloren | closedlost |
| Abgeschlossen und Gerät(e) zurückerhalten | 3548461281 |

Grundsatz, immer die inhaltlich passende Stufe setzen, nie pauschal appointmentscheduled. Ein Deal aus dem Shop-Anfrage-Endpunkt landet auf Shop Anfrage, 5550972114.

## 4. Pflichtfelder je Deal
Aus dem Shop bei Anlage immer gesetzt, Marke und Deal-Quelle aus dem Storefront, dazu Markt und Lane, und hubspot_owner_id, Standard Sascha Blickensdörfer. Grundsatz aus der Arbeitsweise, ein Deal je Vertragsende, kein Bündeln verschiedener Enddaten.

Im weiteren Lebenszyklus durch den Betrieb gepflegt, interne Feldnamen, finanzierende_bank, Werte DLL Bank, Wortmann Finance, ABC Finance, GRENKE. vertragsnummer, anzahl_der_objekte, seriennummer, versendet_am, sobald das Angebot versendet ist.

## 5. Firmenfelder
Standard- und eigene Felder, die wir pflegen. Folgt beim Ausbau.

## 6. Kontaktfelder
Standard- und eigene Felder, die wir pflegen. Folgt beim Ausbau.

## 7. Abo-Felder
Felder für refurbished Abos, Stripe-Bezug, Status, Laufzeit, Rechnung. Folgt in Phase 2, Abgleich mit DB-SCHEMA.md Abschnitt 2.3. Auch am Abo werden Marke und Storefront mitgeführt, gleiche Werte wie am Deal.

## 8. Grundsatz
HubSpot ist der kaufmännische Master. Bei Widerspruch zwischen Shop-Datenbank und HubSpot gilt HubSpot für alles Kaufmännische, die Datenbank für Bestand und Katalog.

## 9. Marken im gemeinsamen Portal
Eine gemeinsame SL-Pipeline für beide Marken. Deal-Feld Marke, Werte Surface und Lenovo, Pflichtfeld an jedem Shop-Deal, interner Feldname noch zu ergänzen. Deal-Quelle je Storefront aus der Storefront-Config, Werte in STOREFRONTS.md Abschnitt 4. Zuordnung, surface ergibt Surface, lenovo ergibt Lenovo. Weitere Marke, weiterer Optionswert, keine neue Pipeline. Angebote verwenden die Vorlage Default Modern.

Warum eine Pipeline, ein Trichter, eine Stufenlogik, eine Auswertung, Filter und Berichte je Marke über das Feld. Zwei Pipelines würden Stufen doppelt pflegen und die Zahlen zerschneiden.
