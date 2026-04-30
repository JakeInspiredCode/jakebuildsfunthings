# Notes for Claude (LLM agents)

This file is loaded automatically into your context. The README is the canonical user-facing doc.

## What this repo is

The Cloudflare Workers static-asset host for **jakebuildsfunthings.com**. `wrangler deploy` ships the entire repo as the worker's asset bundle.

## Deploying

```bash
npx wrangler deploy
```

**You (the LLM) usually cannot run this from a non-interactive shell** — `wrangler` needs OAuth creds from `wrangler login`, and that opens a browser. If `wrangler whoami` succeeds, you're fine; otherwise tell the user to run the deploy from their terminal.

## Generated subdirectories — DO NOT hand-edit

| Path             | Source repo                      | Regenerate with                                                |
|------------------|----------------------------------|----------------------------------------------------------------|
| `l1nx-forge/`    | `~/Projects/l1nx`                | `cd ~/Projects/l1nx && npm run deploy:demo`                    |

Anything in a generated subdir will be wiped by the next regeneration. To change what's there, change the source repo and redeploy.

If you're updating the L1NX demo specifically: prefer running `npm run deploy:demo -- --build-only` from the L1NX repo. That handles the build + copy here, then hands the `wrangler deploy` step back to the user.

## Everything else

The hand-written project pages (`projects/`, `resume/`, `agent-safety-framework/`, `colossus-triage/`, etc.), `index.html`, and `media/` are all hand-edited static files. Edit them in place and `npx wrangler deploy` to ship.
