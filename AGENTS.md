# AGENTS.md — shamwari-web

Rules for AI agents and people working in this repository. They layer on the
org-wide guide, [nyuchi/.github AGENTS.md](https://github.com/nyuchi/.github/blob/main/AGENTS.md).
Where the two conflict, this file wins. Read `README.md` first.

## What this repo is

The planned home of the Shamwari apex site, `shamwari.ai` and
`www.shamwari.ai`: Astro on Cloudflare Workers. It does not own the site yet.
`main` holds a licence, CI wiring, lint config and the README. The site that
serves those hostnames is built from `site/` in
[`shamwari-ai/shamwari`](https://github.com/shamwari-ai/shamwari), and that
monorepo is where site code changes land until the extraction into this repo
is done. Its [`AGENTS.md`](https://github.com/shamwari-ai/shamwari/blob/main/AGENTS.md)
holds the project rules, including the two that must not be weakened:
personal-layer content never reaches a third-party inference provider, and
only open-weight output may train Shamwari Mind.

## Layout

```text
.github/workflows/   ci.yml, pr-title-lint.yml
README.md            what the repo is and how the extraction is staged
LICENSE, NOTICE      Apache-2.0
.prettierrc, .markdownlint.jsonc, .yamllint.yaml, .editorconfig   lint config
```

## Checks

CI (`.github/workflows/ci.yml`) calls the org's reusable workflows:
`reusable-ci-astro-npm.yml` for the build, and `reusable-gitleaks.yml` for the
secret scan. The PR title is linted by `pr-title-lint.yml`. The CI comment
states that `npm run check` is `check.mjs` (dead links and assets, colours with
no base `:root` token, stray client JavaScript, the size budget, language
rules), not `astro check`, and must stay a required step. There is no
`package.json` on `main` yet, so there is nothing to run locally until the
site is imported.

## Conventions

- **Astro, not Hono.** This repo renders pages. Do not add Hono here; it is the
  gateway's routing library.
- **No client JavaScript by default.** The live site ships none. Do not add a
  `client:*` directive without an explicit decision.
- **Conventional Commits** on every commit and PR title; the PR title becomes
  the squash-commit subject.
- **Trunk-based.** `main` is the only target; open every pull request against
  it and merge once CI is green.
- **Pin actions to full commit SHAs** when you add or change a workflow that
  uses third-party actions. The org's reusable workflows are referenced as
  they already are in `ci.yml`.
- **This repository is public.** No secrets, keys, tokens or internal
  hostnames in code, commits, PRs or issues.
- Say "open weights", not "fully open source".

## Out of bounds

- Do not pull the extraction forward by importing history or restructuring
  branches. That is done with `git subtree split -P site` from the monorepo and
  is the owner's call.
- Do not connect this repo to the old Vercel project. See the README.
- Do not change DNS, Cloudflare or deploy configuration from a docs or code PR.
- Do not edit `LICENSE` or `NOTICE`.
