# Routen und SEO (surface.love)

Fassung 2, Stand 27.11.2026, R1 (8152) und SEO10 Teil 2 (8143). Grundlage: E-174, E-176, E-180, E-186, E-215, E-217, E-219, E-228, E-230, E-231, E-234, S14 (C9), S16 (Livegang), S17 (Warenkorb), Vertragstext von CC-SEO (SEO05, 8138).
Fassung 1 vom 25.11.2026, W3 (8097), abgeglichen gegen Shop-`main` `0786e2e`, den Zweig `s17-warenkorb` und `https://surface.love/sitemap.xml` (26 Adressen) am 25.11.2026.

## 0. Geltung
- Dieser Vertrag ist die Pflichtquelle für die Punkte 1 (Adressen) und 2 (SEO) der Auswirkungsprüfung nach E-180. Jeder Shop-PR, der eine Route, eine Weiterleitung, eine Kanonik oder die Sitemap berührt, prüft gegen ihn.
- Er gilt für den Storefront `surface` auf `surface.love`. lenovo.online bekommt einen eigenen Abschnitt, wenn es live geht.
- Die Werte stehen im Shop-Code: `lib/routen.ts`, `lib/stories/paths.ts`, `next.config.mjs`, `proxy.ts`, `lib/seo/`, `config/storefronts/surface.ts`. Weicht der Code von diesem Vertrag ab, ist das ein Fehler im Code oder es braucht zuerst eine Vertragsänderung per Hub-PR.

## 1. Hosts
| Host | Rolle | Index | Verhalten |
|---|---|---|---|
| `surface.love` | kanonische Domain | ja | einzige Domain mit Kanonik, Sitemap und offener robots.txt |
| `www.surface.love` | Alias | nein | 308 auf `https://surface.love`, in einem Sprung auf das Endziel: die Wurzel direkt auf `/de`, Altpfade direkt auf ihr Ziel aus Abschnitt 8. Im Shop (`proxy.ts`). E-176 sieht 301 vor, 308 ist gleichwertig und nötig, weil das Zertifikat für Stamm und www ohne Proxy an der Kante ausgestellt wird |
| `beta.surface.love` und weitere Testdomains aus `config/storefronts/surface.ts` | Vorstufe | nein | `X-Robots-Tag: noindex, nofollow`, meta noindex, robots.txt `Disallow: /`, leere Sitemap |
| jede unbekannte Adresse, etwa eine Vorschau des Hosters | keine | nein | wie Testdomain |
| Länder `at`, `de`, `dk`, `es`, `fr`, `uk` unter surface.love | Altadressen | nein | 301 auf `https://surface.love/de`, an der Kante (E-176) |
| `blog` und `stories` unter surface.love | Altadressen | nein | 301 auf `https://surface.love/de/stories` ohne Pfad, an der Kante (E-176) |
| `http://` auf jedem Host oben | unverschlüsselt | nein | dauerhaft auf `https://surface.love` mit dem Endziel, in höchstens zwei Sprüngen: zuerst hebt der Hoster auf https, dann leitet der Shop auf die kanonische Adresse. „HTTPS erzwingen“ beim Hoster bleibt eingeschaltet. Mehr als zwei Sprünge sind ein Fehler (E-231, ändert E-219 für http) |
| `worklove.shop`, `www.worklove.shop` | frühere Domain | nein | 301 auf `https://surface.love/de`, beim Hoster, nicht im Shop (Entscheidung vom 06.09.2026) |
| `cms.surface.love` | Bilder des alten Shops | nein | ohne DNS-Eintrag, keine Weiterleitung |
| `surface-service.com`, `www.surface-service.com` | Domain für „Surface as a Service“ (E-228) | nein | als Ganzes dauerhaft auf die Zielseite „Device as a Service“ im Shop, `/de/device-as-a-service` (E-234), über http und https, in einem Sprung, beim Hoster. Bis die Zielseite live ist, bleibt die Domain, wie sie ist. Ihre robots.txt sperrt den Abruf nicht, sonst folgt Google der Weiterleitung nicht |

## 2. Adressen, Deutsch
Jede öffentliche Adresse trägt die Sprache als erstes Segment. Aktiv ist nur `de`.

| Pfad | Seitentyp | Index | Kanonik | Sitemap | Slug aus |
|---|---|---|---|---|---|
| `/de` | Startseite | ja | selbst | ja | |
| `/de/geraete` | Geräteübersicht, Reiter mit `?reihe=` | ja | selbst, ohne Parameter | ja | |
| `/de/geraete/{reihe}`, also `/de/geraete/surface-pro` und `/de/geraete/surface-laptop` | Reihenseite, geplant (E-217) | ja | selbst | ja | `key` in `reihen` von `modelle.json`, Texte aus `content/de/reihen/{reihe}.json` |
| `/de/geraete/{modell}` | Modellseite | ja | selbst | ja | `key` in `modelle.json` |
| `/de/geraete/{modell}/konfigurieren` | Zusammenstellung | nein, follow | keine | nein | wie Modellseite |
| `/de/geraete/vergleich` mit `?m=` | Vergleich | nein, follow | keine | nein | |
| `/de/ausstattung` | Ausstattung, nur mit Parametern. Ohne Parameter 308 auf `/de/geraete`, Abschnitt 8 | nein, follow | keine | nein | |
| `/de/anfrage` mit `?pos=` | Warenkorb (E-179) | nein, nofollow | keine | nein | |
| `/de/anfrage/kontakt`, `/de/anfrage/pruefen`, `/de/anfrage/danke` | Anfrage-Schritte und Danke-Seite (S17) | nein, nofollow | keine | nein | |
| `/de/stories` | Surface Stories, Übersicht | ja | selbst | ja | |
| `/de/stories/kategorie/{slug}` | Kategorie | ja | selbst | ja | Sanity |
| `/de/stories/{slug}` | Beitrag | ja | selbst | ab E-167, Punkt 5 | Sanity |
| `/de/impressum`, `/de/datenschutz`, `/de/agb`, `/de/widerruf` | Rechtstexte | ja | selbst | ja | |
| `/de/device-as-a-service` | Zielseite „Device as a Service“, geplant (E-228, E-234) | ja | selbst | ja | |
| `/de/lizenzen/{slug}`, `/de/leistungen/{slug}` | Produktseiten der Bausteine, Abschnitt 3 | ja | selbst | ja | `slug` in `seiten` von `bausteine.json` |
| `/de/lizenzen`, `/de/leistungen` | noch keine Seite (Stufe 2) | 404 | keine | nein | |
| `/de/bausteine` | Bausteintafel, nur intern | nein, nofollow | keine | nein | |
| `/de/api/…` | Schnittstellen | nein | keine | nein | |
| jeder andere Pfad unter `/de/` | Fehlerseite | 404 | keine | nein | |

Pfade ohne Sprache leiten auf `/de` weiter, siehe Abschnitt 8. `/en/…` ist vorbereitet und leitet bis zur Freigabe des Markts auf die deutsche Fassung.

**Reihe und Modell teilen sich das Segment `/de/geraete/`.** Ein Reihenschlüssel ist nie zugleich ein Modellschlüssel. Ein neuer Modellschlüssel in `modelle.json` darf keinem Reihenschlüssel gleichen, und umgekehrt (MODELLE.md, Abschnitt Reihen). Surface Laptop Ultra gehört zur Reihe `surface-laptop`, die 12- und 13-Zoll-Modelle gehören zu `surface-pro` und `surface-laptop`.

**Zielseite „Device as a Service“ (E-228, E-234).** Sie liegt unter `/de/device-as-a-service`. Die Adresse ist endgültig und wird nach der Veröffentlichung nicht umbenannt. Eine indexierte Seite mit Kanonik auf sich selbst und Eintrag in der Sitemap. Sie nennt „Surface as a Service“ deutlich, im Titel oder in der H1 und im Text, und wirbt mit Monatsraten, nie mit Kaufpreisen. Bis die Seite live ist, leitet `surface-service.com` nicht weiter. Offen sind der Wortlaut (Auftrag an CC-Marketing beim Bau) und das Aussehen (nach E-233 mit dem Gesamtentwurf v2), nicht die Adresse.

**Brotkrumen:** Start › Geräte › Reihe › Modell. Die Reihenseite endet bei der Reihe, die Modellseite führt über ihre Reihenseite. Bis die Reihenseiten live sind, entfällt die Stufe Reihe, nach Regel 4.5 verlinkt keine Brotkrume eine Adresse, die es noch nicht gibt oder die weiterleitet.

## 3. Produktseiten der Bausteine (W6, 8100)
Entschieden von Sascha am 25.11.2026. Es gibt zwei Segmente, die Slugs tragen den vollen Produktnamen, und es gibt noch keine Übersichtsseiten.

| Seite (`seite` in `seiten`) | Pfad | Index | Kanonik | Sitemap |
|---|---|---|---|---|
| `m365-standard` | `/de/lizenzen/microsoft-365-business-standard` | ja | selbst | ja |
| `m365-premium` | `/de/lizenzen/microsoft-365-business-premium` | ja | selbst | ja |
| `copilot` | `/de/lizenzen/microsoft-365-copilot-business` | ja | selbst | ja |
| `managed` | `/de/leistungen/managed-workplace` | ja | selbst | ja |
| `garantie` | `/de/leistungen/erweiterte-garantie` | ja | selbst | ja |

- **Lizenzen und Leistungen:** `/de/lizenzen` trägt die drei Microsoft-Lizenzen. `/de/leistungen` trägt unsere eigenen Leistungen, also Managed Workplace und die erweiterte Garantie.
- **Slug:** Er steht im Feld `slug` im Block `seiten` von `bausteine.json` (BAUSTEINE.md, Abschnitt „Produktseiten“) und muss genau dem Pfad oben entsprechen. Mit dieser Fassung ist der Slug keine Vorlage mehr. Sobald die Seite auf `surface.love` steht, gilt Regel 4.1.
- **Übersichten:** `/de/lizenzen` und `/de/leistungen` haben in Stufe 1 keine eigene Seite. Sie antworten mit 404 und werden nicht verlinkt. Die Brotkrumen einer Produktseite führen von der Startseite direkt zur Seite. Die Übersichten kommen mit Stufe 2 (Zubehör) und werden vorher hier eingetragen.
- Die Vormerkung (E-186) liegt im Browser (`sl-vormerkung-v1`) und erzeugt keine eigene Adresse. Danach geht es auf `/de/geraete` weiter.

## 4. Grundregeln für Adressen
1. **Eine veröffentlichte Adresse ändert sich nie ohne 301** und einen Eintrag in der Weiterleitungsliste (Abschnitt 8). Veröffentlicht ist eine Adresse, sobald sie auf `surface.love` erreichbar ist.
2. **Slugs kommen aus den Daten.** Modellseiten aus `modelle.json`, Produktseiten aus `seiten` in `bausteine.json`, Stories aus Sanity. Jede Änderung eines Slugs dort ist eine Adressänderung und braucht Regel 4.1.
3. **Form:** Kleinbuchstaben, Ziffern und Bindestrich, höchstens 96 Zeichen, Umlaute als ae, oe, ue und ss.
4. **Parameter tragen Zustand, nie eigenen Inhalt.** Bekannt sind `reihe`, `m`, `pos` und, mit F-43, `v`. Eine Seite mit Parametern kanonisiert auf die Adresse ohne Parameter oder ist noindex.
5. **Interne Links zeigen nie auf eine Adresse, die weiterleitet.** Navigation, Kopf, Fuß und Stories verlinken das Ziel selbst.
6. **Eine neue Seite steht hier, bevor sie gebaut wird** (E-180). Der Shop-PR nennt den Abschnitt dieses Vertrags.

## 5. Kanonik und hreflang
- **Indexierte Seite:** absolute, selbstbezogene Kanonik auf `https://surface.love` plus Pfad, ohne Parameter.
- **noindex-Seite:** keine Kanonik. noindex und ein Verweis auf eine andere Adresse widersprechen sich.
- **Testdomain und unbekannter Host:** noindex, keine Kanonik auf `surface.love`.
- **Das Layout setzt keine Kanonik.** Jede Seite setzt ihre eigene, damit keine Unterseite still die Kanonik der Startseite erbt.
- **hreflang:** Solange nur Deutsch ausgeliefert wird, gibt es kein hreflang. Mit der zweiten Sprache (EP9) nennt jede indexierte Seite alle Sprachfassungen und `x-default`. `x-default` zeigt auf die deutsche Fassung, bis es eine Sprachwahl gibt. Die Pfadsegmente je Sprache legt EP9 in diesem Vertrag fest.

## 6. Sitemap
- Nur auf `surface.love`, unter `/sitemap.xml`, bei jedem Abruf neu erzeugt. Jeder andere Host liefert eine leere Sitemap.
- **Drin:** alle Adressen mit „Sitemap: ja“ aus den Abschnitten 2 und 3.
- **Nicht drin:** alle noindex-Seiten, Adressen mit Parametern, `/de/api/…`, `/de/bausteine`, Weiterleitungen und Fehlerseiten.
- **Stand 25.11.2026:** 26 Adressen. Startseite, Geräteübersicht, 15 Modellseiten, Stories-Übersicht, 4 Kategorien, 4 Rechtstexte.
- **Zuwachs:** 5 Produktseiten mit W6, die Beiträge der Stories mit E-167, Punkt 5, 2 Reihenseiten mit E-217. `lastmod` der Reihenseite kommt aus `content/de/reihen/{reihe}.json`.
- `lastmod` nennt die letzte inhaltliche Änderung der Seite, nicht den Zeitpunkt des Abrufs. `changefreq` und `priority` sind erlaubt, Suchmaschinen werten sie kaum.

## 7. robots.txt
- `surface.love`: `Allow: /`, `Disallow: /*/api/`, dazu die Zeile `Sitemap: https://surface.love/sitemap.xml`.
- Jeder andere Host: `Disallow: /`. Dazu wie in Abschnitt 1 `X-Robots-Tag` und meta noindex.

## 8. Weiterleitungsliste
Fertig gestellt am 27.11.2026 nach dem Vertragstext von CC-SEO (SEO05, 8138). Grundsätze:

- **Ein Sprung.** Jede Weiterleitung zeigt direkt auf das Endziel, absolut mit `https://surface.love`. Kein Ziel leitet selbst weiter (E-219).
- **Ausnahme http (E-231):** Eine `http://`-Adresse kommt in höchstens zwei dauerhaften Sprüngen an, zuerst Hoster auf https, dann Shop auf das Endziel. Für `https://` bleibt es bei einem Sprung.
- **Dauerhaft.** 301 oder 308. 307 gibt es nur noch vorläufig: für `/en/…` bis zur Freigabe des Markts und für Pfade ohne Sprache bis zur Sprachwahl.
- **Reihenfolge im Shop:** erst Host und Protokoll, dann die Altpfade, dann Kleinschreibung, dann die Sprache. Die Altpfade werden vor der Kleinschreibung geprüft, weil sie Großbuchstaben tragen können.
- **Altpfade** des alten Shops haben die Form `/{kultur}/{markt}/…`, etwa `/de-de/deutschland/…` oder `/en-gb/united-kingdom/…`. Die Regeln gelten für jede Kultur und jeden Markt und unter `surface.love` wie unter `www.surface.love`.
- **410** steht nur bei den benannten Altmustern in der Tabelle, mit Grund in der Zeile. Jede andere unbekannte Adresse bleibt 404.
- Eine pauschale Weiterleitung ist in der Spalte „Art“ markiert.

| Quelle | Ziel | Code | Art | Ort |
|---|---|---|---|---|
| `http://surface.love/{pfad}`, `http://www.surface.love/{pfad}` | zuerst `https://` mit demselben Host und Pfad, dann das Endziel nach den Zeilen unten | dauerhaft | Muster, höchstens zwei Sprünge (E-231) | erst Hoster („HTTPS erzwingen“ bleibt an), dann Shop, `proxy.ts` |
| `https://www.surface.love/{pfad}` | `https://surface.love/{pfad}`, Endziel nach den Zeilen unten | 308 | Muster | Shop, `proxy.ts` |
| `https://surface.love/` | `https://surface.love/de` | 308 | einzeln | Shop, `proxy.ts` |
| Pfad mit Großbuchstaben, etwa `/DE/geraete` | derselbe Pfad klein geschrieben | 308 | Muster | Shop, `proxy.ts` |
| `/{pfad}` ohne Sprache, außer den Altpfaden und der Wurzel | `/de/{pfad}` | 307 | Muster | Shop, `proxy.ts`, vorläufig bis zur Sprachwahl |
| `/en/{pfad}` | `/de/{pfad}` | 307 | Muster | Shop, `proxy.ts`, bis zur Freigabe des Markts |
| `/stories` | `/de/stories` | 308 | einzeln | Shop, `proxy.ts` |
| `worklove.shop/*`, `www.worklove.shop/*` | `https://surface.love/de` | 301 | pauschal | Hoster |
| `{at,de,dk,es,fr,uk}.surface.love/*` | `https://surface.love/de` | 301 | pauschal | Kante |
| `blog.surface.love/*`, `stories.surface.love/*` | `https://surface.love/de/stories` | 301 | pauschal | Kante |
| `surface-service.com/*`, `www.surface-service.com/*`, über http und https | `/de/device-as-a-service` (E-234) | 301 | pauschal, erst wenn die Zielseite live ist (E-228) | Hoster |
| `/de/katalog` | `/de/geraete` | 308 | einzeln | Shop, `next.config.mjs` |
| `/de/konfigurator` | `/de/geraete` | 301 | einzeln | Shop, `next.config.mjs` |
| `/de/konfigurator/{reihe-generation}` | die Reihenseite: `surface-pro…` auf `/de/geraete/surface-pro`, `surface-laptop…` auf `/de/geraete/surface-laptop`. Bis die Reihenseiten live sind, `/de/geraete` | 301 | Muster | Shop, `next.config.mjs` |
| `/de/ausstattung` ohne Parameter | `/de/geraete` | 308 | einzeln | Shop, Seite `ausstattung` |
| `/{kultur}/{markt}/` und `/{kultur}/` | `/de` | 301 | pauschal auf die Startseite | Shop, `proxy.ts` |
| Zubehör: `…/{boutique/accessoires, shop/zubehoer, store/accessories, winkel/accessoires, butik/tilbehoer, tienda/accesorios}/…`, auch Filter und Detailseiten | `/de/geraete` | 301 | pauschal, gilt nur bis zum Bau von W8. Danach zeigen die Regeln auf die Zubehörseiten (E-215) | Shop, `proxy.ts` |
| Zubehör unter der alten Produktliste: `…/{shop/produkte, store/products, shop/geraete, store/devices, boutique/appareils}/…/{name}`, wenn der Name kein Gerät ist | `/de/geraete` | 301 | pauschal, gilt nur bis zum Bau von W8. Danach zeigen die Regeln auf die Zubehörseiten (E-215) | Shop, `proxy.ts` |
| Gerät Surface Pro: Name `surface_pro{zahl}` oder `surface_pro_x` | `/de/geraete/surface-pro`, bis dahin `/de/geraete` | 301 | Muster | Shop, `proxy.ts` |
| Gerät Surface Laptop: Name `surface_laptop…` | `/de/geraete/surface-laptop`, bis dahin `/de/geraete` | 301 | Muster | Shop, `proxy.ts` |
| Gerät ohne Angebot: `surface_go…`, `surface_studio…`, `surface_book…`, `surface_duo…` | `/de/geraete` | 301 | pauschal | Shop, `proxy.ts` |
| Gerät ohne verwandtes Ziel: `surface_hub…`, `hololens…` | keins | 410 | Muster. Grund: Konferenz- und Mixed-Reality-Geräte, kein Angebot | Shop, `proxy.ts` |
| Geräteliste ohne Detail, auch mit Filtern, und `…/bundle` | `/de/geraete` | 301 | pauschal | Shop, `proxy.ts` |
| Lizenz mit Detail: `…/{boutique/licences, shop/lizenzen, store/licences, tienda/licencias}/details/{id}/{name}` | nach Liste L unten | 301 | einzeln | Shop, `proxy.ts` |
| Lizenz von Adobe, Visio oder Power BI | keins | 410 | Muster. Grund: nicht im Angebot, in keinem Business-Paket enthalten | Shop, `proxy.ts` |
| Lizenzliste ohne Detail, auch Kategorien | `/de/lizenzen/microsoft-365-business-standard`, mit Stufe 2 auf `/de/lizenzen` | 301 | pauschal | Shop, `proxy.ts` |
| Leistungen: `…/{boutique/services, shop/dienstleistungen, store/services}`, `…/modern-workplace-definition` | `/de/leistungen/managed-workplace` | 301 | pauschal | Shop, `proxy.ts` |
| Service für Geräte: Name `surface_business_support` oder `hardware_service…` | `/de/leistungen/erweiterte-garantie` | 301 | einzeln | Shop, `proxy.ts` |
| `…/{impressum, imprint}` | `/de/impressum` | 301 | einzeln | Shop, `proxy.ts` |
| `…/{datenschutz, privacy-policy, dataprotectionadvice}` | `/de/datenschutz` | 301 | einzeln | Shop, `proxy.ts` |
| `…/{agb, conditions}` | `/de/agb` | 301 | einzeln | Shop, `proxy.ts` |
| `…/{conocimiento, knowledge}/notebook-leasing-fuer-unternehmen` | `/de/geraete` | 301 | einzeln | Shop, `proxy.ts` |
| Inhaltsseiten ohne Gegenstück: `…/{ueber-uns, about-us, vorteile, advantages, voordelen, faq, kontakt, contact, bestell-ablauf, order-process, market-info, markt-info, market-and-culture, sprache-waehlen}` | `/de` | 301 | pauschal auf die Startseite | Shop, `proxy.ts` |
| `…/{bildung, education}` | keins | 410 | Muster. Grund: kein Angebot für Bildung | Shop, `proxy.ts` |
| `…/{karriere, careers}` und Stellenanzeigen | keins | 410 | Muster. Grund: keine Stellenseite | Shop, `proxy.ts` |
| jeder übrige Pfad unter `/{kultur}/…` | keins | 404 | Auffangregel. Kein 410: 410 gilt nur für die benannten Altmuster oben, jede andere unbekannte Adresse bleibt 404 | Shop, Fehlerseite |

**Liste L, Lizenzen des alten Shops nach Name im Pfad**

| Name im Altpfad | Ziel |
|---|---|
| `m365_business_premium`, `microsoft_365_e3`, `microsoft_365_e5`, `office_365_e3`, `office_365_e5`, `m365_apps_enterprise`, `enterprise_mobility_security_e5`, `microsoft_intune`, `azure_active_directory_premium_1`, `azure_active_directory_premium_2`, `microsoft_cloud_app_security`, `exchange_online_protection` | `/de/lizenzen/microsoft-365-business-premium` |
| `m365_business_standard`, `m365_business_basic`, `ms365_apps_business`, `office_365_e1`, `office_365_f3`, `exchange_online_plan1`, `exchange_online_plan2`, `sharepoint_online_plan_1`, `sharepoint_online_plan_2`, `onedrive_for_business_plan_1`, `onedrive_for_business_plan_2` | `/de/lizenzen/microsoft-365-business-standard` |
| alle Namen mit `adobe_`, `acrobat_`, `creative_cloud`, dazu `visio_online_plan_1`, `visio_online_plan_2`, `power_bi_pro` | 410 |

Die Liste ist damit fertig. Die Zeilen der Fassung 1 mit „seit“ stehen in der Git-History, die offene Zeile zu l16b (7203) entfällt.

## 9. Titel und Beschreibung
- **Muster:** Der Shop setzt den Titel als `{Seitentitel}, Surface.Love`. Der Seitentitel in den Daten enthält die Marke nie selbst.
- **Länge:** Seitentitel höchstens 45 Zeichen, mit Zusatz höchstens 60. Beschreibung 120 bis 155 Zeichen.
- **Jede indexierte Seite hat eine eigene Beschreibung.** Keine Seite erbt die Beschreibung der Startseite.
- **Texte** schreibt CC-Marketing. Microsoft-Namen nach IMAGES.md, Punkt 2. Keine Preise von Microsoft, Raten nur aus unseren Daten (E-099).
- **Keine Rate in Titel oder Beschreibung.** Sie ändert sich mit `products.json`, ein Suchergebnis mit einer alten Zahl wäre falsch.

| Seitentyp | Titel aus | Beschreibung aus |
|---|---|---|
| Startseite | `content/de/common.json`, `meta.defaultTitle` | `meta.description` |
| Geräteübersicht | `content/de/devices.json`, `modelle.uebersicht.title` | eigener Schlüssel in `devices.json` |
| Reihenseite | `meta.titel` in `content/de/reihen/{reihe}.json` | `meta.beschreibung` dort |
| Modellseite | `meta.titel` in `content/de/modelle/{key}.json`, fehlt er, `title` aus `modelle.json` | `meta.beschreibung` dort, fehlt sie, die Einleitung ohne Fußnoten, gekürzt auf 155 Zeichen am Wortende |
| Produktseite | `meta.titel` in `content/de/bausteine/{seite}.json` | `meta.beschreibung` dort |
| Stories, Kategorie, Beitrag | Sanity, Felder der Seite | Sanity |
| Rechtstexte, Impressum | Titel des Texts | eigener Schlüssel in `content/de/recht.json` |
| noindex-Seiten | Schlüssel der Seite | keine Pflicht |

**Strukturierte Daten, Product-Block der Modellseiten (E-230):**
- `lowPrice` im `AggregateOffer` ist die sichtbare Rate der Seite, „ab … netto im Monat“ aus `rateFrom.net` des Shops. Nie ein anderes Minimum, nie von Hand gesetzt (E-029, E-030, E-099). Dazu eine `UnitPriceSpecification` mit Monat und Laufzeit.
- **Der Block ist abschaltbar.** Meldet Google einen Verstoß oder eine manuelle Maßnahme, geht er sofort auf Weg B ohne Preis zurück, ohne neue Entscheidung.
- Lizenzen bleiben ohne Preis. Managed Workplace trägt die eigene Rate aus `bausteine.json`.
- Titel und Beschreibung der Modellseite sagen unmissverständlich, dass es um Leasing zur Monatsrate geht. Die Rate selbst steht dort nicht (siehe oben).
- Die Reihenseiten tragen keinen Product-Block, E-230 gilt nur für die Modellseiten (bestätigt von SL SEO an 8152). Sie tragen CollectionPage, ItemList und BreadcrumbList wie im Vertragstext SEO05, dazu VideoObject (IMAGES.md, Nachtrag Reihenseiten, Punkt 5).

## 10. Search Console
- **Property:** `surface.love` als Domain-Property. Zugang hat Sascha.
- **Sitemap:** `https://surface.love/sitemap.xml` wird in der Property eingereicht. Das liegt seit dem 24.11.2026 offen bei Sascha.
- **Prüfung:** in den ersten vier Wochen nach dem Livegang wöchentlich, danach monatlich und nach jedem Release mit neuen Adressen. Geprüft werden die Berichte „Seiten“ und „Sitemaps“ sowie die Liste der 404-Fehler.
- **Befunde** gehen als Kommentar an F-18 SEO-Grundlage (7168). Der Master leitet daraus Aufträge ab.
- **Suchbegriffe** je Seitentyp liefert CC-Marketing nach. Sie kommen in diesen Abschnitt.

## 11. Abweichungen am 25.11.2026
Abgleich gegen Shop-`main` `0786e2e` und die Live-Seiten. Behoben werden sie mit einem eigenen Auftrag an CC-Shop, die Texte zu Punkt 4 und 6 liefert CC-Marketing.

1. **Kanonik geerbt:** Das Layout setzt für jede Seite `canonical: /de`. Impressum, Datenschutz, AGB und Widerruf sind indexiert und stehen in der Sitemap, zeigen aber mit ihrer Kanonik auf die Startseite. Die Ausstattung erbt sie ebenso.
2. **noindex mit Kanonik:** Die Zusammenstellung verweist auf die Modellseite, der Vergleich auf sich selbst.
3. **Links auf eine Weiterleitung:** Kopf, Hauptnavigation, Fuß und die Linkziele der Stories zeigen auf `/de/konfigurator`. Diese Adresse leitet mit 301 auf `/de/geraete` weiter.
4. **Beschreibung geerbt:** Geräteübersicht, Impressum und Rechtstexte tragen die Beschreibung der Startseite.
5. **robots.txt** sperrt `/de/api/` nicht. `lastmod` in der Sitemap ist der Zeitpunkt des Abrufs.
6. **Marke doppelt im Titel:** `meta.titel` von `managed` und `garantie` enthält „| Surface.Love“, der Shop hängt „, Surface.Love“ noch einmal an.

## 12. Pflege
- Änderungen nur per Hub-PR mit Eintrag im CHANGELOG.
- Neue Seiten, Slugs und Weiterleitungen kommen vor dem Bau hierher (Regel 4.6).
- Der Master gleicht den Vertrag nach jedem Release mit neuen Adressen gegen die Live-Sitemap ab.
