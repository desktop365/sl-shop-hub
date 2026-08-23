# Anfrage-Kontrakt, Endpunkt und Schlüssel

Maßgeblich für die Anfrage-Logik des Neu-Zweigs. Die Logik stammt aus dem ersten Anlauf, früher KONZEPT.md Abschnitt 11. Sie gilt unverändert, nur das Ziel ist jetzt die Hostinger-Node-App als Next.js-API-Route, nicht mehr ein FastAPI-Dienst auf Cloud Run.

## Stand, ehrlich
Ablauf und Schlüssel sind vollständig entworfen, aber der Endpunkt ist im neuen Stack noch nicht gebaut. Die zugehörigen Apps und Zugänge, die HubSpot-Private-App, die Graph-App-Registrierung und das Turnstile-Widget, müssen für den neuen Auftritt geprüft oder neu erstellt und die Schlüssel als Umgebungsvariablen der Hostinger-App gesetzt werden.

## 1. Zweck
Der Neu-Zweig verkauft nicht, er nimmt eine unverbindliche Anfrage entgegen. Aus einer Anfrage entsteht ein Deal in HubSpot und eine Mail an Sales. Kein Warenkorb-Kauf, keine Zahlung, kein Kundenkonto.

## 2. Ablauf des Endpunkts /api/anfrage
1. Eingaben validieren.
2. Turnstile serverseitig prüfen, bei Fehlschlag 400.
3. HubSpot, nur wenn aktiviert, Kontakt upserten und Deal anlegen, Fehler nur loggen.
4. Mail über Microsoft Graph, nur wenn aktiviert, Token holen, sendMail an das interne Ziel.
5. Sobald Validierung und Turnstile in Ordnung sind, immer mit 200 und der Anfrage-ID antworten, auch wenn HubSpot oder Mail intern scheitern. Diese beiden dürfen die Antwort an den Browser nie kippen.
6. Der Vorgang wird zusätzlich im Anfragen-Log der Datenbank festgehalten, siehe DB-SCHEMA.md Abschnitt 2.5.

Anfrage-ID-Format, SL-JJJJMMTT-XXXXXX, sechs hexadezimale Großbuchstaben, siehe DETAILS.md. Marke, Storefront, Markt und Lane gehen aus der erkannten Domain mit an Deal und Log.

## 3. HubSpot, zwei Zugänge
- MCP im Betriebs-Cowork, für die tägliche Arbeit am CRM durch dich und die Agenten.
- API-Token aus dem Shop, mit dem der Anfrage-Endpunkt automatisch den Deal anlegt. Das ist ein eigener Private-App-Token, getrennt vom MCP.

HubSpot ist nachgelagert, keine Preisquelle. Der Shop-Deal landet in der SL-Pipeline auf der Stufe Shop Anfrage, siehe HUBSPOT.md.

## 4. Umgebungsvariablen, Schlüssel
Werte nur als Umgebungsvariable der Hostinger-App, nie im Repo, nie öffentlich, außer dem öffentlichen Turnstile-Sitekey.
- GRAPH_TENANT_ID, GRAPH_CLIENT_ID, GRAPH_CLIENT_SECRET, für den App-only-Mailversand über Graph.
- MAIL_SENDER, technischer Absender shop@surface.love, nie angezeigt. MAIL_TO, Ziel sales@surface.love. MAIL_ENABLED.
- HUBSPOT_ACCESS_TOKEN, der Private-App-Token. HUBSPOT_ENABLED. HUBSPOT_PIPELINE_ID, die SL-Pipeline. HUBSPOT_DEAL_STAGE_ID, Standard Shop Anfrage, Wert 5550972114.
- TURNSTILE_SECRET, plus der öffentliche Turnstile-Sitekey.

Reply-To der Antwortmails ist sales@surface.love, siehe DETAILS.md.

## 5. Zu tun im neuen Stack
- Endpunkt als Next.js-API-Route bauen, inhaltlich wie oben.
- HubSpot-Private-App im Portal 145452563 anlegen oder prüfen, Token setzen.
- Graph-App-Registrierung für shop@surface.love prüfen oder anlegen, App-only-Berechtigung Mail.Send, Zustimmung erteilen.
- Turnstile-Widget prüfen, Hostnamen um worklove.shop und surface.love ergänzen.
