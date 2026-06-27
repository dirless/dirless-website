# dirless-website

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

Static marketing site for [dirless.com](https://dirless.com), served via GitHub Pages. Also hosts the RPM package repository for `x86_64` and `aarch64`.

## Pages

| File | URL |
|------|-----|
| `index.html` | `https://dirless.com/` |
| `how-it-works.html` | `https://dirless.com/how-it-works.html` |
| `faq.html` | `https://dirless.com/faq.html` |

## RPM repository

The RPM repo is hosted at `https://dirless.com/rpm/`. Customers install the repo file:

```sh
curl -Lo /etc/yum.repos.d/dirless.repo https://dirless.com/rpm/dirless.repo
dnf install -y dirless-agent
```

To add a new package: drop the `.rpm` into `rpm/<arch>/` and regenerate `repodata` with `createrepo_c`.

## Deployment

| Branch | URL | How |
|--------|-----|-----|
| `main` | `https://dirless.com` | GitHub Pages auto-deploys on push |
| `staging` | `https://staging.dirless.com` | Manually pulled on the ops machine |

```sh
# Deploy staging
git push origin staging
ssh -i ~/.ssh/id_ed25519_github -p 39124 root@<ops-ip> "git -C /var/www/staging.dirless.com pull"

# Go live: merge staging → main
git checkout main && git merge staging && git push
```

## Nav consistency rule

Every page must have the identical nav on desktop and mobile — copy the nav block from an existing page exactly. Never use conditional classes to hide nav elements at specific screen sizes.
