# jakebuildsfunthings.com

Source for the personal site at **jakebuildsfunthings.com**. Hosted on Cloudflare Workers as a static-asset deployment — `wrangler deploy` ships the entire repo as the worker's asset bundle, so any path served on the live site corresponds 1:1 to a file in this directory.

## Layout

```
.
├── index.html                  # site home
├── wrangler.jsonc              # Cloudflare Workers config (assets.directory = ".")
├── media/                      # shared images, video, etc.
├── projects/, resume/, …       # static project pages — hand-written HTML
└── <project>/                  # generated project pages — DO NOT hand-edit
```

Most subdirectories are **hand-written static pages** built from the home-page Tailwind palette. A handful are **generated outputs** from external project repos and should never be edited in-place — see "Generated subdirectories" below.

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

## Generated subdirectories (don't hand-edit)

| Path           | Source repo               | Regenerate with                                  |
|----------------|---------------------------|--------------------------------------------------|
| `l1nx-forge/`  | `~/Projects/l1nx`         | `cd ~/Projects/l1nx && npm run deploy:demo`      |

The L1NX deploy script builds the static export, replaces `l1nx-forge/` here with the fresh build, and **commits + pushes** so Workers Build redeploys from GitHub. The committed state IS the deploy — never rely on a local-only `wrangler deploy` for these subdirs, since the next push to this repo will revert them to whatever's in `origin/main`.

When adding a new generated subdirectory in the future, document it in the table above so future-you (and any LLMs you bring in) know it's machine-generated and shouldn't be hand-edited.

## Why this setup

One source of truth per project, with the personal site acting as the showcase host. Project repos own their build; the showcase repo owns the routing, hosting config, and the hand-written landing pages. Improvements ship to each project's primary deployment first (e.g., L1NX → Vercel), then a one-line script pulls them through to here.
