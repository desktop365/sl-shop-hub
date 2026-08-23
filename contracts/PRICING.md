# Preis-Kontrakt, Neu-Raten

Maßgeblich für Herkunft und Berechnung der Neu-Raten. Die Rechenlogik stammt aus dem ersten Anlauf, früher in KONZEPT.md Abschnitt 8, jetzt hier. Sie ist stack-neutral und gilt unabhängig davon, wo die Pipeline läuft. Master der Neu-Raten ist die Preis-Pipeline im Repo surface-love-pricing, sie erzeugt products.json nach contracts/DATA-CONTRACT.md.

## Stand, ehrlich
Die Pipeline wurde im Juli gebaut, Parser und Rechenlogik stehen. Sie hat aber noch nie eine gültige products.json in den Bucket geschrieben, der Bucket ist leer, und ob der Distributor-Zugang heute noch funktioniert, ist nicht geprüft. Also gebaut, aber nicht End-zu-End bewiesen. Bevor der Schreibweg oder der Sync angefasst werden, steht eine rein lesende Bestandsaufnahme, siehe Abschnitt 5.

## 1. Quelle
- Distributor Continue, Echtzeit-Preisliste über eine API mit Basic-Auth.
- Abrufgrenze, nur drei Abrufe je 15 Minuten. Deshalb streng zeitgesteuert, täglich um 05:00 Europe/Berlin, ein Lauf. Die App ruft nie direkt beim Distributor ab, nur die Pipeline.
- Zugangsdaten nur als Secret der Pipeline, nie im Repo, nie öffentlich.

## 2. Rechenweg
- EK netto vom Distributor.
- Aufschlag Faktor 1,25 auf den EK netto, ergibt VK netto.
- Aus dem VK netto die Monatsraten je Vertragsart und Wertstaffel über die DLL-Faktortabelle.
- Kaufmännisch gerundet, ROUND_HALF_UP, auf genau zwei Stellen, identisch zur DLL-Bank, weil die Rate so im Vertrag steht.
- Vertragsarten und Laufzeiten wie im Datenvertrag, Leasing 15, 24, 32, 36, Finanzierung 15, 24, 36.

## 3. Ausgaben
- products.json, öffentlich, nur fertige Monatsraten, kein EK, kein VK, keine Faktoren. Kanonisch im Bucket, siehe INFRA.md.
- Interne Preisliste mit EK und VK, ausschließlich intern, nie öffentlich, nie im Hub.

## 4. Refurbished, der andere Preispfad
Refurbished läuft nicht über diese Pipeline. Der Preis ist ein selbst gesetzter Abo-Preis, weil das Gerät uns gehört, regelbasiert je Modell mit Übersteuerung je Einheit, gemastert in MySQL. Siehe LANDKARTE.md Abschnitt 4 und DB-SCHEMA.md Abschnitt 2.2.

## 5. Bestandsaufnahme vor dem Bau
Rein lesend zu klären, bevor Schreibweg und Sync gebaut werden:
- Läuft die Pipeline lokal und erzeugt sie eine products.json, die gegen DATA-CONTRACT.md valide ist.
- Ist der Distributor-Zugang erreichbar, Zugangsdaten gültig, Abrufgrenze beachtet.
- Sind die Raten plausibel gegen bekannte Beispiele.
Erst danach das GCS-Schreibmodul, isoliert, weil google-cloud-storage lokal auf ARM nicht installierbar ist, der Azure-Build aber auf Linux läuft. Details zum Bucket und Service-Account in INFRA.md.
