# Piako Gliding Club website (Hugo prototype)

Static site built with [Hugo](https://gohugo.io) and Tailwind CSS, hosted on GitHub Pages, edited through [Pages CMS](https://pagescms.org).

## Editing (club members)

1. Go to <https://app.pagescms.org>, sign in with GitHub, and open this repository.
2. Choose what to edit from the sidebar: **Notices banner**, **Trial flight prices**, **Aircraft**, **Forms and documents**, or any page.
3. Click **Save**. The live site updates in about a minute.

Notices disappear by themselves the day after their "Show until" date.

Forms and documents: paste the Google Drive sharing link into the link's URL field. Links left empty show "Link to come" instead of a broken link. Who can open a document is controlled by its Drive sharing settings — this site is public.

Shared links (membership application form, GNZ operational forms): each lives once in **Site settings**. Anywhere else (a document row, a link in page text) use its short name as the URL, `membership-application` or `gnz-ops-forms`, and it points at whatever Site settings says. To add one, add a `<name>_url` field to Site settings.

Gift vouchers page: `{{< voucher-email >}}` in the text becomes the trial flights email address (from Site settings), as a link that starts an email with the subject and details filled in. Keep it as typed.

Pages link to people by role, not name — e.g. `[Secretary](/contact/#secretary)` jumps to that card under **Key contacts** on the Contact page. The link is the role in lower case with hyphens for spaces (`#chief-flying-instructor`), so renaming a role (say "Tugmaster" to "Tow master") breaks links to it.

## Development

Needs Hugo extended (0.169+) and Node 24.

```sh
npm install
npm run dev     # http://localhost:1313
npm run build   # output in public/
```

Where things live:

- `content/` — pages (Markdown + front matter). Aircraft are one file each in `content/aircraft/`; the Members page and Forms and documents are in `content/members/`.
- `data/` — notices, trial flight prices, site settings.
- `layouts/` — templates. A page at `content/<name>/index.md` uses `layouts/<name>/page.html`. Shared pieces (header, notices, page heading, call-to-action band) are in `layouts/_partials/`.
- `assets/css/main.css` — Tailwind entry point and design tokens.
- `.pages.yml` — what the CMS lets editors change.

## Deploying

Pushes to `main` deploy via `.github/workflows/deploy.yml`. In the repo's **Settings → Pages**, set the source to **GitHub Actions**.

Works at `<user>.github.io/<repo>/` or on a custom domain. Write internal links from the site root (`/weather/`, `/images/x.jpg`); the `url.html` partial and the Markdown render hooks in `layouts/_markup/` add the base path. Use `partial "url.html"` rather than `relURL` in templates — `relURL` leaves `/x` paths alone.
