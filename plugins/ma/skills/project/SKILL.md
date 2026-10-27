---
name: project
description: Guided entry point of a website, app or software project - reads the state, shows which phases are done and which are missing, then runs the next phase according to the mode (project, pitch, refactoring). Use when the user says "new project", "new client", "let's pick the project back up", "what's next", "nuovo progetto", "riprendiamo il progetto", "andiamo avanti", or opens a project folder without knowing where to restart.
---

# Project — guided command

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md` and
`${CLAUDE_PLUGIN_ROOT}/references/memory.md`.

## Step 1 — Read the state
Read `context/state.md` in the current folder.

- **Missing**: the project has not been started. Run the `onboarding` skill and stop here.
- **Present**: continue with step 2.

## Step 2 — Show where we are
Derive the phase order from the mode recorded in `state.md` (mode table in
`conventions.md`) and show a table:

| Phase | Status | Date | Files |
|---|---|---|---|

Below the table, in three lines:
- **Current phase**: the first phase that is neither `done` nor `skipped`.
- **Waiting on**: what is needed from the user or the client.
- **Next step**: the phase to run now.

## Step 3 — Load the registry skills
Look in `registry/skills.md` for skills with status `approved` whose **Phases** field
contains the next phase. Load them and say so in one line.

## Step 4 — Run the next phase
Run the skill that matches the phase:

| Phase | Skill |
|---|---|
| setup, discovery | `onboarding` |
| style | `style` |
| costs | `costs` |
| contract | `contract` |
| design | `design` |
| acquisition, audit, specs, plan, execution | `refactoring` |

Ask for confirmation in one line ("Moving on to the style phase, shall I?"), then run it.

If **Waiting on** holds answers expected from the client, offer the `questionnaire`
skill in one line instead of asking the user to chase them by hand.

## Skipping or redoing a phase
If the user asks to skip a phase, set it to `skipped` in `state.md` and move to the
next one. If they ask to redo it, set it to `in progress` and run it again. In both
cases record the choice in `context/decisions.md` with the reason.

## Outside a project folder
If the current folder is not empty and holds a different project (code, no `context/`),
do nothing: ask with a single question whether to start a new project here or move to
another folder.
