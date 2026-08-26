# SYNC_TOKEN gesetzt, Sync-Route abgenommen, 26.08.2026

Kurzlauf mit einem Ziel: das letzte unbestätigte Kettenglied schließen. Auftrag
war, die Behauptung aus `berichte/nachtblock-2026-08-25.md` Abschnitt A.3 zuerst
zu prüfen, statt sie zu übernehmen. Sie war zu kurz gegriffen.

## 1. Was die Prüfung ergab

Die Behauptung lautete, das Hostinger-Plugin könne keine Umgebungsvariablen
setzen, deshalb müsse Sascha den Wert von Hand im hPanel eintragen.

Geprüft wurde zweifach:

- **Die Werkzeuge der laufenden Sitzung.** Der Bereich Hosting kennt für Node
  nur Builds, Build-Einstellungen aus einem Archiv, Build-Protokolle, den
  Neustart des Serverprozesses und die Schwachstellenliste. Kein Endpunkt für
  Umgebungsvariablen.
- **Die offizielle API selbst**, über das generierte TypeScript-SDK, das alle
  Operationen der öffentlichen API abbildet. Dort tragen genau sechs Pfade
  `nodejs`, dieselben sechs. Kein Treffer auf `env` oder `environment` im
  gesamten Pfadbestand.

Insoweit stimmte die Behauptung. Sie war aber nur die halbe Frage, denn gesucht
war auch der indirekte Weg, und den gibt es.

## 2. Der gefundene Weg

Die Anwendung läuft nicht als frei gestarteter Prozess, sondern unter Passenger.
Ihre Konfiguration steht im `.htaccess` des Dokumentenwurzelverzeichnisses:
Anwendungswurzel, Startdatei, Node-Binary, Neustartverzeichnis, und darunter
bereits drei `SetEnv`-Zeilen, mit denen die Plattform selbst Werte in die
Prozessumgebung schiebt. Eben dieses Verzeichnis ist über die Datei-API der
Anbindung lesbar und beschreibbar.

Damit war der Weg:

1. Vorhandenes `.htaccess` über die Datei-API lesen und byte-genau
   nachbauen, 463 Bytes, Kontrolle gegen die vom Server gemeldete Größe.
2. Genau **eine** Zeile anhängen, `SetEnv SYNC_TOKEN <Wert>`, sonst nichts.
   Neue Größe 547 Bytes.
3. Datei über die Upload-Schnittstelle der Anbindung ersetzen, TUS-Protokoll,
   zwei Schritte, 201 und 204 mit vollem Versatz.
4. Serverprozess über den Neustart-Endpunkt neu starten. Kein Deploy, kein
   Build, kein Eingriff an Domains, DNS oder Kontoeinstellungen.

Der Wert selbst ist kryptografisch zufällig, 64 Hexzeichen aus
`crypto.randomBytes(32)`. Er steht in keinem Repo, in keinem Bericht, in keiner
Ausgabe und in keinem Protokoll.

## 3. Abnahme

| Prüfung | Erwartet | Ergebnis |
|---|---|---|
| Route ohne Token, vorher | 503 | 503, Variable fehlte |
| Route ohne Token, nachher | 401 | 401 `nicht berechtigt` |
| Route mit falschem Token | 401 | 401 `nicht berechtigt` |
| Trockenlauf | Zähler, nichts geschrieben | 477 Produkte, 3339 Raten, `geschrieben: false` |
| Echter Lauf | schreibt das Leseabbild | 477 Produkte, 3339 Raten, `geschrieben: true` |
| `/de/api/health`, Quelle | `datenbank` | `datenbank` |
| `/de/api/health`, Bestand | Größenordnung Morgenfeed | 477, vor und nach Filter |
| Hinweis leeres Leseabbild | verschwunden | Hinweisliste leer |

Der Feedstand ist durchgehend `2026-08-26T04:08:06Z`, also der Morgenlauf von
heute. Der Sprung von 471 auf 477 Artikel stammt aus diesem Lauf, nicht aus dem
Sync.

**Raten gegen `products.json`:** verglichen wurde nicht eine Stichprobe, sondern
die vollständige Menge. Die Katalogseite trägt 477 Karten, `products.json` trägt
477 Artikel mit `rate_from`, der Mengenvergleich über 323 verschiedene
Nettoraten ergibt **null Abweichungen**. Drei Karten zusätzlich namentlich
gegengeprüft, netto und brutto, alle gleich.

**Nebenprobe:** die Konfigurationsdatei ist von außen nicht abrufbar, drei
Varianten getestet, jeweils 403 ohne Inhalt.

## 4. Was offen bleibt

- **Deploy-Festigkeit.** Ein neues Deploy erzeugt das `.htaccess` neu und
  verliert die Zeile. Die Route fällt dann auf 503 zurück, der Shop selbst
  bleibt heil, weil er über das Leseabbild liest. Dauerhaft gehört der Wert in
  die Umgebungsvariablen des hPanels, siehe `contracts/HOSTINGER-RULES.md`
  Abschnitt 7.
- **Bildmodelle.** Der Sync meldet null Bildmodelle und null MSKU-Zuordnungen.
  Das ist erwartet, `images.json` bleibt leer, solange die Fotos fehlen, siehe
  Board b3.
- **Zeitplan.** Der Sync läuft weiterhin von Hand. Ein Zeitplan kurz nach dem
  04:00-UTC-Lauf ist der nächste sinnvolle Schritt, er ist noch nicht
  eingerichtet.
