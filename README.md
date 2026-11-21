# Piako Gliding Club website (Hugo prototype)

Static site built with [Hugo](https://gohugo.io) and Tailwind CSS, hosted on GitHub Pages, edited through [Pages CMS](https://pagescms.org).

## Editing (club members)

1. Go to <https://app.pagescms.org>, sign in with GitHub, and open this repository.
2. Choose what to edit from the sidebar: **Notices banner**, **Trial flight prices**, **Aircraft**, or one of the pages.
3. Click **Save**. The live site updates in about a minute.

Notices disappear by themselves the day after their "Show until" date.

## Development

Needs Hugo extended (0.169+) and Node 24.

```sh
npm install
npm run dev     # http://localhost:1313
npm run build   # output in public/
```

Where things live:

- `content/` — pages (Markdown + front matter). Aircraft are one file each in `content/aircraft/`.
- `data/` — notices, trial flight prices, site settings.
- `layouts/` — templates. A page at `content/<name>/index.md` uses `layouts/<name>/page.html`.
- `assets/css/main.css` — Tailwind entry point and design tokens.
- `.pages.yml` — what the CMS lets editors change.

## Deploying

Pushes to `main` deploy via `.github/workflows/deploy.yml`. In the repo's **Settings → Pages**, set the source to **GitHub Actions**.

Links written in Markdown (e.g. `[webcams](/weather/)`) assume the site is served from the domain root, so use a custom domain rather than `<user>.github.io/<repo>/`.
