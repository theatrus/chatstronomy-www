# chatstronomy-www

The marketing site for **[chatstronomy.com](https://chatstronomy.com/)** — the
rebrand of [theatrus/spacecat](https://github.com/theatrus/chatstronomy), a N.I.N.A.
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
| `index.html` | landing page |
| `terms.html` | terms of service for the Discord application |
| `privacy.html` | privacy statement, same substance, separately linkable |
| `assets/` | images, favicon |

Branding comes from `theatrus/chatstronomy` (`assets/branding/`) — the same
artwork on every surface. `assets/logo.png` is the transparent master,
`favicon.ico` carries the Windows sizes, and the graph samples are real output
from the app rather than mock-ups.

The landing page also tracks the separately released
[`theatrus/chatstronomy-nina-plugin`](https://github.com/theatrus/chatstronomy-nina-plugin):
native Direct integration, local Discord/Matrix delivery, Advanced API
compatibility, multi-machine hub pairing, and development-build installation.
Keep its install warning accurate: ordinary CI packages contain the pinned,
signed Rust runtime but an unsigned development `Chatstronomy.dll`; official
plugin tags sign and verify both before packaging.

`terms.html` and `privacy.html` exist because Discord's application settings ask
for a Terms of Service URL and a Privacy Policy URL before an app can be
verified or listed. They describe software you run yourself; there is no service
here to have an account with.

## Editing

Plain files — no generator, no npm. Analytics and the cross-site "More projects"
band are injected by nginx from shared snippets, so no tag belongs in the HTML
(see `tfinfra docs/www-sites.md`).


## The multi-server change is a terms change

`terms.html` and `privacy.html` currently say the application talks to nothing
of ours, which is true of the self-hosted version and **stops being true the day
a coordinating service ships**. Both pages are scoped to the self-hosted
application and say a service is planned, so neither becomes false on its own —
but neither covers a service either.

Before that service takes its first connection it needs its own terms and
privacy statement covering, at minimum: what it stores and for how long, where
it runs, who can see an observatory's data, what happens to it on account
closure, and what a compromise of the service means for connected equipment —
which, if it can relay control commands, is the same equipment risk described
under "Telescope control", now with our infrastructure in the path.
