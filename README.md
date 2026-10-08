# Evara By The Ganges — Vercel Deployment

## Project type
This is a **static HTML project** — plain `.html` files with inline `<style>` and `<script>`, no framework.
It is **not** Next.js and **not** React/Vite, and there is no build step: Vercel serves the files in `public/` directly as static assets.

## Structure
```
evara-vercel/
├── package.json        minimal — only for local preview, no real build
├── vercel.json          clean URLs (e.g. /about instead of /about.html) + image caching
├── .gitignore
└── public/
    ├── index.html               Homepage (was evara-by-the-ganges-homepage.html)
    ├── about.html
    ├── stay.html
    ├── amenities.html
    ├── explore.html
    ├── apartments.html          (not linked in nav — kept for reference)
    ├── booking-contact.html
    ├── blog.html
    ├── blog-post-sample.html
    ├── guest-policy.html
    ├── privacy-policy.html
    ├── refund-policy.html
    └── images/                  all site photos (~5MB, 19 files)
```

## Fonts
No self-hosted font files are included. All typography (Cormorant Garamond + Jost) loads live from Google Fonts via `<link>` tags already in each page's `<head>`. This requires no extra setup — Vercel's CDN doesn't need to serve fonts itself, Google's CDN does. If you'd rather self-host the fonts (for offline builds or stricter CSP), say so and they can be downloaded and added under `public/fonts/`.

## Deploying

**Option A — Vercel CLI**
```bash
npm i -g vercel
cd evara-vercel
vercel --prod
```

**Option B — Drag and drop / Git**
1. Push this folder to a GitHub repo (or drag the folder into vercel.com/new).
2. In the Vercel dashboard, import the repo/folder.
3. Framework Preset: choose **"Other"** (Vercel will auto-detect no build needed).
4. Output directory: `public` (Vercel should auto-detect this from `vercel.json`, but confirm it during import).
5. Deploy.

No environment variables, database, or backend are required — every page is fully self-contained. The booking/contact form (`booking-contact.html`) has no backend on this static version (`onsubmit="return false;"`); it posts nowhere. If you want working form submissions, that needs either a serverless function (Vercel supports this with an `/api` folder) or a form service like Formspree.

## Clean URLs
`vercel.json` sets `"cleanUrls": true`, so once deployed, `/about`, `/stay`, `/booking-contact`, etc. all work without the `.html` extension — matching the relative links already used across the pages.

## Notes
- `evara-by-the-ganges-theme.zip` (the parallel WordPress theme) is a separate deliverable and is **not** part of this Vercel project — WordPress needs PHP + a database, which Vercel's static hosting does not provide.
