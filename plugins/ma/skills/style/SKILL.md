---
name: style
description: Collects the visual direction of the project - existing logo and brand, reference sites or apps, keywords, what to avoid and constraints - automatically gathers award-level references from Awwwards for the client's sector, and writes it all into context/style.md as the brief for the design. Use when the user says "let's talk style", "here are the references", "I like this site", "let's do a moodboard", "parliamo di stile", "ecco i riferimenti", "facciamo il moodboard", or when style is the next phase in the state.
---

# Style — references and visual direction

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md`, `${CLAUDE_PLUGIN_ROOT}/references/git.md`,
`${CLAUDE_PLUGIN_ROOT}/references/memory.md` and
`${CLAUDE_PLUGIN_ROOT}/references/inspiration.md`.

Prerequisite: `context/discovery.md`. If it is missing, run `onboarding` first.

## Step 1 — The questions
At most 4 per turn, free-text answers always allowed. First check `context/` and
`registry/preferences.md` (`design` scope): what is already known is confirmed, not
asked again.

1. **Existing logo and brand**: are there any? Ask for the files in `references/`
   (logo, brand manual, palette, fonts) and say which ones arrived.
2. **References**: 2–5 sites or apps, as links or screenshots in `references/`.
   If the user has none, say in one line that step 2 will propose some, and move on.
3. **Keywords**: 3–5 adjectives for the feeling to convey (e.g. essential, warm,
   technical, luxurious).
4. **What to avoid**: styles, colours, clichés, competitors not to resemble.
5. **Constraints**: mandatory brand colours, licensed fonts, required accessibility
   level, languages, technical constraints from the discovery.

## Step 2 — Automatic references (Awwwards)
Always run, even when the user supplied their own references: they are complemented,
never replaced.

Follow `${CLAUDE_PLUGIN_ROOT}/references/inspiration.md`: build the queries from sector
and keywords, fetch Awwwards first, fall back to the secondary galleries, and write
`context/inspiration.md` with the table required there.

Then say, in two lines: how many references were gathered, from which source, and the
three recurring principles that came out of them. If fewer than 3 were usable, say so
and carry on: the phase is not blocked.

## Step 3 — Break the references down
For **every** reference — the user's and the automatic ones — write a row in
`context/style.md`:

| Reference | What to take | What not to take |
|---|---|---|
| link or file | typography, grid, colour, animation, tone — be specific | what does not fit this project |

"What to take" must be a concrete principle ("very large headings with tight leading",
"400 ms fade page transitions"), never a generic verdict ("it looks nice").

## Step 4 — The existing brand
If there is a logo or a brand manual:
- derive the palette (hex with the role of each colour) and the character of the brand;
- list them as **constraints** at the top of `context/style.md`, separate from the
  hypotheses;
- flag any problems in one line (insufficient contrast, font with no web licence).

## Step 5 — Synthesis
Close `context/style.md` with:
- **Direction in one sentence**: where we are going.
- **Keywords** and **what to avoid**, as lists.
- **Constraints** that must be respected.
- **To settle in design**: the points where the references contradict each other.
- **Inspiration**: a one-line pointer to `context/inspiration.md` and how many rows it holds.

## Closing
1. Record the choices in `context/decisions.md`.
2. Update `context/state.md`: phase `style` = `done`, current phase = next of the mode.
3. Commit `ma: style`.
4. State in one line the next phase according to the mode.

## Rules
- References give **principles**, never identical layouts, logos, copy or images.
- Never promise a result "like" a reference: the idea is borrowed, not the site.
- An automatic reference that clashes with "what to avoid" is dropped, and the drop is
  noted in one line.
