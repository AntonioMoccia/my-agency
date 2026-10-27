---
name: onboarding
description: Prepares the project folder (template, folders, git, state) and runs the client discovery with questions on business, goal, audience, market, typology, features, content, constraints and what already exists. Use when the user says "start the onboarding", "new project", "new client", "let's start the website", "let's do the discovery", "avvia l'onboarding", "nuovo cliente", "facciamo la discovery", or when the project skill finds no context/state.md.
---

# Onboarding — setup and discovery

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md`, `${CLAUDE_PLUGIN_ROOT}/references/git.md`
and `${CLAUDE_PLUGIN_ROOT}/references/memory.md`.

---

# Part A — Setup

## A1 — Copy the template
If `context/state.md` is missing, copy the template without overwriting anything:

```
cp -Rn "${CLAUDE_PLUGIN_ROOT}/template/." .
```

If `${CLAUDE_PLUGIN_ROOT}` is unavailable, look for the `template` folder of the `ma`
plugin in the plugin cache (`~/.claude/plugins/`). Say in one line what was copied.

Special cases:
- The folder already has `context/state.md`: copy nothing, skip to part B.
- The folder already holds a different project (code, no `context/`): ask with **a
  single question** whether to copy the template here or into a new subfolder.

## A2 — Working folders
Make sure `context/`, `references/`, `design/proposals/` and `contract/` exist. Create
**only** the missing ones, with a `.gitkeep` if they stay empty. Do not rename or move
anything else.

## A3 — Project, mode and language
Ask in a single turn:
1. **Project or client name**.
2. **Mode**: `project` (full engagement), `pitch` (proposal to win the client),
   `refactoring` (existing website, app or software).
3. **Language** of the replies and of every client-facing deliverable (discovery,
   questionnaire, design copy, contract). Default **Italian**.

If `registry/preferences.md` holds a default mode (`mode` scope) or a default language
(`language` scope), offer it pre-selected and say so in one line.

## A4 — Git and state
1. `git init` if the folder is not a repository, with the `.gitignore` from `git.md`.
2. Create `context/state.md` in the format of `state.md`: project, mode, language,
   current phase `discovery`, today's date, and the phase table for the chosen mode,
   all `todo` except `setup` = `done`.
3. Commit `ma: setup`.

---

# Part B — Discovery

Write the answers into `context/discovery.md`, **one section per group**, in the order
of the table. Ask at most 4 questions per turn and follow the golden rule: whatever is
already in `context/` or in the preferences is not asked, it is confirmed.

## B0 — Who answers
Ask in one line how the discovery should run:

| Route | When | What happens |
|---|---|---|
| **Live** | The user knows the answers, or the client is on the call | Ask the groups below directly |
| **Questionnaire** | The answers are the client's and the client is not here | Run the `questionnaire` skill with the `discovery` set, then come back here to merge |
| **Mixed** | The user answers what they know, the client fills the rest | Ask the groups below, then send a questionnaire limited to the gaps |

In **pitch** mode, prefer the live route: speed matters more than completeness.

| Group | Questions |
|---|---|
| Business | Sector, what they sell or offer, how long they have been going, size, territory |
| Goal | What the project must achieve in 6–12 months (a number if possible), why now |
| Audience | Ideal customer, how they arrive, what they must do on the site or app, doubts before buying |
| Market | 2–3 competitors, what they do better or worse |
| Typology | Brochure site, portfolio, ecommerce, blog, web app, mobile app, business software |
| Features | Key features for the typology (forms, bookings, catalogue, members area, integrations, languages) |
| Content | Who writes the copy, who supplies photos and video, who updates after launch and how often |
| Constraints | Indicative budget, deadline and the reason for it, who decides and who approves |
| Existing | Current site, app or software (**mandatory in refactoring**), domains and accounts already in place |

Notes:
- **Typology** and **Features**: offer the options as multiple choice, do not leave them open.
- **Existing** in refactoring mode: also ask for the repository or the access, they will
  be needed in the acquisition phase. Never ask for credentials in writing here.
- Every relevant choice also goes into `context/decisions.md`.

## Closing
1. Summary table (`Group | Short answer`), with one line for the points left open.
2. Update `context/state.md`: `discovery` = `done`, current phase = next phase of the
   mode, today's date, `Waiting on` and `Next step`. A questionnaire sent and not yet
   returned goes into `Waiting on` with its date, and `discovery` stays `in progress`.
3. Commit `ma: discovery`.
4. Say in one line which phase comes next according to the mode, and ask whether to proceed.
