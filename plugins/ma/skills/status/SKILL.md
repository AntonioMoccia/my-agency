---
name: status
description: Read-only view of a project's state - phase table, current phase, what is being waited on, next step, and the registry skills the next phase needs. Use when the user says "where are we", "project status", "what's missing", "what are we waiting for", "a che punto siamo", "stato del progetto", "cosa manca".
---

# Project status

This skill **modifies no files**: read-only. No commit.

Read `${CLAUDE_PLUGIN_ROOT}/references/conventions.md` and
`${CLAUDE_PLUGIN_ROOT}/references/state.md`.

## Step 1 — Read
- `context/state.md` of the current project.
- `registry/skills.md` of the plugin (from the cache or the local clone, see `memory.md`).

If `context/state.md` does not exist, say in one line that the project has not been
started and suggest `/ma:project`. Stop.

## Step 2 — Show
1. **Header**: project, mode, language, current phase, last updated.
2. **Phases**, in the order of the mode:

| Phase | Status | Date | Files |
|---|---|---|---|

3. **Waiting on**: list of what is needed from the user or the client. If empty, write
   "nothing". A questionnaire sent and not yet returned is listed here with its date.
4. **Next step**: a single line.
5. **Registry skills for the next phase**: skills with status `approved` whose
   **Phases** field contains the next phase.

| Skill | When to use it |
|---|---|

If there are none, write "no extra skills for this phase".

## Step 3 — Consistency
If the files in `context/` do not match the table (for example `context/style.md`
exists but the `style` phase is still `todo`), flag it in one line as a warning,
**without correcting the file**: the fix belongs to the phase's own skill.
