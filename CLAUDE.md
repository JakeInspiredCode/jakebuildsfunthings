# Notes for Claude (LLM agents)

This file is loaded automatically into your context. The README is the canonical user-facing doc.

## What this repo is

The Cloudflare Workers static-asset host for **jakebuildsfunthings.com**. `wrangler deploy` ships the entire repo as the worker's asset bundle.

## Deploying

**Cloudflare Workers Build is connected to this repo and auto-deploys from `origin/main` on every push.** So the normal deploy flow is just `git push origin main`; Workers Build picks it up and ships ~60 seconds later. No `wrangler deploy` call needed.

**Critical pitfall:** a local-only `wrangler deploy` is silently overwritten by the next `git push` to this repo, because Workers Build redeploys whatever's in `origin/main` afterward. If the working tree has changes that aren't committed, `wrangler deploy` ships them temporarily, then the next push reverts everything to the committed state. Always commit + push to make a deploy stick.

## Generated subdirectories — DO NOT hand-edit

| Path             | Source repo                      | Regenerate with                                                |
|------------------|----------------------------------|----------------------------------------------------------------|
| `l1nx-forge/`    | `~/Projects/l1nx`                | `cd ~/Projects/l1nx && npm run deploy:demo`                    |

Anything in a generated subdir will be wiped by the next regeneration. To change what's there, change the source repo and redeploy.

If you're updating the L1NX demo specifically: run `npm run deploy:demo` from the L1NX repo. It builds, replaces `l1nx-forge/` here, commits, and pushes — Workers Build then redeploys from origin/main automatically. Works fine from non-interactive shells.

## Everything else

The hand-written project pages (`projects/`, `resume/`, `agent-safety-framework/`, `colossus-triage/`, etc.), `index.html`, and `media/` are all hand-edited static files. Edit them in place and `npx wrangler deploy` to ship.
