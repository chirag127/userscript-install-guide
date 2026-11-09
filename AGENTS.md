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
## 📚 Documentation lives in ONE place (mandatory)

All documentation for every repository in this workspace is **single-sourced** in the
umbrella repository:

```
c:\ws\docs\okf├── bundle.md            collection overview
├── index.md             catalogue of every concept and script note
├── concepts/            shared knowledge (architecture, testing, metadata, …)
└── scripts/             one note per userscript repository
```

### Rules

1. **Never create an `okf/` folder in this repository.** It is not duplicated here, by
   design. There was once a copy in every repo: 278 files describing 42 unique documents,
   with `concepts/architecture.md` physically present 32 times. Every edit had to be
   propagated to 30 repositories and drift was unavoidable.
2. **Never hand-edit a copy.** There are no copies. Edit the canonical file under
   `c:\ws\docs\okf\`.
3. **This repository's note is** `c:\ws\docs\okf\scripts\<repo-name>.md`. If it does not
   exist, add it before adding the script.
4. **Link, do not paste.** In `README.md`, link to the canonical note with a relative path
   from the workspace, e.g. `[documentation](../../../../../docs/okf/scripts/<repo-name>.md)`.
5. **Verify** with `node c:\ws\scripts\check-okf.mjs` — it exits `0` only when nothing is
   duplicated and every repository is linked and documented.
6. When adding a new script: create the repo, add `docs/okf/scripts/<repo-name>.md`, add it
   to the tables in `docs/okf/bundle.md` and `docs/okf/index.md`, then run the checker.

Full detail: `c:\ws\docs\okf\concepts\okf-requirement.md`.
