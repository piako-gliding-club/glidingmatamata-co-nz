# Agent notes

The club website: Hugo + Tailwind, deployed to GitHub Pages, edited by club members through Pages CMS. See [README.md](README.md) for how it's built, where things live and how editors use it.

## GitHub access

Agents work as a GitHub App installed on the `piako-gliding-club` org, so commits and PRs show as the bot rather than a person. The App's private key is a `.pem` file kept **outside the repo** (`*.pem` is gitignored — never commit one).

[`scripts/gh`](scripts/gh) runs `gh` with a token for this org's installation. It mints and caches the token itself (they expire hourly). It needs the [`gh-token`](https://github.com/Link-/gh-token) extension (`gh extension install Link-/gh-token`) and `~/.config/gh-app-piako.env`:

```sh
GH_APP_ID=<app id>
GH_APP_KEY=$HOME/path/to/app.private-key.pem
# GH_APP_REAL_GH=/opt/homebrew/bin/gh   # if gh isn't at /usr/bin/gh
```

- `gh` commands: run `scripts/gh …` (e.g. `scripts/gh pr create`), not plain `gh`, which may be signed in as someone else.
- `git push`/`fetch`: once per clone, make git use it for credentials:

  ```sh
  git config credential.https://github.com.helper ''
  git config --add credential.https://github.com.helper "!$PWD/scripts/gh auth git-credential"
  ```

If it fails with "isn't installed", the App needs installing on the org (with access to this repo) by an org owner.

## Working here

- Commit and push only when asked. Don't push to `main` without the human's go-ahead — every push to `main` deploys the live site.
- Run `npm run build` before pushing; it must finish with no warnings.
- Check UI changes in a browser at phone (390px) and desktop widths.
- Things editors change through the CMS must stay in `.pages.yml`: any new front-matter field or data file needs a matching entry, or the CMS may drop it on save.
