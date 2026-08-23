# Designsprache und Tokens

Ruhig, premium, minimalistisch. Grosszuegige Weissraeume. Genau eine Hauptaktion je Bildschirm.

## Farben und Rollen
- Cyan #00A3E0 (PANTONE 299 C) ist der EINZIGE Akzent. Nur drei Dinge duerfen cyan sein:
  der aktive Schritt, die Rate "ab X pro Monat", der primaere Button. Dadurch sticht das Wesentliche heraus.
- Text: Tinten-Schwarz #1A1A1A, Sekundaertext Grau #6B6B70.
- Reines Schwarz #000000 (PANTONE Black 6 C) nur fuer Logo und Wortbild-Ersatz.
- Flaechen: Weiss #FFFFFF, Sektionen sehr helles Grau #F5F6F7, Linien #E6E7E9.
- Status als kleiner Punkt, nie cyan: gruen verfuegbar, bernstein im Zulauf, grau auf Anfrage.
- Hinweis: die Herz-SVG nutzt minimal abweichend #00A3DE. Verbindlich ist #00A3E0, im App-Einsatz
  ueber currentColor faerben.

## Typografie
- Hausschrift laut Farbwelt: Segoe Pro (Light, Semibold).
- Web-Stapel: "Segoe UI Variable", "Segoe UI", system-ui, -apple-system, BlinkMacSystemFont, Roboto,
  "Helvetica Neue", Arial, sans-serif. Auf Windows rendert echtes Segoe, markennah und kostenlos.
- Gewichte: 300 Light fuer grosse Ueberschriften, 400 Fliesstext, 600 Semibold fuer Buttons und Hervorhebung.
- Schriftgroessen grosszuegig: Display 40 bis 56, H1 32, H2 24, H3 20, Body 16 bis 17, Klein 14.

## Form, Raum, Bewegung
- 8er-Raster, weiche Ecken um 14px, sehr sparsame Schatten nur an schwebenden Elementen.
- Buttons: genau ein primärer pro Bildschirm, cyan gefüllt, Semibold. Daneben höchstens ein dezenter
  sekundaerer als Outline.
- Bewegung zurueckhaltend. Herz: Doppel-Herzschlag, sanfter Skalierungspuls alle rund 3,5s, beim
  Ueberfahren ein einzelner Schlag. Kann zugleich Ladeindikator sein. Rate zaehlt beim Umschalten sanft hoch.
