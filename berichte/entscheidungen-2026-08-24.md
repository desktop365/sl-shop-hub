# Entscheidungen vom 24.08.2026

Antworten auf die sechs offenen Fragen aus `berichte/nachtlauf-2026-08-24.md`
Abschnitt 5, plus die Faktor-Historien-Frage aus Abschnitt 7. Damit ist der
Morgenplan durchgehend baubar, es hängt keine Frage mehr an einer Entscheidung.

| # | Frage | Antwort |
|---|---|---|
| 1 | Preis-Pipeline schreibt nach GCS, Azure-Blob-Weg gestrichen | **Ja** |
| 2 | `sl-bilder` als privates Repo unter desktop365 | **Ja** |
| 3 | `_thumb`-Varianten der Ersatzbilder in den Bucket | **Nein** |
| 4 | Neutrale Platzhalter bleiben dauerhaft | **Ja** |
| 5 | Faktortabelle bleibt unversioniert | **Nein**, sie wird versioniert |
| 6 | Zustandsendpunkt ohne rohe Fehlermeldungen | **Ja** |
| – | Git-Historie wegen des Aufschlagsfaktors bereinigen | **Nein** |

## 1. GCS statt Azure Blob, ja

`contracts/INFRA.md` ist maßgeblich, und der Bucket steht bereits, ebenso der
Leseweg des Shops über `GCS_BASE_URL`. Ein zweiter Objektspeicher brächte einen
zweiten Zugang, eine zweite Domain und eine zweite Fehlerquelle, ohne einen
einzigen Vorteil.

## 2. `sl-bilder` privat unter desktop365, ja

Das Repo hält Herstellerfotos und später eigene Produktaufnahmen. Deren
Weitergaberecht ist nicht geklärt, also bleibt das Repo privat. Öffentlich
sichtbar werden die Bilder ohnehin erst über den Bucket, dafür braucht es kein
öffentliches Repo.

## 3. Keine `_thumb`-Dateien der Ersatzbilder in den Bucket, nein

Der Resolver setzt im Fallback-Zweig Hauptbild und Vorschau nachweislich auf
dieselbe URL, er fragt die Vorschaudateien also nie ab. Was nie abgerufen wird,
gehört nicht in den Bucket, sonst liegt dort totes Material, das niemand pflegt.
Die Dateien bleiben im Repo, sie kosten dort nichts.

## 4. Neutrale Platzhalter bleiben dauerhaft, ja

Sie sind neutral, rechtlich unbedenklich und über alle Familien einheitlich. Ein
Ersatzbild soll ehrlich als Ersatzbild erkennbar sein. Ein echtes Produktfoto an
dieser Stelle würde ein Gerät zeigen, das die Variante gar nicht ist. Echte Fotos
kommen als Bildmodelle nach `images.json`, nicht als Fallback.

## 5. Faktortabelle wird versioniert, nein

Ohne Versionierung existiert die Rechengrundlage des gesamten Katalogs auf genau
einem Rechner, ohne Historie und ohne Sicherung. Sie wandert deshalb in das
private Repo `surface-love-pricing`, das genau für solche Geschäftslogik
existiert. Dass das Repo privat bleibt, ist damit Bedingung, nicht Nebensache.

## 6. Zustandsendpunkt ohne rohe Fehlermeldungen, ja

Der Endpunkt ist öffentlich, und eine durchgereichte Datenbankfehlermeldung
enthält je nach Treiber Host, Benutzer und Datenbanknamen. Das gehört korrigiert,
bevor surface.love auf die App zeigt. Der Hinweistext bleibt fachlich, der
technische Grund geht nur ins Log.

## Faktor-Historie nicht bereinigen, nein

Der Aufschlagsfaktor stand als konkrete Zahl in `contracts/PRICING.md` in diesem
öffentlichen Repo. Er ist heute daraus entfernt, an seiner Stelle steht nur noch
der Verweis auf den versionierten Wert im privaten Pricing-Repo. Ebenfalls
entfernt wurde der `markup_factor`-Eintrag aus den meta-Blöcken von
`data/products.sample.json` und `data/shop-products.json`, dieselbe Leckage an
zwei weiteren Stellen.

Die Git-Historie wird **nicht** umgeschrieben. Eine Historienbereinigung ändert
jeden Commit-Hash, entwertet jeden bereits gezogenen Klon und ist gegenüber einem
Wert, der bereits öffentlich stand, ohnehin keine echte Rücknahme. Der Faktor
gilt damit ab heute als nicht mehr vertraulich, nur eben als nicht mehr
fortgeschrieben: künftige Änderungen des Wertes finden ausschließlich im privaten
Repo statt und erscheinen hier nie wieder.
