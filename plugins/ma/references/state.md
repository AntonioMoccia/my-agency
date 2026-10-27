# Project state format

File: `context/state.md` in the client project folder. It is the source of truth on
where the project stands.

## Template to use

```markdown
# Project state
| Item | Value |
|---|---|
| Project | |
| Mode | project / pitch / refactoring |
| Language | it / en / … |
| Current phase | |
| Last updated | YYYY-MM-DD |

## Phases
| Phase | Status | Date | Files |
|---|---|---|---|

## Next step
-

## Waiting on
-
```

## Rules
- Update `state.md` at the end of every phase, before the commit.
- Possible phase statuses: `todo`, `in progress`, `done`, `skipped`.
- The **Files** column lists what the phase produced (e.g. `context/discovery.md`).
- **Current phase** is the first phase that is neither `done` nor `skipped`, following
  the order of the mode.
- **Waiting on** lists what is needed from the user or the client (materials,
  approvals, data). A questionnaire sent and not yet returned goes here, with its date.
- **Language** is the project language: see `conventions.md`. It is asked once during
  onboarding and drives every client-facing deliverable.
- `Last updated` always in `YYYY-MM-DD` format.
- The phases to list are those of the chosen mode: see the table in `conventions.md`.
