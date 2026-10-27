# Git rules

## Client project repository
- During setup, if the folder is not a Git repository, run `git init`.
- Make sure a `.gitignore` exists with at least:

```
node_modules/
.next/
.env*
!.env.example
.DS_Store
```

- At the end of every phase: `git add -A` and `git commit -m "ma: <phase>"`.
  - Design: `ma: design vN` (one iteration, one commit).
  - Refactoring, execution: `ma: step N` (one step, one commit).
  - Questionnaire: `ma: questionnaire` when sent, `ma: questionnaire answers` when the
    answers are merged.
- **No `git push`**, unless the user explicitly asks.
- If the commit fails (for example, Git identity not configured), explain the command
  to run in two lines:

```
git config user.name "Name"
git config user.email "email@example.com"
```

  and carry on with the work: a missed commit does not block the phase.

## Plugin repository
The plugin registry is only written in the local clone of `my-agency`, with commit and
push: see `${CLAUDE_PLUGIN_ROOT}/references/memory.md`.
