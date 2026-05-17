# Field Notes — My Trips

A static archive of trip field guides. The repo root is a hub site that links out to one self-contained microsite per trip. Hosted on Vercel as plain static HTML — no build step.

## Live URLs

| | |
|---|---|
| Hub | `/` |
| A trip | `/trips/<slug>/` |

## Repo layout

```
.
├── index.html              ← Hub: lists every trip as a card
├── vercel.json             ← Clean URLs, trailing slash
├── trips/                  ← One folder per trip — deployed
│   └── point-reyes-2026/
│       └── index.html
└── _src/                   ← Working files — gitignored, never deployed
    └── point-reyes-2026/
        ├── *.skill         ← brand/style + content skills
        ├── destinations.txt
        └── hotel confirmation.PNG
```

Anything under `_src/` is local-only (raw photos, source notes, `.skill` files, drafts). Anything under `trips/` and the root `index.html` ships to Vercel.

## Adding a new trip

1. Pick a URL-safe slug: lowercase, kebab-case, year suffix — e.g. `tokyo-2026`.
2. Create the folders:
   ```bash
   mkdir -p trips/tokyo-2026 _src/tokyo-2026
   ```
3. Put working files (skills, raw photos, drafts) in `_src/tokyo-2026/`.
4. Put the finished `index.html` (and any `assets/`) in `trips/tokyo-2026/`.
5. Add a new `<a class="trip-card">` block to the root `index.html`, pointing at `/trips/tokyo-2026/`.
6. Commit and push — Vercel redeploys on push.

## Local preview

Any static file server works. From the repo root:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

## Deployment

Vercel is wired to this repo. Project → Settings:

- **Framework Preset:** Other
- **Root Directory:** `./` (repo root)
- **Build Command:** *(none)*
- **Output Directory:** *(none — serves repo root)*

`vercel.json` enables clean URLs and trailing slashes so `/trips/point-reyes-2026/` resolves to `trips/point-reyes-2026/index.html`.

## Conventions

- One `index.html` per trip. The trip folder *is* the deploy — no nested `deploy/` subfolders.
- URL slugs are kebab-case, no spaces, no encoded characters.
- Mirror each trip folder under `_src/` for working files, so source and deploy stay paired by name.
