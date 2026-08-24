# ことば LINE (Kotoba Line)

A self-contained Japanese learning app: hiragana → katakana → vocabulary → grammar → conversation, run as a metro line. Spaced repetition, confusion-pair detection, TTS audio, experimental pronunciation scoring, and an AI conversation partner that stays at your exact level.

One file. No build step, no dependencies, no server.

## Run it

**Locally:** open `index.html` in a browser. Done.

**On GitHub Pages:**

1. Create a repository (public or private with Pages enabled) and push all files in this folder.
2. Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
3. Your app is live at `https://<username>.github.io/<repo>/` within a minute or two.

## Install on iPhone (standalone app)

1. Deploy to GitHub Pages first (the service worker needs HTTPS).
2. Open the Pages URL in **Safari** (must be Safari, not Chrome).
3. Tap **Share → Add to Home Screen → Add**.
4. Launch it from the home screen icon. It runs fullscreen with no browser chrome, and after the first load it works offline (except conversation mode, which needs a connection).

iOS notes, honestly:

- **Your progress is safe.** Home-screen web apps get their own persistent storage that iOS does not purge the way it can with regular Safari site data. A full reset or deleting the app icon erases it.
- **Audio**: download the Japanese voice first (Settings → Accessibility → Spoken Content → Voices → Japanese → Kyoko). iOS requires a tap before audio plays, so the first sound in a session starts on your first button press.
- **Pronunciation scoring** is the one feature iOS may refuse: speech recognition support in home-screen web apps is unreliable. When unavailable, the app automatically shows self-grade buttons instead. On desktop Chrome the mic scoring works fully.

## Progress storage

All progress lives in your browser's `localStorage`, keyed to the site's domain. It survives restarts and updates to the app, but it does not sync between devices or browsers. Clearing site data erases it (the in-app Full Reset does the same, deliberately).

## Conversation mode (Claude)

Conversation mode calls the Anthropic API directly from your browser. First use asks for an API key from [console.anthropic.com](https://console.anthropic.com). The key is stored only in your browser's `localStorage`.

**Never commit an API key to the repo.** The app never asks you to put it in a file.

## Browser notes

- **TTS**: needs a Japanese voice on the device. Chrome desktop ships one. iPhone/Mac: Settings → Accessibility → Spoken Content → Voices → Japanese → download Kyoko.
- **Pronunciation scoring**: uses the Web Speech API (`ja-JP` recognition). Works in Chrome and Edge; Firefox and most iOS browsers don't support it, and the app falls back to honest self-grading. Requires HTTPS (GitHub Pages is HTTPS) and mic permission.
- Everything else works in any modern browser.
