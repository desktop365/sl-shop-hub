# Märkte, Sprachen, Währungen, Vertragsarten

Status: Gerüst. Überschriften stehen, der Feininhalt folgt mit der Markt-Config im Shop-Repo.

Master der Werte ist die Config im Shop-Repo unter config/markets, dieses Dokument beschreibt sie.
Mehrsprachig und mehrmarktfähig ist von Anfang an strukturell angelegt, nicht nachgerüstet.

## 1. Marktliste
| Markt | Status | Sprache | Währung |
|---|---|---|---|
| Deutschland, DE | aktiv | Deutsch | Euro |
| USA, US | vorbereitet, nicht sichtbar | Englisch | US-Dollar |

## 2. Deutschland, aktiv
- Sprache: Deutsch, echte Umlaute.
- Währung und Darstellung: Euro, netto ist B2B-Standard, brutto als Komfortwert.
- Vertragsarten und Laufzeiten: Leasing 15, 24, 32, 36 Monate. Finanzierung 15, 24, 36 Monate.
  Refurbished im Abo, Laufzeiten noch festzulegen.
- Rechtliche Texte: Impressum, Datenschutz, AGB, Widerruf, Versand und Zahlung. Stand noch einzutragen.
- Kontaktdaten: Anschrift, Telefon, Mailadresse für den Markt. Noch einzutragen.

## 3. USA, vorbereitet
- Sprache: Englisch.
- Währung und Darstellung: US-Dollar, Steuerlogik abweichend, noch zu klären.
- Vertragsarten und Laufzeiten: noch festzulegen, DLL-Anbindung für den Markt offen.
- Rechtliche Texte: noch offen.
- Kontaktdaten: noch offen.
- Der Markt ist definiert und deaktiviert, er wird nicht ausgeliefert.

## 4. Was je Markt konfigurierbar ist
Sprache, Währung, Steuerdarstellung, Vertragsarten mit Laufzeiten, rechtliche Texte, Kontaktdaten,
Verfügbarkeit und Preise. Die Felder und ihr Format folgen mit der Config.

## 5. Zusammenspiel
- Preise und Raten je Markt: Bezug zu [DATA-CONTRACT.md](DATA-CONTRACT.md).
- Aktionen je Markt: Geltungsbereich in [PROMOS.md](PROMOS.md).
