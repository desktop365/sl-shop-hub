# REFURBISHED, Kontrakt
Stand: 2026-11-07, nach E-099. Gilt fuer den Service-Vertrag und den Verkauf
der geprueften Geraete aus eigenem Bestand ueber den Shop. Im Shop heissen sie
„Geprüfte Geräte“, das Wort „refurbished“ steht nur in diesem internen Kontrakt
und in Feldwerten, nie in der Oberflaeche. Neue und gepruefte Geraete sind zwei
getrennte Welten. Geprüfte Geräte und Kasse gehoeren nicht zu Beta 1 (E-101).
Bei Widerspruch gilt ARBEITSWEISE.md, dann dieser Kontrakt.

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
- Service-Vertrag mit SL, Mindestlaufzeit 12 Monate, danach monatlich kuendbar.
- Kuendigungsfrist nach der Mindestlaufzeit: 1 Monat zum Monatsende.
- Monatsrate: setzt Sascha je Geraet. Einzige Quelle ist `abo_36m` in HubSpot.
  Der Feldname ist historisch, gemeint ist die Monatsrate des Service. Die Rate
  wird nie im Code fest verdrahtet.
- Kauf ist eine stille Option NUR auf der Produktseite des geprueften Geraets.
  Er erscheint nie in Teasern, Querverweisen, Kampagnen oder Vergleichen. In der
  Kasse erscheint der Kaufpreis nur im Kaufweg.
- Kaufpreis: HubSpot-Feld `sl_kaufpreis_netto` je Geraet, setzt Sascha. Ist das
  Feld leer, ist das Geraet nicht kaufbar. Die Entscheidung vom 17.09.2026 „kein
  Kaufpreis im Shop“ ist damit fuer gepruefte Geraete aufgehoben, fuer neue
  Geraete gilt sie weiter.
- `price`, `hs_price_eur` und `standard_vk` sind bei geprueften Geraeten leer
  und werden nicht gelesen. Dort stand frueher die Summe ueber 36 Monate, die
  wie ein Kaufpreis aussah.
- Preisanker: die kleinste echte Monatsrate, Zielwert 29,90 Euro fuer das
  guenstigste Geraet.
- Einkaufspreise erscheinen nirgends im Shop-Umfeld. Kaufpreis und Monatsrate
  sind Angebotsdaten und zulaessig.

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
Demo-, OPENBOX- und Vorfuehrgeraete sind keine geprueften Geraete, sie
erscheinen nie im Shop (PRICING.md Abschnitt 7).

## 9. Rechtliches
Mietbedingungen, AGB und Datenschutz-Update sind Voraussetzung des
Launchs und laufen ueber Sascha mit anwaltlicher Pruefung.
