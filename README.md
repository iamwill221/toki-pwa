# Toki · 時 — Japanese Time & Numbers PWA

A clean iOS-styled progressive web app to practice telling time and counting in Japanese.

## Files

- `index.html` — the entire app (HTML + CSS + JS in one file)
- `manifest.json` — PWA metadata (name, icon, colors, install behavior)
- `sw.js` — service worker for offline support

## Run locally (for testing)

You **cannot** just double-click `index.html` and expect the service worker to register — browsers require HTTPS or `http://localhost` for service workers. Run a quick local server:

```bash
# Python (already installed on macOS / most Linux)
python3 -m http.server 8000

# Or Node
npx serve .
```

Then open `http://localhost:8000` in Safari or Chrome.

## Deploy as a real PWA (free options)

Any static HTTPS host works. Easiest paths:

### GitHub Pages
1. Create a new GitHub repo, push these three files to the root
2. Repo Settings → Pages → Source: `main` branch, root folder
3. Wait ~1 min, your app is at `https://YOUR_USERNAME.github.io/REPO_NAME/`

### Netlify (drag-and-drop)
1. Go to https://app.netlify.com/drop
2. Drag the folder containing these three files
3. Done — you get an HTTPS URL instantly

### Vercel / Cloudflare Pages
Same idea — connect a Git repo or upload, both free.

## Install on iPhone

Once it's live on HTTPS:

1. Open the URL in **Safari** (not Chrome — Chrome can't install PWAs on iOS)
2. Tap the Share button (square with up arrow)
3. Scroll down → **"Add to Home Screen"**
4. The 時 icon appears on your home screen
5. Launch from the icon — runs fullscreen, no Safari UI, works offline

## Install on Android

1. Open in Chrome
2. Three-dot menu → **"Install app"** or **"Add to Home screen"**
3. Same offline behavior

## Updating the app later

When you change `index.html`, also bump the cache version in `sw.js`:

```js
const CACHE = 'toki-v3';  // was v2
```

Next time users open the app online, the new service worker activates, clears the old cache, and they get the fresh version.

## Tech notes

- **Zero dependencies** — pure HTML/CSS/JS, no build step, no npm
- **Offline-first** — service worker caches everything on first load
- **Light & dark mode** — auto-adapts to system preference
- **iOS-native feel** — SF Pro typography, system colors, segmented controls, bottom sheets, swipe-to-dismiss
- **Safe area aware** — respects iPhone notch and home indicator

## Features

- Random time generation with three difficulty modes
- Random number generation (1–99,999) with selectable ranges
- Hiragana display + optional romaji
- Two reference sheets (Time / Numbers) with sound-change markers
- Streak counter (resets when you peek at the answer)
- Keyboard shortcuts: Space/Enter to reveal, →/N for next, Esc to close sheets
- Haptic feedback on supported devices
