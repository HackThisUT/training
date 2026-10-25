# Andreas Training – PWA

Eine Progressive Web App, optimiert für Safari auf dem iPhone (iOS 16+),
bereitgestellt über **GitHub Pages** unter
`https://<USER>.github.io/<REPO>/`.

## Dateien

| Datei | Zweck |
|---|---|
| `index.html` | App-Shell (alle bisherigen Funktionen erhalten) |
| `manifest.webmanifest` | PWA-Manifest (Name, Icons, Theme) |
| `sw.js` | Service Worker (Offline-Cache + Update-Strategie) |
| `icons/` | PWA- & Apple-Touch-Icons |
| `README.md` | diese Anleitung |

## Auf GitHub Pages veröffentlichen

1. Repository auf GitHub anlegen (z. B. `andreas-training`).
2. Diese fünf Einträge (Ordner `icons/` inklusive) in das **Repo-Root** committen
   (`index.html`, `manifest.webmanifest`, `sw.js`, `icons/`, `README.md`).
3. GitHub → **Settings → Pages** → *Build and deployment* → Source: **Deploy from a branch**,
   Branch: `main`, Folder: `/ (root)`.
4. Nach ca. einer Minute ist die App erreichbar unter
   `https://<USER>.github.io/<REPO>/`.

> **Unterpfad beachten:** Alle Pfade in Manifest & Service Worker sind **relativ**
> (`./`, `./icons/…`), damit die App auch unter
> `https://<USER>.github.io/<REPO>/` korrekt aufgelöst wird.

## Am iPhone installieren

1. In Safari `https://<USER>.github.io/<REPO>/` öffnen.
2. Unten mittig auf das **Teilen-Symbol** tippen.
3. *„Zum Home-Bildschirm"** auswählen, Name bestätigen, **Hinzufügen**.
4. Die App startet dann im **Standalone-Modus** (ohne Safari-Leiste).

Der dezente Hinweis-Banner in der App erscheint nur, solange man sie nicht
über den Home-Bildschirm geöffnet hat. Mit **OK** wird er ausgeblendet
(`localStorage.andreasIosHintDismissed = "1"`).

## Daten & Backup

- Alle Daten liegen lokal im **localStorage** (`andreasKompassV2`).
- Über die Symbole **↥ Export** und **↧ Import** in der Kopfzeile kann
  jederzeit ein JSON-Backup erzeugt bzw. wieder eingespielt werden.
- Vor Updates / Gerätewechsel unbedingt **Export** nutzen und das
  `andreas-kompass-v2.json` sicher aufbewahren.

## Cache-Update bei neuen Versionen

Der Service Worker verwendet eine **Versionskonstante** `CACHE_NAME` in
`sw.js`. Bei jeder Änderung an App oder Icons:

1. `sw.js` öffnen.
2. `const CACHE_NAME = 'andreas-pwa-v1';` → z. B. auf `v2` erhöhen.
3. Commit & push – beim nächsten App-Start wird der alte Cache gelöscht
   und die neue Version geladen. Es erscheint kurz der Toast
   „Neue Version verfügbar – neu laden".

## Lokal testen

```bash
# beliebiges statisches Tool, z. B.:
python3 -m http.server 8080
# dann http://localhost:8080/ im Browser öffnen
```

> **Hinweis:** Service Worker registrieren sich nur über `http(s)://`,
> nicht über `file://`.

## Browser-Support

- iOS Safari 16.4+ für volle PWA-Funktionen (Standalone, Add to Home).
- Aktuelle Chrome / Edge / Firefox für `manifest.webmanifest` & SW.
