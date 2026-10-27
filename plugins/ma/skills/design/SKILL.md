---
name: design
description: Generates 2-3 genuinely different design directions (palette, typography, grid, animation, desktop and mobile home), gathering fresh Awwwards references first, then has the user pick or combine them, iterates until approval and keeps the resources table up to date with missing copy and images. Use when the user says "do the design", "generate the proposals", "let's do the mockups", "generate the resources", "I like A but with B's typography", "fammi il design", "genera le proposte", "facciamo i mockup".
---

# Design — proposals, selection, iteration

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md`, `${CLAUDE_PLUGIN_ROOT}/references/git.md`,
`${CLAUDE_PLUGIN_ROOT}/references/memory.md` and
`${CLAUDE_PLUGIN_ROOT}/references/inspiration.md`. The quality checklist is in
`references/proposals.md`: apply it to every proposal before showing it.

## Step 0 — Prerequisites
`context/discovery.md` and `context/style.md` are required. If they are missing, run
`onboarding` or `style` first.

In **project** mode, if the `contract` phase in `context/state.md` is not `done`, warn
in one line ("The contract is not closed yet: design is the most expensive part") and
ask for confirmation before proceeding.

## Step 1 — References before proposals
Never start from a blank page. Follow
`${CLAUDE_PLUGIN_ROOT}/references/inspiration.md`:

- `context/inspiration.md` **missing**: gather the references now (Awwwards first) and
  write it.
- `context/inspiration.md` **present and older than 30 days**, or a new iteration after
  a rejected round: refresh it with one new query, adding rows, deleting none.
- `context/inspiration.md` **present and fresh**: use it as it is, and say so in one line.

Say in one line how many references are in play and the principles taken from them.

## Step 2 — Proposals
Generate **2–3 genuinely different directions**: not three variants of one idea, but
three different answers to the brief. In **pitch** mode, a single light proposal, hero
section only.

Every proposal contains:

| Item | Detail |
|---|---|
| Name | One word that identifies it |
| Idea | One sentence: what it bets on and why it works for this client |
| References | 1–3 rows from `context/inspiration.md` and the principle taken from each |
| Palette | Hex with the role of every colour (background, text, primary, accent, borders, states) |
| Typography | A pair of **open source** fonts (Google Fonts or similar), with scale and weights |
| Grid | Columns, gutter, max width, vertical rhythm |
| Animation | 3–5 key animations, each with its **no-animation fallback** (`prefers-reduced-motion`) |
| Home | Desktop **and** mobile |

Two proposals must not cite the same principle from the same reference: if they do, one
of them is not a different direction.

## Step 3 — Where to produce the design
In this order, using the first one available:
1. **Design artifact type**, if available;
2. **Figma**, if connected;
3. **static HTML page** in `design/proposals/vN/<proposal-name>/index.html`.

Say in one line which route was used.

Always save in `design/proposals/vN/README.md` the description of every proposal (the
table from step 2) and the link or path to the design.

## Step 4 — Selection
Ask, in a single question:
- which proposal to keep, or
- which proposals, or
- **which parts of each** (e.g. "A's palette, B's typography, C's hero");

and always **the reason**. Record everything in `context/decisions.md`: date, phase
`design`, decision, reason.

## Step 5 — Iteration
Generate `vN+1` as a **synthesis of the choices**, not as a new round of proposals.
Repeat proposals → selection until the user approves. Every iteration closes with the
commit `ma: design vN`.

If a whole round is rejected, refresh the references (step 1) before the next round:
repeating the same inspiration produces the same proposals.

## Step 6 — Resources
Fill and keep `resources/resources.md` updated with one row for every resource the
design genuinely requires. Statuses: `Missing`, `Present`, `Generated`, `To approve`.
- Generate realistic **copy** for every section, in the tone of the keywords: **never
  lorem ipsum**. Status `To approve`.
- For every **missing image**, write subject, framing and format in the notes, so the
  user can produce or shoot it. If an image generator is available, use it and mark
  `Generated`.
- Never overwrite resources with status `Present`.
- If the copy depends on information only the client has (claims, numbers, names), run
  the `questionnaire` skill with the `content` set instead of inventing it.

## Step 7 — Approval
When the user approves:
1. write "Design approved on YYYY-MM-DD" in `context/state.md` and `context/decisions.md`;
2. phase `design` = `done`;
3. summary table: `Present | Generated | To approve | Still missing`;
4. commit `ma: design vN`;
5. a single next step (usually the development in `site/`, or the next phase of the mode).

## Rules
- References give **principles**: never identical layouts, logos, copy or images.
- No photographs of real people taken from the web.
- Use only the palette, fonts and copy decided in the previous steps: no surprise
  colours or fonts.
- Do not start the code in `site/` before approval.
