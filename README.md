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
native Direct integration, local Discord/Matrix delivery, deprecated Advanced
API compatibility for existing installations, and multi-machine pairing through
the recommended [Chatstronomy Hub](https://hub.chatstronomy.com/). Installation is through
N.I.N.A.'s plugin manager: use the built-in official repository when the public
listing is available, or add the development repository alongside it:

`https://raw.githubusercontent.com/theatrus/chatstronomy-nina-plugin/main/registry`

Keep its install warning accurate: development packages contain the pinned,
signed Rust runtime but an unsigned development `Chatstronomy.dll`; official
plugin tags sign and verify both before packaging.

`terms.html` and `privacy.html` exist because Discord's application settings ask
for a Terms of Service URL and a Privacy Policy URL before an app can be
verified or listed. They currently describe only software you run yourself and
do not cover the hosted Hub.

## Editing

Plain files — no generator, no npm. Analytics and the cross-site "More projects"
band are injected by nginx from shared snippets, so no tag belongs in the HTML
(see `tfinfra docs/www-sites.md`).


## The Hub requires service terms

`terms.html` and `privacy.html` currently say the application talks to nothing
of ours, which remains true only of the self-hosted version. Both pages are
scoped to the self-hosted application and say a service is planned, so neither
covers the hosted Hub.

Before public hosted launch, the Hub needs its own terms and privacy statement
covering, at minimum: what it stores and for how long, where it runs, who can
see an observatory's data, what happens to it on account closure, and what a
compromise of the service means for connected equipment — which, if it can
relay control commands, is the same equipment risk described under "Telescope
control", now with our infrastructure in the path.
