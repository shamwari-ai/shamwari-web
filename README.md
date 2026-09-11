# Shamwari Web

> The public apex site — `shamwari.ai` and `www.shamwari.ai`. Astro on Cloudflare Workers.

[![Lint](https://github.com/shamwari-ai/shamwari-web/actions/workflows/lint.yml/badge.svg)](https://github.com/shamwari-ai/shamwari-web/actions/workflows/lint.yml)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
![Astro](https://img.shields.io/badge/Astro-BC52EE?style=flat-square&logo=astro&logoColor=white)
![Cloudflare Workers](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=flat-square&logo=cloudflare&logoColor=white)

**Live:** [shamwari.ai](https://shamwari.ai) | **Default branch:** `scaffold` | **Code still lives in:** [`shamwari/site`](https://github.com/shamwari-ai/shamwari/tree/main/site)

---

## What it is

This repository will own the Shamwari apex site. It does not own it yet.

`scaffold` — the default branch, and the one you are reading — holds a
licence, CI wiring and this file. `main` is deliberately empty so the
extraction can `git subtree split -P site` out of
[`shamwari`](https://github.com/shamwari-ai/shamwari) and push history
straight in without a merge or a force. Merge `scaffold` **after** that
import lands.

## The site is live; this repo is not what serves it

[shamwari.ai](https://shamwari.ai) and [www.shamwari.ai](https://www.shamwari.ai)
both answer, from Cloudflare, with four pages — home, `/blueprint/`,
`/project/` and `/contact/`. They are built from `site/` in the monorepo:
Astro with `output: 'static'`, served by Workers static assets, using
`@bundu/ui`'s React primitives with no `client:*` directive anywhere, so no
page ships a byte of client JavaScript.

That is worth stating plainly because this README previously said the apex
resolved to nothing. It did not; it does now.

Static output is also why the monorepo's `site/` holds no bindings and no
secrets — the reason the split is safe to do at all.

## The SSR gap is real

The target in `shamwari`'s `docs/desired-cloudflare-state.md` is Astro **SSR**
with `UserObject` and `ConversationObject` Durable Object bindings. What
exists today is a static build with neither. That is a feature to write, not
a directory to move, and it is gated on the same open question as the Durable
Objects themselves: whether personal-scope state may rest in DO storage at all.

## Retire the stale Vercel project as part of this

A pre-pivot Vercel project still exists on Vercel's side and now builds from a
tree with no app in it. **Do not point this repo at it.** Delete or re-target
it deliberately during the extraction rather than leaving it failing — or,
worse, silently serving a stale build alongside a working Worker. The same
project is why `platform.shamwari.ai` currently answers `200` with a page that
is not the console.

## Astro, not Hono

This repo renders pages, so Astro owns routing and layout. Hono is the
gateway's routing library for an API with no pages. They are not
interchangeable — see "What not to do" in `docs/repo-split.md`.

## Ecosystem

- [`shamwari`](https://github.com/shamwari-ai/shamwari) — the umbrella;
  `docs/desired-cloudflare-state.md` has the target architecture and
  `docs/repo-split.md` the extraction plan
- [`shamwari-platform`](https://github.com/shamwari-ai/shamwari-platform) —
  the customer console, the other Astro surface
- [`docs`](https://github.com/shamwari-ai/docs) —
  [docs.shamwari.ai](https://docs.shamwari.ai)
- [Org standards](https://github.com/shamwari-ai/.github/blob/main/ORG_STANDARDS.md)

## Contributing

See the org's
[CONTRIBUTING.md](https://github.com/shamwari-ai/.github/blob/main/CONTRIBUTING.md),
[SECURITY.md](https://github.com/shamwari-ai/.github/blob/main/SECURITY.md) and
[CODE_OF_CONDUCT.md](https://github.com/shamwari-ai/.github/blob/main/CODE_OF_CONDUCT.md).

## Licence

Licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
— see `LICENSE` and `NOTICE`.

© Bundu Foundation. Shamwari is Bundu Foundation IP, sold commercially under
Nyuchi Africa.
