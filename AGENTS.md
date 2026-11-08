# AGENTS.md — userscript-install-guide

Guidance for AI coding agents (and humans) working on this repository.

## 🎯 What this repo is

The **install and usage guide** for the YouTube userscript collection. Documentation only — **no script code lives here.**

| File | Purpose |
|------|---------|
| `README.md` | The guide. |
| `AGENTS.md` | This file. |
| `LICENSE` | MIT. |

## 🧭 Golden rules

1. **Docs only.** Never add a `.user.js` file here.
2. **Every script repo's README must link back here.** When adding a script, add its row to the tables in §7 of README.md.
3. **This guide links out to every script.** Keep the links resolving — a dead install link is worse than no guide.
4. **Keep instructions manager-neutral but ScriptCat-first.** ScriptCat is the recommendation; Tampermonkey and Violentmonkey must still work.
5. **State the real caveats.** Batch actions are sequential (~0.5–0.9 s/item). Do not imply instant bulk operations.
6. **Warn against installing the toolkit *and* its component scripts together** — actions would run twice.

## 🔗 Repos this guide links to

### Aggregate
- `chirag-youtube-userscripts` — collection index
- `youtube-hotkeys-userscripts` — hotkeys hub
- `yt-multiselect-toolkit-userscript` — merged panel

### Bulk selection & actions
- `yt-bulk-select-userscript` (☑)
- `yt-filter-select-userscript` (⚏)
- `yt-select-smart-userscript` (✨)
- `yt-playlist-tools-userscript` (☰)

### Loading
- `yt-load-entire-page-userscript` (↓)

### Hotkeys
- `yt-hotkey-like-userscript` (`a`)
- `yt-hotkey-dislike-userscript` (`d`)
- `yt-hotkey-next-userscript` (`n`)
- `yt-hotkey-prev-userscript` (`p`)

## ✅ Checking install links

Every install URL is `https://github.com/chirag127/<repo>/raw/main/<repo-short>.user.js`. Verify:

```bash
curl -sL -o /dev/null -w "%{http_code}\n" <url>   # expect 200
```

GitHub's raw CDN lags a few minutes after a push — that is propagation, not breakage.

## 🚀 Release checklist

- [ ] New scripts added to the §7 tables.
- [ ] All install links return HTTP 200.
- [ ] Troubleshooting section still accurate.
- [ ] Pushed to `main`.

## ⛔ Out of scope

No instructions for defeating anti-bot or CAPTCHA systems. This guide covers legitimate UI automation only.
