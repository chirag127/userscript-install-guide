# 📖 Userscript Install Guide

> A complete, beginner-friendly walkthrough for installing and using userscripts — with real, working YouTube examples.

[![userscript](https://img.shields.io/badge/userscript-guide-blue)](https://github.com/chirag127/userscript-install-guide)
[![license](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

---

## 📚 Contents

1. [What is a userscript?](#1-what-is-a-userscript)
2. [Step 1 — Install a userscript manager](#2-step-1--install-a-userscript-manager)
3. [Step 2 — Install a script](#3-step-2--install-a-script)
4. [Step 3 — Check it's running](#4-step-3--check-its-running)
5. [Updating scripts](#5-updating-scripts)
6. [Troubleshooting](#6-troubleshooting)
7. [The YouTube collection](#7-the-youtube-collection)
8. [Writing your own](#8-writing-your-own)

---

## 1. What is a userscript?

A **userscript** is a small JavaScript file that a browser extension runs on specific websites. It can add buttons, change layouts, and automate repetitive clicking — without installing a full extension.

It's just a `.user.js` text file with a metadata header:

```javascript
// ==UserScript==
// @name         My Script
// @match        https://www.youtube.com/*
// @version      1.0.0
// @downloadURL  https://example.com/my.user.js
// @updateURL    https://example.com/my.user.js
// ==/UserScript==
```

`@match` decides which sites it runs on. `@updateURL` lets it update itself.

**Userscripts run with your logged-in session.** Only install scripts whose source you can read or whose author you trust. Every script in this guide's collection is plain, readable JavaScript with no obfuscation and no network calls to third parties.

---

## 2. Step 1 — Install a userscript manager

You need a manager. Pick one:

### 🥇 ScriptCat — recommended

1. Go to **[scriptcat.org](https://scriptcat.org/)** and follow the install link for your browser (Chrome, Edge, Firefox).
2. Or install directly from the Chrome Web Store and search "ScriptCat".
3. Pin the extension so you can see its icon.

**Why ScriptCat:** modern API support, background scripts, one-click install straight from a `.user.js` URL, and automatic updates from GitHub raw URLs.

### 🥈 Tampermonkey

1. **[tampermonkey.net](https://www.tampermonkey.net/)** → pick your browser.
2. Confirm the install prompt and pin the icon.

The long-standing standard. Everything in this guide works with it.

### 🥉 Violentmonkey

1. **[violentmonkey.github.io](https://violentmonkey.github.io/)** → get it for your browser.
2. Open source alternative, lightweight and reliable.

> **Firefox note:** userscript managers there may ask you to enable "Allow access to file URLs" or grant host permissions before scripts run. Accept the prompt.

---

## 3. Step 2 — Install a script

### The easy way (install link)

1. Find a script's **install link** — it ends in `.user.js`.
2. **Click it.** Your manager intercepts the page and shows an **Install** screen.
3. Read the script's name and permissions, then click **Install**.

Example — installing the toolkit:

> **[⬇ Install YouTube Multiselect Toolkit](https://github.com/chirag127/yt-multiselect-toolkit-userscript/raw/main/yt-multiselect-toolkit.user.js)**

That's it. Reload any YouTube tab.

### The manual way (paste)

If clicking does nothing:

1. Open the `.user.js` URL in your browser and select all → copy.
2. Click your manager's icon → **Create a new script** / **+**.
3. Paste, replacing the template, and save.

### The local-file way (developing)

1. Manager icon → **Create a new script**.
2. Paste your file contents, save.
3. For live editing, point the manager at a local file path in its settings.

---

## 4. Step 3 — Check it's running

After installing:

1. **Reload the target site.** Userscripts don't attach to pages that were already open.
2. Look for the script's UI — the YouTube scripts add a **round button, bottom-left**.
3. Open DevTools (<kbd>F12</kbd>) → **Console**. Our scripts log a ready line:
   ```
   [YouTube Multiselect Toolkit] ready - 17 videos found
   ```
4. Your manager's icon shows a **badge count** of scripts active on the current page.

If the button doesn't appear, jump to [Troubleshooting](#6-troubleshooting).

---

## 5. Updating scripts

Scripts installed from a GitHub raw URL update themselves, because they declare:

```
// @updateURL   https://github.com/<user>/<repo>/raw/main/<name>.user.js
// @downloadURL https://github.com/<user>/<repo>/raw/main/<name>.user.js
```

**ScriptCat:** checks automatically; force one with the extension menu → **Update scripts** / **Check updates**.
**Tampermonkey:** Dashboard → **Installed userscripts** → **Check for userscript updates**.
**Violentmonkey:** Dashboard → **Check updates**.

To update manually, just click the install link again — the manager replaces the old copy.

> **Note on delays:** GitHub's raw CDN caches for a few minutes. If you just published a new version and the manager says "no update", wait a bit and retry. The URL itself is not broken.

**Best practice:** read the changelog before updating, especially for scripts that act on your data. Ours only ever do what you click.

---

## 6. Troubleshooting

### The script's button doesn't appear

| Check | Fix |
|-------|-----|
| Did you reload the page? | Userscripts attach on load — press <kbd>F5</kbd> |
| Is the script enabled? | Manager → the script's toggle must be on |
| Does `@match` cover this URL? | Check the script header; `/watch` pages need `youtube.com/*` |
| Is another script throwing? | DevTools Console — a red error can abort later scripts |
| Is the manager allowed on this site? | Some managers default to "ask"; allow the domain |

### Console shows "Cannot redefine property"

Another extension is modifying YouTube's globals — commonly ad-block scriptlets. Disable the conflicting extension on YouTube and reload.

### Console shows a `TrustedHTML` error

A different userscript is doing unsafe DOM writes. Disable it; it isn't ours.

### Page freezes / "Page Unresponsive"

Prior debugging sessions can leave a modal dialog open. Close the tab and open a fresh one. Our scripts never block the main thread — batch operations are throttled on purpose.

### Updates never arrive

1. Confirm the `@updateURL` returns the script: open it in a tab. You should see JavaScript.
2. Check the manager's update interval setting.
3. Reinstall by clicking the install link once.

### Two copies of the same script

You installed it in two managers, or twice in one. Delete the duplicate — otherwise actions run twice. Our scripts guard against double-injection internally, but you should still keep one copy.

---

## 7. The YouTube collection

All scripts live in their own repos and each README links back here.

### 🧰 Start here — everything in one panel

| Script | What it does |
|--------|--------------|
| **[yt-multiselect-toolkit](https://github.com/chirag127/yt-multiselect-toolkit-userscript)** | Select, filter, find duplicates, save, reorder, reverse, load entire pages — all in one panel |

### Or install individual scripts

| Script | Button | What it does |
|--------|--------|--------------|
| **[yt-bulk-select](https://github.com/chirag127/yt-bulk-select-userscript)** | ☑ | Select all/none/invert/shorts, save to Watch later or any playlist, remove, copy, export |
| **[yt-filter-select](https://github.com/chirag127/yt-filter-select-userscript)** | ⚏ | Select by text or regex, invert matches |
| **[yt-select-smart](https://github.com/chirag127/yt-select-smart-userscript)** | ✨ | Select duplicates or unavailable videos |
| **[yt-playlist-tools](https://github.com/chirag127/yt-playlist-tools-userscript)** | ☰ | Move to top/bottom, remove, reverse a playlist |
| **[yt-load-entire-page](https://github.com/chirag127/yt-load-entire-page-userscript)** | ↓ | Auto-scroll until every video is loaded |

### ⌨️ Single-key hotkeys

| Script | Key | Action |
|--------|-----|--------|
| **[yt-hotkey-like](https://github.com/chirag127/yt-hotkey-like-userscript)** | <kbd>a</kbd> | 👍 Like |
| **[yt-hotkey-dislike](https://github.com/chirag127/yt-hotkey-dislike-userscript)** | <kbd>d</kbd> | 👎 Dislike |
| **[yt-hotkey-next](https://github.com/chirag127/yt-hotkey-next-userscript)** | <kbd>n</kbd> | ⏭️ Next video |
| **[yt-hotkey-prev](https://github.com/chirag127/yt-hotkey-prev-userscript)** | <kbd>p</kbd> | ⏮️ Previous video |

**Full index:** [chirag-youtube-userscripts](https://github.com/chirag127/chirag-youtube-userscripts)

### Choosing between merged and individual

- **Pick the toolkit** if you want one button and everything in one place. It's one script to maintain and it can't conflict with itself.
- **Pick individual scripts** if you only want one or two features, or you prefer separate update cycles.

Don't install the toolkit *and* its components — the actions would run twice.

---

## 8. Writing your own

Minimal, working template:

```javascript
// ==UserScript==
// @name         Hello YouTube
// @namespace    https://example.com
// @version      1.0.0
// @description  Logs the current video ID
// @match        https://www.youtube.com/*
// @grant        none
// @run-at       document-idle
// ==/UserScript==

(function () {
  "use strict";
  const m = /[?&]v=([A-Za-z0-9_-]{11})/.exec(location.href);
  if (m) console.log("Video ID:", m[1]);
})();
```

**Guidelines that matter on a single-page app like YouTube:**

1. **Wait for the DOM.** `@run-at document-idle`, then check `document.body` exists.
2. **Guard against double injection** using `document.documentElement.dataset`. A `window` flag won't work across isolated worlds.
3. **Watch for navigation.** YouTube swaps content without reloading; use a `MutationObserver`.
4. **Don't hijack typing.** If you listen for keys, ignore `<input>` / `<textarea>` / `contenteditable`, and `stopPropagation()` in your own fields.
5. **Prefer the UI over private APIs.** Clicking real buttons survives redesigns; `/youtubei/v1/*` calls do not.
6. **Throttle batch actions.** Sequential with ~500 ms between steps beats a parallel burst that desyncs menus.
7. **Avoid obfuscation.** Readable code is why people will trust your script.

---

## 📄 License

[MIT](./LICENSE) © 2026 chirag127

---

## 🔗 All repositories

- [chirag-youtube-userscripts](https://github.com/chirag127/chirag-youtube-userscripts) — collection index
- [youtube-hotkeys-userscripts](https://github.com/chirag127/youtube-hotkeys-userscripts) — hotkey scripts hub
- [yt-multiselect-toolkit-userscript](https://github.com/chirag127/yt-multiselect-toolkit-userscript) — all-in-one panel
- Individual scripts linked in [§7](#7-the-youtube-collection)
