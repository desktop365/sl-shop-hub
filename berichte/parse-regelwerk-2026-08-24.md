# Parse-Regelwerk, MSKU zu Modellreihe und Attributen

Vorlage des Preislisten-Chats fuer v2, Zuordnungsschicht nach VARIANTEN.md.
Grundlage ist der Sortiments-Abruf vom 24.08.2026, 145.487 Zeilen. Alle
Zahlen sind gemessen, nicht geschaetzt. Enthaelt keine Preise.

## 1. Grundsaetze
- Nie raten. Ein Attribut, das nicht sicher erkannt wird, bleibt leer.
- Faellt eine MSKU durch, erscheint sie einstufig mit Rohnamen, nie gar nicht.
- Kuration uebersteuert das Parsen immer, nie umgekehrt.
- Das Regelwerk ordnet nur an, es rechnet nie. Raten kommen je MSKU aus
  products.json.
- Regeln sind versionierte Konfiguration, kein fest verdrahteter Code.

## 2. Gemessene Grundlage
| | Microsoft | Lenovo mobil |
|---|---|---|
| Geraete im Zuschnitt | 444 | 413 |
| Titel mit Bildschirmgroesse | 420 von 440 | 412 von 413 |
| Titel mit RAM- und Speichermuster | hoch | 410 von 413 |
| Titel mit Generationskennung | ueber Reihenname | 412 von 413 |
| Titel mit Farbe | 287 von 503 | 0 von 413 |
| Titel mit CPU nach Standardmuster | hoch | 269 von 413 |

## 3. Regelwerk Microsoft
Reihe aus dem Namen, Surface Laptop, Surface Pro, Surface Go, Surface
Laptop Studio, Surface Hub. Generation als angehaengte Ziffer, Laptop8,
Pro12. Fehlt sie, bleibt die Generation leer, nicht 1.
Bildschirmgroesse aus dem Zollzeichen, Dezimaltrenner Komma oder Punkt.
Prozessor aus Kuerzeln, CU5 und CUX5 ergeben Core Ultra 5, CU7 und CUX7
Core Ultra 7, Elite Snapdragon X Elite, Plus Snapdragon X Plus, SQ3
Microsoft SQ3, N200 Intel N200.
Hauptspeicher folgt unmittelbar dem Prozessorkuerzel, Speicherkapazitaet
aus den uebrigen GB- und TB-Angaben, hoechster plausibler Wert.
Farbe im Klartext, Platinum wird Platin, Black Schwarz, Graphite Graphit.
Betriebssystem aus W11P, W11H, W10P.
Zusatzmerkmale, 5G aus dem Titel, ohne Netzteil aus o.Netz und Varianten.

## 4. Regelwerk Lenovo
Reihe aus dem fuehrenden Token nach dem Herstellernamen. Gemessen,
ThinkPad 289, TP als Kurzform 51, ThinkBook 37, V-Serie 22, Tab und
ThinkTab 10.
Wichtig, TP ist dieselbe Reihe wie ThinkPad und muss normalisiert werden,
sonst entstehen zwei Reihen fuer dieselben Geraete.
Generation aus dem Muster G gefolgt von einer Ziffer, 412 von 413.
Bildschirmgroesse aus dem Zollzeichen, Dezimaltrenner Komma oder Punkt.
Hauptspeicher und Speicherkapazitaet aus dem Muster Zahl Schraegstrich
Zahl, 410 von 413. Links der Hauptspeicher in GB, rechts die
Speicherkapazitaet, dreistellig in GB oder mit TB-Suffix.
Prozessor ueber eine erweiterbare Nachschlagetabelle, nicht ueber ein
einzelnes Muster. Ein Standardmuster trifft nur 269 von 413. Nicht
getroffen werden unter anderem RAI7P-350 und RAI-7-P-350, R5-P-215,
R7-P-250, UX7-358H, U300, sowie Helio G85, D6300, D8300 und D6400 bei
Android-Geraeten. Diese Schreibweisen gehoeren als Eintraege in die
Tabelle, damit sie ohne Codeaenderung ergaenzbar sind.
Panel aus WUXGA, FHD, 2.8K, 3K, 2,5K, WQXGA. Grafik aus RTX- und
Radeon-Angaben. Konnektivitaet aus 4G und 5G.
Betriebssystem aus W11P, W11H, FreeDos, Android.

## 5. Farbe, ein Befund mit Folgen fuer SICHTBARKEIT.md
Kein einziger der 413 Lenovo-Titel traegt eine Farbe. Die
Alternativen-Rangfolge des spaeten Checks beginnt mit anderer Farbe.
Fuer Lenovo ist diese Stufe nicht befuellbar. Vorschlag, die Rangfolge
formuliert die Farbstufe als bedingt, faellt sie aus, ruecken
Speicherkapazitaet und Hauptspeicher auf. Fuer Microsoft bleibt die
Rangfolge unveraendert.

## 6. Faelle, die Kuration brauchen
- Zwoelf Microsoft-Handelsartikel verkuerzen sich auf sechs Anzeigenamen.
  Verschiedene EAN, also echte Artikel, kein Entfernen. Das unterscheidende
  Merkmal fehlt im Titel und muss im Anzeigenamen ergaenzt werden.
- 20 von 440 Microsoft-Geraeten ohne Bildschirmgroesse im Titel.
- Die Zeichenfolge BW in elf Lenovo-Titeln ist ungeklaert. Nicht raten,
  bis der Distributor sie erklaert.
- Android-Tablets der Reihen Tab, Idea Tab und ThinkTab liegen in den
  Kategorien TPC und TPG, tragen aber Android statt Windows. Ob sie in
  einen B2B-Leasingshop gehoeren, ist eine kaufmaennische Frage, offen.
- Zubehoer bleibt einstufig, keine Reihe, keine Varianten.

## 7. Was die Nachtmessung praezisiert
Zwei Messungen des Laufs vom 25.08. koennen dieses Regelwerk verbessern.
Ob description strukturierte Angaben traegt, dann verschiebt sich Arbeit
vom Titel in ein sauberes Feld. Und wie viel Struktur der Titel ohne den
Filter CLEANUP_PRODUCT_TITLE zurueckgewinnt, gemessen wurden Klammern und
Schraegstriche bei 23 von 440 Microsoft-Geraeten.
