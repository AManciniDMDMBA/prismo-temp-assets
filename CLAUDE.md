# CLAUDE.md

Guidance for Claude Code (and other AI assistants) working in this repository.

## What this repository is

`AManciniDMDMBA/prismo-temp-assets` — a **public**, deliberately temporary staging
area for assets belonging to the Prismo Shopify storefront (dental / orthodontic
instruments). It is not an application. There is no build, no test suite, no
package manager, no CI, and no runtime.

It exists for two jobs:

1. **Ad-hoc image CDN.** Because the repo is public, anything committed here is
   immediately fetchable over `raw.githubusercontent.com` and can be referenced
   from a Shopify theme, blog post, product description, or email before the
   image has a permanent home on the Shopify CDN.
2. **Liquid scratch space.** Shopify section/snippet `.liquid` files are staged
   here so they can be reviewed and diffed in git, then pasted into the live
   theme editor. The theme itself lives in Shopify, *not* in this repo.

### Raw URL pattern

```
https://raw.githubusercontent.com/AManciniDMDMBA/prismo-temp-assets/main/<path>
```

Pin to `main` (or a commit SHA for stability). Note that raw URLs break the
moment a file is renamed, moved, or deleted — see the lifecycle rule below.

## The central convention: files here are disposable

"temp" in the repo name is load-bearing. The normal life of a file is:

**commit → reference by raw URL / paste into theme → delete once it has a
permanent home.**

The history shows both halves of this cycle:

- `blog/why-blend-in-hero.jpg` was added, then removed with
  `cleanup: image now on Shopify CDN`.
- `prismo-chat-shipping.liquid` was added, patched (`temp: chat shipping patch
  v2`), then removed with `cleanup` once it was live in the theme.

**Implications for anyone working here:**

- Do **not** treat deletion as data loss or try to "restore" missing assets.
  A file's absence from the working tree usually means it graduated.
- Do **not** refactor, reorganize, or "tidy" the flat root layout. Churn breaks
  live raw URLs pointing at published pages.
- Before deleting or renaming anything, confirm it is no longer referenced by a
  live storefront page. This repo cannot tell you that — ask the user.
- Deleted content stays in git history forever, and the repo is public. Never
  commit customer data, order exports, API keys, Shopify tokens, or anything
  else that must not be world-readable. Removing it in a later commit does not
  unpublish it.

## Current contents

Flat root layout; subdirectories are created only when a batch warrants one
(`blog/` existed for a post's hero image, and was removed with its contents).

| File | Notes |
| --- | --- |
| `gold_cut3.png` | 2474×1979 RGBA, cutout product shot |
| `unicorn_cut3.png` | 3065×2452 RGBA, cutout product shot |
| `pro-kit-purple.png` | 1024×1536 RGBA, PRISMOPRO kit marketing image |

Images are committed full-size (1.5–2.3 MB PNGs) with transparency preserved —
`_cut` in a name signals a background-removed cutout. There is no `.gitignore`
and no image pipeline; do not add compression tooling or convert formats unless
asked, since the raw URL of an existing asset must not change.

## Liquid conventions

Derived from `prismo-chat-shipping.liquid` (removed in `0125b48`; recover it for
reference with `git show b028fd2:prismo-chat-shipping.liquid`). Follow these when
adding or editing a section here:

- **Shape.** A single `<script>` wrapping one IIFE, followed by a `{% schema %}`
  block with `name`, `settings`, and a matching `presets` entry so the section is
  addable in the theme editor.
- **Patch, don't rebuild.** These files are behavioral patches layered onto an
  existing theme. They attach `document`-level listeners in the **capture phase**
  (`addEventListener(..., true)`) and call `stopPropagation()` / `preventDefault()`
  only when they intend to handle an event, letting everything else fall through
  to the theme's own handlers.
- **Theme DOM contract.** The chat widget is addressed by id — `chatMessages`,
  `chatInput`, `chatSendBtn` — and rendered with classes `chat-msg`,
  `chat-bubble`, `chat-avatar`, `chat-typing`. Bail out silently (`if (!input ||
  !msgs) return;`) when the nodes are absent; the script loads on pages without
  the widget.
- **Patches must not collide.** Each patch owns a topic and explicitly defers on
  another patch's topic — the shipping patch tests `SIZING_RX` first and returns
  so the sizing patch can answer. When adding a patch, check the existing ones
  for overlap and add a matching guard.
- **Matching is intent-aware, not keyword-soup.** Country/keyword matching
  normalizes case and strips diacritics, requires either shipping context words
  or a short message before firing, and flags ambiguous proper nouns (`!jordan`,
  `!chad`, `!georgia`) as context-required so a person's name doesn't trigger a
  shipping answer.
- **Escape user input.** User-authored text goes through `escHtml()`; only
  bot-authored strings are injected as HTML.
- **Copy rules matter.** Never state that Prismo does not ship somewhere —
  unmatched countries fall through to the generic knowledge-base answer.
  Sanctioned destinations (e.g. North Korea) are excluded from matching rather
  than answered negatively. Keep the existing brand voice: shipping is 2–5
  business days, and orders over $2,400 ship free with code `PRISMOPRO`.
  **Verify shipping terms, prices, and promo codes with the user before
  changing them** — this is customer-facing commercial copy, not test data.

## Workflow

- **Branch.** Develop on the branch assigned for the session; create it locally
  if needed. Never push to `main` without explicit permission.
- **Push.** `git push -u origin <branch-name>`. On network failure, retry up to
  four times with exponential backoff (2s, 4s, 8s, 16s).
- **Pull requests.** Do not open one unless the user asks. The repo has no PR
  template and no history of PRs — work has historically landed directly.
- **Verification.** There is nothing to run or lint. "Correct" means the asset
  renders and the raw URL resolves; for Liquid, it means the snippet behaves in
  the theme. Both are verified by the user on the live storefront, so state what
  you changed and what still needs their eyes on it — never claim a change is
  confirmed working in the store.

### Commit messages

Short, lowercase, no trailing period. Match the existing register:

- `add pro kit`, `add gold_cut3` — new assets
- `blog hero: why blend in graphic` — scoped asset with purpose
- `temp: chat shipping patch`, `temp: chat shipping patch v2` — staged code
  expected to be removed later
- `cleanup`, `cleanup: image now on Shopify CDN` — removal, ideally naming where
  the content went

Prefer `temp:` for anything you already know is transitional, and say in the
`cleanup` message where the content ended up.

## Things not to do here

- Don't add tooling: no `package.json`, build step, linter, CI workflow, or
  image optimizer. Nothing consumes this repo as a project.
- Don't write a README that contradicts the temporary nature of the repo, or
  document assets that are about to be deleted.
- Don't rename or move existing files as a side effect of another task.
- Don't add binaries larger than needed for the storefront's use, and don't
  commit source/working files (PSD, AI, raw exports) — only the final asset that
  a page will actually load.
