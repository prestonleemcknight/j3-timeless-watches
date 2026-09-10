# J3 Timeless Watches — customer preview

A single-page preview of the new storefront, built to be sent to a customer as
a link. Real catalog, real photography, real prices and real plan terms, pulled
from the current Big Cartel store. Checkout is not connected.

```
index.html      the whole site — markup, styles, catalog and app in one file
hero/           the exploded-watch film (MP4 + WebM)
```

No build step. No dependencies. Open `index.html` and it runs.

## Publish it

This folder is already an initialised git repository with the first commit
made, so there is nothing to stage. Create an empty repository on GitHub named
`j3-timeless-watches` — no README, no .gitignore, no licence — then run two
commands from this folder:

```bash
git remote add origin https://github.com/<your-username>/j3-timeless-watches.git
git push -u origin main
```

Git will ask for your username and a password: the password is a **personal
access token**, not your account password (github.com → Settings → Developer
settings → Personal access tokens). If you would rather not deal with tokens,
install the GitHub CLI and run `gh auth login` first, and the push just works.

The commit is authored as `prestonleemcknight@gmail.com`. To change it:

```bash
git -c user.name="Your Name" -c user.email="you@example.com" commit --amend --reset-author --no-edit
```

Then in the repository on github.com: **Settings → Pages → Source →
GitHub Actions**. The workflow in `.github/workflows/pages.yml` runs on every
push to `main` and publishes the folder as-is.

Your link, about a minute later:

```
https://<your-username>.github.io/j3-timeless-watches/
```

Send that to a customer. Every push to `main` updates it.

**Public repository, public link.** GitHub Pages sites are visible to anyone
who has the URL, and on a free account the repository must be public for Pages
to work. Nothing here is sensitive — no keys, no customer data, no order data —
but the preview is not private, so treat the URL as shareable rather than
secret. It carries `<meta name="robots" content="noindex">` so it stays out of
search results until the real domain is live.

## Two things to know

**The product photography is hot-linked to Big Cartel.** The images live at
`assets.bigcartel.com` and load straight from there. That keeps this repository
small and the photos identical to what is listed today — but it also means the
preview depends on that store staying up. When the Big Cartel store is retired,
the photos need to be downloaded and committed to this repository first, and
the image URLs in `index.html` repointed at them.

**This is the preview, not the shop.** Cart and checkout are deliberately
inert. The full Next.js application — Stripe checkout, payment plans, order
email, the admin surface — is a separate codebase and needs a real host
(Vercel, Fly, a container anywhere) plus a Postgres database. Pages can only
serve static files, which is exactly why this preview is one.

## Updating it

Regenerate `index.html` from the source project and commit it. The film in
`hero/` only changes when the clip does.
