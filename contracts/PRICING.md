# Preis-Kontrakt, Neu-Raten

Maßgeblich für Herkunft und Berechnung der Neu-Raten. Die Rechenlogik stammt aus dem ersten Anlauf, früher in archive/KONZEPT.md Abschnitt 8, jetzt hier. Sie ist stack-neutral und gilt unabhängig davon, wo die Pipeline läuft. Master der Neu-Raten ist die Preis-Pipeline im Repo surface-love-pricing, sie erzeugt products.json nach contracts/DATA-CONTRACT.md.

## Stand
Stand 07.11.2026, nach E-099. Die Pipeline schreibt products.json in den Bucket, der Shop liest sie von dort über die Sync-Route in sein Leseabbild. B2 (Board 7875) ergänzt `specs` und `category`. DATA-CONTRACT.md wird nach dem B2-Bericht angeglichen, bis dahin gilt bei Laufzeiten und Vertragsarten dieser Kontrakt. Abschnitt 5 ist die Bestandsaufnahme von damals und bleibt als Historie stehen.

## 1. Quelle
- Distributor Continue, Echtzeit-Preisliste über eine API mit Basic-Auth.
- Abrufgrenze, nur drei Abrufe je 15 Minuten. Deshalb streng zeitgesteuert, täglich um 05:00 Europe/Berlin, ein Lauf. Die App ruft nie direkt beim Distributor ab, nur die Pipeline.
- Zugangsdaten nur als Secret der Pipeline, nie im Repo, nie öffentlich.

## 2. Rechenweg
- EK netto vom Distributor.
- Aufschlag mit einem internen Faktor auf den EK netto, ergibt VK netto. Der Wert steht nicht in diesem Repo, er liegt versioniert im privaten Pricing-Repo surface-love-pricing.
- Aus dem VK netto die Leasing-Monatsraten je Wertstaffel über die DLL-Faktortabelle.
- Kaufmännisch gerundet, ROUND_HALF_UP, auf genau zwei Stellen, identisch zur DLL-Bank, weil die Rate so im Vertrag steht.
- Laufzeiten in products.json unter `rates.leasing`: 24, 36, 48, 60, 72 Monate. Was der Shop davon zeigt, steht in Abschnitt 6.

## 3. Ausgaben
- products.json, öffentlich, nur fertige Monatsraten, kein EK, kein VK, keine Faktoren. Kanonisch im Bucket, siehe INFRA.md.
- Interne Preisliste mit EK und VK, ausschließlich intern, nie öffentlich, nie im Hub.

## 4. Geprüfte Geräte, der andere Preispfad
Geprüfte Geräte (eigener Bestand, im Shop nie „refurbished“) laufen nicht über diese Pipeline. Die Monatsrate des Service setzt Sascha je Gerät, einzige Quelle ist `abo_36m` in HubSpot, der Feldname ist historisch. Der Kaufpreis steht in `sl_kaufpreis_netto`. Master ist HubSpot, nicht MySQL (E-099). Einzelheiten in REFURBISHED.md. DB-SCHEMA.md Abschnitt 2.2 ist in diesem Punkt überholt.

## 5. Bestandsaufnahme vor dem Bau
Rein lesend zu klären, bevor Schreibweg und Sync gebaut werden:
- Läuft die Pipeline lokal und erzeugt sie eine products.json, die gegen DATA-CONTRACT.md valide ist.
- Ist der Distributor-Zugang erreichbar, Zugangsdaten gültig, Abrufgrenze beachtet.
- Sind die Raten plausibel gegen bekannte Beispiele.
Erst danach das GCS-Schreibmodul, isoliert, weil google-cloud-storage lokal auf ARM nicht installierbar ist, der Azure-Build aber auf Linux läuft. Details zum Bucket und Service-Account in INFRA.md.

## 6. Neue Geräte im Shop (E-099)
- Nur Leasing über DLL. Keine Finanzierung, keine Kaufoption, kein Kaufpreis.
- Wählbar sind 24, 36 und 48 Monate, Voreinstellung 48. Die beworbene ab-Rate ist die 48-Monats-Rate.
- Die Raten kommen fertig aus products.json, Feld `rates.leasing`. 60 und 72 Monate liefert die Pipeline mit, der Shop blendet sie aus.
- Der Shop rechnet nie selbst. Keine Faktoren, kein EK, kein VK im Shop-Umfeld. Menge mal Rate und der Hinweis zur Mehrwertsteuer sind Anzeige, keine Preisbildung.

## 7. Demo-Geräte (E-099)
Demo-, OPENBOX- und Vorführgeräte sind Partnerware beim Einkauf. Sie erscheinen nie im Katalog, nicht im aktiven Bestand von HubSpot, nicht in products.json und nicht im Shop. Der Filter besteht doppelt: in der Pipeline und zusätzlich als zweite Sperre im Shop-Code, dort in Sync und Anzeige, mit Zähler im Sync-Log. Begriffe: Demo als eigenes Wort, Demoware, Vorführ, Vorfuehr, OPENBOX, Open Box.
