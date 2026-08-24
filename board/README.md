# Projekt-Board, Melde-Regel

## Quelle der Wahrheit
board/board.json in diesem Repo. Das Dashboard im Master-Chat liest die Datei
ueber die raw-URL und rechnet Fortschritt, Jetzt dran und Wartet selbst aus.
Niemand zaehlt von Hand.

## Felder je Aufgabe
id, phase, titel, owner, status, haengt_von (Liste von ids), notiz,
gemeldet_von, datum. Status ist genau einer aus: offen, laeuft, geliefert,
erledigt, blockiert. geliefert heisst uebergeben und wartet auf Abnahme,
erst erledigt loest Abhaengigkeiten.

## Owner-Kuerzel
master (Master-Chat), katalog (Preislisten-Chat), design (Design-Strang),
code (Claude Code), sascha, betrieb, ziel (Meilenstein).

## Wer meldet wie
- Claude Code aktualisiert am Ende jedes Laufs die betroffenen Eintraege
  direkt in board/board.json (Status, notiz, gemeldet_von, datum) und
  committet sie mit den uebrigen Aenderungen. Er ist der Haupt-Schreiber.
- Chats ohne Git-Zugang (Design-Strang, Preislisten-Chat) geben am Ende
  einer Lieferung einen Meldeblock im Format unten aus. Sascha traegt ihn
  ein, oder der naechste Claude-Code-Lauf uebernimmt ihn.
- Der Master-Chat pflegt die Struktur: Aufgaben, Owner, Abhaengigkeiten,
  Phasen, und aktualisiert bei Planaenderungen.
- Der Betrieb meldet erledigte Tests und kaufmaennische Schritte.

## Meldeformat, genau diese fuenf Zeilen
MELDUNG BOARD
aufgabe: <id>
status: <neuer Status>
was: <ein Satz, was geliefert oder erledigt wurde>
von: <owner-Kuerzel>
