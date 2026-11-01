---
name: kiss
description: Explain a technical topic to a developer the keep-it-simple way, as one plain HTML page. A short route of the whole flow comes first, then one stamped step per stop, each with a big flat drawing on the left and a few words with the real names on the right. Use when the user types /kiss <topic>, /kiss simple <topic> or /kiss deep <topic>, or asks for a simple, KISS or "explain it plainly" explainer of how some tech, system, flow or piece of code works, or which of two options to pick.
license: MIT
---

# kiss

Explain the topic to a developer in one self-contained HTML page they get in two minutes. **Zoom, don't simplify**: show the whole route first, then walk it one stop at a time with the real names. Simple means fewer ideas at a time, never wrong ones.

Input: $ARGUMENTS

- If it starts with `simple` or `deep`, that word is the depth and the rest is the topic. Otherwise the depth is `normal`.
- If the topic is empty, use the topic from the conversation.

## Before you write

- If the topic names code in the current project, read that code first. Use its real names, files and flow.
- For a general topic, check the facts against a primary source (a spec or the official docs) when you can fetch one.
- Find the one concrete trace that carries the topic: "You press Send on a note to Bob." The page follows that trace stop by stop. Do not open with a definition.
- Pick ONE everyday metaphor that runs the whole way, in the words and in the drawings (a post office: letters, a post box, a receipt, a filing cabinet). Never mix in a second one. Where the metaphor bends the truth (a guest list that holds one name), say so in one sentence in that step.
- Pick the shape. "How does X work" walks the route. "X or Y?" gives the pick in the lede, the two options as `.doors`, and the reasons in a why step.

## The page

Start from [template.html](template.html). Copy its `<head>` and `<style>` unchanged except the `<title>`, and replace the content. Use only the template's components. [example.html](example.html) is a finished page at `normal` depth. Copy its drawing style, not its topic.

1. **Hero** (`header.hero`):
   - `.eyebrow`: the area and "explained simply" ("Email · explained simply").
   - h1: 2–6 words, such as "How an email travels". For a decision: "Polling or WebSocket?".
   - The lede `p`: 1–2 sentences with the trace and the answer. Bold 2–3 key words with `<b>`. A real name in the lede goes in `<code>`.
   - `.route`: 4–7 stops in the order of the trace, each a `span.stop` with a short real name or plain word (`:587`, `MX lookup`), with a `span.arrow` (→) between stops. Keep it on one line at desktop width: about 70 characters in all.
2. **Steps** (`section.step`, how many: see Depth). Walk the route in order. Each step covers one or two neighboring stops, so the idea of every stop appears in a step (its label need not). A fact that is not on the route goes in the step where it bites, or in the end box.
   - `.pic`: one drawing (see Drawings).
   - `.words`: a `.head` with the `.stamp` number and an h2 that says what happens, in plain words and without a period. Then 1–3 short paragraphs: what happens in plain words, then the real mechanism with the real names in `<code>`.
   - `.tags`: one tag per metaphor word or plain word, mapped to its real name (`receipt = 250 reply`). Give each mapping once, in the first step that uses it.
   - Add at most two of these, when one is the clearest form: a table in `.scroll` (2–5 rows, at most 3 columns so it fits a phone; use `.pill.yes`, `.pill.no` or `.pill.new` only for states), `.ba` (the same thing in two states or at two times, 2–3 short items each), `.doors` (two separate paths, each with an h3, a sentence and an optional `<pre>`), or a `<pre>` (a request, a response or a short code block).
   - `.big-idea`: the sentence a reader repeats to a colleague, in any step, the why step included. Use at most two per page.
3. **Why** (optional at every depth): one more `section.step` with `.stamp.why`, an h2 that starts with "Why", and an `ol.reasons` of 2–3 reasons, each led by a bold sentence. Use it when the design choice is the surprising part. Its drawing shows the main reason. It does not count as a step.
4. **End box** (`section.status`): an h2 in plain words ("Before you rely on it"), then a list. Each `li` holds a pill and a sentence:
   - `catch` (`.pill.no`): the one thing that bites people, and what to do instead.
   - `ask next` (`.pill.new`): a question a sharp reader asks next, in bold, then a 1–2 sentence answer. Give one `li` per question (how many: see Depth).
   - `simplified` (`.pill.new`): what the page leaves out on purpose, in one line.
   - `sources` (`.pill.yes`): the primary sources you used, as links, or the project files as code chips.
   - `not verified` (`.pill.no`): any claim you could not check. Omit this `li` when there is none.

## Depth

| | `simple` | `normal` (default) | `deep` |
|---|---|---|---|
| Reader | new to the field | a developer new to this topic | an engineer who wants the internals |
| Steps | 3–4, plain words in the drawings | 4–6, real names in the drawings | 6–8, usually plus a why step |
| Words in a step | plain words only | plain words, then 1–3 sentences with real names | plain words, then the mechanism with its failure modes and real numbers (latency, sizes, limits) |
| Code | none | at most two `<pre>` blocks of up to 10 lines | requests, responses and snippets of up to 20 lines each |
| `ask next` | 1 | 2–3 | 4–5 |
| Prose | 250–450 words | 500–900 words | 900–1,500 words |

Count prose as the visible text of the hero, the steps and the end box. Do not count SVGs, `<pre>` blocks, the route or the tags.

## Drawings

Draw for a reader with a photographic memory: they should recall the page as pictures. The template's drawings show the paint. Draw your own topic's objects.

- **One scene per step**: 1–3 big flat objects doing the step. A laptop drops a letter in a post box. A card file shows the right row. A filing cabinet has one drawer open. The main object fills about a third of the card.
- **When the order of messages is the point** (mostly at `deep`), draw a short sequence instead: the objects small at the top, dashed `s-line` lifelines down, and numbered `s-ink` lines between them. End each line in a small filled triangle (`f-ink`).
- **Paint only with the template's classes**: fills `f-surface`, `f-bg`, `f-line`, `f-muted`, `f-ink`, `f-accent`, `f-yes`, `f-no`, and strokes `s-ink`, `s-muted`, `s-line`, `s-accent`. Do not write colors, so dark mode works.
- **The object in play** has an `s-ink` outline, `stroke-width` 2.5–3, with rounded corners. Objects that wait get `s-line` at width 2. Draw a move as a dashed `s-muted` curve (`stroke-dasharray="5 5"`, width 2), or one solid `s-ink` line for the move that matters.
- **One orange thing per drawing**: the part that decides, filled `f-accent` or outlined with a dashed `s-accent`. A group that reads as one thing (three ticks, one row across three servers) counts as one. When two parts are equal, mark the one this step is about. Text on an orange fill uses `svg-ta`, real name or not. Rows that are "on" can use `f-yes` at `opacity` .2–.35; they are not orange.
- **Simple shapes**: a person is a circle head on a rounded body, a letter is a rectangle with a V, text on a screen or a card is grey bars (`f-line`). No faces, icons or emoji.
- **Labels**: a title in `svg-tb`, a real name in `svg-t`, a caption under an object in `svg-tm`. Set `text-anchor` on every label. Keep labels under about 16 characters: shorten a long name with an ellipsis (`dns4.p08…`) and give the full name in the words. To check fit, a mono character is about 7.2 units wide in `svg-t` and 6.6 in `svg-tm`; a display character is about 8.5 in `svg-tb`.
- **Size**: `viewBox="0 0 340 220"` (230 when a scene needs more room). Labels at 11 units or larger, at most three objects across, and marks 10 units inside the edges, so it reads on a phone.
- Put `role="img"` and a full-sentence `aria-label` on every drawing. Do not use ids, `<defs>`, filters or gradients in a drawing.

## Words

- Short sentences (5–15 words). A sentence that carries several real names may run longer. Active voice. Present tense. Bold the key word, not the sentence.
- Plain word first, then the real name in a code chip: "a guest list (`Access-Control-Allow-Origin`)".
- Give one or two real magnitudes per step when they help ("retry after at least 30 minutes"). Never invent a number: a number is measured (say how and when, in `sources`: "measured with `dig` on 1 Nov 2026"), sourced, or marked as an example (in a `<pre>` comment or in `simplified`).
- A hedged claim ("often", "usually") needs a source or a `not verified` item.
- No JavaScript.
- Never add: taglines, a table of contents, an intro or conclusion section, a label above a heading, decorative emoji, external images, frameworks.
- `<title>`: a 2–4 word name, such as "How an Email Travels", "The Guest List", "Polling or WebSocket?".

## Deliver

If your environment can publish or render an HTML artifact, publish the page that way. Otherwise save it as `kiss-<topic-slug>.html` in the current directory and give the path. Then reply in at most two lines: the h1, and where the page is.
