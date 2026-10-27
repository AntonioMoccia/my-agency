---
name: skill
description: Finds, evaluates, installs, lists and removes third-party skills in the ma plugin, keeping a registry of the approved and rejected ones and applying a security checklist before every installation. Use when the user says "find a skill for...", "add this skill", "which skills do we have", "remove the skill", "cerca una skill per...", "aggiungi questa skill", "quali skill abbiamo".
---

# Skill — the plugin feeding itself

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md` and
`${CLAUDE_PLUGIN_ROOT}/references/memory.md`. The evaluation criteria and the security
checklist are in `references/evaluation.md`: always apply them.

Actions: `find <need>` · `add <link or path>` · `list` · `remove <name>`.

---

## find `<need>`

1. **Registry first.** Read `registry/skills.md`. If an `approved` or `rejected` skill
   already exists for that need, say so in one line (with the reason if rejected) and
   **stop**, unless the user explicitly asks for alternatives.
2. **Search the web** in the sources listed in `references/evaluation.md`, starting from
   the official ones and working down.
3. **Propose at most 3 candidates** in a table:

| Name | Source | Licence | Popularity | Last updated | What it does | Scripts included |
|---|---|---|---|---|---|---|

   Popularity = stars or installs. "Scripts included" = yes/no.
4. **For the candidate the user picks**: download it into a temporary folder, read it
   **in full** (every file, not just `SKILL.md`) and apply the security checklist.
5. **Show**: a summary of what it does and what it modifies, and **the full contents of
   every script** it includes. Then ask for explicit approval. Nothing is installed
   without approval.

## add `<link or path>`

Same evaluation and same approval as `find`, starting from the link, file or folder the
user supplied. Step 1 (the registry check) still applies, to avoid duplicating a skill
that is already there.

## Installation (only after approval)

Write into the **local clone** of the repository, as described in `memory.md`.

**Licence compatible with copying** (MIT, Apache-2.0, BSD, ISC and similar):
1. Copy into `<repo>/plugins/ma/skills/<name>/`.
2. Add `<repo>/plugins/ma/skills/<name>/SOURCE.md` with: url, author, licence, version or
   commit, date acquired.
3. If the frontmatter `name` collides with an existing skill, adapt it (e.g. `gsap-anim`
   instead of `anim`) and note it in `SOURCE.md`.

**Licence missing or incompatible** (no licence, GPL where not compatible, "all rights
reserved", personal use only):
- **copy nothing**;
- record the skill with status `link-only`, so it stays consultable as a reference
  without entering the plugin.

**In both cases:**
1. Update `registry/skills.md`, filling in **"When to use it"** (one concrete sentence)
   and **"Phases"** (the phases where it should be loaded: setup, discovery, style,
   costs, contract, design, acquisition, audit, specs, plan, execution).
2. Bump the **patch version** of the plugin in
   `plugins/ma/.claude-plugin/plugin.json` (e.g. 0.4.0 → 0.4.1).
3. Commit and push following `memory.md`, with the message `ma: registry skill <name>`.
4. Suggest `claude plugin marketplace update my-agency`.

**If the skill is rejected**: record it with status `rejected` and the reason in "When to
use it" (e.g. "rejected: script that sends data to an external URL"). It exists so the
same skill is not proposed again. Commit and push as above.

## list

Show `registry/skills.md` as a table, grouped by status (`approved`, `link-only`,
`rejected`). Add a count row. No file changes.

## remove `<name>`

1. Ask for confirmation, showing the registry row.
2. Delete `<repo>/plugins/ma/skills/<name>/` in the local clone.
3. Remove the entry from `registry/skills.md`, or move it to `rejected` with the reason if
   the user wants to remember the decision.
4. Bump the patch version, commit and push following `memory.md`.

## Rules

- No installation, copy or push without the user's explicit approval.
- Read **every** file of a skill before approving it: instructions can hide in
  `references/`.
- **One single** item from the security checklist is enough to reject the skill, or to
  require explicit confirmation showing the exact point in the file.
- Never install directly into the plugin cache: it is read-only.
