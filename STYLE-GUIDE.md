# Slidev Presentation Style Guide

Rules for creating and editing presentations in this Slidev setup.

---

## Philosophy

- **One idea per slide.** If a slide makes two arguments, split it.
- **Sparse copy, rich narration.** Slide text is a visual anchor. Speaker notes carry the explanation. The audience listens, not reads.
- **Why before what.** Lead with the reasoning, not the recommendation.

---

## Slide Text Rules

| Guideline | Target |
|---|---|
| Bullets per slide | 3–5 max |
| Words per bullet | 5–7 |
| Heading | Short declarative phrase or question |
| Sentences on slide | Avoid; fragments preferred |
| Emphasis | Bold one key term; `v-mark` for live annotation |

### Recommended patterns

- **Stat headline:** `<BigStat value="1 in 4" label="Survival to discharge" />` — hero number, short subtitle. No bullets needed.
- **Claim + elaboration:** A bold one-liner, then a plain-text line adding one layer of nuance.
- **Formula as code:** `` `CPP = Aortic diastolic − RA diastolic` ``
- **Color-coded cards:** `<CardGrid :items="[...]" />` for categorized concepts.

### What to avoid on slides

- Full sentences or paragraphs (speaker notes only)
- Nested bullets
- Jargon without immediate context for the audience

---

## Speaker Notes Voice

- **Casual oral register.** Write as if talking to a small group. Contractions, direct address, rhetorical questions.
- **Narrative arc.** Hook → content → takeaway. 4–8 sentences.
- **`[click]` cues.** Mark every `v-click` beat. `[click] First: the key finding.`
- **Interaction cues.** `[Let audience respond.]` to remind the presenter to pause.
- **Citations in `footerText`**, not notes. Notes reference studies casually: "Abella's 2005 study showed..."
- **Timer checkpoints.** Add `[~15 min mark]` at section boundaries to pace delivery.

---

## Visual & Interactive Patterns

### Click reveals
- Every conceptual unit gets its own `v-click`. Tables: per row. Cards: per card. Lists: per item.

### `v-mark` annotations
- `v-mark.red` — strikethrough or emphasis on a misconception
- `v-mark.underline.red` / `.yellow` — key stat underline
- `v-mark.highlight.yellow` — spotlight a phrase
- `v-mark.blue.box` — boxed number callout

### Components

- **`<BigStat>`** — hero number with subtitle. Props: `value`, `label`, `valueClass`.
- **`<CardGrid>`** — color-coded card layout. Props: `items` (array of `{title, body, color}`), `cols` (`'2'`/`'3'`/`'4'`), `reveal` (default true). Colors: red, amber, yellow, green, blue, sky, purple, gray.
- **`<RevealImage>`** — progressive image reveal with covers and annotation lines. Requires `clicks: N` in frontmatter.
- Extract any SVG or chart over ~15 lines into a dedicated `.vue` component.

### Emoji
- Sparingly. Only as visual anchors in card layouts, never in running text or headings.

---

## Color Language

| Color | Meaning |
|---|---|
| Red | Danger, key stat, critical action |
| Amber/Yellow | Caution, secondary emphasis |
| Green | Positive outcome, correct action |
| Blue/Sky | Neutral info, metrics |
| Purple | Alternate category |
| Gray | Supporting text, de-emphasis |

---

## Structural Rhythm

Sections follow this pattern:

1. **Section divider** (`SectionEditor`) — every 6–10 content slides
2. **Concept** — one big idea, centered
3. **Evidence** — chart, table, or stat callout
4. **Implication** — what this means in practice
5. Repeat 2–3 concepts per section

End with a **case or application** section, then a **summary** that mirrors the roadmap slide with answers filled in.

Budget ~1.5 min/slide. Use `layout: center` + `class: text-center` as the default for single-concept slides. Be consistent — don't mix bare default layout with centered layout for the same slide type.

---

## Layout Notes

Most layouts are self-explanatory from their names. Specifics worth knowing:

- **`SectionEditor`** — slots are `::title::` and `::subtitle::`.
- **`contrast`** — a CSS class (not a layout) that gives any slide a dark background. Use on evidence/data slides to visually separate them from concept slides.
- **`image-left`/`image-right`** — add `class: contrast flex flex-col justify-center text-center` for dark variant.

---

## Transitions

- Set `transition: slide-left` globally.
- Override with `transition: fade` on individual content slides within a section for less visual noise.
- Keep `slide-left` for section boundaries.

---

## Frontmatter

```yaml
layout: center
class: text-center
footerText: "Author et al. Journal Year;Vol(Issue):Pages."
clicks: 3                # only with RevealImage or manual click counts
hidefooter: "true"       # title slide only
transition: fade         # per-slide override
```
