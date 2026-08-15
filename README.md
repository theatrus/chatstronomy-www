# chatstronomy-www

The marketing site for **[chatstronomy.com](https://chatstronomy.com/)** — the
rebrand of [theatrus/spacecat](https://github.com/theatrus/spacecat), a N.I.N.A.
observing assistant that reports an imaging session to Discord and Matrix and,
optionally, accepts control of the rig from a chat channel.

Static HTML, no build step. Served by nginx on ec2admin from
`/www/chatstronomy.com`, which is a checkout of this repo: **push to `main` and
it deploys** via a flotswarm webhook.

| | |
|---|---|
| Docroot | `/www/chatstronomy.com` |
| Deploy | flotswarm action `deploy-chatstronomy-www` |
| TLS | per-site Let's Encrypt (certbot timer) |
| DNS | Porkbun A/AAAA -> ec2admin (`tfinfra roots/porkbun/chatstronomy-com.tf`) |

## Contents

| Path | What |
|---|---|
| `index.html` | landing page — **placeholder, copy not written yet** |
| `terms.html` | terms of service for the Discord application |
| `privacy.html` | privacy statement, same substance, separately linkable |
| `assets/` | images, favicon |

`terms.html` and `privacy.html` exist because Discord's application settings ask
for a Terms of Service URL and a Privacy Policy URL before an app can be
verified or listed. They describe software you run yourself; there is no service
here to have an account with.

## Editing

Plain files — no generator, no npm. Analytics and the cross-site "More projects"
band are injected by nginx from shared snippets, so no tag belongs in the HTML
(see `tfinfra docs/www-sites.md`).

## To do before launch

- Marketing copy for `index.html` (deliberately a placeholder; it carries
  `noindex` until it says something).
- A favicon and an OG image in `assets/` — no `<link rel="icon">` is referenced
  yet, so nothing 404s in the meantime.
- Review `terms.html` and `privacy.html` before pointing Discord's application
  settings at them.
