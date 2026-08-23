> Abgelöst und archiviert. Beschreibt den ersten Anlauf mit FastAPI auf Google Cloud Run aus der AI-Studio-Zeit, keine Vorgabe mehr. Gültig sind LANDKARTE.md, ARBEITSWEISE.md, STATUS.md und die Kontrakte unter contracts. Die wertvollen Teile, Rechenlogik und Anfrage-Logik, stehen jetzt in contracts/PRICING.md und contracts/ANFRAGE.md.

# Kickoff-Prompt für Phase 0, Claude Code

Status: Platzhalter. Der Inhalt folgt, sobald die Entscheidung zum Objektspeicher gefallen ist, siehe
LANDKARTE.md Abschnitt 17, offener Punkt 4, GCS behalten oder zu Hostinger ziehen.

Warum erst dann: der Kickoff legt fest, woher der Shop products.json, images.json und die Bilddateien
liest. Ohne die Entscheidung würde der Prompt einen Pfad vorgeben, der gleich wieder geändert werden muss.

## Was der Prompt später enthalten wird
- Auftrag und Abgrenzung für Phase 0, Fundament nach ARBEITSWEISE.md Abschnitt 8.
- Verweis auf das Hub-Repo als Quelle der Wahrheit, mit den Pfaden zu ARBEITSWEISE.md, LANDKARTE.md und
  den Kontrakten unter contracts.
- Stack und Rahmen: Next.js plus MySQL bei Hostinger, mehrsprachig und mehrmarktfähig von Anfang an.
- Designtokens aus brand, Herz-Logo, Farben, Typo.
- Ablageort für Katalog, Bildschicht und Medien, Ergebnis der Objektspeicher-Entscheidung.
- Leitplanken aus ARBEITSWEISE.md Abschnitt 7, deutsch mit echten Umlauten, keine Secrets im Repo, keine
  internen Preise, nur fertige Monatsraten.
- Abnahmekriterien für Phase 0.
