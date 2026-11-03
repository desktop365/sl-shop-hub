# AENDERUNGEN v9 gegenüber v8

Stand 09.09.2026, Paket surface-love-prototyp-v9, selbstlauffähig (index.html, OFFLINE-Schalter aktiv, keine externen Abhängigkeiten). Basis v8, unangetastet.

## Aufgabe A, Mengenstaffel entfernt

- Der Block "mengenstaffel" (ab 5 Geräten, Faktor 0,95) ist ersatzlos aus dem Demo-Datenblock gestrichen, keine Ersatz-Staffel.
- Der Anzeigemechanismus bleibt vollständig im Code: sofortiges Zählen der Summenleiste, Mikrozeile unter der Rate (max. 200 ms), Nachzählen mit Hinweis bei Serverabweichung, Sequenzschutz. Er hat im Demo-Datenstand nur keinen Auslöser mehr (serverRate == lokale Summe); die Hinweis-Referenz ist gegen den fehlenden Block abgesichert.

## Aufgabe B, freigegebene Texte (wörtlich, nur im Datenblock)

- Alle zehn Bausteine tragen die freigegebenen Titel, Nutzen-Sätze und Nebenzeilen (Surface Slim Pen, Tastatur mit Trackpad, Surface Dock, Copilot, Business Standard/Premium, Garantie plus ein/zwei Jahre, Managed Workplace "wir verwalten" / "in Ihrer Umgebung"). Keine Zahl in Nutzen- und Mehrwertsätzen, keine Redaktionsvermerke.
- garantie_2: der Laufzeitbezug ("passend zu drei Jahren Laufzeit") erscheint nur bei Laufzeit 36 Monate (Feld nebenzeile_36, Kontext-abhängig gerendert).
- Copilot: Oder-Voraussetzung (Standard ODER Premium) neu im Datenmodell (benoetigt_oder). Hinweiszeile wörtlich "Setzt Microsoft 365 Business Standard oder Premium voraus, wird mit ausgewählt." Zuwahl ohne Lizenz wählt Business Standard sichtbar mit; Abwahl der letzten Lizenz wählt Copilot mit ab. Tastatur bleibt auf die Reihe Pro begrenzt (in Laptop-Reihen nicht gerendert).
- Managed: Hinweiszeile "Setzt Microsoft 365 Business Premium voraus, wird mit ausgewählt."; bei Abwahl der Voraussetzung wörtlich "Ohne Microsoft 365 Business Premium entfällt Managed Workplace." Lenovo behält eigene Bausteintitel und die lenovo.online-Tenant-Nebenzeile.
- Mehrwertsätze der Stufenwahl je Reihe (pro, laptop, ultra) im Datenblock; die Ultra-Sätze liegen bereit, die Reihe ist nicht bestellbar. Die Sätze sind freigegeben und tragen keine Demo-Kennzeichnung; Deltas bleiben Demo-gekennzeichnet.
- Schnellweg: Erklärzeile "Wählt alle empfohlenen Bausteine. Jede Zeile lässt sich einzeln wieder abwählen.", Aktion je Positionszeile "Entfernen".
- Kuration neu, Etikett überall exakt "Empfohlen": pen und tastatur nur in Reihe Pro, m365_premium in allen Reihen und Stufen, garantie_2 nur bei Laufzeit 36 Monate, managed_a in den Reihen Laptop und Pro. Empfehlungen sind jetzt Regeln im Datenblock (ids, optional reihen, laufzeit), nicht mehr eine Einzel-Id je Kategorie.

## Aufgabe C, "Im Paket enthalten" (Refurbished-Detailseite)

- Neue Sektion unter der Gerätegalerie, über den Zusatzoptionen: halbfette Satzschreibungszeile "Im Paket enthalten" (kein Versalien-Etikett) mit dem Satz "Dieses Gerät kommt mit geprüftem Zubehör, jedes Teil mit eigenen Bildern." Bestandsinformation, keine Verkaufsfläche: Kacheln ohne Preis und ohne Schalter, Gerätegalerie bleibt sortenrein.
- Kacheln: Thumbnail 80 px plus Name, "2×" bei Mehrfachstücken, ganze Kachel klickbar, 44-px-Trefferfläche im Halo-Muster, sichtbarer Fokusring (:focus-visible).
- Klick öffnet das vorhandene Blatt-Muster: mobil als ziehbares Bottom Sheet mit Griffleiste (30-%-Schwelle, Wisch, Rückfeder), auf Desktop seitlich. Inhalt: Titel, eigene Galerie NUR dieses Zubehörs (main plus gallery), Zustandszeile "Geprüfter Rückläufer". Kein Preis, keine Aktion außer Schließen; Schließen kehrt exakt an die Scrollposition zurück.
- Galerie-Chrome wächst mit dem Bildbestand: ein Bild ohne Pfeile/Punkte/Thumbleiste, ab zwei Bildern Punkte, ab vier zusätzlich Thumbleiste. Fehlt das Bildmodell komplett, rendert die Kachel als Textchip mit Name und Menge, ohne Bildfläche.
- Daten: enthalten_zubehoer am Refurbished-Angebot (bildmodell_id, titel, titel_kurz, menge); Bildmodelle im Demo-Datenblock (zubehoer_bildmodelle): dockingstation EIN Bild, dock-2 ZWEI Bilder, slim-pen EIN Bild (Menge 2), neutrale Offline-Platzhalter. Demo: Surface Pro 9.
- Sichtbarkeit außerhalb: Typ-Karte der Refurbished-Liste mit einer Textzeile "inkl. Dock, Dock 2, 2× Slim Pen"; Positionslisten von Kasse und Ausstattungs-Summenleiste zeigen das Zubehör als Unterzeilen der Geräteposition ohne eigene Beträge.
- Messpunkt: data-mess="zubehoer_galerie" mit data-mess-zubehoer-id am Kachel-Klick.

## Bewusst nicht angefasst

Alle Seiten und Flüsse aus v7/v8, Systemsprache (150/260/550 ms, eine Ease, Federn nur an kleinen Objekten), Zählmoment exklusiv in der Summenleiste, stille Karten, Reduced-Motion-Neutralisierung, die vier freigegebenen Kampagnentexte (wortgleich), Demo-Kennzeichnung aller Zahlen, Refurb- und Fokus-Regeln, beide Marken aus demselben Markup.

## Bewusste Abweichungen

- Zum Nachweis des Textchip-Falls (fehlendes Bildmodell) trägt der Demo-Datensatz Surface Pro 8 32 GB ein Zubehör "Netzteil 65 W" ohne Bildmodell. Reiner Demo-Datensatz, kein neues Feature.
- Copilot behält zusätzlich den Zustand "bedingt ab advanced" aus bk1 (über den Demo-Schalter erlebbar); die neue Oder-Voraussetzung ergänzt ihn, ersetzt ihn nicht.
- Die Mehrwertsätze ersetzen die bisherigen Demo-Sätze mit Zahlen ("plus 8 € im Monat: 32 GB…") vollständig — Kriterium "keine Zahl im Mehrwertsatz".
