# dirless-website

Static website for [dirless.com](https://dirless.com), served via GitHub Pages. Also hosts the RPM package repository for `x86_64` and `aarch64`.

## What it contains

| File/Directory | Purpose |
|----------------|---------|
| `index.html` | Landing page |
| `how-it-works.html` | How it works — four components explained |
| `faq.html` | FAQ page |
| `dirless.png` | Logo |
| `favicon.ico` | Favicon |
| `CNAME` | `dirless.com` — GitHub Pages custom domain |
| `rpm/x86_64/` | RPM repo (repodata + packages) for x86_64 |
| `rpm/aarch64/` | RPM repo (repodata + packages) for aarch64 |
| `rpm/dirless.repo` | Yum/DNF repo file customers add to `/etc/yum.repos.d/` |

## Nav consistency rule

Every page must have the **identical nav** on desktop and mobile. The full nav link set is:
- How it works → `/how-it-works.html`
- Features → `/#features`
- Pricing → `/#models`
- FAQ → `/faq.html`
- GitHub → (blue `nav-cta` button)
- Sign up → (green `nav-cta` button → `https://portal.dirless.com/register`)

When adding a new page, copy the nav block from an existing page exactly. Never use conditional classes to hide nav elements on specific screen sizes — the GitHub button is visible on all pages at all screen sizes.

## Contact email

`info@dirless.com` — displayed on the site as HTML entity encoding to resist scraping. Do not write the address as plain text in HTML.

## RPM repository

The RPM repo is hosted at `https://dirless.com/rpm/`. Customers install the repo file then install packages with `dnf install dirless-agent` etc.

To add a new RPM package: build the `.rpm`, add it to the appropriate arch directory, then regenerate `repodata` with `createrepo_c`.

## Deployment

Pushing to the `main` branch deploys automatically via GitHub Pages. No build step — everything is static.
