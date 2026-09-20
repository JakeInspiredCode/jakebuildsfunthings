# jakebuildsfunthings.com

Source for the personal site at **jakebuildsfunthings.com**. Hosted on Cloudflare Workers as a static-asset deployment — `wrangler deploy` ships the entire repo as the worker's asset bundle, so any path served on the live site corresponds 1:1 to a file in this directory.

## Layout

```
.
├── index.html                  # site home
├── wrangler.jsonc              # Cloudflare Workers config (assets.directory = ".")
├── .assetsignore               # what must NOT be served (see below)
├── _redirects                  # redirects, e.g. the retired /l1nx-forge/ demo
├── media/                      # shared images, video, etc.
└── projects/, resume/, …       # static project pages — hand-written HTML
```

The subdirectories are **hand-written static pages** built from the home-page Tailwind palette.

### Everything here is public unless `.assetsignore` lists it

Because `assets.directory` is the repo root, every file is uploaded and served at its path. `.assetsignore` (same syntax as `.gitignore`) keeps the repo's plumbing — `.git/`, `CLAUDE.md`, `README.md`, `wrangler.jsonc`, `.claude/` — off the live site. If you add a file that isn't meant to be public, list it there.

## Deploying

**Cloudflare Workers Build is connected to this repo and auto-deploys from `origin/main` on every push** (~60 seconds after the push lands). So the normal deploy flow is just:

```bash
git add <whatever you changed>
git commit -m "…"
git push origin main
# wait ~60 seconds, refresh the site
```

You can also publish manually with `npx wrangler deploy` for instant feedback (useful when iterating on a hand-written page), but be aware that **a local-only deploy is silently overwritten by the next `git push`** because Workers Build redeploys from `origin/main` afterward. Always commit + push if you want the change to stick.

Worker name is `jakebuildsfunthings`; the apex domain `jakebuildsfunthings.com` is bound to it via Cloudflare's custom-domain config.

**One-time setup for manual `wrangler deploy`:** `npx wrangler login` against the Cloudflare account that owns the worker.

### Local preview

```bash
python3 -m http.server 8080
```

Then open <http://localhost:8080>. Good enough for a static site; no need for the wrangler dev server unless you're testing Worker-specific behavior (you're not — this site is static assets only).

## Projects hosted elsewhere

Projects with their own deployment are **linked to**, not copied in.

| Project | Lives at | Repo |
|---|---|---|
| DC-Tech-Forge | <https://forge.jakebuildsfunthings.com> (Vercel) | `~/Projects/l1nx` |

DC-Tech-Forge (formerly "L1NX Forge") used to be published here as a generated static copy under `l1nx-forge/`, rebuilt and committed by a deploy script in its repo — about 5 MB of build output per deploy. That pipeline is retired. `_redirects` sends `/l1nx-forge/*` to the new domain so links already in circulation keep working.

## Why this setup

One source of truth per project, with the personal site acting as the showcase. Project repos own their build and their hosting; this repo owns the hand-written landing pages and links out to them.
