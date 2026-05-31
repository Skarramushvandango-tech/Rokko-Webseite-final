# Rokko! Records — Regeln für Entwickler

> **Stand: 31.05.2026 — verbindlich.** Diese Datei ist die maßgebliche Spezifikation.
> Bei Widerspruch zwischen Code und dieser Datei gilt diese Datei.

---

## ⛔ FÜR KI-AGENTEN (Replit Agent, Claude, GPT, etc.)

**NIEMALS `dist/` direkt bearbeiten, neu bauen oder committen.**

`dist/` steht in `.gitignore` — es wird NICHT in git getrackt.
GitHub Pages baut bei jedem Push auf `main` automatisch neu (mit `BASE_PATH=/rokko-web/`).
Ein manueller Build ohne diese Variable erzeugt eine kaputte Seite mit 404-Fehlern.

### Was du als Agent NICHT tun darfst:
- `npm run build` / `pnpm run build` ausführen und das Ergebnis committen
- Dateien in `dist/` direkt bearbeiten oder löschen
- `.gitignore` ändern um `dist/` wieder zu tracken

### Was du stattdessen tust:
- Nur `src/`, `index.html`, `public/`, `scripts/`, `package.json`, `tsconfig.json` bearbeiten
- Änderungen committen — GitHub Actions übernimmt Build + Deploy automatisch

---

## Absolute Verbote (niemals ändern)

1. **::before Pseudo-Elemente**
   - NIE `::before` oder `::after` auf `.artists-section` oder `.artist-grid` hinzufügen.
   - Diese erzeugen rote/schwarze Balken.

2. **wirsindrokko.png Abstand**
   - NIE den Abstand UNTER `wirsindrokko.png` entfernen oder verändern
     (`padding-bottom: var(--section-gap)` muss erhalten bleiben).
   - Der schwarze Hintergrund der `.artists-section` (`rgba(0,0,0,0.6)`) MUSS bündig
     an `wirsindrokko.png` anliegen — d. h. `.wirsindrokko-wrap` hat KEIN `padding-top`.

3. **Video-Header (oben, schwarz)**
   - NIE Loop, Controls oder Play-Button zum Video-Header hinzufügen.
   - Kein `controls`, kein `loop`, kein `muted` entfernen.

4. **Artist-Popups**
   - NUR Spotify, Apple Music, Amazon in den Streaming-Links.
   - KEINE SoundCloud, Beatport, YouTube, TikTok, Facebook Links.

---

## News-Feld (verbindliches Layout — Vorlage: `optischesmaster.png`)

Maßgeblich ist `public/assets/banners/optischesmaster.png`. Das News-Feld besteht aus
EINEM roten Rahmen (`.news-frame`) mit folgender Anordnung:

1. **„News"-Überschrift** sitzt oben links auf der Outline des Rahmens.
2. **Datum „JUNE|13"** oben links im Rahmen.
3. **Cover** direkt unter dem Datum, links:
   - quadratisch (`aspect-ratio: 1/1`) — das Artwork ist quadratisch, NIE verzerren;
   - sehr klein, Breite ≈ Breite des Textes „JUNE|13" darüber.
4. **Titel unter dem Cover**, zwei Zeilen, weiß, max. so breit wie das Cover:
   - Zeile 1: „Sukram"  ·  Zeile 2: „I Am War".
5. **Video** rechts: so groß wie möglich (füllt den restlichen Platz), ragt nach oben
   über die obere Outline des Rahmens (Versatz `margin-top: -20px`).
6. **Player-Leiste** unten im Video: flach — Ton links, Play mittig, Vollbild rechts;
   genau EIN Play-Button.
7. **Streaming-Dienste** (Spotify / Apple Music / amazon music): klein, unter dem Video
   zentriert; darüber der Satz „Ab dem 13. Juni überall auf:".

Alles UNTERHALB des News-Feldes (Merch, Social-Square 2×2, Wallpaper) bleibt unverändert.

---

## Deployment

### GitHub Pages (automatisch)

Bei jedem Push auf `main` baut GitHub Actions die Seite neu und deployed sie automatisch.
URL: https://skarramushvandango-tech.github.io/rokko-web/

Der `dev`-Branch wird bei jedem Push per Action `validate-dev` gebaut/geprüft
(grüner Lauf = übernahmebereit). Erst nach grünem `dev`-Build nach `main` mergen.

### Manuelles FTP-Deployment (Netcup)

1. ZIP der gebauten Seite verwenden (Build mit `BASE_PATH=./`, `index.html` im ZIP-Root).
2. Inhalt per FTP (FileZilla, WinSCP) auf den Netcup-Server hochladen.
3. Browser-Cache leeren (Strg+Shift+R).

### WICHTIG

- `dist/` ist in `.gitignore` — NIEMALS in git committen.
- Nur `src/`, Configs und `public/` gehören in git.
- `node_modules/` ebenfalls NICHT in git.
