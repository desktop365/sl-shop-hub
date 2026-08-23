# Nachtlauf 24.08.2026, Gesamtkarte und Morgenplan

Bestandsaufnahme des Katalog-Blocks über alle vier Repos, überwiegend rein lesend.
Nichts deployt, nichts in den Objektspeicher geschrieben, kein Distributor-Abruf,
im Shop-Repo keine einzige Änderung.

Ausführliche Einzelberichte:
`surface-love-pricing/docs/nachtlauf-2026-08-24-bericht.md` und
`sl-bilder/docs/nachtlauf-2026-08-24-bericht.md`.

## Die drei wichtigsten Erkenntnisse

1. **Die Rechenlogik ist gesund, der Schreibweg existiert nicht.** 358 Artikel
   sauber erzeugt, 2506 Raten nachgerechnet, null Abweichungen. Aber `storage.py`
   und `plausibility.py` in der Preis-Pipeline sind reine Gerüste, die bei jedem
   Aufruf abbrechen. Der Timer-Lauf käme nicht einmal bis dorthin, weil er eine
   Funktion aufruft, die es im Modul gar nicht gibt.
2. **Die Preis-Pipeline zielt im Code noch auf Azure Blob Storage, nicht auf GCS.**
   Das widerspricht contracts/INFRA.md. Die Bild-Seite ist dagegen korrekt auf den
   Bucket konfiguriert. Bevor jemand den Schreibweg baut, muss diese Frage entschieden
   sein, sonst wird zweimal gebaut.
3. **Es gibt keine Bild-Pipeline.** `sl-bilder` besteht aus drei leeren Ordnern.
   Kein Code, keine Quellbilder, kein Repo, weder lokal noch auf GitHub. Was in
   ARBEITSWEISE.md als Pipeline beschrieben ist, muss von null gebaut werden.

## 1. Die Kette, Glied für Glied

| # | Glied | Zustand | Beleg |
|---|---|---|---|
| 1 | Distributor zu Preis-Pipeline | **ungeprüft** | Keine Zugangsdaten lokal. `local.settings.json` trägt nur Runtime und Storage, keine der drei erwarteten Distributor-Variablen. Kein Abruf gemacht. |
| 2 | Rechenlogik | **fertig** | Trockenlauf mit lokaler CSV, 1031 Artikel gelesen, 358 Surface-Artikel erzeugt, 0 übersprungen. 2506 Raten nachgerechnet, null Abweichungen. 37 neue Unit-Tests grün. |
| 3 | products.json gegen den Datenvertrag | **fast**, zwei Abweichungen | Alle Pflichtfelder da, Laufzeiten korrekt, brutto stimmt bei jeder Rate, rate_from ist überall das echte Minimum. Zwei Befunde, siehe Abschnitt 2. |
| 4 | Preis-Pipeline zu Bucket | **fehlt ganz** | `storage.py` hat drei Funktionen, alle werfen `NotImplementedError`. Kein GCS-Import, kein Bucket-Name, kein Paket in `requirements.txt`. Der Timer ruft zusätzlich `storage.lade_oeffentlich()` auf, das es im Modul nicht gibt. |
| 5 | Bild-Pipeline zu Bucket | **fehlt ganz** | `sl-bilder` hat 0 Dateien in `source`, `build` und `scripts`. Kein Git-Repo, und unter `desktop365` existiert kein Repo `sl-bilder`. |
| 6 | Fallback-Bilder | **jetzt vorbereitet** | Vier Hauptbilder und vier Vorschaubilder erzeugt, WebP, 1200 x 1200 und 400 x 400, sRGB, ohne Metadaten, alle weit unter den Richtgrößen. Liegen lokal in `sl-bilder/build`, nicht hochgeladen. |
| 7 | Bucket | **leer, bestätigt** | Öffentliches Listing des Buckets liefert `KeyCount 0`. `products.json`, `images.json` und `images/_fallback.webp` antworten jeweils mit HTTP 404. |
| 8 | Bucket zu Datenbank, der Sync | **gebaut, läuft auf dem Server nicht** | `db/sync.ts` ist vollständig und sauber. Er wird über `tsx` gestartet, und `tsx` steht nur in `devDependencies`. |
| 9 | Datenbank | **steht und ist erreichbar** | Live-Abruf von `/de/api/health`: `datenbank: konfiguriert`, und die Antwort kommt aus dem Zweig, der die Datenbank erfolgreich gelesen hat. |
| 10 | Datenbank zu Shop | **fertig** | Repository, Hersteller-Filter, Bild-Resolver und Katalogseite stehen. Der Shop zeigt ehrlich null Geräte. |
| 11 | Shop live | **fertig** | `https://worklove.shop/de/api/health` antwortet mit `status: bereit`, Storefront surface über den Hostnamen erkannt, Markt DE, Lane neu. |

**Der einzige harte Blocker ist Glied 4 und 5, der Schreibweg in den Bucket.**
Alles davor rechnet, alles danach wartet nur auf Daten.

### Der Live-Zustand, wörtlich

```
katalog.quelle           bucket
katalog.imKatalog        0
hinweise[0]              products.json liegt nicht unter dem Objektspeicher
hinweise[1]              Rueckfall auf Beispieldaten ist hier nicht erlaubt
hinweise[2]              Das Leseabbild ist leer, bitte npm run sync:catalog
```

Das ist genau das erwartete Verhalten. `CATALOG_ALLOW_SEED` steht auf false und
greift korrekt, es werden keine Beispieldaten als echter Katalog ausgeliefert.

## 2. Zwei Befunde am Datenvertrag

**Befund A, ein Faktorwert steht im öffentlichen meta-Block.** Die Funktion, die
den meta-Block baut, wird für die öffentliche und die interne Datei gleichermaßen
benutzt. Dadurch trägt die öffentliche `products.json` ein Feld `markup_factor`.
Der Datenvertrag verbietet Faktorwerte in der öffentlichen Datei ausdrücklich.
Praktisch schwerwiegend, weil sich damit aus jeder veröffentlichten Rate
rückwärts rechnen lässt. Die Produkteinträge selbst sind sauber, geprüft über alle
vorkommenden Schlüssel. Die Leckage sitzt allein im meta-Block und ist eine
Zeile Code.

**Befund B, `availability` ist bei allen 358 Einträgen vertragswidrig.** Der
Vertrag sagt, bei unbekanntem Status wird das Feld weggelassen. Die Pipeline
schreibt stattdessen `status: unknown`. Ursache: die vorliegende CSV vom 05.07.
hat gar keine Spalten für Verfügbarkeit und Bestand, obwohl der Client sie
erwartet. Ob der Feed sie heute liefert, ist ohne Zugangsdaten nicht zu klären.

## 3. Shop-Sync, die Erkenntnisse in Kurzform

- **Auslösung: nur Skript, keine API-Route.** `npm run sync:catalog`, dahinter
  `tsx db/sync.ts`. Es gibt einen Trockenlauf mit `--dry-run`. Unter `app/[locale]/api`
  liegt einzig die Route `health`, es gibt keine Sync-Route und auch noch keine
  Anfrage-Route.
- **`tsx` steht nur in `devDependencies`.** Genau der Punkt aus STATUS.md. Der
  Hostinger-Build nutzt den Produktionsbaum, damit fehlt `tsx` auf dem Server und
  der Sync ist dort nicht startbar. Eine Zeile in `package.json`.
- **Umgebungsvariablen des Syncs:** `DATABASE_URL` und `GCS_BASE_URL`. Dazu
  `CATALOG_ALLOW_SEED` für den Rückfall auf Beispieldaten. Alle drei sind laut
  STATUS.md in Hostinger gesetzt, und der Live-Abruf bestätigt, dass Datenbank
  und Basis-URL wirken. **Es fehlt keine Variable.**
- **Was fehlt, damit der Sync läuft und der Katalog größer null wird:** erstens
  Daten im Bucket, zweitens `tsx` im Produktionsbaum. Sonst nichts. Der Sync-Code
  selbst ist vollständig, er schreibt Produkte, Raten, Bildmodelle und
  MSKU-Zuordnungen, ersetzt die Raten je Produkt vollständig und schreibt nichts
  in die Quelle zurück.

### Der Familien-Fallback, die Ableitungsregel

`products.json` trägt kein Familienfeld, das ist richtig so, die Bildlogik gehört
nicht in die Preis-Pipeline. Der Shop leitet die Familie deshalb aus dem
Produktnamen ab, mit drei Textvergleichen in dieser Reihenfolge: enthält der Name
`laptop`, dann `surface-laptop`. Enthält er `surface pro` oder `pro `, dann
`surface-pro`. Enthält er `mouse`, `dock` oder `pen`, dann `zubehoer`. Sonst kein
Treffer, und es greift das generische Ersatzbild.

**Die Regel ist dokumentiert, aber messbar ungenau.** Gegen die 358 real erzeugten
Produkte gerechnet:

| Ergebnis | Artikel | Anteil |
|---|---|---|
| surface-laptop | 217 | 60,6 % |
| surface-pro | 98 | 27,4 % |
| kein Treffer, generisches Bild | 31 | 8,7 % |
| zubehoer | 12 | 3,4 % |

**28 von 358 landen beim falschen oder unnötig generischen Ersatzbild.** Neunzehn
Zubehörartikel werden als `surface-pro` eingestuft, darunter sämtliche Type Cover
und ein VGA-Adapter, der nur deshalb trifft, weil in seinem Namen die Zeichenfolge
`pro ` vorkommt. Neun weitere Zubehörartikel, unter anderem Surface Dial, zwei
Netzteile und ein Travel Hub, fallen ganz durch und bekommen das generische Bild,
obwohl es ein Zubehör-Ersatzbild gibt. Das ist kein Blocker, aber es sieht im
Katalog sofort schlecht aus, solange `images.json` leer ist, und genau dieser
Zustand steht bevor.

### Thumbs bei Fallbacks, die Frage ist beantwortet

**Der Resolver erwartet für Fallbacks keine eigenen Vorschaudateien.** Im
Fallback-Zweig setzt er Hauptbild und Vorschau auf dieselbe URL. Eigene
`_thumb`-Dateien für die vier Ersatzbilder werden also nicht gebraucht. Sie
wurden vorsorglich miterzeugt, sollten aber nicht in den Bucket, damit dort
nichts Totes liegt. Für echte Bildmodelle gilt das nicht, dort wird `thumb`
ausgewertet und fällt nur ersatzweise auf das Hauptbild zurück.

### Die vorgemerkte Meldung, Zustand dokumentiert, nicht geändert

Der Katalogzugriff hat zwei getrennte Rückfallpfade. Ist die Datenbank erreichbar
und das Leseabbild nur leer, lautet der Hinweis „Das Leseabbild ist leer, bitte
npm run sync:catalog ausführen". Diese Meldung ist korrekt, und **genau sie steht
derzeit live**. Der zweite Pfad fängt jeden Fehler beim Lesen ab und meldet „Die
Datenbank war nicht erreichbar", obwohl dort auch ein Schemafehler oder eine
fehlerhafte Abfrage landet. Die Meldung ist also nicht falsch, sondern zu
allgemein, und sie feuert aktuell nicht.

Zwei Dinge fallen zusätzlich auf, beide unverändert gelassen: der Text hängt die
rohe Fehlermeldung an, und diese Hinweise gehen unverändert in die Antwort des
öffentlichen Zustandsendpunkts. Eine Datenbankfehlermeldung enthält je nach
Treiber Host, Benutzer und Datenbanknamen. Das gehört geprüft, bevor die Domain
umgeschaltet wird.

## 4. Morgenplan, bis zum ersten echten Gerät im Shop

In dieser Reihenfolge.

| # | Schritt | Label |
|---|---|---|
| 1 | Befund A abstellen, den Faktor aus dem öffentlichen meta-Block nehmen. Eine Zeile. Der bereits vorhandene Test springt dann von xfail auf grün. | **jetzt baubar** |
| 2 | Entscheiden, ob der Schreibweg nach GCS geht oder nach Azure Blob. Ohne diese Antwort ist Schritt 4 nicht sinnvoll zu bauen. | **braucht Entscheidung** |
| 3 | `tsx` in `package.json` von `devDependencies` nach `dependencies` verschieben. Eine Zeile, danach ist der Sync auf dem Server startbar. | **jetzt baubar** |
| 4 | Schreibmodul der Preis-Pipeline bauen, isoliert in einer eigenen Datei, plus die fehlende Plausibilitätsprüfung und die im Timer aufgerufene, aber nicht vorhandene Lesefunktion. Test mit gemocktem Client, kein echter Upload. | **jetzt baubar**, sobald 2 entschieden ist |
| 5 | Distributor-Zugang prüfen, Zugangsdaten in die Umgebung der Pipeline legen, ein einziger Abruf. Dabei klären, ob der Feed Verfügbarkeit und Bestand liefert, und danach Befund B abstellen. | **braucht Zugangsdaten** |
| 6 | Repo für `sl-bilder` anlegen, Sichtbarkeit entscheiden, `.gitignore` für `.env` und `.venv` anlegen, das vorbereitete Fallback-Set committen. | **braucht Entscheidung** |
| 7 | Die vier Fallback-Bilder in den Bucket laden, ohne die Vorschauvarianten, plus die minimale `images.json` v2. Danach zeigt der Shop für jedes Gerät ein sauberes Ersatzbild. | **jetzt baubar** |
| 8 | Ersten echten Lauf der Preis-Pipeline in den Bucket, Ergebnis gegen den Datenvertrag prüfen. | **braucht Zugangsdaten** |
| 9 | `npm run sync:catalog` auf dem Server, danach `/de/api/health` prüfen, Katalog muss größer null sein. | **jetzt baubar**, sobald 7 und 8 stehen |
| 10 | Ableitungsregel für den Familien-Fallback nachschärfen, Zubehör zuerst prüfen, erst danach `surface pro`, und die Zeichenfolge `pro ` nicht mehr allein zählen lassen. | **jetzt baubar** |

Schritte 1, 3 und 10 sind zusammen unter einer Stunde Arbeit und machen den
Unterschied zwischen einem Katalog, der peinlich aussieht, und einem, der trägt.

## 5. Offene Entscheidungen, als Ja-Nein-Fragen

1. Schreibt die Preis-Pipeline künftig in den GCS-Bucket slshopv2-media, so wie es
   contracts/INFRA.md festlegt, und wird der Azure-Blob-Weg aus Code und README
   gestrichen? **Ja oder nein.**
2. Soll `sl-bilder` als privates Repo unter der Organisation desktop365 angelegt
   werden? **Ja oder nein.**
3. Sollen die erzeugten `_thumb`-Varianten der vier Ersatzbilder in den Bucket,
   obwohl der Resolver sie nachweislich nicht abfragt? Empfehlung nein. **Ja oder nein.**
4. Bleiben die neutralen Platzhalter mit dem SL-Herz die dauerhaften Ersatzbilder,
   oder sollen sie später durch echte Produktfotos je Familie ersetzt werden?
   **Dauerhaft ja oder nein.**
5. Ist es in Ordnung, dass die Faktortabelle der Preis-Pipeline nicht versioniert
   ist und damit nur auf diesem einen Rechner existiert? Empfehlung nein, sie
   gehört ins private Pipeline-Repo. **Ja oder nein.**
6. Soll der Zustandsendpunkt künftig ohne rohe Fehlermeldungen antworten, bevor
   surface.love auf die App zeigt? Empfehlung ja. **Ja oder nein.**

## 6. Was der Nachtlauf bewusst nicht getan hat

- Kein Distributor-Abruf. Es lag eine lokale CSV vor, und Zugangsdaten gab es
  nicht. Das Abrufkontingent wurde nicht angetastet.
- Kein Schreibmodul für den Objektspeicher. Die Vorbedingung war eine gegen den
  Datenvertrag gültige `products.json`. Wegen Befund A und B war sie nicht erfüllt.
  Einen Schreibweg zu bauen, der einen Faktorwert veröffentlicht, wäre genau der
  Fehler gewesen, den die Prüfung verhindern soll.
- Kein Repo für `sl-bilder` angelegt. Das ist eine nach außen wirkende Handlung
  mit einer Sichtbarkeitsentscheidung.
- Im Shop-Repo nichts geändert, nicht einmal die vorgemerkte Meldung. Jeder Push
  auf main deployt.
- Die erzeugte `products.json` liegt außerhalb jeder Git-Historie und wurde nicht
  committet. Die vorhandenen Exportdateien vom Juni wurden nicht überschrieben.

## 7. Ein Hinweis, der nicht zum Auftrag gehörte

Beim Schreiben dieses Berichts unter Leitplanke 7 ist aufgefallen, dass
`contracts/PRICING.md` in Abschnitt 2 den Aufschlagsfaktor als konkrete Zahl
nennt. Dieses Repo ist öffentlich. Damit steht der Wert, den Befund A aus der
`products.json` heraushalten soll, bereits im Hub. Ein Löschen allein hilft nicht,
weil die Git-Historie öffentlich bleibt. Das ist deshalb keine schnelle Korrektur,
sondern eine bewusste Entscheidung: Historie bereinigen oder den Wert als nicht
mehr vertraulich einstufen. Nicht angefasst, nur gemeldet.
