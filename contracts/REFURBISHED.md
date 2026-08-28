# REFURBISHED, Kontrakt
Stand: 2026-08-28. Gilt fuer die direkte Vermietung und den Verkauf der
refurbished Geraete aus eigenem Bestand ueber den Shop. Bei Widerspruch
gilt ARBEITSWEISE.md, dann dieser Kontrakt.

## 1. Bestandsfuehrung, HubSpot ist der Master
HubSpot (Portal 145452563) fuehrt jeden Geraetestatus: verfuegbar,
reserviert, vermietet, verkauft, in Aufbereitung. Grund: es wird auch
ausserhalb des Shops vermietet und verkauft. Die Excel-Bestandsliste war
einmalige Importquelle (Import durch Strom 10, eigene Produktkategorie
Refurbished, ohne Preise, getrennt von den Neugeraete-Produkten). Nach dem
Import pflegt der Vertrieb Statusaenderungen ausschliesslich in HubSpot.
Je Geraet gefuehrt: Seriennummer, Typ, Konfiguration, Status,
Ursprungsvertrag, bei Verkauf der Kaeufer. Zubehoer als Mengenartikel.

## 2. Leseabbild im Shop
Der Shop fuehrt KEINEN eigenen Bestand. Er liest zyklisch je Typ die
verfuegbare Stueckzahl und die kleinste Monatsrate aus HubSpot in ein
Leseabbild (gleiches Muster wie der Neugeraete-Katalog). Anzeige nur, was
das Leseabbild kennt. Reservierung und Buchung sind Statusaenderungen in
HubSpot, nie nur lokale Zustaende.

## 3. Kaufmaennische Eckwerte (Konfigurationswerte, kein Code)
- Mindestlaufzeit der Miete: 6 Monate, danach monatlich kuendbar.
- Kuendigungsfrist nach der Mindestlaufzeit: 1 Monat zum Monatsende.
- Kauf wird zusaetzlich angeboten: Miete prominent, Kauf als stille
  Option NUR auf der Refurbished-Produktseite, kein Kaufpreis in Teasern,
  Querverweisen oder Kampagnen.
- Preisanker: die kleinste echte Monatsrate, Zielwert 29,90 Euro fuer das
  guenstigste Geraet. Raten je Typ sind Konfigurationsdaten, sie werden
  von Sascha gesetzt und nie im Code fest verdrahtet.
- Einkaufspreise erscheinen nirgends im Shop-Umfeld. Refurbished-
  Verkaufspreise und Monatsraten sind Angebotsdaten und zulaessig.

## 4. Checkout und Zahlungsarchitektur
Checkout laeuft ueber Stripe. GRUNDSATZ: genau EIN System fakturiert.
Zwei zulaessige Muster, die Festlegung erfolgt als Nachtrag zu diesem
Kontrakt, sobald das Objektmodell aus dem HubSpot-Import (r8) und der
Stripe-Konto-Stand (r3) vorliegen:
a) Stripe fuehrt Abo und Rechnung, HubSpot spiegelt Deal, Abo-Objekt und
   Reporting.
b) HubSpot Commerce fuehrt die Subscription und Rechnung, Stripe ist nur
   Zahlungsabwickler.
Ablauf verbindlich: Checkout-Start setzt das Geraet in HubSpot auf
reserviert. Zahlung setzt vermietet (oder verkauft) und erzeugt Contact,
Deal in der Refurb-Pipeline auf gewonnen sowie das Abonnement. Abbruch:
Freigabe der Reservierung nach Frist (Konfigurationswert, Startwert 30
Minuten) und ein Deal in der Abbruch-Stage mit Herkunftsdaten.
WARNUNG: die laufende Subscriptions-Bereinigung im Portal (Altbestand,
Backend-Loeschung beantragt) muss von neuen Refurb-Abos strikt getrennt
bleiben, Koordination vor dem ersten echten Abo.

## 5. Tracking und Attribution
Checkout-Abbrueche werden als Deals mit Herkunft getrackt: UTM-Parameter,
Kampagne, Kanal. Retargeting (z. B. LinkedIn) nur mit Consent und
aktualisierter Datenschutzerklaerung. Es gilt die Linie aus E-031: kein
Tracking, das die Datenschutzerklaerung sprengt.

## 6. Auftritt im Shop (Kurzform, Details im r6-Auftrag an Strom 50)
Eigener Refurbished-Bereich mit den Lagervarianten und Zustandsklassen.
Dezente Textzeile im Neugeraete-Konfigurator unterhalb der Rate, nur bei
passendem Bestand. Refurbished als klar gekennzeichnete Sofort-Alternative
im spaeten Verfuegbarkeits-Moment der Neugeraete. Rueckverweis von jeder
Refurb-Seite auf das Neugeraet. Eine Startseiten-Flaeche.
Fokus-Schutz: Refurb-Hinweise typografisch sekundaer, nie die Akzentfarbe,
maximal ein Beruehrungspunkt je Bildschirm, nie im Neugeraete-Checkout,
keine Preisvergleichstabellen neu gegen refurbished.

## 7. Bilder
Microsoft-Standardbilder der Bildmodelle (IMAGES.md), immer mit
Refurbished-Kennzeichnung und Zustandsklasse. Keine Fotos je Einzelgeraet.

## 8. Abgrenzungen
Der spaete Verfuegbarkeits-Check der Neugeraete (SICHTBARKEIT.md) gilt
hier nicht, der eigene Bestand ist die Wahrheit. Refurbished-Artikel des
Distributors (articleType REF) bleiben aus dem Feed-Scope ausgeschlossen.

## 9. Rechtliches
Mietbedingungen, AGB und Datenschutz-Update sind Voraussetzung des
Launchs und laufen ueber Sascha mit anwaltlicher Pruefung.
