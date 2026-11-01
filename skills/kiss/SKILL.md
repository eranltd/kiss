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
2. **At a glance.** The cast strip (`.cast`) under the lede: 4–6 members of the flow (actors, or the one object that carries it, such as the token) in the order of the trace, each once (a round trip too), in plain words with its character and a short real term, the deciding one circled (`li.hl`). Caption: what is circled and why, then "The drawings below zoom into each part." Then **In plain words.** 2–4 sentences.
3. **3–6 zooms.** Each zoom opens one part of the glance (a part may get more than one zoom):
   - a headline that makes one claim and ends with a period;
   - a drawing with the real names (a numbered sequence diagram for a flow, a state machine for states, a layout for data);
   - a caption: "Highlighted: <the step that matters>, because <why>.";
   - **In plain words.** 1–3 sentences;
   - **Under the hood.** The real mechanism, its numbers matching the drawing's numbers (see Depth). A code block goes right after it.
4. **The catch.** The one thing that bites people.
5. **Push further.** Questions a sharp reader asks next: failure modes, races, what to cache, how to test. Each is a `<details>` with the question as `<summary>` and a 1–2 sentence answer inside.
6. **Footer.** What you simplified on purpose, in one line. One or two primary sources (a spec, an RFC, the official docs, or the project files as chips). Mark any claim you could not check as "not verified".

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

Draw for a reader with a photographic memory: they should recall the page as pictures.

- **Draw with the cast.** The template's sprite holds hand-drawn characters: `ico-browser`, `ico-server`, `ico-person`, `ico-phone`, `ico-robot` (actors, with faces), and `ico-db`, `ico-letter`, `ico-key`, `ico-lock`, `ico-list`, `ico-clock`, `ico-cloud`, `ico-gear`, `ico-box`, `ico-shield`, `ico-bolt`, `ico-stop`, `ico-check`. Place one with `<use href="#ico-server" x y width height/>`.
- **One character per actor, all page long.** The same character and color in the strip and in every drawing: on top of its lifeline in a flow, beside its part in a layout or a state picture. Recolor with `style="--fill:var(--c-pink)"` only to tell two of a kind apart. When an actor changes role (a follower becomes the leader), color by role and say so in the caption.
- **One picture per zoom that a reader could recall with closed eyes**: the letter with a stamp, the lock on the door, the stop sign on the reply.
- If the cast lacks an object, draw it the same way: a 64×64 `<symbol>`, the `o` outline class, one crayon fill, a face only for an actor.
- **Red pen marks what matters.** One per drawing: a `.pen` ellipse around it, tilted a few degrees, and `.hot` with `url(#arrow-hl)` for its path when it has one; both mark the same thing. Everything else stays ink. Keep the pen at least 10 units inside the drawing's edges so it is not clipped.
- `.wire` is the main path. `.wire.cut` (dashed) is async, optional, or off the hot path.
- In a flow, numbered `.num-bg` + `.num` circles match the numbers in the text. A layout or a state picture needs no numbers.
- Keep real names short in drawings and in the strip (about 16 characters: `ACAO header`, `Origin`). Give the full name in the words.
- Text is centered. Add `class="… start"` or `"… end"` to align a label left or right.
- Label a store or outside system with why it is there: "Redis · locks, 30-day TTL".
- **Fit a phone.** A `viewBox` 400 units wide, at most 3 actors across, labels at 13 units or larger. With more actors, stack the flow top to bottom, or draw 3 and say in the footer what the real system has ("Raft clusters usually run five servers").
- `role="img"` and a full-sentence `aria-label` on every drawing. Use the template's shared markers and filter; do not define ids inside a drawing.

## Words

- Short sentences (5–15 words). Active voice. Present tense. Bold the key word, not the sentence. A sentence in **Under the hood.** or a caption may run longer to name its real terms.
- Plain word first, then the real term in a code chip: "a guest list (`Access-Control-Allow-Origin`)".
- Give one or two real magnitudes where they help ("a Redis call is about 1 ms"). Never invent a number: a number is measured, sourced, or marked as an example ("say, 40 ms").
- No JavaScript unless the page needs tabs or a stepper. `<details>` needs none.
- Never add: taglines, a table of contents, an intro or conclusion section, floating labels such as "Step 1" or "The catch" above a heading, decorative emoji, external images, frameworks.
- Title: a 2–4 word name, such as "How a Request Travels", "The Guest List", "Cache On, Server Off", "Polling or WebSocket?".

## Deliver

If your environment can publish or render an HTML artifact, publish the page that way. Otherwise save it as `kiss-<topic-slug>.html` in the current directory and give the path. Then reply in at most two lines: the h1, and where the page is.
