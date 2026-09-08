# shamwari-web

`shamwari.ai` and `www.shamwari.ai` — the public apex site. Astro with SSR
on Cloudflare Workers.

> **This branch is scaffolding.** `main` is deliberately empty so the
> extraction can `git subtree split -P site` out of
> [`shamwari`](https://github.com/shamwari-ai/shamwari) and push history
> straight in. Merge this branch **after** that import lands.

## The apex is currently broken

This is not a clean lift-out. Today `site/` is a **static** Astro build with
no bindings and no SSR, and the SvelteKit app that used to serve the apex
was removed in the pivot — so what actually resolves at `shamwari.ai` is
nothing. The desired end state is Astro **SSR** with `UserObject` and
`ConversationObject` Durable Object bindings. That is a real gap to build,
not just a directory to move.

## Retire the Vercel project as part of this

A stale pre-pivot Vercel project still exists on Vercel's side and now
builds from a tree with no app in it. **Do not point this repo at it.**
Delete or re-target it deliberately during the extraction rather than
leaving it failing — or, worse, silently serving a stale build alongside a
working Worker.

## Astro, not Hono

This repo renders pages, so Astro owns routing and layout. Hono is the
gateway's routing library for an API with no pages. They are not
interchangeable — see "What not to do" in the repo-split plan.

## Related

- [`shamwari`](https://github.com/shamwari-ai/shamwari) — umbrella; `docs/desired-cloudflare-state.md` has the target architecture
- [Org standards](https://github.com/shamwari-ai/.github/blob/main/ORG_STANDARDS.md)
