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
<!-- okf-requirement -->
## 🧠 OKF documentation requirement (mandatory)

**Every repository in this collection MUST ship an Open Knowledge Format (OKF) bundle in `okf/`.**

A repository without `okf/` is **incomplete**, even if the script works.

### What must exist

```
okf/
├── bundle.md      overview of the collection
├── index.md       catalogue of concepts
├── concepts/      all shared concept notes (architecture, metadata, scriptcat-and-sctl,
│                  testing, youtube-dom, okf-requirement)
└── scripts/       THIS repository's own script note (where one applies)
```

### Rules

1. **Never hand-edit** a repository's `okf/` copy. The canonical bundle is
   `repos/own/public/userscripts/okf/` in the `c:\ws` monorepo.
2. After changing the canonical bundle, regenerate every copy:
   `node okf/sync-okf.mjs`
3. Verify nothing has drifted: `node okf/sync-okf.mjs --check` — must exit `0`.
4. `README.md` must link to `okf/`. `AGENTS.md` (this file) must restate this requirement.
5. When adding a new script, add its note at `okf/scripts/<repo-name>.md` in the canonical
   bundle first, then sync.
6. Record durable knowledge here as a concept note: fragile selectors, platform rules,
   rejected alternatives, and mistakes that already cost time.

Full detail: [`okf/concepts/okf-requirement.md`](okf/concepts/okf-requirement.md)
