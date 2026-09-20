# Notes for Claude (LLM agents)

This file is loaded automatically into your context. The README is the canonical user-facing doc.

## What this repo is

The Cloudflare Workers static-asset host for **jakebuildsfunthings.com**. `wrangler deploy` ships the entire repo as the worker's asset bundle.

## Deploying

**Cloudflare Workers Build is connected to this repo and auto-deploys from `origin/main` on every push.** So the normal deploy flow is just `git push origin main`; Workers Build picks it up and ships ~60 seconds later. No `wrangler deploy` call needed.

**Critical pitfall:** a local-only `wrangler deploy` is silently overwritten by the next `git push` to this repo, because Workers Build redeploys whatever's in `origin/main` afterward. If the working tree has changes that aren't committed, `wrangler deploy` ships them temporarily, then the next push reverts everything to the committed state. Always commit + push to make a deploy stick.

## Everything in the repo is served — unless `.assetsignore` says otherwise

`wrangler.jsonc` sets `assets.directory` to `"."`, so every file here is uploaded and publicly reachable at its path. [`.assetsignore`](.assetsignore) (gitignore syntax) is the only thing that keeps repo plumbing off the live site — before it existed, `/.git/config`, `/CLAUDE.md` and `/wrangler.jsonc` were all being served. **If you add a file that isn't meant to be public, add it there.** After deploying, check with `curl -sI https://jakebuildsfunthings.com/<path>`.

## Redirects

[`_redirects`](_redirects) holds them (`source destination code`, one per line). Cloudflare applies a redirect even when a file exists at that path.

DC-Tech-Forge (formerly "L1NX Forge") used to be published here as a generated static copy under `l1nx-forge/`, rebuilt by an `npm run deploy:demo` script in its repo. **That pipeline is retired.** The app lives at <https://forge.jakebuildsfunthings.com> (Vercel, from `~/Projects/l1nx`), and `/l1nx-forge/*` 301s there. Don't recreate the directory. There are currently no generated subdirectories.

## Everything else

The hand-written project pages (`projects/`, `resume/`, `agent-safety-framework/`, `colossus-triage/`, etc.), `index.html`, and `media/` are all hand-edited static files. Edit them in place, commit, and push.
