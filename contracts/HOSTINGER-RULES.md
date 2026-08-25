# Hostinger-MCP, projekt-getrennte Anbindung

Stand: 25.08.2026. Ergänzt INFRA.md Abschnitt 1 um die Frage, wie Claude Code das
Hostinger-Konto anspricht. Jedes Projekt spricht ausschliesslich sein eigenes
Hostinger-Konto an. Kein manuelles Konten-Wechseln, keine Vermischung.

Kontonummern, Ablage der API-Token und offene Rotationen stehen nicht hier, sondern
in der privaten Vollfassung unter VSCode-Configs/_shared/HOSTINGER-RULES.md.

## 1. Prinzip
- Pro Projekt vier Hostinger-MCP-Server im LOCAL Scope, also in `~/.claude.json` unter
  `projects["<projektpfad>"].mcpServers`. Local-Scope-Server laden nur in ihrem Projekt
  und landen nicht im Repo.
- Das Konto hängt am API-Token im `env` des Servers, nicht am Arbeitsverzeichnis. Der
  Token hat laut Paket-Quellcode Vorrang vor OAuth.
- Es gibt bewusst keine globalen Hostinger-Server. Global wäre immer nur ein Konto aktiv,
  wegen der geteilten OAuth-Datei, genau das war die Fehlerquelle.

## 2. Zuordnung Projekt zu Konto
| Projektpfad | Konto | Domains | Bereiche |
|---|---|---|---|
| c:/Dev/Erkenntniswiderspruch | Konto A | erkenntniswiderspruch.de | wordpress, hosting, domains, dns |
| c:/Dev/surface-love-pricing | Konto B | worklove.shop, surface-service.com | wordpress, hosting, domains, dns |

Servernamen je Projekt: `hostinger-wordpress`, `hostinger-hosting`, `hostinger-domains`,
`hostinger-dns`. `command` ist `npx.cmd`, `args` sind `--package=hostinger-api-mcp@latest`
plus das jeweilige `hostinger-<bereich>-mcp`. Im `env` stehen `USER_AGENT` und `PATH` 1:1
aus einem vorhandenen Eintrag, dazu der Token des Kontos.

## 3. Neues Projekt hinzufügen
1. Im hPanel des betreffenden Kontos einen API-Token erzeugen.
2. Im Workspace des Projekts das Token-Popup-Skript ausführen, Token einfügen.
3. Claude Code legt die vier Server im LOCAL Scope dieses Projekts an, Token aus der
   Temp-Datei, `USER_AGENT` und `PATH` aus einem vorhandenen Eintrag übernehmen.
   Temp-Datei danach löschen.
4. Session neu starten, mit `/mcp` prüfen, dass die vier als Projekt-Server erscheinen,
   und mit einem Live-Aufruf prüfen, dass das richtige Konto antwortet.

## 4. Token
Token gehören nie ins Repo, nie in eine Ausgabe, nie in einen Bericht. Wird ein Token
sichtbar, wird er im hPanel rotiert und der alte widerrufen. Das Verfahren und der Stand
offener Rotationen stehen in der privaten Vollfassung.

## 5. Weitere Bereiche
`agency-hosting`, `billing` und `reach` sind eigene MCP-Bereiche desselben Anbieters. Sie
werden bei Bedarf projekt-lokal mit dem passenden Token nachgezogen, nicht global.
