# Storefronts, Einmarken-Auftritte je Domain

Status: Gerüst mit festgelegtem Modell. Die Struktur steht, die konkreten Werte je Storefront folgen mit
der Config im Shop-Repo.

Master der Werte ist die Config im Shop-Repo, dieses Dokument beschreibt sie. Es gilt zusammen mit
[MARKETS.md](MARKETS.md) und [HUBSPOT.md](HUBSPOT.md).

## 1. Begriff
Ein Storefront ist eine Konfiguration je Domain. Sie legt fest, welche Marke auftritt, welche Optik gilt,
welcher Hersteller-Filter auf den Katalog wirkt, welche rechtlichen Texte und Kontaktdaten gezeigt werden,
mit welchem Absender Mails hinausgehen und mit welchen Parametern nach HubSpot geschrieben wird.

Die App erkennt beim Aufruf die Domain, lädt den passenden Storefront und rendert den Auftritt danach.
Eine Codebasis, ein HubSpot, ein Bestand. Nach außen getrennte Marken-Shops, die nichts voneinander wissen.

## 2. Drei Achsen, die sich kombinieren
| Achse | Was sie bestimmt | Woher |
|---|---|---|
| Storefront | Marke, Domain, Optik, Hersteller-Filter, Absender, HubSpot-Parameter | dieses Dokument |
| Markt | Land, Sprache, Währung, Recht, Vertragsarten | [MARKETS.md](MARKETS.md) |
| Lane | Zweig neu oder refurbished, Kassenweg, Preislogik | [DATA-CONTRACT.md](DATA-CONTRACT.md), [DB-SCHEMA.md](DB-SCHEMA.md) |

Die Achsen sind unabhängig und werden kombiniert. Ein Aufruf ist immer ein Tripel aus Storefront, Markt
und Lane, zum Beispiel surface, Deutschland, refurbished. Nicht jede Kombination ist freigeschaltet, was
aktiv ist, steht je Storefront unter aktive Märkte und in MARKETS.md.

## 3. Storefront-Liste
| id | Domain | Hersteller | Marken-Identität | Märkte | Status |
|---|---|---|---|---|---|
| surface | surface.love | Microsoft Surface | Herz und Cyan | Deutschland aktiv, USA vorbereitet | aktiv |
| lenovo | lenovo.online | Lenovo | eigene Marke, noch zu gestalten | Deutschland aktiv, USA vorbereitet | vorbereitet |

- surface ist der bestehende Auftritt und der Referenzfall.
- lenovo ist angelegt und noch nicht live. Er geht mit derselben Codebasis und demselben Bestandsmodell an
  den Start, sobald Marke, Recht und Sortiment stehen.

## 4. Felder je Storefront
- **id** stabiler Schlüssel, klein geschrieben, zum Beispiel surface, lenovo. Wird in Daten und in HubSpot
  mitgeführt.
- **Domains** eine oder mehrere, eine davon ist kanonisch, die übrigen leiten dorthin.
- **Marken-Identität** Logo, Token-Satz für Farben, Typo und Radius, Name der Marke für Titel und Texte.
- **Hersteller-Filter** welche Hersteller der Storefront zeigt. Der Katalog ist herstellerneutral, der
  Filter schneidet ihn zu. Ein Gerät, das nicht zum Filter passt, ist im Storefront nicht auffindbar.
- **Rechtliche Texte** Impressum, Datenschutz, AGB, Widerruf, Versand und Zahlung, je Storefront und Markt.
- **Kontaktdaten** Anschrift, Telefon, Mailadresse, wie sie im Auftritt erscheinen.
- **Mail-Absender** Absenderadresse und Anzeigename für ausgehende Mails, getrennt je Storefront.
- **HubSpot-Markenwert** der Wert des Deal-Feldes Marke, siehe [HUBSPOT.md](HUBSPOT.md) Abschnitt 9.
- **HubSpot-Deal-Quelle** der Quellenwert, der je Storefront am Deal gesetzt wird.
- **Aktive Märkte** welche Märkte aus MARKETS.md dieser Storefront ausliefert.
- **SEO** kanonische Domain, eigene Sitemap und robots je Storefront, getrennte Metadaten. Kein Inhalt
  erscheint unter zwei Domains ohne Kanonik.

## 5. Regel, kein markenübergreifender Querverkauf
Der eingebaute Querverkauf zwischen neu und refurbished bleibt innerhalb einer Marke. Ein Surface-Besucher
sieht nie ein Lenovo-Angebot und umgekehrt. Verwandte Produkte, Banner, Empfehlungen und Suchergebnisse
respektieren den Hersteller-Filter des Storefronts ohne Ausnahme.

Das ist bewusst so: die Auftritte sind nach außen eigenständige Marken-Shops, ein Hinweis auf die andere
Marke würde den Einmarken-Charakter zerstören.

## 6. Was geteilt wird und was getrennt
- Geteilt: Codebasis, Datenbank, refurbished Bestand, Preislogik, HubSpot-Portal und Deal-Pipeline,
  Bild-Pipeline, Betriebsabläufe.
- Getrennt: Domain, Marke und Optik, Sortiment über den Hersteller-Filter, rechtliche Texte, Kontaktdaten,
  Mail-Absender, SEO, alles was der Kunde sieht.

## 7. Hinweis zu Lenovo
Der Name lenovo.online und die Verwendung des Lenovo-Logos unterliegen den Partner- und Markenregeln von
Lenovo. Beides ist vor dem Livegang gegen den Partnervertrag zu prüfen, Domainname, Logo, Wortmarke in
Titeln und Metadaten sowie die Darstellung als Händler. Ergibt die Prüfung eine Einschränkung, ändert das
nur die Marken-Identität dieses Storefronts, nicht das Modell.

## 8. Offene Punkte
- Marken-Identität für lenovo, Logo, Tokens, Name im Auftritt.
- Ergebnis der Partner- und Markenprüfung.
- Sortimentsschnitt für lenovo, welche Lenovo-Linien der Storefront zeigt.
- Absenderadressen und Postfächer je Storefront.
