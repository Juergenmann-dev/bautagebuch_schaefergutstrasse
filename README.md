# bautagebuch_sch-fergutstrasse
Privates Bautagebuch für die Renovierung Schäfergutstraße. Aufgaben, Kosten, Fotos und Fortschritt für zwei historische Gebäude. Offline-fähige Single-File HTML-App mit Firebase-Authentifizierung.

## Firebase einrichten

1. **Lokale Konfiguration:** `firebase-config.example.js` als `firebase-config.js` kopieren und deine Firebase-Daten eintragen. Die Datei `firebase-config.js` wird nicht ins Repo committed (steht in `.gitignore`).

2. **GitHub Pages:** Im Repo liegt ein Workflow unter `.github/workflows/deploy-pages.yml`. Unter **Settings → Pages** Quelle „GitHub Actions“ wählen. Unter **Settings → Secrets and variables → Actions** ein Secret `FIREBASE_CONFIG_B64` anlegen; Inhalt = **Base64** der kompletten Datei `firebase-config.js` (z. B. lokal: `base64 -i firebase-config.js | pbcopy`). Beim Push wird gebaut und der API-Key kommt nur aus dem Secret, nicht aus dem Repo.

3. **API-Key absichern (wichtig):** In der [Google Cloud Console](https://console.cloud.google.com/apis/credentials) deinen Firebase-/Browser-API-Key öffnen und unter „Anwendungseinschränkungen“ **HTTP-Referrer** wählen. Nur deine Domains eintragen, z. B.:
   - `https://deinname.github.io/*`
   - `http://localhost:*` (für lokales Testen)
   So kann der Key nur von deiner Seite aus genutzt werden, auch wenn er im Frontend sichtbar ist.

### Checkliste (einmalig)

- [ ] **GitHub:** Repo → **Settings → Pages** → Build and deployment: Source = **GitHub Actions**
- [ ] **GitHub:** **Settings → Secrets and variables → Actions** → New repository secret: Name `FIREBASE_CONFIG_B64`, Wert = kompletten Inhalt der Datei `firebase-config.b64.txt` (liegt lokal, wird nicht committed) einfügen
- [ ] **Google Cloud:** [API-Schlüssel](https://console.cloud.google.com/apis/credentials) → deinen Browser-Key → Anwendungseinschränkungen = **HTTP-Referrer**, deine GitHub-Pages-URL + `http://localhost:*` eintragen
- [ ] Optional: `firebase-config.b64.txt` nach dem Eintragen des Secrets lokal löschen
