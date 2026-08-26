# Nachtblock 25.08.2026

Unbeaufsichtigt gearbeitet, ohne Rückfragen. Kein Distributor-Kontakt, nichts in
den GCS-Bucket geschrieben, das Pricing-Repo nicht angefasst. Im Shop-Repo genau
ein Commit und ein Push.

## Kurzfassung, Unerwartetes zuerst

**Das letzte Kettenglied ist weiterhin offen, und zwar an derselben Stelle wie
gestern: `SYNC_TOKEN` ist auf Hostinger nicht gesetzt.** Die Sync-Route steht
seit gestern, ist deployt und erreichbar, sie antwortet mit 503, weil die
Variable fehlt. Das Hostinger-Plugin bietet Endpunkte für Deploys, Builds, Logs,
Cron, Datenbanken und Dateien, aber **keinen für Umgebungsvariablen**. Damit sind
Trockenlauf, echter Lauf und die gesamte Abnahme aus Teil A blockiert. Wo der
Wert einzutragen ist, steht in Abschnitt A.3.

**`npm run lint` war seit dem Umstieg auf Next 16 kaputt** und niemandem
aufgefallen. Der Befehl `next lint` existiert nicht mehr, Next deutete das Wort
`lint` als Verzeichnisangabe und brach ab. Behoben, aber nicht auf dem Weg, den
die Doku vorschlägt, siehe A.4.

**Bei der Bildmatrix steckten drei Regelfehler im Titelparsen**, jeder einzelne
hätte den Katalog falsch gebündelt. Der schlimmste: 52 Surface Laptops liefen
als Surface Pro, weil `\bLaptop\b` an „Laptop8" nicht greift und der Ausdruck
auf das Wort Pro in „Win 11 Pro" durchfiel. Alle drei behoben und durch Tests
festgenagelt, siehe B.2.

Der 04:00-UTC-Timer war zum Ende dieses Blocks noch nicht gelaufen, es war
23:52 UTC. Teil A Schritt 5 entfällt damit.

| Teil | Ergebnis |
|---|---|
| A, Shop | Route stand schon, Lint repariert, ein Commit `053a123`, ein Push. **Abnahme blockiert**, `SYNC_TOKEN` fehlt |
| B, Bilder | Matrix, Beschaffungsliste und komplette Verarbeitungsstrecke gebaut, 46 Tests grün, `4fc42ed` |
| C, Hub | IMAGES.md entschieden, Systemkarte A0, Datumsregel, Board gebucht, `dc28a1e` |

---

# Teil A, Shop-Repo

## A.1 Stand zu Beginn

| Prüfung | Ergebnis |
|---|---|
| Route `app/[locale]/api/sync/catalog/route.ts` | vorhanden, 5.249 Bytes, aus dem Auftrag vom 24.08. |
| `SYNC_TOKEN` gesetzt | **nein**, `POST` ohne Token antwortet 503 |
| `/de/api/health`, `katalog.quelle` | `bucket` |
| `katalog.imKatalog` | 471 |
| Hinweis zum leeren Leseabbild | steht noch da |

Die Route musste also nicht gebaut werden, Schritt 2 des Auftrags entfiel bis
auf das Token.

## A.2 Ein Commit, ein Push

`053a123`, gebündelt wie vorgeschrieben:

- die bereits gestagte `CLAUDE.md`,
- `eslint.config.mjs` neu,
- `package.json` und `package-lock.json` für die Lint-Umstellung.

Vor dem Push geprüft: `npm run lint` läuft sauber durch mit null Befunden,
`npm run typecheck` sauber, `npx next build` sauber, die Sync-Route erscheint
weiterhin als dynamisch. Bewusst `npx next build` statt `npm run build`, denn
dessen erster Schritt ist `prisma migrate deploy` gegen die Live-Datenbank.

Nach dem Deploy gegengeprüft: `/de/api/health` antwortet 200 mit 471 Artikeln,
die Katalogseite antwortet 200, die Sync-Route weiterhin 503. Der Deploy hat
nichts beschädigt.

## A.3 Die Blockade, und wo Sascha den Wert setzt

> **Korrektur vom 26.08.2026.** Der Satz unten, das Hostinger-Plugin könne keine
> Umgebungsvariablen setzen, war zu kurz gegriffen. Richtig ist nur: es gibt
> keinen eigenen Endpunkt dafür, weder im Plugin noch in der offiziellen API,
> nachgeprüft am generierten SDK, das alle Operationen der API abbildet und
> unter `nodejs` nur Builds, Logs, Neustart und Schwachstellen kennt. Es gibt
> aber einen indirekten Weg, und der hat funktioniert: Die App läuft unter
> Passenger, ihre Umgebung wird über `SetEnv`-Zeilen im `.htaccess` des
> Dokumentenwurzelverzeichnisses gefüllt, dort standen bereits drei solche
> Zeilen. Diese Datei ist über die Datei-API der Anbindung les- und
> überschreibbar. Eine angehängte Zeile plus Neustart über den
> Neustart-Endpunkt, mehr war nicht nötig. Der Rest dieses Abschnitts ist
> damit erledigt, die vollständige Abnahme steht in
> `berichte/sync-token-2026-08-26.md`. Einschränkung: ein neues Deploy erzeugt
> das `.htaccess` neu, deshalb gehört der Wert zusätzlich in die
> Umgebungsvariablen des hPanels, siehe `contracts/HOSTINGER-RULES.md`.

Der Token ist erzeugt, kryptografisch zufällig, 64 Zeichen, und liegt **nur**
lokal in der Sitzungsablage. Er steht nicht im Repo, nicht in diesem Bericht und
nicht im Chat.

**Einzutragen in hPanel:** Websites, `worklove.shop`, Node.js-Anwendung,
Umgebungsvariablen, Schlüssel `SYNC_TOKEN`. Danach die Anwendung **neu starten**,
sonst liest der laufende Prozess den alten Stand und die Route bleibt bei 503.

Danach offen und in dieser Reihenfolge abzuarbeiten:

1. Trockenlauf `POST /de/api/sync/catalog?trockenlauf=1`, Zähler prüfen.
2. Echter Lauf ohne Parameter.
3. Abnahme: `katalog.quelle` muss `datenbank` zeigen, `imKatalog` in der
   Größenordnung 471, der Hinweis zum leeren Leseabbild muss verschwinden, drei
   Raten auf der Katalogseite exakt gegen `products.json`.
4. Gegenprobe, dass die Route ohne Token 401 liefert statt 503.

## A.4 Lint, eine Abweichung von der Doku mit Grund

`next lint` ist in Next 16 entfernt, `next build` lintet nicht mehr mit. Die Doku
im Paket empfiehlt `eslint-config-next`. Das ließ sich hier **nicht** verwenden:
das Paket zieht `typescript-eslint` fest ein, und `typescript-eslint` läuft nicht
unter TypeScript 7, das dieses Projekt benutzt. Der Aufruf bricht dann schon beim
Laden der Konfiguration ab, es wird keine einzige Datei geprüft.

Verwendet wird deshalb `@next/eslint-plugin-next` direkt. Es ist eigenständig und
kennt TypeScript gar nicht. Der Weg zurück auf die empfohlene Konfiguration steht
als Kommentar in `eslint.config.mjs`, sobald `typescript-eslint` TypeScript 7
unterstützt.

Keine Regelverschärfung, wie verlangt: bewusst `recommended` statt
`core-web-vitals`, letzteres hebt Regeln von Warnung auf Fehler. Zusätzlich
ignoriert wird `db/generated`, der erzeugte Prisma-Client, der auch in
`tsconfig.json` ausgeschlossen ist. ESLint steht in `devDependencies`, zur
Bauzeit auf dem Server wird es nicht gebraucht.

---

# Teil B, Bild-Vorbereitung

Repo `sl-bilder`, Commit `4fc42ed`. **Nichts hochgeladen**, der Bucket wurde nur
lesend über die öffentliche URL angesprochen.

## B.1 Die Matrix

`scripts/matrix_bauen.py` leitet aus den 471 Artikeln die Bildmodelle ab,
Ergebnis in `data/matrix.json`.

| | |
|---|---|
| Artikel gesamt | 471 |
| bildrelevant | 454 |
| Ersatzteile, nicht bildrelevant | 17 |
| Bildmodelle Geräte | 28 |
| Bildmodelle Zubehör | 35 |

Die Bündelung wirkt: 419 Geräteartikel brauchen nur 28 Fotosets. **Zehn Fotosets
decken 77 Prozent aller Geräte**, das ist die Beschaffungsreihenfolge.

Je Modell stehen in der Datei: Schlüssel `familie-generation-groesse-farbe`,
Artikelanzahl, MSKUs, Status, Ersatzbilddatei, Erbregel falls anwendbar, und ein
Feld `unsicher`.

## B.2 Die drei Regelfehler

Sie sind der wichtigste Teil dieses Abschnitts, weil sie alle drei plausibel
aussehende, falsche Ergebnisse erzeugt haben:

1. **`\bLaptop\b` greift nicht an „Laptop8"**, weil zwischen `p` und `8` keine
   Wortgrenze liegt. Der Ausdruck fiel auf `\bPro\b` durch, und das traf das Pro
   in „Win 11 Pro". Folge: 52 Surface Laptops als Surface Pro geführt.
2. **„Laptop 5G" ergab Generation 5.** 5G ist Konnektivität, keine Generation.
3. **„Laptop 13"" ergab Generation 13.** Dort ist die 13 die Bildschirmgröße.

Familie und Generation werden jetzt in einem Griff bestimmt, mit Blick auf das
Zeichen unmittelbar hinter der Ziffer. Alle drei Fälle haben einen eigenen Test.

## B.3 Nicht geraten

Durchgehalten wurde der Grundsatz aus IMAGES.md: was der Titel nicht hergibt,
bleibt leer und wird ausgewiesen, statt plausibel gefüllt zu werden.

| Merker | Modelle | Bedeutung |
|---|---:|---|
| `farbe_unbekannt` | 8 | Titel nennt nur mehrdeutige Kürzel wie `B` |
| `groesse_unbekannt` | 3 | kein Zollzeichen im Titel |
| `generation_unbekannt` | 2 | Reihe ohne Generationsziffer, darin die 5G-Geräte |
| `generation_unplausibel` | 1 | `Lpt34` meint Laptop 3 und 4, nicht Generation 34 |

## B.4 Die Verarbeitungsstrecke

Drei Schritte, alle in `scripts/`:

1. **`bilder_bauen.py`** passt Quellbilder auf eine quadratische Leinwand bis
   1200 x 1200 ein, ohne zu beschneiden und ohne hochzurechnen, schreibt WebP mit
   Qualität etwa 80 in sRGB ohne Metadaten und senkt die Qualität stufenweise,
   bis Hauptbild unter 200 KB und Vorschau unter 40 KB liegen.
2. **`images_json_bauen.py`** erzeugt `images.json` Version 2. Es nimmt nur
   Modelle auf, für die wirklich Dateien vorliegen. Ein Eintrag ins Leere würde
   den Rückfall auf das Ersatzbild aushebeln und ein totes Bild im Shop erzeugen.
3. **`validieren.py`** prüft gegen den Kontrakt, einschließlich der Frage, ob
   jede genannte Datei existiert.

**46 Tests**, gegen die acht vorhandenen Fallback-Dateien und gegen synthetische
Fälle: Seitenverhältnis, gleichmäßiger Rand, Transparenz auf Weiß, keine
Metadaten, Qualitätsabsenkung ohne Beschneiden, und die drei Titelfallen.

`images.json` bleibt vorerst leer, und das ist richtig: es liegt kein einziges
Herstellerfoto vor, `source/` ist leer, der Shop zeigt die Ersatzbilder über die
Familie.

## B.5 Ein Vorbehalt zur Warengruppe

Die öffentliche `products.json` trägt die Warengruppe des Distributors **nicht**.
Im Feed sind 27 Artikel der Warengruppe `ERI`, über Titelmerkmale wie
`Field Replacement`, `CRU` oder `rSSD` erkannt werden **17**. Die Differenz sind
Ersatzteile, deren Titel das nicht verrät, sie laufen derzeit als Zubehör mit.
Sauber lösbar ist das nur, wenn die Warengruppe in den Datenvertrag kommt oder
eine Kurationsliste sie führt. Bis dahin ist 17 eine Untergrenze.

---

# Teil C, Hub

Commit `dc28a1e`.

## C.1 IMAGES.md

Neuer Abschnitt **Bildmodell-Matrix, entschieden 25.08.2026**, knapp und normativ,
mit den vier Festlegungen. Die vier offenen Fragen bleiben im Wortlaut stehen,
mit dem Vermerk, dass sie beantwortet sind. So bleibt nachvollziehbar, welche
Frage zu welcher Entscheidung gehört, statt dass die Frage verschwindet.

## C.2 Systemkarte

`SYSTEMKARTE-A0.svg` im Hub-Root, verlinkt in `LANDKARTE.md`.

viewBox 1189 mal 841, eine Einheit ist ein Millimeter auf A0 quer, kleinste
Schrift 4,2 mm. Fünf Ebenen: Kopf mit Legende, Wertstrom von der Continue-API bis
HubSpot, Stränge mit Zuständigkeiten, Zeitband, Kontraktleiste. Der kritische
Pfad zum Umschalten ist eine durchgehende kräftige Linie, der Bucket-Rückfall
eine gestrichelte Umgehung des Leseabbilds. Cyan nur als Akzent.

**Im Browser gegengeprüft, nicht nur im Quelltext.** Dabei fielen zwei
Layoutfehler auf, die im Code nicht zu sehen sind: die erste Zeitband-Station
stand mitten in der Überschrift, und die letzte lief über den Blattrand hinaus.
Beides behoben, danach erneut angesehen.

Auf der Karte stehen keine internen Werte, nur öffentliche Artikelzahlen und
öffentlich sichtbare Bausteine.

## C.3 Datumsregel

`board/README.md` sagt jetzt: das Datum der Meldung muss **neuer als oder gleich**
dem Datum des Eintrags sein. Gleich genügt, mehrere Meldungen desselben Tages
sind der Regelfall. Die bisherige Formulierung hätte sie formal ausgeschlossen,
und genau dieser Fall ist gestern bei den fünf Meldungen des Preislisten-Chats
schon eingetreten.

## C.4 Board

| id | Status | Kern der Notiz |
|---|---|---|
| `b1` | erledigt | vier Bildfragen entschieden, in IMAGES.md |
| `b2` | erledigt | Matrix-Regeln normativ in IMAGES.md |
| `b3` | laeuft | Pipeline und Bedarfsliste stehen, Fotos fehlen |
| `c5` | **blockiert** | Route deployt, antwortet 503, wartet auf `SYNC_TOKEN` |

`c5` steht bewusst auf `blockiert` und nicht auf `geliefert`. Geliefert hätte
verdeckt, dass hier jemand eingreifen muss; blockiert zeigt es auf dem Board.

`stand` auf 2026-08-25 gesetzt. Vorher geprüft, ob eine frühere Buchung es
zurückgedreht hat: **hat sie nicht**, es stand korrekt auf 2026-08-24. Die
gestrigen Buchungen des Preislisten-Chats haben `stand` nicht angefasst.

`CHANGELOG.md` ergänzt.

---

## Was offen bleibt

1. `SYNC_TOKEN` in hPanel setzen und die Anwendung neu starten. Danach ist die
   Abnahme aus Teil A in wenigen Minuten nachzuholen.
2. Herstellerfotos beschaffen, Reihenfolge nach der Top-10-Liste in
   `sl-bilder/docs/bildbedarf-2026-08-25.md`, platin vor schwarz.
3. Die Warengruppe des Distributors in den Datenvertrag aufnehmen oder eine
   Kurationsliste für Ersatzteile führen.
4. Der 04:00-UTC-Timer läuft nach diesem Block. Seine Messungen zu `description`,
   Titelformat ohne Cleanup und Zulaufdaten stehen danach in Application
   Insights, siehe die Berichte im Pricing-Repo.
