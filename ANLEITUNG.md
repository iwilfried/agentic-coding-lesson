# Agentic Coding · Mini-Lesson (PWA)

**Learning Factory** · Mobile Lern-App mit 6 Kurzlektionen, Kurz-Checks, Praxisaufgabe, Abschlussquiz und Spickzettel.
Installierbar wie eine App, läuft offline.

```
agentic-coding-lesson/
├── index.html              ← App-Shell (Ansichten, Quiz-Logik, Fortschritt)
├── lesson.js               ← alle Inhalte (Lektionen, Quiz, Spickzettel)
├── manifest.webmanifest    ← PWA-Metadaten
├── sw.js                   ← Service Worker (Offline-Cache)
├── icon-192.png / icon-512.png / icon-maskable-512.png
└── ANLEITUNG.md            ← dieses Dokument
```

## Lokal testen

```bash
cd agentic-coding-lesson
python -m http.server 5500
```

Öffnen: <http://localhost:5500>. Hinweis: Manche Ports (z. B. 8765) sind unter Windows durch Hyper-V reserviert
und liefern `WinError 10013`. Dann einfach einen anderen Port nehmen.

## Veröffentlichen

Eine PWA mit Offline-Funktion braucht **HTTPS**. Wie beim Glossar geht das z. B. über GitHub Pages, Netlify oder Cloudflare Pages:
Ordnerinhalt hochladen, den Link an die Studierenden geben. Auf dem Handy:

- **iPhone (Safari):** Teilen → „Zum Home-Bildschirm“
- **Android (Chrome/Edge):** Button „Als App installieren“ in der App oder Browser-Menü → „App installieren“

## Inhalte ändern

Alles steht in `lesson.js`. Schritt-Typen:

| Typ | Felder |
|---|---|
| `text` | `title`, `html` |
| `quiz` | `q`, `options`, `correct` (Index ab 0), `explain` |
| `task` | `title`, `html` (Praxisaufgabe am eigenen Rechner) |

Fortschritt und Quiz-Bestwert werden pro Gerät im Browser gespeichert (`localStorage`). Es werden keine Daten an einen Server gesendet.

## Updates ausrollen

Bei jeder Änderung an `index.html`, `lesson.js` oder den Icons in `sw.js` die `CACHE_VERSION` hochzählen
(z. B. `v1.0.0` → `v1.0.1`). Sonst sehen installierte Apps eventuell noch den alten Stand.
