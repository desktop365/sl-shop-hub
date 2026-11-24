# Preis-Kontrakt, Neu-Raten

Maßgeblich für Herkunft und Ausgabe der Neu-Raten. Die Rechenlogik selbst ist intern und steht versioniert im privaten Pricing-Repo, nicht in diesem öffentlichen Hub (E-092). Master der Neu-Raten ist die Preis-Pipeline im Repo surface-love-pricing, sie erzeugt products.json nach contracts/DATA-CONTRACT.md.

## Stand
Stand 24.11.2026, nach E-099 und B2 (Board 7875). Die Pipeline schreibt products.json in den Bucket, der Shop liest sie von dort über die Sync-Route in sein Leseabbild. Das Schema samt `specs` und `category` steht in DATA-CONTRACT.md, angeglichen am 24.11.2026. Abschnitt 5 ist die Bestandsaufnahme von damals und bleibt als Historie stehen.

## 1. Quelle
- Echtzeit-Preisliste des Lieferanten über eine API. Lieferant und Zugangsweg stehen nur im privaten Pricing-Repo.
- Abrufgrenze, nur drei Abrufe je 15 Minuten. Deshalb streng zeitgesteuert, täglich um 05:00 Europe/Berlin, ein Lauf. Die App ruft nie direkt beim Lieferanten ab, nur die Pipeline.
- Zugangsdaten nur als Secret der Pipeline, nie im Repo, nie öffentlich.

## 2. Rechenweg
- Der Weg vom Lieferantenpreis zur Monatsrate ist intern. Er steht versioniert im privaten Pricing-Repo surface-love-pricing (E-092).
- Kaufmännisch gerundet, ROUND_HALF_UP, auf genau zwei Stellen, weil die Rate so im Vertrag steht.
- Laufzeiten in products.json unter `rates.leasing`: 24, 36 und 48 Monate, `rate_from` ist die 48-Monats-Rate. Das gilt ab dem Nachtlauf am 25.11.2026 (P08), vorher lieferte die Pipeline zusätzlich 60 und 72 Monate. Was der Shop zeigt, steht in Abschnitt 6.

## 3. Ausgaben
- products.json, öffentlich, nur fertige Monatsraten, kein EK, kein VK, keine Faktoren. Kanonisch im Bucket, siehe INFRA.md.
- Interne Preisliste, ausschließlich intern, nie öffentlich, nie im Hub.

## 4. Geprüfte Geräte, der andere Preispfad
Geprüfte Geräte (eigener Bestand, im Shop nie „refurbished“) laufen nicht über diese Pipeline. Die Monatsrate des Service setzt Sascha je Gerät, einzige Quelle ist `abo_36m` in HubSpot, der Feldname ist historisch. Der Kaufpreis steht in `sl_kaufpreis_netto`. Master ist HubSpot, nicht MySQL (E-099). Einzelheiten in REFURBISHED.md. DB-SCHEMA.md Abschnitt 2.2 ist in diesem Punkt überholt.

## 5. Bestandsaufnahme vor dem Bau
Rein lesend zu klären, bevor Schreibweg und Sync gebaut werden:
- Läuft die Pipeline lokal und erzeugt sie eine products.json, die gegen DATA-CONTRACT.md valide ist.
- Ist der Distributor-Zugang erreichbar, Zugangsdaten gültig, Abrufgrenze beachtet.
- Sind die Raten plausibel gegen bekannte Beispiele.
Erst danach das GCS-Schreibmodul, isoliert, weil google-cloud-storage lokal auf ARM nicht installierbar ist, der Azure-Build aber auf Linux läuft. Details zum Bucket und Service-Account in INFRA.md.

## 6. Neue Geräte im Shop (E-099)
- Nur Leasing. Keine Finanzierung, keine Kaufoption, kein Kaufpreis.
- Wählbar sind 24, 36 und 48 Monate, Voreinstellung 48. Die beworbene ab-Rate ist die 48-Monats-Rate.
- Die Raten kommen fertig aus products.json, Feld `rates.leasing`. Die Pipeline liefert öffentlich nur 24, 36 und 48 Monate. Der Shop filtert zusätzlich auf die Laufzeiten seines Markts und nimmt die ab-Rate selbst aus `rates.leasing`, nicht aus `rate_from`.
- Der Shop rechnet nie selbst. Keine Faktoren, kein EK, kein VK im Shop-Umfeld. Menge mal Rate und der Hinweis zur Mehrwertsteuer sind Anzeige, keine Preisbildung.

## 7. Demo-Geräte (E-099)
Demo-, OPENBOX- und Vorführgeräte erscheinen nie im Katalog, nicht im aktiven Bestand von HubSpot, nicht in products.json und nicht im Shop. Der Filter besteht doppelt: in der Pipeline und zusätzlich als zweite Sperre im Shop-Code, dort in Sync und Anzeige, mit Zähler im Sync-Log. Begriffe: Demo als eigenes Wort, Demoware, Vorführ, Vorfuehr, OPENBOX, Open Box.
