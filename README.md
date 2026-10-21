# HelloCoffee

Eine JavaScript-Webseite, die `HelloCoffee` ausgibt. Ein Cloudflare Worker liefert die statischen Dateien aus.

## Voraussetzungen

- Node.js ab Version 22 mit npm
- Java ab Version 17 und Maven 3.9.x für den Maven-Build
- Ein Cloudflare-Konto nur für die Veröffentlichung

## Mit Maven bauen

```sh
mvn package
```

Maven installiert die festgeschriebenen npm-Abhängigkeiten mit `npm ci`, baut die Webseite nach `target/site` und erstellt `target/hello-coffee-1.0.0-site.zip`.

## Lokal entwickeln

```sh
npm ci
npm run dev
```

Wrangler baut die Webseite automatisch vor dem Start und liefert sie lokal auf Port 8787 aus. Änderungen unter `public/` werden durch den Build von Wrangler übernommen.

## Cloudflare-Worker bauen

```sh
npm ci
npm run build:worker
```

Dieser Dry-Run prüft und bündelt den Worker unter `target/worker`, ohne etwas zu veröffentlichen. Die statischen Dateien liegen unter `target/site`.

## Bei Cloudflare veröffentlichen

```sh
npx wrangler login
npm run deploy
```

Wrangler baut die Webseite und veröffentlicht den Worker mit den statischen Dateien. Die öffentliche `workers.dev`-Adresse wird nach erfolgreichem Deployment ausgegeben. Für CI können stattdessen `CLOUDFLARE_API_TOKEN` und `CLOUDFLARE_ACCOUNT_ID` sicher in der CI-Umgebung hinterlegt werden. Zugangsdaten nicht ins Repository schreiben.

Der Worker-Name kann in `wrangler.jsonc` angepasst werden. Für eine eigene Domain muss zusätzlich eine Domain im Cloudflare-Konto konfiguriert werden.

## Aufbau

- `public/index.html`: Seite mit sichtbarem Text, auch ohne JavaScript
- `public/app.js`: setzt den Text per JavaScript
- `scripts/build.mjs`: kopiert die Webseite nach `target/site`
- `worker/index.js`: leitet Anfragen an Cloudflare Static Assets weiter
- `pom.xml`: Maven-Build und ZIP-Paketierung
