# Space Bastards Scoreboard

A self-contained, single-file scoreboard for the Space Bastards tabletop game. No build step, no backend, no dependencies beyond a Google Fonts stylesheet link — it's one HTML file you can open directly, host anywhere, or embed.

## What it does

- Tracks each bastard's **kills**, **deaths**, and **points** with big, TV-friendly tally-mark styling. Tap any number to add one, press-and-hold (or right-click) to subtract one — no edit mode needed to keep score mid-game.
- Reaching 3 kills gives a bastard a persistent "Winner" badge plus a one-time confetti/banner celebration.
- Flip on **Edit** to add/rename/remove bastards and snap or upload a mini photo. Starts with an empty roster — add your own crew.
- **Campaign** panel logs each finished game (name, date, per-bastard kills/deaths/points) — tap "End Game & Start New One" to archive the current round and reset kills, deaths, *and* points to zero for everyone.
- Animated starfield/nebula background, comic-style logo.
- All data lives in the browser's `localStorage` — nothing is sent anywhere. Use **Transfer Data** to copy a JSON snapshot between devices/browsers (there's no live sync between devices by design — see below).

## Running it

Just open `index.html` in a browser, or host it as a static file (GitHub Pages, Netlify, S3, your own server — anything that serves plain HTML works).

### GitHub Pages

Settings → Pages → Deploy from branch → `main` / root. The site will be live at `https://<username>.github.io/space-bastards-scoreboard/`.

## Using it in a React Native app

The easiest integration is loading this file in a `WebView` — no need to reimplement the UI natively:

```jsx
import { WebView } from 'react-native-webview';

// Option A: bundle index.html with the app and load it locally
<WebView source={require('./assets/index.html')} />

// Option B: point at a hosted copy (e.g. GitHub Pages)
<WebView source={{ uri: 'https://<username>.github.io/space-bastards-scoreboard/' }} />
```

`localStorage` works inside a WebView's own storage context, so edits persist across app restarts on that device, same as in a regular browser tab.

## Multi-device sync

There's currently no shared backend — each device/browser keeps its own copy in `localStorage`. If you later want a phone's edits to show up live on a TV or another device, that needs a small real-time backend (Firebase is the easiest drop-in option); ask and it can be wired in without changing the rest of the app.

## Roadmap ideas

- Live sync across devices (Firebase or similar)
- Drag-to-reorder roster
- Richer campaign stats (leaderboards across games)
