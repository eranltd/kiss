# kiss

Keep it simple. Explain any tech topic to a developer as one plain HTML page.

![The top of a kiss page: the title, a two-line trace, the route of stops, and step 1 with a laptop, an orange key and a post box](docs/hero.png)

```
/kiss how CORS works
/kiss deep how CORS works
/kiss simple how CORS works
/kiss how our auth middleware works
/kiss polling or websockets?
```

**Zoom, don't simplify.** You get one page with:

- **The trace and the route.** One concrete example in two sentences, then every stop it makes, in order.
- **One stamped step per stop.** A big flat drawing on the left. On the right, what happens in plain words, then the real names.
- **One orange thing per drawing.** The part that decides.
- **A why step** when the design choice is the surprising part.
- **An honest end box.** The catch, the questions to ask next, what was simplified, the sources, and anything not verified.

## Depth

Simple means fewer ideas, never wrong ones. Pick how far down you go:

| | Reader | What changes |
|---|---|---|
| `simple` | new to the field | 3–4 steps in plain words. No code. |
| default | a developer new to the topic | 4–6 steps with the real names, each with a short "under the hood". |
| `deep` | an engineer who wants the internals | 6–8 steps plus a why step: failure modes, real numbers, requests and code. |

![A step in dark mode: a filing cabinet with the INBOX drawer in orange and Bob's phone on the left, the stamp, claim and words on the right](docs/zoom.png)

Ask about code in your project and it reads the code first, then uses the real file and function names.

The page is a single HTML file in Claude's palette (black ink, warm greys, one orange): no framework, light and dark mode, phone-friendly. If your Claude can publish artifacts, it publishes one. Otherwise it saves `kiss-<topic>.html`.

The skill ships a reference page, [`skills/kiss/example.html`](skills/kiss/example.html) (how an email reaches an inbox), that sets the drawing bar for every run.

See [examples/](examples/): CORS at two depths ([`how-cors-works.html`](examples/how-cors-works.html), [`how-cors-works-deep.html`](examples/how-cors-works-deep.html)), Raft consensus ([`how-raft-works.html`](examples/how-raft-works.html)), Google One Tap ([`how-google-one-tap-works.html`](examples/how-google-one-tap-works.html)) and DNS ([`how-dns-works.html`](examples/how-dns-works.html)).

<img src="docs/phone-dark.jpg" alt="The same step on a phone in dark mode: the cabinet drawing above its stamped heading and words" width="320">

## Install

```
/plugin marketplace add eranltd/claude-plugins
/plugin install kiss@eranltd
```

That marketplace also lists [pixel-pet](https://github.com/eranltd/pixel-pet). To add this repo on its own instead: `/plugin marketplace add eranltd/kiss`, then `/plugin install kiss@kiss`.

## Why not ELI5?

ELI5 talks to a five-year-old. `kiss` talks to someone who studied this stuff and is new to this one topic: few words and big pictures, but it keeps the real terms, shows the mechanism, and points at where it lives in the code.

## License

MIT
