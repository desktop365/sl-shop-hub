# Promotions, Preisaktionen

Status: Gerüst. Überschriften stehen, der Feininhalt folgt mit der Promotions-Schicht in Phase 2.

Eine Aktionsschicht über den Grundpreisen, datengetrieben, Pflege über Admin oder Agent, nie im Code.
Master ist die MySQL-Tabelle, siehe [DB-SCHEMA.md](DB-SCHEMA.md) Abschnitt 2.4.

## 1. Regelmodell
Je Aktion ein Datensatz mit diesen Bestandteilen:
- Typ: Prozentabschlag oder fester Abschlag.
- Wert: die Höhe des Abschlags.
- Geltung: Hersteller, Modell, Zustand neu oder refurbished, Markt. Kombinierbar, Feinheiten folgen.
- Zeitraum: Beginn und Ende.
- Code: optional, Aktion greift dann nur mit Eingabe.
- Banner: optional, Text und Sichtbarkeit im Shop.

## 2. Anzeige im Shop
- Darstellung als statt-jetzt, der Grundpreis bleibt sichtbar.
- Kennzeichnung auf Produktkarte und Produktdetail, Regeln folgen.
- Bannerfläche, Platzierung und Zeitsteuerung folgen.
- Grundsatz: öffentlich sind ausschließlich fertige Monatsraten, nie Faktoren oder interne Werte.

## 3. Abbildung im Checkout
- Refurbished: die Aktion geht als Stripe-Gutschein in das Abo, Zuordnung Aktion zu Gutschein folgt.
- Neu: die Aktion geht als berücksichtigter Angebotspreis in die Anfrage und in den HubSpot-Deal, es gibt
  keinen Sofortkauf und damit keinen Gutschein.

## 4. Kollision und Vorrang
Was gilt, wenn mehrere Aktionen auf ein Produkt passen. Regel folgt.

## 5. Pflege und Nachweis
Wer Aktionen anlegt, wie sie geprüft werden, wie abgelaufene Aktionen behandelt werden. Folgt.
