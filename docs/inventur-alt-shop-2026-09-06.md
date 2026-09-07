# Inventur des alten Shops

Auftrag des Masters vom 06.09.2026. Erhoben am 07.09.2026 durch CC (Azure DevOps).
Stand: **Bereich 1 abgeschlossen, Bereich 2 und 3 offen.**

## Wozu diese Datei da ist und wozu nicht

Diese Inventur sammelt, was der alte Shop an Adressen, Rechtstexten und sonst
brauchbarem Material im Quellcode, im Board und im Wiki hinterlassen hat. Sie
inventarisiert, sie bewertet nicht und sie uebernimmt nichts.

**Diese Inventur ersetzt den Alt-URL-Export aus der Google Search Console und aus
Cloudflare nicht.** Sie kennt nur, was im Code steht oder was jemand einmal in
einen Vorgang geschrieben hat. Welche Adressen tatsaechlich aufgerufen werden,
welche in fremden Seiten verlinkt sind und welche im Index stehen, steht hier
nicht. Wer die Weiterleitungsliste fuer den Livegang baut, braucht beide Quellen.

## Suchraum, wie er tatsaechlich aussah

| Quelle | Umfang | Bemerkung |
|---|---|---|
| Bereichsknoten `Surface.Love\Alt-Shop-2024` (Id 394) | **1802 Vorgaenge**, Ids 4224 bis 6025 | deutlich groesser als die im Auftrag genannten rund 200 |
| Repo `PT.SurfaceShop.Web` | 552 MB, ASP.NET Core MVC mit Squidex als CMS | die Hauptquelle fuer Bereich 1 |
| Repo `PT.SurfaceShop.Admin` | 3,8 MB | internes Backend, fuer Bereich 1 ohne Belang |
| Repo `PT.SurfaceShop.Environment` | 43 KB | ARM-Vorlagen fuer die Azure-Ressourcen |
| Repo `PT.SurfaceShop.Service` | 2 Dateien | leer bis auf `.gitignore` und `README.md` |
| Repo `PT.SurfaceShop.PoC` | 2 Dateien | leer bis auf `.gitignore` und `README.md` |
| fremdes Wiki | 23 Dateien, 8 Seiten | liegt in einem fremden Projekt der Organisation, Inhalt betrifft einen anderen Auftrag, **kein Bezug zum Surface-Love-Shop** |
| Repo `SLSHOPAISTUDIO` | **nicht gefunden** | in keinem der 19 Projekte der Organisation desktop365 vorhanden, siehe Abschnitt "Nicht gefunden, obwohl erwartet" |

Die Codesuche der Organisation (`search_code`) ist nicht verfuegbar, sie meldet
`infoCode 6`, also keinen Index. Gearbeitet wurde deshalb ueber die Dateibaeume
und ueber gezielte Abrufe einzelner Ordner.

---

# 1. Adressen und Weiterleitungen

## Die Zahl zuerst

**300 Adressmuster** stehen im Quellcode: 288 eindeutige lokalisierte Muster in
289 Attributzeilen sowie 12 fest verdrahtete Routen. Dazu kommen **41 konkrete
Alt-Adressen**, die in zwei Anhaengen aus der Google Search Console am Board
haengen, und **150 Vorgaenge** im Alt-Shop-Bereich, deren Titel Adressen,
Weiterleitungen, Sitemap oder SEO betreffen.

## Wie die Adressen aufgebaut sind

Jede oeffentliche Seite des alten Shops liegt unter `/{culture}/{market}/...`.
Das Kultursegment ist das volle Locale-Kuerzel in Kleinschreibung, das
Marktsegment ist ein sprechender Name. Belegt ist `/de-de/deutschland/...`, das
steht so in der Weiterleitungsschicht des Shops. Die Route setzt beide Werte
klein, `LowercaseUrls` ist eingeschaltet.

Der Code kennt acht Kulturen: `en-GB`, `en-US`, `de-DE`, `de-AT`, `da-DK`,
`fr-FR`, `nl-NL` und `es-ES`. Sie werden in `Startup.cs` registriert und jede
Seite traegt fuer alle sechs Sprachfamilien ein eigenes Pfadmuster. **Zur
Laufzeit sind davon aber nur zwei aktiv.** Die Middleware `RedirectMarketInfo`
laesst ausschliesslich `en-GB` und `de-DE` samt der Maerkte `GB` und `DE` durch
und schickt alles andere auf `/de-de/deutschland/market-info`. Daenisch,
Franzoesisch, Niederlaendisch, Spanisch und auch `de-AT` und `en-US` sind im
Code vollstaendig ausgebaut, aber praktisch abgeschaltet. Fuer die
Weiterleitungsliste heisst das: die Muster existieren, sie koennen im Index
stehen, sie liefern heute aber keine Seite mehr aus.

Das Marktsegment selbst kommt nicht aus dem Code, sondern aus dem CMS. Es steht
in `LocalizedUrlSegments` der Markt-Entitaet in Squidex. Im Repo ist nur
`deutschland` belegt. **Die vollstaendige Liste der Marktsegmente laesst sich
ohne Squidex-Zugang nicht ermitteln.**

## Die Adressmuster im Code

Die folgende Liste ist flach und vollstaendig. `Quelle` nennt die Datei unter
`/src/PT.SurfaceShop.Web/Controllers/` und die Zeile, `Sprache` das Kuerzel aus
dem Attribut, wobei `default` das englische Muster meint, das ohne passenderen
Treffer greift.

| Pfadmuster | Quelle | Sprache | Seitentyp | Weiterleitung vorhanden |
|---|---|---|---|---|
| `/{culture}/{market}/about-us/` | AboutUs:21 | default | Inhaltsseite, Ueber uns | nein |
| `/{culture}/{market}/ueber-uns/` | AboutUs:22 | de | Inhaltsseite, Ueber uns | nein |
| `/{culture}/{market}/om-os/` | AboutUs:23 | da | Inhaltsseite, Ueber uns | nein |
| `/{culture}/{market}/sur-nous` | AboutUs:24 | fr | Inhaltsseite, Ueber uns | nein |
| `/{culture}/{market}/over-ons` | AboutUs:25 | nl | Inhaltsseite, Ueber uns | nein |
| `/{culture}/{market}/sobre-nosotros` | AboutUs:26 | es | Inhaltsseite, Ueber uns | nein |
| `/{culture}/{market}/store/accessories/` | Accessories:30 | default | Kategorie-Einstieg Zubehoer | nein |
| `/{culture}/{market}/shop/zubehoer/` | Accessories:31 | de | Kategorie-Einstieg Zubehoer | nein |
| `/{culture}/{market}/butik/tilbehoer/` | Accessories:32 | da | Kategorie-Einstieg Zubehoer | nein |
| `/{culture}/{market}/boutique/accessoires/` | Accessories:33 | fr | Kategorie-Einstieg Zubehoer | nein |
| `/{culture}/{market}/winkel/accessoires/` | Accessories:34 | nl | Kategorie-Einstieg Zubehoer | nein |
| `/{culture}/{market}/tienda/accesorios/` | Accessories:35 | es | Kategorie-Einstieg Zubehoer | nein |
| `/{culture}/{market}/store/accessories/categories/all/{*filterlink}` | Accessories:46 | default | Filterliste Zubehoer, alle | nein |
| `/{culture}/{market}/shop/zubehoer/kategorien/alle/{*filterlink}` | Accessories:47 | de | Filterliste Zubehoer, alle | nein |
| `/{culture}/{market}/butik/tilbehoer/kategorier/alle/{*filterlink}` | Accessories:48 | da | Filterliste Zubehoer, alle | nein |
| `/{culture}/{market}/boutique/accessoires/categories/tous/{*filterlink}` | Accessories:49 | fr | Filterliste Zubehoer, alle | nein |
| `/{culture}/{market}/winkel/accessoires/categorieen/alle/{*filterlink}` | Accessories:50 | nl | Filterliste Zubehoer, alle | nein |
| `/{culture}/{market}/tienda/accesorios/categorias/todo/{*filterlink}` | Accessories:51 | es | Filterliste Zubehoer, alle | nein |
| `/{culture}/{market}/store/accessories/1001/categories/0/all/{*filterlink}` | Accessories:68 | en | Filterliste Zubehoer, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/shop/zubehoer/1001/kategorien/0/alle/{*filterlink}` | Accessories:69 | de | Filterliste Zubehoer, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/butik/tilbehoer/1001/kategorier/0/alle/{*filterlink}` | Accessories:70 | da | Filterliste Zubehoer, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/boutique/accessoires/1001/categories/0/tous/{*filterlink}` | Accessories:71 | fr | Filterliste Zubehoer, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/winkel/accessoires/1001/categorieen/0/alle/{*filterlink}` | Accessories:72 | nl | Filterliste Zubehoer, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/tienda/accesorios/1001/categorias/0/todo/{*filterlink}` | Accessories:73 | es | Filterliste Zubehoer, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/store/accessories/categories/recommended/{*filterlink}` | Accessories:84 | default | Filterliste Zubehoer, empfohlen | nein |
| `/{culture}/{market}/shop/zubehoer/kategorien/empfohlen/{*filterlink}` | Accessories:85 | de | Filterliste Zubehoer, empfohlen | nein |
| `/{culture}/{market}/butik/tilbehoer/kategorier/anbefalet/{*filterlink}` | Accessories:86 | da | Filterliste Zubehoer, empfohlen | nein |
| `/{culture}/{market}/boutique/accessoires/categories/recommande/{*filterlink}` | Accessories:87 | fr | Filterliste Zubehoer, empfohlen | nein |
| `/{culture}/{market}/winkel/accessoires/categorieen/aanbevolen/{*filterlink}` | Accessories:88 | nl | Filterliste Zubehoer, empfohlen | nein |
| `/{culture}/{market}/tienda/accesorios/categorias/recomendado/{*filterlink}` | Accessories:89 | es | Filterliste Zubehoer, empfohlen | nein |
| `/{culture}/{market}/store/accessories/1001/categories/10008/recommended/{*filterlink}` | Accessories:120 | en | Filterliste Zubehoer empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/shop/zubehoer/1001/kategorien/10008/empfohlen/{*filterlink}` | Accessories:121 | de | Filterliste Zubehoer empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/butik/tilbehoer/1001/kategorier/10008/anbefalet/{*filterlink}` | Accessories:122 | da | Filterliste Zubehoer empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/boutique/accessoires/1001/categories/10008/recommande/{*filterlink}` | Accessories:123 | fr | Filterliste Zubehoer empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/winkel/accessoires/1001/categorieen/10008/aanbevolen/{*filterlink}` | Accessories:124 | nl | Filterliste Zubehoer empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/tienda/accesorios/1001/categorias/10008/recomendado/{*filterlink}` | Accessories:125 | es | Filterliste Zubehoer empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/store/accessories/details/{productId}/{productName}/{id?}` | Accessories:136 | default | Detailseite Zubehoer | nein |
| `/{culture}/{market}/shop/zubehoer/details/{productId}/{productName}/{id?}` | Accessories:137 | de | Detailseite Zubehoer | nein |
| `/{culture}/{market}/butik/tilbehoer/detaljer/{productId}/{productName}/{id?}` | Accessories:138 | da | Detailseite Zubehoer | nein |
| `/{culture}/{market}/boutique/accessoires/details/{productId}/{productName}/{id?}` | Accessories:139 | fr | Detailseite Zubehoer | nein |
| `/{culture}/{market}/winkel/accessoires/details/{productId}/{productName}/{id?}` | Accessories:140 | nl | Detailseite Zubehoer | nein |
| `/{culture}/{market}/tienda/accesorios/detalles/{productId}/{productName}/{id?}` | Accessories:141 | es | Detailseite Zubehoer | nein |
| `/{culture}/{market}/advantages/` | Advantages:24 | default | Inhaltsseite, Vorteile | nein |
| `/{culture}/{market}/vorteile/` | Advantages:25 | de | Inhaltsseite, Vorteile | nein |
| `/{culture}/{market}/fordele/` | Advantages:26 | da | Inhaltsseite, Vorteile | nein |
| `/{culture}/{market}/avantages/` | Advantages:27 | fr | Inhaltsseite, Vorteile | nein |
| `/{culture}/{market}/voordelen` | Advantages:28 | nl | Inhaltsseite, Vorteile | nein |
| `/{culture}/{market}/ventajas` | Advantages:29 | es | Inhaltsseite, Vorteile | nein |
| `/{culture}/{market}/store/bundle/{productid}/{productName}/` | Bundles:30 | default | Detailseite Bundle | nein |
| `/{culture}/{market}/shop/bundle/{productid}/{productName}/` | Bundles:31 | de | Detailseite Bundle | nein |
| `/{culture}/{market}/butik/bundle/{productid}/{productName}/` | Bundles:32 | da | Detailseite Bundle | nein |
| `/{culture}/{market}/boutique/bundle/{productid}/{productName}/` | Bundles:33 | fr | Detailseite Bundle | nein |
| `/{culture}/{market}/winkel/bundle/{productid}/{productName}/` | Bundles:34 | nl | Detailseite Bundle | nein |
| `/{culture}/{market}/tienda/bundle/{productid}/{productName}/` | Bundles:35 | es | Detailseite Bundle | nein |
| `/{culture}/{market}/careers/` | Careers:25 | default | Inhaltsseite, Karriere | nein |
| `/{culture}/{market}/karriere/` | Careers:26 | de | Inhaltsseite, Karriere | nein |
| `/{culture}/{market}/jobs/` | Careers:27 | da | Inhaltsseite, Karriere | nein |
| `/{culture}/{market}/carriere/` | Careers:28 | fr | Inhaltsseite, Karriere | nein |
| `/{culture}/{market}/carriere-nl/` | Careers:29 | nl | Inhaltsseite, Karriere | nein |
| `/{culture}/{market}/oportunidades-trabajo/` | Careers:30 | es | Inhaltsseite, Karriere | nein |
| `/{culture}/{market}/careers/jobs/{positionid}/{positiontitle}/{locationid}/{locationname}/` | Careers:40 | default | Detailseite Stellenangebot | nein |
| `/{culture}/{market}/karriere/jobs/{positionid}/{positiontitle}/{locationid}/{locationname}/` | Careers:41 | de | Detailseite Stellenangebot | nein |
| `/{culture}/{market}/arbejdskarriere/jobs/{positionid}/{positiontitle}/{locationid}/{locationname}/` | Careers:42 | da | Detailseite Stellenangebot | nein |
| `/{culture}/{market}/carriere/jobs/{positionid}/{positiontitle}/{locationid}/{locationname}/` | Careers:43 | fr | Detailseite Stellenangebot | nein |
| `/{culture}/{market}/carriere/jobs/{positionid}/{positiontitle}/{locationid}/{locationname}/` | Careers:44 | nl | Detailseite Stellenangebot | nein |
| `/{culture}/{market}/oportunidades-trabajo/empleos/{positionid}/{positiontitle}/{locationid}/{locationname}/` | Careers:45 | es | Detailseite Stellenangebot | nein |
| `/{culture}/{market}/store/shoppingcart/clientdetails/` | ClientDetails:30 | default | Checkout, Kundendaten | nein |
| `/{culture}/{market}/shop/warenkorb/kundendaten/` | ClientDetails:31 | de | Checkout, Kundendaten | nein |
| `/{culture}/{market}/butik/indkoebskurv/kundedata/` | ClientDetails:32 | da | Checkout, Kundendaten | nein |
| `/{culture}/{market}/boutique/panier/donnees-clients/` | ClientDetails:33 | fr | Checkout, Kundendaten | nein |
| `/{culture}/{market}/winkel/winkelwagen/klantgegevens` | ClientDetails:34 | nl | Checkout, Kundendaten | nein |
| `/{culture}/{market}/tienda/carrito-compra/datos-clientes` | ClientDetails:35 | es | Checkout, Kundendaten | nein |
| `/{culture}/{market}/store/shoppingcart/update-client-details/` | ClientDetails:81 | default | Checkout, Kundendaten speichern (POST) | nein |
| `/{culture}/{market}/shop/warenkorb/kundendaten-aktualiseren/` | ClientDetails:82 | de | Checkout, Kundendaten speichern (POST) | nein |
| `/{culture}/{market}/butik/indkoebskurv/opdater-kundedata/` | ClientDetails:83 | da | Checkout, Kundendaten speichern (POST) | nein |
| `/{culture}/{market}/boutique/panier/mise-a-jour-donnees-clients/` | ClientDetails:84 | fr | Checkout, Kundendaten speichern (POST) | nein |
| `/{culture}/{market}/winkel/winkelwagen/klantgegevens-updaten` | ClientDetails:85 | nl | Checkout, Kundendaten speichern (POST) | nein |
| `/{culture}/{market}/tienda/carrito-compra/datos-clientes-actualizar` | ClientDetails:86 | es | Checkout, Kundendaten speichern (POST) | nein |
| `/{culture}/{market}/contact` | ContactUs:35 | default | Formularseite Kontakt | nein |
| `/{culture}/{market}/kontakt` | ContactUs:36 | de | Formularseite Kontakt | nein |
| `/{culture}/{market}/kontaktoplysninger` | ContactUs:37 | da | Formularseite Kontakt | nein |
| `/{culture}/{market}/contactez-nous` | ContactUs:38 | fr | Formularseite Kontakt | nein |
| `/{culture}/{market}/contact-nl` | ContactUs:39 | nl | Formularseite Kontakt | nein |
| `/{culture}/{market}/contacto` | ContactUs:40 | es | Formularseite Kontakt | nein |
| `/{culture}/{market}/send-message` | ContactUs:107 | default | Kontaktformular absenden (POST) | nein |
| `/{culture}/{market}/nachricht-senden` | ContactUs:108 | de | Kontaktformular absenden (POST) | nein |
| `/{culture}/{market}/send-besked` | ContactUs:109 | da | Kontaktformular absenden (POST) | nein |
| `/{culture}/{market}/envoyer-un-message` | ContactUs:110 | fr | Kontaktformular absenden (POST) | nein |
| `/{culture}/{market}/bericht-sturen` | ContactUs:111 | nl | Kontaktformular absenden (POST) | nein |
| `/{culture}/{market}/enviar-mensaje` | ContactUs:112 | es | Kontaktformular absenden (POST) | nein |
| `/{culture}/{market}/send-short-message` | ContactUs:126 | default | Kurzkontakt absenden (POST) | nein |
| `/{culture}/{market}/kurze-nachricht-senden` | ContactUs:127 | de | Kurzkontakt absenden (POST) | nein |
| `/{culture}/{market}/send-kort-besked` | ContactUs:128 | da | Kurzkontakt absenden (POST) | nein |
| `/{culture}/{market}/envoyer-court-message` | ContactUs:129 | fr | Kurzkontakt absenden (POST) | nein |
| `/{culture}/{market}/bericht-kort-sturen` | ContactUs:130 | nl | Kurzkontakt absenden (POST) | nein |
| `/{culture}/{market}/enviar-mensaje-corto` | ContactUs:131 | es | Kurzkontakt absenden (POST) | nein |
| `/{culture}/{market}/education/` | DigitalEducation:23 | default | Inhaltsseite, Digitale Bildung | nein |
| `/{culture}/{market}/bildung/` | DigitalEducation:24 | de | Inhaltsseite, Digitale Bildung | nein |
| `/{culture}/{market}/uddannelse/` | DigitalEducation:25 | da | Inhaltsseite, Digitale Bildung | nein |
| `/{culture}/{market}/éducation/` | DigitalEducation:26 | fr | Inhaltsseite, Digitale Bildung | nein |
| `/{culture}/{market}/onderwijs` | DigitalEducation:27 | nl | Inhaltsseite, Digitale Bildung | nein |
| `/{culture}/{market}/educacion` | DigitalEducation:28 | es | Inhaltsseite, Digitale Bildung | nein |
| `/Error` | Error:14 | default | Fehlerseite | nein |
| `/{culture}/{market}/store/faq/` | FAQ:21 | default | Inhaltsseite, FAQ | nein |
| `/{culture}/{market}/shop/faq/` | FAQ:22 | de | Inhaltsseite, FAQ | nein |
| `/{culture}/{market}/butik/faq/` | FAQ:23 | da | Inhaltsseite, FAQ | nein |
| `/{culture}/{market}/boutique/faq/` | FAQ:24 | fr | Inhaltsseite, FAQ | nein |
| `/{culture}/{market}/winkel/faq/` | FAQ:25 | nl | Inhaltsseite, FAQ | nein |
| `/{culture}/{market}/tienda/faq` | FAQ:26 | es | Inhaltsseite, FAQ | nein |
| `/{culture}/{market}/imprint/` | Imprint:22 | default | Rechtstext, Impressum | nein |
| `/{culture}/{market}/impressum/` | Imprint:23 | de | Rechtstext, Impressum | nein |
| `/{culture}/{market}/kolofon/` | Imprint:24 | da | Rechtstext, Impressum | nein |
| `/{culture}/{market}/mentions-legales/` | Imprint:25 | fr | Rechtstext, Impressum | nein |
| `/{culture}/{market}/opdruk/` | Imprint:26 | nl | Rechtstext, Impressum | nein |
| `/{culture}/{market}/aviso-legal/` | Imprint:27 | es | Rechtstext, Impressum | nein |
| `/{culture}/{market}/knowledge/{seoName}/` | LandingPage:21 | default | Landingpage aus dem CMS | nein |
| `/{culture}/{market}/wissen/{seoName}/` | LandingPage:22 | de | Landingpage aus dem CMS | nein |
| `/{culture}/{market}/viden/{seoName}/` | LandingPage:23 | da | Landingpage aus dem CMS | nein |
| `/{culture}/{market}/savoir/{seoName}/` | LandingPage:24 | fr | Landingpage aus dem CMS | nein |
| `/{culture}/{market}/kennis/{seoName}/` | LandingPage:25 | nl | Landingpage aus dem CMS | nein |
| `/{culture}/{market}/conocimiento/{seoName}/` | LandingPage:26 | es | Landingpage aus dem CMS | nein |
| `/{culture}/{market}/store/licences/` | Licences:30 | default | Kategorie-Einstieg Lizenzen | nein |
| `/{culture}/{market}/shop/lizenzen/` | Licences:31 | de | Kategorie-Einstieg Lizenzen | nein |
| `/{culture}/{market}/butik/licenser/` | Licences:32 | da | Kategorie-Einstieg Lizenzen | nein |
| `/{culture}/{market}/boutique/licences/` | Licences:33 | fr | Kategorie-Einstieg Lizenzen | nein |
| `/{culture}/{market}/winkel/licenties/` | Licences:34 | nl | Kategorie-Einstieg Lizenzen | nein |
| `/{culture}/{market}/tienda/licencias/` | Licences:35 | es | Kategorie-Einstieg Lizenzen | nein |
| `/{culture}/{market}/store/licences/categories/all/{*filterlink}` | Licences:46 | default | Filterliste Lizenzen, alle | nein |
| `/{culture}/{market}/shop/lizenzen/kategorien/alle/{*filterlink}` | Licences:47 | de | Filterliste Lizenzen, alle | nein |
| `/{culture}/{market}/butik/licenser/kategorier/alle/{*filterlink}` | Licences:48 | da | Filterliste Lizenzen, alle | nein |
| `/{culture}/{market}/boutique/licences/categories/tous/{*filterlink}` | Licences:49 | fr | Filterliste Lizenzen, alle | nein |
| `/{culture}/{market}/winkel/licenties/categorieen/licences/alle/{*filterlink}` | Licences:50 | nl | Filterliste Lizenzen, alle | nein |
| `/{culture}/{market}/tienda/licencias/categorias/licences/todo/{*filterlink}` | Licences:51 | es | Filterliste Lizenzen, alle | nein |
| `/{culture}/{market}/store/licences/1001/categories/0/all/{*filterlink}` | Licences:67 | en | Filterliste Lizenzen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/shop/lizenzen/1001/kategorien/0/alle/{*filterlink}` | Licences:68 | de | Filterliste Lizenzen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/butik/licenser/1001/kategorier/0/alle/{*filterlink}` | Licences:69 | da | Filterliste Lizenzen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/boutique/licences/1001/categories/0/tous/{*filterlink}` | Licences:70 | fr | Filterliste Lizenzen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/winkel/licenties/1001/categorieen/0/alle/{*filterlink}` | Licences:71 | nl | Filterliste Lizenzen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/tienda/licencias/1001/categorias/0/todo/{*filterlink}` | Licences:72 | es | Filterliste Lizenzen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/store/licences/categories/recommended/{*filterlink}` | Licences:83 | default | Filterliste Lizenzen, empfohlen | nein |
| `/{culture}/{market}/shop/lizenzen/kategorien/empfohlen/{*filterlink}` | Licences:84 | de | Filterliste Lizenzen, empfohlen | nein |
| `/{culture}/{market}/butik/licenser/kategorier/anbefalet/{*filterlink}` | Licences:85 | da | Filterliste Lizenzen, empfohlen | nein |
| `/{culture}/{market}/boutique/licences/categories/recommande/{*filterlink}` | Licences:86 | fr | Filterliste Lizenzen, empfohlen | nein |
| `/{culture}/{market}/winkel/licenties/categorieen/aanbevolen/{*filterlink}` | Licences:87 | nl | Filterliste Lizenzen, empfohlen | nein |
| `/{culture}/{market}/tienda/licencias/categorias/recomendado/{*filterlink}` | Licences:88 | es | Filterliste Lizenzen, empfohlen | nein |
| `/{culture}/{market}/store/licences/1001/categories/10008/recommended/{*filterlink}` | Licences:119 | en | Filterliste Lizenzen empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/shop/lizenzen/1001/kategorien/10008/empfohlen/{*filterlink}` | Licences:120 | de | Filterliste Lizenzen empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/butik/licenser/1001/kategorier/10008/anbefalet/{*filterlink}` | Licences:121 | da | Filterliste Lizenzen empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/boutique/licences/1001/categories/10008/recommande/{*filterlink}` | Licences:122 | fr | Filterliste Lizenzen empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/winkel/licenties/1001/categorieen/10008/aanbevolen/{*filterlink}` | Licences:123 | nl | Filterliste Lizenzen empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/tienda/licencias/1001/categorias/10008/recomendado/{*filterlink}` | Licences:124 | es | Filterliste Lizenzen empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/store/licences/details/{productId}/{productName}/{id?}` | Licences:135 | default | Detailseite Lizenz | nein |
| `/{culture}/{market}/shop/lizenzen/details/{productId}/{productName}/{id?}` | Licences:136 | de | Detailseite Lizenz | nein |
| `/{culture}/{market}/butik/licenser/detaljer/{productId}/{productName}/{id?}` | Licences:137 | da | Detailseite Lizenz | nein |
| `/{culture}/{market}/boutique/licences/details/{productId}/{productName}/{id?}` | Licences:138 | fr | Detailseite Lizenz | nein |
| `/{culture}/{market}/winkel/licenties/details/{productId}/{productName}/{id?}` | Licences:139 | nl | Detailseite Lizenz | nein |
| `/{culture}/{market}/tienda/licencias/detalles/{productId}/{productName}/{id?}` | Licences:140 | es | Detailseite Lizenz | nein |
| `/{culture}/{market}/store/market-and-culture/` | MarketCulture:23 | default | Markt- und Sprachauswahl | nein |
| `/{culture}/{market}/shop/sprache-waehlen/` | MarketCulture:24 | de | Markt- und Sprachauswahl | nein |
| `/{culture}/{market}/butik/vaelg-sprog/` | MarketCulture:25 | da | Markt- und Sprachauswahl | nein |
| `/{culture}/{market}/boutique/choix-de-langue/` | MarketCulture:26 | fr | Markt- und Sprachauswahl | nein |
| `/{culture}/{market}/winkel/taal-kiezen/` | MarketCulture:27 | nl | Markt- und Sprachauswahl | nein |
| `/{culture}/{market}/tienda/elegir-idioma/` | MarketCulture:28 | es | Markt- und Sprachauswahl | nein |
| `/{culture}/{market}/market-info/` | MarketInfo:24 | default | Hinweisseite, Markt nicht verfuegbar | nein |
| `/{culture}/{market}/markt-info/` | MarketInfo:25 | de | Hinweisseite, Markt nicht verfuegbar | nein |
| `/{culture}/{market}/marked-info/` | MarketInfo:26 | da | Hinweisseite, Markt nicht verfuegbar | nein |
| `/{culture}/{market}/marche-info` | MarketInfo:27 | fr | Hinweisseite, Markt nicht verfuegbar | nein |
| `/{culture}/{market}/markt-informatie` | MarketInfo:28 | nl | Hinweisseite, Markt nicht verfuegbar | nein |
| `/{culture}/{market}/mercado-info` | MarketInfo:29 | es | Hinweisseite, Markt nicht verfuegbar | nein |
| `/{culture}/{market}/store/modern-workplace-definition/` | ModernWorkplace:23 | default | Inhaltsseite, Modern Workplace | nein |
| `/{culture}/{market}/shop/modern-workplace-definition/` | ModernWorkplace:24 | de | Inhaltsseite, Modern Workplace | nein |
| `/{culture}/{market}/butik/modern-workplace-definition/` | ModernWorkplace:25 | da | Inhaltsseite, Modern Workplace | nein |
| `/{culture}/{market}/boutique/definition-modern-workplace/` | ModernWorkplace:26 | fr | Inhaltsseite, Modern Workplace | nein |
| `/{culture}/{market}/winkel/modern-workplace-definition` | ModernWorkplace:27 | nl | Inhaltsseite, Modern Workplace | nein |
| `/{culture}/{market}/tienda/definicion-modern-workplace` | ModernWorkplace:28 | es | Inhaltsseite, Modern Workplace | nein |
| `/{culture}/{market}/order-process/` | OrderProcess:23 | default | Inhaltsseite, Bestellablauf | nein |
| `/{culture}/{market}/bestell-ablauf/` | OrderProcess:24 | de | Inhaltsseite, Bestellablauf | nein |
| `/{culture}/{market}/bestillingsproces/` | OrderProcess:25 | da | Inhaltsseite, Bestellablauf | nein |
| `/{culture}/{market}/processus-de-commande/` | OrderProcess:26 | fr | Inhaltsseite, Bestellablauf | nein |
| `/{culture}/{market}/bestelproces` | OrderProcess:27 | nl | Inhaltsseite, Bestellablauf | nein |
| `/{culture}/{market}/proceso-compra` | OrderProcess:28 | es | Inhaltsseite, Bestellablauf | nein |
| `/{culture}/{market}/privacy-policy/` | Privacy:24 | default | Rechtstext, Datenschutz | nein |
| `/{culture}/{market}/datenschutz/` | Privacy:25 | de | Rechtstext, Datenschutz | nein |
| `/{culture}/{market}/privatlivspolitik/` | Privacy:26 | da | Rechtstext, Datenschutz | nein |
| `/{culture}/{market}/protection-des-donnees/` | Privacy:27 | fr | Rechtstext, Datenschutz | nein |
| `/{culture}/{market}/gegevensbescherming` | Privacy:28 | nl | Rechtstext, Datenschutz | nein |
| `/{culture}/{market}/proteccion-datos` | Privacy:29 | es | Rechtstext, Datenschutz | nein |
| `/{culture}/{market}/check-privacypolicy/` | Privacy:38 | default | Rechtstext, Datenschutz mit Einwilligung | nein |
| `/{culture}/{market}/hinweise-datenschutz/` | Privacy:39 | de | Rechtstext, Datenschutz mit Einwilligung | nein |
| `/{culture}/{market}/databeskyttelsesmeddelelse/` | Privacy:40 | da | Rechtstext, Datenschutz mit Einwilligung | nein |
| `/{culture}/{market}/remarques-protection-des-donnees/` | Privacy:41 | fr | Rechtstext, Datenschutz mit Einwilligung | nein |
| `/{culture}/{market}/gegevensbescherming-controleren` | Privacy:42 | nl | Rechtstext, Datenschutz mit Einwilligung | nein |
| `/{culture}/{market}/politica-privacidad` | Privacy:43 | es | Rechtstext, Datenschutz mit Einwilligung | nein |
| `/{culture}/{market}/store/products/` | Products:42 | default | Shop-Startseite, Produkte | nein |
| `/{culture}/{market}/shop/produkte/` | Products:43 | de | Shop-Startseite, Produkte | nein |
| `/{culture}/{market}/butik/produkter/` | Products:44 | da | Shop-Startseite, Produkte | nein |
| `/{culture}/{market}/boutique/produits/` | Products:45 | fr | Shop-Startseite, Produkte | nein |
| `/{culture}/{market}/winkel/producten/` | Products:46 | nl | Shop-Startseite, Produkte | nein |
| `/{culture}/{market}/tienda/productos/` | Products:47 | es | Shop-Startseite, Produkte | nein |
| `/{culture}/{market}/store/devices/` | Products:78 | default | Liste Geraete | nein |
| `/{culture}/{market}/shop/geraete/` | Products:79 | de | Liste Geraete | nein |
| `/{culture}/{market}/butik/enheder/` | Products:80 | da | Liste Geraete | nein |
| `/{culture}/{market}/boutique/appareils/` | Products:81 | fr | Liste Geraete | nein |
| `/{culture}/{market}/winkel/apparaten/` | Products:82 | nl | Liste Geraete | nein |
| `/{culture}/{market}/tienda/dispositivos/` | Products:83 | es | Liste Geraete | nein |
| `/{culture}/{market}/store/devices/{productId}/{productName}/{id?}` | Products:110 | default | Detailseite Geraet | nein |
| `/{culture}/{market}/shop/geraete/{productId}/{productName}/{id?}` | Products:111 | de | Detailseite Geraet | nein |
| `/{culture}/{market}/butik/enheder/{productId}/{productName}/{id?}` | Products:112 | da | Detailseite Geraet | nein |
| `/{culture}/{market}/boutique/appareils/{productId}/{productName}/{id?}` | Products:113 | fr | Detailseite Geraet | nein |
| `/{culture}/{market}/winkel/apparaten/{productId}/{productName}/{id?}` | Products:114 | nl | Detailseite Geraet | nein |
| `/{culture}/{market}/tienda/dispositivos/{productId}/{productName}/{id?}` | Products:115 | es | Detailseite Geraet | nein |
| `/{culture}/{market}/store/devices/{productId}/{productName}/{variantId?}/{variantName?}` | Products:116 | default | Detailseite Geraet | nein |
| `/{culture}/{market}/shop/geraete/{productId}/{productName}/{variantId?}/{variantName?}` | Products:117 | de | Detailseite Geraet | nein |
| `/{culture}/{market}/butik/enheder/{productId}/{productName}/{variantId?}/{variantName?}` | Products:118 | da | Detailseite Geraet | nein |
| `/{culture}/{market}/boutique/appareils/{productId}/{productName}/{variantId?}/{variantName?}` | Products:119 | fr | Detailseite Geraet | nein |
| `/{culture}/{market}/winkel/apparaten/{productId}/{productName}/{variantId?}/{variantName?}` | Products:120 | nl | Detailseite Geraet | nein |
| `/{culture}/{market}/tienda/dispositivos/{productId}/{productName}/{variantId?}/{variantName?}` | Products:121 | es | Detailseite Geraet | nein |
| `/{culture}/{market}/store/products/details/{productId}/{productName}/{id?}` | Products:132 | default | Detailseite Produkt, verteilt weiter | ja, 301 je Kategorie |
| `/{culture}/{market}/shop/produkte/details/{productId}/{productName}/{id?}` | Products:133 | de | Detailseite Produkt, verteilt weiter | ja, 301 je Kategorie |
| `/{culture}/{market}/butik/produkter/detaljer/{productId}/{productName}/{id?}` | Products:134 | da | Detailseite Produkt, verteilt weiter | ja, 301 je Kategorie |
| `/{culture}/{market}/boutique/produits/details/{productId}/{productName}/{id?}` | Products:135 | fr | Detailseite Produkt, verteilt weiter | ja, 301 je Kategorie |
| `/{culture}/{market}/winkel/producten/details/{productId}/{productName}/{id?}` | Products:136 | nl | Detailseite Produkt, verteilt weiter | ja, 301 je Kategorie |
| `/{culture}/{market}/tienda/productos/detalles/{productId}/{productName}/{id?}` | Products:137 | es | Detailseite Produkt, verteilt weiter | ja, 301 je Kategorie |
| `/{culture}/{market}/store/services/` | Services:30 | default | Kategorie-Einstieg Dienstleistungen | nein |
| `/{culture}/{market}/shop/dienstleistungen/` | Services:31 | de | Kategorie-Einstieg Dienstleistungen | nein |
| `/{culture}/{market}/butik/tjenester/` | Services:32 | da | Kategorie-Einstieg Dienstleistungen | nein |
| `/{culture}/{market}/boutique/services/` | Services:33 | fr | Kategorie-Einstieg Dienstleistungen | nein |
| `/{culture}/{market}/winkel/diensten/` | Services:34 | nl | Kategorie-Einstieg Dienstleistungen | nein |
| `/{culture}/{market}/tienda/servicios/` | Services:35 | es | Kategorie-Einstieg Dienstleistungen | nein |
| `/{culture}/{market}/store/services/categories/all/{*filterlink}` | Services:46 | default | Filterliste Dienstleistungen, alle | nein |
| `/{culture}/{market}/shop/dienstleistungen/kategorien/alle/{*filterlink}` | Services:47 | de | Filterliste Dienstleistungen, alle | nein |
| `/{culture}/{market}/butik/tjenester/kategorier/alle/{*filterlink}` | Services:48 | da | Filterliste Dienstleistungen, alle | nein |
| `/{culture}/{market}/boutique/services/categories/tous/{*filterlink}` | Services:49 | fr | Filterliste Dienstleistungen, alle | nein |
| `/{culture}/{market}/winkel/diensten/categorieen/alle/{*filterlink}` | Services:50 | nl | Filterliste Dienstleistungen, alle | nein |
| `/{culture}/{market}/tienda/servicios/categorias/todo/{*filterlink}` | Services:51 | es | Filterliste Dienstleistungen, alle | nein |
| `/{culture}/{market}/store/services/1001/categories/0/all/{*filterlink}` | Services:67 | en | Filterliste Dienstleistungen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/shop/dienstleistungen/1001/kategorien/0/alle/{*filterlink}` | Services:68 | de | Filterliste Dienstleistungen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/butik/tjenester/1001/kategorier/0/alle/{*filterlink}` | Services:69 | da | Filterliste Dienstleistungen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/boutique/services/1001/categories/0/tous/{*filterlink}` | Services:70 | fr | Filterliste Dienstleistungen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/winkel/diensten/1001/categorieen/0/alle/{*filterlink}` | Services:71 | nl | Filterliste Dienstleistungen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/tienda/servicios/1001/categorias/0/todo/{*filterlink}` | Services:72 | es | Filterliste Dienstleistungen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/store/services/categories/recommended/{*filterlink}` | Services:83 | default | Filterliste Dienstleistungen, empfohlen | nein |
| `/{culture}/{market}/shop/dienstleistungen/kategorien/empfohlen/{*filterlink}` | Services:84 | de | Filterliste Dienstleistungen, empfohlen | nein |
| `/{culture}/{market}/butik/tjenester/kategorier/anbefalet/{*filterlink}` | Services:85 | da | Filterliste Dienstleistungen, empfohlen | nein |
| `/{culture}/{market}/boutique/services/categories/recommande/{*filterlink}` | Services:86 | fr | Filterliste Dienstleistungen, empfohlen | nein |
| `/{culture}/{market}/winkel/diensten/categorieen/aanbevolen/{*filterlink}` | Services:87 | nl | Filterliste Dienstleistungen, empfohlen | nein |
| `/{culture}/{market}/tienda/servicios/categorias/recomendado/{*filterlink}` | Services:88 | es | Filterliste Dienstleistungen, empfohlen | nein |
| `/{culture}/{market}/store/services/1001/categories/10008/recommended/{*filterlink}` | Services:119 | en | Filterliste Dienstl. empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/shop/dienstleistungen/1001/kategorien/10008/empfohlen/{*filterlink}` | Services:120 | de | Filterliste Dienstl. empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/butik/tjenester/1001/kategorier/10008/anbefalet/{*filterlink}` | Services:121 | da | Filterliste Dienstl. empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/boutique/services/1001/categories/10008/recommande/{*filterlink}` | Services:122 | fr | Filterliste Dienstl. empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/winkel/diensten/1001/categorieen/10008/aanbevolen/{*filterlink}` | Services:123 | nl | Filterliste Dienstl. empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/tienda/servicios/1001/categorias/10008/recomendado/{*filterlink}` | Services:124 | es | Filterliste Dienstl. empfohlen, alte Form | ja, 301 auf die neue Form |
| `/{culture}/{market}/store/services/details/{productId}/{productName}/{id?}` | Services:135 | default | Detailseite Dienstleistung | nein |
| `/{culture}/{market}/shop/dienstleistungen/details/{productId}/{productName}/{id?}` | Services:136 | de | Detailseite Dienstleistung | nein |
| `/{culture}/{market}/butik/tjenester/detaljer/{productId}/{productName}/{id?}` | Services:137 | da | Detailseite Dienstleistung | nein |
| `/{culture}/{market}/boutique/services/details/{productId}/{productName}/{id?}` | Services:138 | fr | Detailseite Dienstleistung | nein |
| `/{culture}/{market}/winkel/diensten/details/{productId}/{productName}/{id?}` | Services:139 | nl | Detailseite Dienstleistung | nein |
| `/{culture}/{market}/tienda/servicios/detalles/{productId}/{productName}/{id?}` | Services:140 | es | Detailseite Dienstleistung | nein |
| `/{culture}/{market}/store/shoppingcart/` | ShoppingCart:38 | default | Warenkorb | nein |
| `/{culture}/{market}/shop/warenkorb/` | ShoppingCart:39 | de | Warenkorb | nein |
| `/{culture}/{market}/butik/indkoebskurv/` | ShoppingCart:40 | da | Warenkorb | nein |
| `/{culture}/{market}/boutique/panier/` | ShoppingCart:41 | fr | Warenkorb | nein |
| `/{culture}/{market}/winkel/winkelwagen/` | ShoppingCart:42 | nl | Warenkorb | nein |
| `/{culture}/{market}/tienda/carrito-compra/` | ShoppingCart:43 | es | Warenkorb | nein |
| `/{culture}/{market}/store/clientdetails/` | ShoppingCart:317 | default | Checkout, Kundendaten | nein |
| `/{culture}/{market}/shop/kundendaten/` | ShoppingCart:318 | de | Checkout, Kundendaten | nein |
| `/{culture}/{market}/butik/kundedata/` | ShoppingCart:319 | da | Checkout, Kundendaten | nein |
| `/{culture}/{market}/boutique/donnees-clients/` | ShoppingCart:320 | fr | Checkout, Kundendaten | nein |
| `/{culture}/{market}/winkel/klantgegevens/` | ShoppingCart:321 | nl | Checkout, Kundendaten | nein |
| `/{culture}/{market}/tienda/datos-cliente/` | ShoppingCart:322 | es | Checkout, Kundendaten | nein |
| `/{culture}/{market}/store/shoppingcart/order-summary/` | Summary:37 | default | Checkout, Zusammenfassung | nein |
| `/{culture}/{market}/shop/warenkorb/zusammenfassung/` | Summary:38 | de | Checkout, Zusammenfassung | nein |
| `/{culture}/{market}/butik/indkoebskurv/ordreoversigt/` | Summary:39 | da | Checkout, Zusammenfassung | nein |
| `/{culture}/{market}/boutique/panier/resume/` | Summary:40 | fr | Checkout, Zusammenfassung | nein |
| `/{culture}/{market}/winkel/winkelwagen/overzicht/` | Summary:41 | nl | Checkout, Zusammenfassung | nein |
| `/{culture}/{market}/tienda/carrito-compra/resumen/` | Summary:42 | es | Checkout, Zusammenfassung | nein |
| `/{culture}/{market}/conditions/` | TandC:21 | default | Rechtstext, AGB | nein |
| `/{culture}/{market}/agb/` | TandC:22 | de | Rechtstext, AGB | nein |
| `/{culture}/{market}/standardvilkaar/` | TandC:23 | da | Rechtstext, AGB | nein |
| `/{culture}/{market}/conditions-generales/` | TandC:24 | fr | Rechtstext, AGB | nein |
| `/{culture}/{market}/condities` | TandC:25 | nl | Rechtstext, AGB | nein |
| `/{culture}/{market}/condiciones-generales` | TandC:26 | es | Rechtstext, AGB | nein |
| `/{culture}/{market}/store/thank-you` | ThankYou:51 | default | Bestellabschluss, Danke-Seite | nein |
| `/{culture}/{market}/shop/vielen-dank` | ThankYou:52 | de | Bestellabschluss, Danke-Seite | nein |
| `/{culture}/{market}/butik/mange-tak` | ThankYou:53 | da | Bestellabschluss, Danke-Seite | nein |
| `/{culture}/{market}/boutique/merci-beaucoup` | ThankYou:54 | fr | Bestellabschluss, Danke-Seite | nein |
| `/{culture}/{market}/winkel/hartelijk-dank` | ThankYou:55 | nl | Bestellabschluss, Danke-Seite | nein |
| `/{culture}/{market}/tienda/muchas-gracias` | ThankYou:56 | es | Bestellabschluss, Danke-Seite | nein |

### Die zwoelf fest verdrahteten Routen

| Pfad | Quelle | Seitentyp | Weiterleitung vorhanden |
|---|---|---|---|
| `/` | Home:26 | Einstieg, verteilt nach Herkunftsland weiter | ja, 302 auf Produktseite oder Marktauswahl |
| `/sitemap.xml` | SiteMap:26 | Sitemap | nein |
| `/education` | DigitalEducation:38 | Altadresse Bildungsseite | ja, 301 auf die lokalisierte Bildungsseite |
| `/{culture}/{market}/dataprotectionadvice` | DataProtectionAdvice:14 | Rechtstext, Datenschutzhinweis | nein |
| `/{culture}/{market}/UpdateMarketAndCulture` | MarketCulture:43 | Markt- und Sprachwechsel (POST) | nein |
| `/{culture}/{market}/savetocart` | Products:193 | In den Warenkorb legen (POST) | nein |
| `/ShoppingCart` | ShoppingCart:21 | Warenkorb, Controller-Vorgabe | nein |
| `/{culture}/{market}/ShoppingCart/AddMoreProducts` | ShoppingCart:164 | Warenkorb, weitere Artikel (POST) | nein |
| `/{culture}/{market}/ShoppingCart/addnewchildproduct` | ShoppingCart:202 | Warenkorb, Unterartikel (POST) | nein |
| `/{culture}/{market}/ShoppingCart/deleteproducts` | ShoppingCart:229 | Warenkorb, loeschen (POST) | nein |
| `/{culture}/{market}/ShoppingCart/updatecart` | ShoppingCart:253 | Warenkorb, aktualisieren (POST) | nein |
| `/{culture}/{market}/ShoppingCart/updatechildproduct` | ShoppingCart:281 | Warenkorb, Unterartikel aendern (POST) | nein |

## Was die Sitemap ausgibt

`SiteMapController` erzeugt `/sitemap.xml` selbst. Er schreibt 13 feste Knoten
mit fester Gewichtung, dazu einen Knoten je Bundle mit 0,8 und einen je
Produktdetailseite mit 0,7, jeweils aus `productId` und `SeoProductName`
gebildet. Zu jedem Knoten schreibt er `hreflang`-Alternativen fuer die
unterstuetzten Kulturen.

| Knoten | Gewicht |
|---|---|
| Produkte | 1,0 |
| Bundles (je Bundle) | 0,8 |
| Produktdetail (je Produkt) | 0,7 |
| Ueber uns | 0,6 |
| Vorteile, Karriere, Bestellablauf | 0,5 |
| Kontakt, FAQ | 0,4 |
| Impressum, Datenschutz, AGB | 0,2 |
| Markt- und Sprachauswahl, Marktinfo, Modern Workplace | 0,1 |

In `/src/PT.SurfaceShop.Web/wwwroot` liegen ausserdem `robots.txt` und
`google591594f30f3c52fd.html`, die Bestaetigungsdatei fuer die Google Search
Console. Die `robots.txt` erlaubt alles und verweist auf
`https://surface.love/sitemap.xml`.

## Aeltere Adressgenerationen, die es wirklich gegeben hat

Der heutige Code ist die dritte Generation. Zwei aeltere sind an den Vorgaengen
belegt, mit konkreten Adressen aus der Google Search Console. Diese Muster
stehen in keinem Code mehr, sie koennen aber weiterhin im Index stehen und in
fremden Seiten verlinkt sein.

**Erste Generation, ohne Kultur und Markt, belegt bis Januar 2019:**

| Muster | Quelle | Seitentyp | Weiterleitung vorhanden |
|---|---|---|---|
| `/store/rent/licences/{id}/{name}` | Vorgang 4648, 4649 | Detailseite Lizenz, Miete | nein, lief auf 404 |
| `/store/rent/devices/{id}/{name}/{vid}/{vname}` | Vorgang 5696 | Detailseite Geraet, Miete | nein, lief auf 500 |
| `/store/lease/devices/{id}/{name}/{vid}/{vname}` | Vorgang 5696 | Detailseite Geraet, Leasing | nein, lief auf 500 |
| `/store/rent/bundle/{id}/{name}` | Vorgang 5696 | Detailseite Bundle, Miete | nein, lief auf 500 |
| `/store/finance/licences?subcategoryid=&subcategoryname=` | Vorgang 5640 | Filterliste Lizenzen, Finanzierung | nein, lief auf 500 |
| `/home/details/{id}` | Vorgang 5640 | Detailseite, aelteste Form | nein, lief auf 500 |
| `/?action=Index&controller=Products` | Vorgang 5696 | Einstieg mit Steuerparametern | nein, lief auf 500 |

**Zweite Generation, mit Kultur und Markt, aber mit der Finanzierungsform im
Pfad, belegt Januar 2019:**

| Muster | Quelle | Seitentyp | Weiterleitung vorhanden |
|---|---|---|---|
| `/{culture}/{market}/shop/mieten/geraete/{id}/{name}/{vid}/{vname}` | Vorgang 5696 | Detailseite Geraet, Miete, deutsch | nein |
| `/{culture}/{market}/store/rent/devices/{id}/{name}/{vid}/{vname}` | Vorgang 5640 | Detailseite Geraet, Miete, englisch | nein |
| `/{culture}/{market}/shop/cart_ordertype_{n}/accessories/details/{id}/{name}?vid=&SelectedVariantName=` | Vorgang 5640 | Detailseite Zubehoer mit Bestellart im Pfad | nein |
| `/{culture}/{market}/store/faq`, `/{culture}/{market}/shop/faq` | Vorgang 5696 | FAQ, ohne Schraegstrich am Ende | nein |
| `/{culture}/{market}/shop/geraete`, `/{culture}/{market}/store/devices` | Vorgang 5696 | Geraeteliste, ohne Schraegstrich am Ende | nein |
| `/{culture}/{market}/vorteile`, `/{culture}/{market}/advantages` | Vorgang 5696 | Vorteile, ohne Schraegstrich am Ende | nein |
| `/{culture}/{market}/kontakt`, `/{culture}/{market}/contact` | Vorgang 5696 | Kontakt, ohne Schraegstrich am Ende | nein |
| `/{0}/contact` | Vorgang 5640 | fehlerhaft erzeugte Adresse mit Platzhalter | nein |

Die 41 Adressen selbst liegen als zwei CSV-Anhaenge an den Vorgaengen 5640
(`Google Report Serverfehler 5xx.csv`, 28 Adressen) und 5696
(`Index Coverage Drilldown 2019-01-31.csv`, 13 Adressen). Sie sind dort
abrufbar und deshalb hier nicht abgeschrieben.

Bemerkenswert an der zweiten Generation: die Adressen enden dort **ohne**
Schraegstrich, der heutige Code erzeugt sie **mit**. Wer die Weiterleitungen
baut, muss beide Formen bedienen.

## Weiterleitungen, die es heute schon gibt

| Weiterleitung | Art | Quelle |
|---|---|---|
| Alles ausser `en-GB`/`GB` und `de-DE`/`DE` auf `/de-de/deutschland/market-info` | 302 | `Extensions/RedirectMarketInfo.cs` |
| `/` auf die Produktseite des per IP erkannten Marktes, sonst auf die Marktauswahl | 302 | `Home:26` |
| `/education` auf die lokalisierte Bildungsseite | 301 | `DigitalEducation:38-41` |
| Filterlisten alter Form (mit `1001` und Kategorie-Ids) auf die neue Form, je Sprache | 301 | Accessories:76 und 128, Licences:75 und 127, Services:75 und 127 |
| Produktdetail auf die Detailseite der richtigen Kategorie, also Zubehoer, Lizenz, Dienstleistung oder Geraet | 301 | `Products:146-179` |
| Abgelaufenes Bundle auf die Uebersicht | im Code angelegt | Vorgang 5769 |

Was **nicht** im Code steht: eine Weiterleitung von `www.surface.love` auf
`surface.love` oder umgekehrt. Vorgang 4797 "www. Weiterleitungen 4.3" ist
geschlossen, traegt aber keine Beschreibung. Die Regel liegt also entweder in
Azure vor der Anwendung oder sie ist nur mehr am Vorgang dokumentiert.

## Die Vorgaenge, die fuer die Weiterleitungsliste wirklich zaehlen

Von den 150 Treffern sind diese die tragenden. Sie sind entweder nicht
abgearbeitet worden oder sie beschreiben eine Regel, die der neue Shop
uebernehmen muss.

| Id | Zustand | Titel | Warum er zaehlt |
|---|---|---|---|
| 4338 | Closed | Product change (link change), redirect option | haelt die Regel fest: aendert sich die Adresse eines Produkts, muss die alte per 301 auf die neue zeigen, und warnt vor mehrstufigen Ketten |
| 4444 | Closed | URL simplification for filter pages | zeigt alte und neue Filteradresse im Vergleich und stellt die Frage 301 oder 302, die im Vorgang nicht beantwortet ist |
| 4493 | **New** | hreflang are on the sitemap | offen |
| 4513 | **New** | Alle URLs ohne Sonderzeichen, Leerzeichen, Hochkomma | offen |
| 4540 | **New** | SEO metadata code change, Squidex | offen |
| 4670 | **New** | remove old link from menu | offen |
| 4671 | **New** | check all links, because they are really wrong in production | offen |
| 4673 | **New** | redirect "old link" traffic | nennt die konkrete Regel fuer `/education` samt Zielseite |
| 4800 | Closed | kurze URL und Masterseiten | beschreibt den Umbau auf Masterseiten und sagt ausdruecklich "alte URLs 301" |
| 5029 | **New** | Surface Duo, Link Maerkte DE und AT fuehrt in UK und US auf eine Microsoft-Seite | offen, fuehrt aus dem Shop hinaus |
| 5703 | Closed | URL Anpassung als Vorbereitung der Internationalisierung | beschreibt die Einfuehrung von Kultur und Markt in die Adresse samt 301 |
| 5721 | Closed | Definition URL-Struktur fuer alle Seitentypen | der Ort, an dem die Struktur definiert wurde, am Vorgang selbst steht nichts |
| 5896 | **New** | Sitemap bei Google einreichen | offen |
| 5903 | **New** | Verwendung der Sitemap | offen |
| 5966 | **New** | einzelne Varianten von Produkten als Deep Link erreichbar machen | offen |

## worklove.shop

Im gesamten Projekt Surface.Love gibt es **sechs** Vorgaenge, die das Wort
`worklove` fuehren, und alle sechs liegen im neuen Board, nicht im Alt-Shop:
6975, 6985, 7010, 7073, 7203 und 7204. Im Bereichsknoten `Alt-Shop-2024`
kommt `worklove` an keiner Stelle vor, auch nicht in Beschreibungen oder
Verlaeufen. In keinem der 19 Projekte der Organisation gibt es ein Repo, das
zu worklove.shop gehoert.

Fuer die Weiterleitung heisst das: **aus dem alten Shop laesst sich zu
worklove.shop nichts gewinnen.** Welche Adressen unter dieser Domain je
erreichbar waren, steht weder im Code noch am Board. Die Domain ist damit ein
Fall fuer den Cloudflare- und Search-Console-Export, nicht fuer diese Inventur.
Die Entscheidung des Masters vom 06.09., worklove.shop per 301 auf
`www.surface.love` zu legen, bleibt davon unberuehrt, sie braucht nur keine
Einzelpfade.

---

# 2. Rechtstexte

Noch nicht erhoben. Der erste Befund aus Bereich 1 vorweg, weil er die Suche
lenkt: die Rechtstexte liegen **nicht** im Repo, sondern als Inhalt im CMS. Das
Repo fuehrt nur die Datenmodelle `Imprint`, `Privacy` und `TandC` samt der
zugehoerigen Squidex-Repositories und Controller. Ohne Squidex-Zugang laesst
sich aus dem Repo kein einziger Rechtstext lesen. Vorgang 4245 ("imprint url
muss auf dem cms speichert werden", Zustand Resolved) bestaetigt das.

# 3. Sonst Brauchbares

Noch nicht erhoben.

---

# Nicht gefunden, obwohl erwartet

| Erwartet | Befund |
|---|---|
| Repo `SLSHOPAISTUDIO` | existiert in keinem der 19 Projekte der Organisation desktop365. Entweder liegt es in einer anderen Organisation, es ist geloescht, oder der Name lautet anders. |
| Bezug des fremden Wikis zum alten Shop | das Wiki liegt in einem fremden Projekt der Organisation und betrifft einen anderen Auftrag. Zum Surface-Love-Shop steht dort nichts. |
| Marktsegmente der Adressen | im Repo ist nur `deutschland` belegt, die uebrigen liegen als Daten in Squidex. |
| `www`-Weiterleitung im Code | nicht vorhanden, siehe oben. |
| Adressen von worklove.shop | im gesamten Alt-Shop-Bestand nicht vorhanden. |
| Der Volltext der beiden Google-Listen als Datei im Repo | die 41 Adressen liegen ausschliesslich als CSV-Anhang an den Vorgaengen 5640 und 5696. |
