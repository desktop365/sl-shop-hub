# Infrastruktur, die Umgebung schwarz auf weiß

Hält fest, was wo läuft, damit kein Chat mehr rät. Ergänzt LANDKARTE.md Abschnitt 14 um die konkreten Projekte, Buckets, Zugänge und Domains.

## 1. Hosting, die neue App
- Hostinger, Business-Tarif, gemanagtes Node-Hosting, Server in Frankfurt, IP 92.113.22.128.
- App surface-love-shop, Next.js, verbunden mit GitHub, Auto-Deploy bei jedem Push auf main.
- Datenbank MySQL u704706543_shop2, auf demselben Server, Verbindung über 127.0.0.1, nicht localhost.
- Verwaltung aus Claude Code über das Hostinger-Plugin.
- Arbeitsadresse worklove.shop, live mit Zertifikat. surface-service.com registriert, im Review.

## 2. Google Cloud, zwei Projekte, klar getrennt
- Projekt slshopv2, Projektnummer 197908221956. Enthält nur den Bucket slshopv2-media in europe-west2. Er hält die Medien und die Live-Dateien products.json und images.json. Der neue Shop liest von hier über GCS_BASE_URL. Das bleibt.
- Projekt slwebai26. Enthält den alten AI-Studio-Shop als Cloud-Run-Dienst in europe-west1. Genau dieser Dienst läuft heute noch unter surface.love. Bleibt live bis zum Umschalten. Offen, Gemini-API-Schlüssel aus dem Privatkonto hierher migrieren.

## 3. Der GCS-Schreibzugang
- Die Preis-Pipeline und die Bild-Pipeline schreiben in den Bucket slshopv2-media.
- Empfehlung, ein dedizierter Service-Account im Projekt slshopv2 mit Schreibrecht nur auf diesen Bucket, Schlüssel nur als Secret der Pipeline, nie im Repo.
- Der Shop hat nur Lesezugriff über die öffentliche URL, keinen Schreibzugang.

## 4. Cloudflare
- Cloudflare ist die Kante für surface.love, DNS, CDN, WAF, und das Turnstile-Widget.
- Aktueller Stand, CNAME www auf ghs.googlehosted.com, DNS only, Apex per Weiterleitung auf www. Zeigt also auf den alten Cloud-Run-Shop.
- surface.love bleibt bei Cloudflare.
- Turnstile-Widget, Modus Managed, gegen Spam am Anfrage-Endpunkt, siehe ANFRAGE.md.

## 5. Der Umschaltweg, später
Wenn der neue Shop steht, wandert surface.love bei Cloudflare vom alten Cloud-Run-Dienst auf die Hostinger-App, sonst nichts. Der alte Shop und das Projekt slwebai26 können danach stillgelegt werden. Bis dahin unberührt.

## 6. Öffentliche Aufrufe
- Medien und Daten, https://storage.googleapis.com/slshopv2-media/... , ohne End-Slash in GCS_BASE_URL.
- Bilder je Datei, https://storage.googleapis.com/slshopv2-media/images/{Dateiname}.
