# Routen und SEO (surface.love)

Fassung 1, Stand 25.11.2026, W3 (8097). Grundlage: E-174, E-176, E-180, E-186, S14 (C9), S16 (Livegang), S17 (Warenkorb).
Abgeglichen gegen Shop-`main` `0786e2e`, den Zweig `s17-warenkorb` und `https://surface.love/sitemap.xml` (26 Adressen) am 25.11.2026.

## 0. Geltung
- Dieser Vertrag ist die Pflichtquelle für die Punkte 1 (Adressen) und 2 (SEO) der Auswirkungsprüfung nach E-180. Jeder Shop-PR, der eine Route, eine Weiterleitung, eine Kanonik oder die Sitemap berührt, prüft gegen ihn.
- Er gilt für den Storefront `surface` auf `surface.love`. lenovo.online bekommt einen eigenen Abschnitt, wenn es live geht.
- Die Werte stehen im Shop-Code: `lib/routen.ts`, `lib/stories/paths.ts`, `next.config.mjs`, `proxy.ts`, `lib/seo/`, `config/storefronts/surface.ts`. Weicht der Code von diesem Vertrag ab, ist das ein Fehler im Code oder es braucht zuerst eine Vertragsänderung per Hub-PR.

## 1. Hosts
| Host | Rolle | Index | Verhalten |
|---|---|---|---|
| `surface.love` | kanonische Domain | ja | einzige Domain mit Kanonik, Sitemap und offener robots.txt |
| `www.surface.love` | Alias | nein | 308 auf `https://surface.love` mit Pfad und Abfrage, im Shop (`proxy.ts`). E-176 sieht 301 vor, 308 ist gleichwertig und nötig, weil das Zertifikat für Stamm und www ohne Proxy an der Kante ausgestellt wird |
| `beta.surface.love` und weitere Testdomains aus `config/storefronts/surface.ts` | Vorstufe | nein | `X-Robots-Tag: noindex, nofollow`, meta noindex, robots.txt `Disallow: /`, leere Sitemap |
| jede unbekannte Adresse, etwa eine Vorschau des Hosters | keine | nein | wie Testdomain |
| Länder `at`, `de`, `dk`, `es`, `fr`, `uk` unter surface.love | Altadressen | nein | 301 auf `https://surface.love/de`, an der Kante (E-176) |
| `blog` und `stories` unter surface.love | Altadressen | nein | 301 auf `https://surface.love/de/stories` ohne Pfad, an der Kante (E-176) |

## 2. Adressen, Deutsch
Jede öffentliche Adresse trägt die Sprache als erstes Segment. Aktiv ist nur `de`.

| Pfad | Seitentyp | Index | Kanonik | Sitemap | Slug aus |
|---|---|---|---|---|---|
| `/de` | Startseite | ja | selbst | ja | |
| `/de/geraete` | Geräteübersicht, Reiter mit `?reihe=` | ja | selbst, ohne Parameter | ja | |
| `/de/geraete/{modell}` | Modellseite | ja | selbst | ja | `key` in `modelle.json` |
| `/de/geraete/{modell}/konfigurieren` | Zusammenstellung | nein, follow | keine | nein | wie Modellseite |
| `/de/geraete/vergleich` mit `?m=` | Vergleich | nein, follow | keine | nein | |
| `/de/ausstattung` | Ausstattung | nein, follow | keine | nein | |
| `/de/anfrage` mit `?pos=` | Warenkorb (E-179) | nein, nofollow | keine | nein | |
| `/de/anfrage/kontakt`, `/de/anfrage/pruefen`, `/de/anfrage/danke` | Anfrage-Schritte und Danke-Seite (S17) | nein, nofollow | keine | nein | |
| `/de/stories` | Surface Stories, Übersicht | ja | selbst | ja | |
| `/de/stories/kategorie/{slug}` | Kategorie | ja | selbst | ja | Sanity |
| `/de/stories/{slug}` | Beitrag | ja | selbst | ab E-167, Punkt 5 | Sanity |
| `/de/impressum`, `/de/datenschutz`, `/de/agb`, `/de/widerruf` | Rechtstexte | ja | selbst | ja | |
| `/de/lizenzen/{slug}`, `/de/leistungen/{slug}` | Produktseiten der Bausteine, Abschnitt 3 | ja | selbst | ja | `slug` in `seiten` von `bausteine.json` |
| `/de/lizenzen`, `/de/leistungen` | noch keine Seite (Stufe 2) | 404 | keine | nein | |
| `/de/bausteine` | Bausteintafel, nur intern | nein, nofollow | keine | nein | |
| `/de/api/…` | Schnittstellen | nein | keine | nein | |
| jeder andere Pfad unter `/de/` | Fehlerseite | 404 | keine | nein | |

Pfade ohne Sprache leiten auf `/de` weiter, siehe Abschnitt 8. `/en/…` ist vorbereitet und leitet bis zur Freigabe des Markts auf die deutsche Fassung.

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
- **Zuwachs:** 5 Produktseiten mit W6, die Beiträge der Stories mit E-167, Punkt 5.
- `lastmod` nennt die letzte inhaltliche Änderung der Seite, nicht den Zeitpunkt des Abrufs. `changefreq` und `priority` sind erlaubt, Suchmaschinen werten sie kaum.

## 7. robots.txt
- `surface.love`: `Allow: /`, `Disallow: /*/api/`, dazu die Zeile `Sitemap: https://surface.love/sitemap.xml`.
- Jeder andere Host: `Disallow: /`. Dazu wie in Abschnitt 1 `X-Robots-Tag` und meta noindex.

## 8. Weiterleitungsliste
| Quelle | Ziel | Code | Ort | seit |
|---|---|---|---|---|
| `www.surface.love/{pfad}` | `https://surface.love/{pfad}` | 308 | Shop, `proxy.ts` | 24.11.2026, E-176 |
| `{at,de,dk,es,fr,uk}.surface.love/*` | `https://surface.love/de` | 301 | Kante | 24.11.2026, E-176 |
| `blog.surface.love/*`, `stories.surface.love/*` | `https://surface.love/de/stories` | 301 | Kante | 24.11.2026, E-176 |
| `/stories` | `/de/stories` | 308 | Shop, `proxy.ts` | AB#8033 |
| `/{pfad}` ohne Sprache | `/de/{pfad}` | 307 | Shop, `proxy.ts` | vorläufig bis zur Sprachwahl |
| `/en/{pfad}` | `/de/{pfad}` | 307 | Shop, `proxy.ts` | bis zur Freigabe des Markts |
| `/de/katalog` | `/de/geraete` | 308 | Shop, `next.config.mjs` | S09 |
| `/de/konfigurator`, `/de/konfigurator/{reihe-generation}` | `/de/geraete` | 301 | Shop, `next.config.mjs` | S14 (C9) |
| Pfade des alten Shops unter `www.surface.love` | offen | 301 | offen | l16b (7203) |

- Die Tabelle für den alten Shop entsteht aus dem Export der Search Console (l16a, 7202) und der Inventur `docs/inventur-alt-shop-2026-09-06.md`. Sie gilt nur für Adressen mit echten Aufrufen. Eine pauschale Weiterleitung auf die Startseite wird je Zeile markiert.
- Die Rechtstexte des alten Shops bekommen je eine 1:1-Weiterleitung auf die neue Rechtsseite (l17d, 7210).

## 9. Titel und Beschreibung
- **Muster:** Der Shop setzt den Titel als `{Seitentitel}, Surface.Love`. Der Seitentitel in den Daten enthält die Marke nie selbst.
- **Länge:** Seitentitel höchstens 45 Zeichen, mit Zusatz höchstens 60. Beschreibung 120 bis 155 Zeichen.
- **Jede indexierte Seite hat eine eigene Beschreibung.** Keine Seite erbt die Beschreibung der Startseite.
- **Texte** schreibt CC-Marketing. Microsoft-Namen nach IMAGES.md, Punkt 2. Keine Preise von Microsoft, Raten nur aus unseren Daten (E-099).

| Seitentyp | Titel aus | Beschreibung aus |
|---|---|---|
| Startseite | `content/de/common.json`, `meta.defaultTitle` | `meta.description` |
| Geräteübersicht | `content/de/devices.json`, `modelle.uebersicht.title` | eigener Schlüssel in `devices.json` |
| Modellseite | `title` aus `modelle.json` | Einleitung aus `content/de/modelle/{key}.json`, ohne Fußnoten |
| Produktseite | `meta.titel` in `content/de/bausteine/{seite}.json` | `meta.beschreibung` dort |
| Stories, Kategorie, Beitrag | Sanity, Felder der Seite | Sanity |
| Rechtstexte, Impressum | Titel des Texts | eigener Schlüssel in `content/de/recht.json` |
| noindex-Seiten | Schlüssel der Seite | keine Pflicht |

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
