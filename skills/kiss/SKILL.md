---
name: kiss
description: Explain a technical topic to a developer the keep-it-simple way, as one plain HTML page. The whole thing at a glance first, then drawings that zoom into each box with the real names, each followed by the same idea in plain words. Use when the user types /kiss <topic>, /kiss simple <topic> or /kiss deep <topic>, or asks for a simple, KISS or "explain it plainly" explainer of how some tech, system, flow or piece of code works, or which of two options to pick.
license: MIT
---

# kiss

Explain the topic to a developer in one self-contained HTML page they get in two minutes. **Zoom, don't simplify**: show the whole thing at a glance, then zoom into each part with the real names. Simple means fewer ideas at a time, never wrong ones.

Input: $ARGUMENTS

- If it starts with `simple` or `deep`, that word is the depth and the rest is the topic. Otherwise the depth is `normal`.
- If the topic is empty, use the topic from the conversation.

## Before you write

- If the topic names code in the current project, read that code first. Use its real names, files and flow. Say how you checked: "read in `src/router.ts`", "hit the endpoint".
- For a general topic, check the facts against a primary source (a spec or the official docs) when you can fetch one.
- Find the one concrete trace that carries the topic: "You type `github.com` and press Enter. 300 ms later the page is there." Open with that, not with a definition.
- Pick ONE everyday metaphor if it helps the glance. Never mix in a second one.
- Pick the shape. "How does X work" gets a glance and zooms. "X or Y?" gets a decision page: the pick in the h1, both options at a glance, then why.

## The page

Start from [template.html](template.html). Keep its tokens, dark mode and layout. Replace the content.

1. **Hero.** An h1 that IS the answer in one short sentence. A lede of 1–2 sentences with the concrete trace.
2. **At a glance.** The route under the lede (`.cast`, drawn as pills): 4–6 stops of the flow (actors, or the one object that carries it, such as the token) in the order of the trace, each once (a round trip too), in plain words with its character and a short real term. Mark the deciding stop with `li.hl` (a dashed yellow pill): where the answer is made, or where it breaks. Caption: what is marked and why, then "The drawings below zoom into each part." Then **In plain words.** 2–4 sentences.
3. **Zooms** (how many: see Depth). Each zoom opens one part of the glance (a part may get more than one zoom):
   - a headline that makes one claim and ends with a period;
   - a picture: a scene (the metaphor's objects doing the step), or a diagram when the order of messages is the point (see Drawings);
   - a caption: "Yellow: <the thing that matters>, because <why>." (in a diagram: "Highlighted: …");
   - **In plain words.** 1–3 sentences;
   - **Under the hood.** The real mechanism, its numbers matching the drawing's numbers (see Depth). A code block goes right after it;
   - one `.tag` per metaphor word, mapping it to its real name: `guest list = Access-Control-Allow-Origin`. Give each mapping once, in the first zoom that uses it.
4. **The catch.** The one thing that bites people.
5. **Push further.** Questions a sharp reader asks next: failure modes, races, what to cache, how to test. Each is a `<details>` with the question as `<summary>` and a 1–2 sentence answer inside.
6. **Footer.** What you simplified on purpose, in one line. The primary sources you used (specs, RFCs, official docs, or the project files as chips). Mark any claim you could not check as "not verified".

## Depth

| | `simple` | `normal` (default) | `deep` |
|---|---|---|---|
| Reader | new to the field | a developer new to this topic | an engineer who wants the internals |
| Zooms | 2–3, plain words in the drawings | 3–5, real names in the drawings | 4–6, sequence diagrams and state machines |
| Under the hood | none | 1–3 sentences | a numbered step list with real names, plus failure modes and real numbers (latency, sizes, limits) |
| Code | none | at most two blocks under 10 lines, only where code is the clearest picture | real snippets, under 20 lines each |
| Push further | 2 | 3 | 5 |
| Prose | 250–450 words | 500–900 words | 900–1,500 words |

Count prose as all visible text in the body except SVGs and `<pre>` blocks. Code chips and strip labels count.

## Drawings

Draw for a reader with a photographic memory: they should recall the page as pictures. [example.html](example.html) shows the bar; copy its drawing style, not its topic.

- **Scenes first.** Each zoom's picture is a scene: 1–3 big objects doing the step. A phone with its button sends two letters. A mailbox hands a letter to a clerk. A filing cabinet's drawers have on/off switches. Draw a sequence diagram only when the order of messages is the point (mostly at `deep`).
- **Draw objects big and flat.** The main object fills about a third of the card. Flat fills from the palette (`f-surface`, `f-bg`, `f-line`, `f-blue`, `f-accent`, `f-yes`, `f-no`), thick ink outlines (`s-ink`, `stroke-width` 2.5–3), rounded corners. Join objects with dashed curves (`s-muted`, `stroke-dasharray="5 5"`) and one solid ink line for the main move.
- **One yellow thing per scene**: the object that decides (`f-accent`). In a diagram, mark it with a `.pen` highlighter blob and a `.hot` path instead.
- **Labels are small.** Real names in mono under the object (`svg-t`, `svg-tm`), a title in display (`svg-tb`), text on yellow in `svg-ta`. Set `text-anchor` on each label. Keep real names short (about 16 characters); give the full name in the words.
- **The cast** (`<use href="#ico-…">`) can act in a scene, scaled up to about 84 units (1.3×; past that its outlines get too thick, so draw bigger objects yourself): `ico-browser`, `ico-server`, `ico-person`, `ico-phone`, `ico-laptop`, `ico-robot` (actors, with faces), `ico-db`, `ico-letter`, `ico-key`, `ico-lock`, `ico-list`, `ico-clock`, `ico-cloud`, `ico-gear`, `ico-box`, `ico-shield`, `ico-bolt`, `ico-stop`, `ico-check`, and props `ico-cabinet`, `ico-book`, `ico-bell`, `ico-bin`, `ico-door`, `ico-mailbox`, `ico-search`, `ico-switch-on`, `ico-switch-off`. Draw your own object when a scene needs one; keep the same look.
- **One object per actor, all page long.** The same drawing and color in the route and in every scene. When an actor changes role, color by role and say so in the caption.
- **A diagram**, when you need one: lifelines (`.life`), messages (`.wire`, `.wire.cut` for async), the shared `url(#arrow)` / `url(#arrow-hl)` markers, numbered `.num-bg` + `.num` circles that match the text, `.n` / `.t` / `.l` labels (centered; add `start` or `end` to align).
- **Every drawing is 340 units wide** (`viewBox="0 0 340 H"`), labels at 11 units or larger, at most 3 actors across, so it reads on a phone. Keep marks 10 units inside the edges.
- `role="img"` and a full-sentence `aria-label` on every drawing. Do not define ids inside a drawing.

## Words

- Short sentences (5–15 words). Active voice. Present tense. Bold the key word, not the sentence. A sentence in **Under the hood.** or a caption may run longer to name its real terms.
- Plain word first, then the real term in a code chip: "a guest list (`Access-Control-Allow-Origin`)".
- Give one or two real magnitudes where they help ("a Redis call is about 1 ms"). Never invent a number: a number is measured, sourced, or marked as an example ("say, 40 ms").
- At most two `.big` lines per page: the sentence a reader repeats to a colleague.
- Show states with pills: `.pill.yes`, `.pill.no`, `.pill.new`.
- No JavaScript unless the page needs tabs or a stepper. `<details>` needs none.
- Never add: taglines, a table of contents, an intro or conclusion section, floating labels such as "Step 1" or "The catch" above a heading, decorative emoji, external images, frameworks.
- Title: a 2–4 word name, such as "How a Request Travels", "The Guest List", "Cache On, Server Off", "Polling or WebSocket?".

## Deliver

If your environment can publish or render an HTML artifact, publish the page that way. Otherwise save it as `kiss-<topic-slug>.html` in the current directory and give the path. Then reply in at most two lines: the h1, and where the page is.
