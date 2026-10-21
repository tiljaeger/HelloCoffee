# Arbeitsablauf für HelloCoffee

Diese Anweisungen gelten für das gesamte Repository und für alle Coding-Agenten, die daran arbeiten. Explizite Anweisungen des Nutzers haben Vorrang.

## Aufgaben und Issues

- Für jedes größere Feature und jeden Fehler dient möglichst ein eigenes GitHub Issue als Aufgabenbeschreibung. Kleine Änderungen können direkt im Chat beauftragt werden; ein Issue ist keine Voraussetzung.
- Ein Issue sollte Ziel, gewünschtes Verhalten und überprüfbare Akzeptanzkriterien enthalten. Fehlende Details soweit möglich aus dem Projekt ableiten; nur bei wesentlichen Unklarheiten nachfragen.
- Ein übergebenes Issue vor der Umsetzung lesen und die Arbeit auf dessen Umfang begrenzen. Keine zusätzlichen Issues oder Kommentare ohne Auftrag veröffentlichen.

## Branch, Umsetzung und Prüfung

1. Arbeitsverzeichnis und vorhandene Änderungen prüfen. Fremde Änderungen erhalten.
2. Für eine neue Aufgabe einen eigenen Branch auf Basis des aktuellen `origin/main` anlegen, zum Beispiel `feat/12-dark-mode`, `fix/15-button` oder `docs/agent-workflow`. Bei Fortsetzung eines bestehenden Pull Requests dessen Branch verwenden. Nicht direkt auf `main` committen oder pushen.
3. Den vorhandenen Checkout verwenden. Cloud-Aufgaben sind bereits isoliert; keinen zusätzlichen Git-Worktree ohne ausdrücklichen Auftrag anlegen.
4. Die Änderung gezielt umsetzen und betroffene Dokumentation aktualisieren. Keine Zugangsdaten, `node_modules`, Build-Ausgaben oder lokale Konfiguration committen.
5. Änderungen passend prüfen. Für Änderungen an Anwendung, Abhängigkeiten oder Build-Konfiguration `mvn package` und `npm run build:worker` ausführen. Bei verändertem Seitenverhalten zusätzlich mit `npm run dev` starten und die betroffene Funktion prüfen. Ein Build allein ersetzt keinen Funktionstest. Für reine Dokumentationsänderungen Inhalt und `git diff --check` prüfen; keine unnötigen Builds ausführen.
6. Ergebnisse ehrlich dokumentieren: bestandene, fehlgeschlagene und nicht ausführbare Prüfungen unterscheiden. Relevante Fehler untersuchen und beheben oder als konkrete Einschränkung melden.

## Commit und Pull Request

- Änderungen mit einer kurzen, aussagekräftigen Commit-Nachricht committen. Eine vom Nutzer vorgegebene Nachricht exakt übernehmen.
- Bei beauftragter Umsetzung den Aufgabenbranch nach GitHub pushen und einen Pull Request gegen `main` erstellen, sofern der Nutzer die Arbeit nicht ausdrücklich auf lokale Änderungen beschränkt.
- Der Pull Request beschreibt Problem, Änderung und tatsächlich ausgeführte Prüfungen. Wenn ein Issue vollständig gelöst wird, `Closes #<Nummer>` in die Beschreibung aufnehmen; ansonsten das Issue nur referenzieren.
- Den Pull-Request-Link und relevante Einschränkungen zum Abschluss nennen. Fehlt API-Zugriff für die PR-Erstellung, den erreichten Stand und den konkreten nächsten Schritt melden; keinen erstellten PR behaupten.
- Pull Requests zur Prüfung durch den Nutzer offen lassen. Nur nach ausdrücklichem Auftrag mergen. Keine Force-Pushes auf `main`.
- Deployment auf Cloudflare ist ein eigener Schritt und erfolgt nur auf ausdrücklichen Auftrag. `npm run build:worker` ist ein Dry-Run und veröffentlicht nichts.

## Projektbefehle

Voraussetzungen und Deployment stehen in `README.md`. Node.js ab 22, Java ab 17 und Maven 3.9.x verwenden.

- `mvn package`: gesperrte npm-Abhängigkeiten installieren, Webseite bauen und ZIP paketieren.
- `npm run build:worker`: Cloudflare Worker und Assets für ein Deployment prüfen.
- `npm run dev`: lokalen Worker für Entwicklung und Funktionstests starten.

In der vorbereiteten Cloud-Umgebung, falls vorhanden, zuerst `source /workspace/.tools/hellocoffee-env.sh` ausführen. Dies aktiviert Maven sowie die dort benötigten Proxy- und Cache-Einstellungen. Keine Cloud-spezifischen Pfade als allgemeine Voraussetzung für lokale Entwicklung voraussetzen.
