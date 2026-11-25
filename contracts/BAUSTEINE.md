# Bausteine der Ausstattung (bausteine.json)

Stand 25.11.2026, F-49 und W6 (8100). Grundlage: Checkout-Baukasten bk1 (Treppe), E-065, E-076, E-099, E-103, E-105, E-106, E-156, E-157, E-182, E-183, E-185, E-186, E-187.

## Zweck
Die Ausstattungsseite zwischen Gerät und Anfrage bietet in fester Reihenfolge an: Zubehör, Lizenzen, Garantie, Managed Workplace. Alle Raten kommen fertig aus der Preis-Pipeline, der Shop rechnet nicht (E-099). Der Shop zeigt nur Bausteine, die zur gewählten Laufzeit eine Rate in den Daten haben.

## Quellen
- **Zubehör:** Artikel mit `category: "zubehoer"` in products.json. Die Passung steht in `fits`, einer Liste von Geräteschlüsseln (E-106). Ohne `fits` wird der Artikel nicht angeboten. Das Feld `art` (DATA-CONTRACT) ordnet ihm Titel und Nutzensatz aus dem Copy-Baukasten zu.
- **Lizenzen, Garantie, Managed Workplace:** bausteine.json im Bucket neben products.json, jede Nacht von der Preis-Pipeline geschrieben.

## Geräteschlüssel
`familie-generation-groesse`, etwa `surface-pro-11-13` oder `surface-laptop-8-13-8`. Größe mit Bindestrich statt Komma. `*` steht für alle Geräte.

## Aufbau bausteine.json
```
{ "meta": { "generated_at", "currency", "vat_rate", "contract_types": { "leasing": [24, 36, 48] }, "count" },
  "items": [ ... ],
  "seiten": [ ... ] }
```
`seiten` ist optional, Aufbau im Abschnitt „Produktseiten“. Alte Leser ignorieren den Block.

Je Eintrag:
- `id`: stabiler Slug des Eintrags.
- `baustein`: Schlüssel aus dem Konzept, er bestimmt Texte und Regeln im Shop. Erlaubt sind `lizenz_m365_standard`, `lizenz_m365_premium`, `lizenz_copilot`, `garantie_1`, `garantie_2`, `garantie_3`, `garantie_2_plus`, `garantie_3_plus`, `managed_modell_a` und `managed_modell_b`.
- `kategorie`: `lizenz`, `garantie` oder `managed`.
- `msku`: optional, die Artikelnummer, wo es eine gibt.
- `name`: Artikelbezeichnung, im Shop nur als Nebenzeile. Titel und Nutzensatz kommen aus dem Copy-Baukasten (F-19).
- `gilt_fuer`: Liste von Geräteschlüsseln oder `["*"]`.
- `je`: `geraet` oder `platz`. Die Startmenge ist die Gerätemenge.
- `benoetigt`: optional, Liste von Bausteinen, von denen mindestens einer gewählt sein muss.
- `schliesst_aus`: optional, Liste von Bausteinen, die nicht zugleich gewählt sein dürfen.
- `rates.leasing`: je `{ "term", "net", "gross" }` genau für 24, 36 und 48 Monate. `gross` ist `net` mal 1,19, kaufmännisch gerundet.

Fehlt eine Rate zur gewählten Laufzeit, erscheint der Baustein bei dieser Laufzeit nicht. Es gibt keinen Schätzwert und kein „Preis auf Anfrage“ im Baukasten (bk1, Zustand 7).

## Regeln
- Garantie gibt es nur zusammen mit einem Neugerät, nie im Weg der geprüften Geräte (F-37).
- Die Garantien schließen sich gegenseitig aus. Empfohlen ist `garantie_2` bei 36 Monaten und `garantie_3` bei 48 Monaten, bei 24 Monaten gibt es keine Empfehlung (E-103). Die Plus-Varianten tragen keine Empfehlung.
- Lizenzen werden auf volle Jahre gerechnet (E-076) und stecken in der Rate (E-065). Die Pipeline bildet daraus die Raten je Laufzeit.
- `lizenz_copilot` setzt `lizenz_m365_standard` oder `lizenz_m365_premium` voraus.
- Managed Workplace setzt `lizenz_m365_premium` voraus. Wählt der Kunde Managed, wählt der Shop Premium sichtbar mit. Wählt er Premium ab, entfällt Managed, mit Hinweiszeile (bk1, Zustand 6).
- Bausteine gibt es nur an einem Gerät (E-182). Lizenzen, Garantie, Managed Workplace und Zubehör hängen immer an genau einem Gerät der Anfrage, eine Anfrage ohne Gerät gibt es nicht. Wird etwas ohne Wahl eines Geräts dazugebucht, hängt es am ersten Gerät im Warenkorb.
- Wird ein Gerät aus dem Warenkorb entfernt, entfallen seine Bausteine mit ihm. Vorher zeigt der Shop einen deutlichen Hinweis, was mit entfernt wird, danach gibt es Rückgängig (E-182).
- Nichts ist vorausgewählt (bk1, rote Linie 1), mit einer Ausnahme (E-183): Bei einem Gerät mit `copilot_plus` aus modelle.json sind `lizenz_copilot` und als Voraussetzung `lizenz_m365_premium` vorausgewählt. Das gilt auf jedem Weg, auf dem ein Copilot+ PC in den Warenkorb kommt. Geräte ohne `copilot_plus` haben keine Vorauswahl. „Komplett ausstatten“ wählt die empfohlenen Bausteine, jede Zeile bleibt einzeln abwählbar.
- Beide vorausgewählten Lizenzen bleiben abwählbar, in der Ausstattung und im Warenkorb. Wer `lizenz_copilot` an einem Copilot+ PC abwählt, bekommt vorher einen deutlichen Hinweis, dass es ein Copilot+ PC ist und die Lizenz dazu sinnvoll ist. Wird `lizenz_m365_premium` abgewählt und keine andere Basislizenz gewählt, entfällt `lizenz_copilot` mit Hinweiszeile, wie bei Managed Workplace (E-183).
- Die Raten auf Geräte- und Modellseiten bleiben reine Geräteraten, ohne vorausgewählte Lizenzen (E-183).
- Fehlende Voraussetzung (E-187): Kommt ein Baustein an ein Gerät, dem seine Voraussetzung fehlt, wählt der Shop sie sichtbar mit, auf jedem Weg (Ausstattung, Produktseite, Vormerkung). Bei `lizenz_copilot` ist das `lizenz_m365_premium`, bei Managed Workplace ebenso. Die mitgewählte Lizenz bleibt abwählbar, dann gilt die Hinweiszeile aus der Regel zu Managed Workplace und E-183. Gesperrt wird nichts.
- Vormerkung (E-186): Wählt der Kunde auf einer Produktseite einen Baustein, ohne dass ein Gerät im Warenkorb liegt, sagt ihm der Shop, dass es den Baustein nur mit einem Gerät gibt, merkt ihn vor und führt ihn zur Geräteauswahl. Bei Copilot ist sie auf Copilot+ PCs gefiltert, alle Geräte bleiben erreichbar. Kommt danach das erste Gerät in den Warenkorb, hängt der vorgemerkte Baustein an diesem Gerät, mit dessen Laufzeit und Menge, sichtbar ausgewählt und abwählbar. Das ist die zweite Ausnahme von „Nichts ist vorausgewählt“.
  - Gespeichert wird im Browser unter `sl-vormerkung-v1`, als Liste von Baustein-Schlüsseln ohne Doppel. Garantien schließen sich auch hier aus, die zuletzt gewählte Stufe gilt.
  - Solange etwas vorgemerkt ist, zeigt die Geräteauswahl eine Leiste mit dem Namen des Bausteins und „Verwerfen“.
  - Die Vormerkung wird gelöscht, sobald sie an einem Gerät hängt oder der Kunde sie verwirft. Garantie bleibt an Neugeräte gebunden (F-37): Kommt zuerst ein geprüftes Gerät in den Warenkorb, bleibt die Garantie vorgemerkt und die Leiste sagt das.

## In der Anfrage
Jeder Baustein ist eine eigene Position direkt hinter seinem Gerät, mit derselben Laufzeit (E-105, E-182). In HubSpot wird er eine Deal-Position mit dem Schlüssel `baustein` und der Menge. Im Warenkorb sind die Mengen der Bausteine nur lesbar, geändert werden sie über „Bearbeiten“ in der Ausstattung. Einzelne Bausteine lassen sich im Warenkorb direkt entfernen, mit Rückgängig (E-182).

## Produktseiten (W6, P15, D-C13, M06)
Fünf Seiten nach einer Vorlage: `m365-standard`, `m365-premium`, `copilot`, `managed`, `garantie`. Die Adressen legt ROUTEN-UND-SEO.md fest (W3), bis dahin gelten die Slugs aus `seiten` als Vorschlag.

Je Eintrag in `seiten`:
- `seite`: Schlüssel der Seite.
- `slug`: Vorschlag für die Adresse.
- `bausteine`: Liste der Baustein-Schlüssel auf der Seite, bei Managed zwei, bei Garantie fünf.
- `name_microsoft`: Name, wie ihn microsoft.com/de-de heute führt, sonst `null` (Managed). Die Seite zeigt diesen Namen.
- `dienste`: Liste von Dienst-Schlüsseln aus `word`, `excel`, `powerpoint`, `onenote`, `loop`, `clipchamp`, `outlook`, `exchange`, `teams`, `onedrive`, `sharepoint`, `entra_id`, `windows`, `intune`, `defender`, `purview`, `copilot`. `teams` nur, wenn unser Artikel Teams enthält.
- `voraussetzung`: `null` oder ein Objekt, entweder `{ "benoetigt_einen_von": [Baustein-Schlüssel] }` oder `{ "nur_mit": "neugeraet" }`.
- `geraete_hinweis`: `null` oder `copilot_plus`.
- `quellen`: Liste `{ "url", "stand" }`, nur für die Pflege, nie im Shop sichtbar.

Regeln der Seiten:
- Raten kommen nur aus `items` (E-099), `seiten` trägt keine. Der Kopf zeigt die Rate bei 48 Monaten, darunter die bei 24 und 36.
- Hat ein Baustein Raten je Gerät (`gilt_fuer` mit mehr als einem Schlüssel), zeigt der Kopf „ab“ und die kleinste Rate bei 48 Monaten über alle Einträge. Liegt ein passendes Gerät im Warenkorb, zeigt die Schnellansicht dessen Rate.
- „Enthalten“ zeigt die Logos aus `dienste` mit dem Namen als Text daneben. Bei Copilot ist das nur `copilot`. Darunter folgt eine zweite Reihe „Copilot arbeitet in diesen Apps Ihrer Basislizenz“ mit genau den Apps, für die der Seitentext einen Satz unter `enthalten.dienste` hat, ohne Zähler im Kopf. So entsteht nicht der Eindruck, Copilot enthalte die Apps.
- „Passende Geräte“ zeigt die Gerätekarten unverändert wie auf `/de/geraete` (W1). Bei `geraete_hinweis: copilot_plus` nur Copilot+ PCs, bei Garantie nur Modelle aus `gilt_fuer`.
- Der Hauptknopf heißt „Zu einem Gerät hinzufügen“. Ohne Gerät im Warenkorb gilt die Vormerkung, mit einem Gerät die Schnellansicht, mit mehreren die Auswahl „An welches Gerät?“. Die Menge ist die Gerätemenge der Position.
- Texte kommen aus `content/de/bausteine/{seite}.json` im Shop, die Sätze je Dienst aus `content/de/bausteine/dienste.json` (M06). Logos und Aufmacher nach IMAGES.md, Nachtrag Bausteine und Dienste.

## Nicht in bausteine.json
Keine EK-, VK- oder Faktorwerte (E-092). Keine Texte außer `name`.
