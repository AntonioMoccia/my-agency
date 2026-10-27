# Shared conventions

These rules apply to every skill in the `ma` plugin.

## Language
The plugin's own files are in English. What the plugin **writes and says** follows the
**project language**, recorded as `Language` in `context/state.md`.

Order of resolution:
1. `Language` in `context/state.md` (asked once during onboarding);
2. the `language` scope in `registry/preferences.md`;
3. default: **Italian**.

The project language applies to replies to the user and to every client-facing
deliverable: discovery, questionnaire, style brief, design copy, costs, contract,
generated texts. File and folder **names** stay in English in all cases.

## Output form
- Schematic output: tables where possible, short sentences, no padding.
- Exactly **one next step** at the end of every reply.

## The three modes
The mode is recorded in `context/state.md` and decides the order of the phases.

| Mode | Phase order |
|---|---|
| Project | setup → discovery → style → costs → contract → design |
| Pitch | setup → discovery → style → design (1 light proposal) → costs → contract |
| Refactoring | setup → discovery → acquisition → audit → specs → costs → contract → plan → execution |

## Golden rule: never ask what is already known
Before asking anything, check in this order:
1. the project's `context/` (`discovery.md`, `style.md`, `decisions.md`, `costs.md`, `questionnaire.md`, `inspiration.md`);
2. `registry/preferences.md` in the plugin;
3. `registry/skills.md` in the plugin.

If the answer is already there, use it and say so in one line: "Using Next.js, as per
your preferences". Ask for confirmation only — never repeat the question.

## Decisions
Every choice the user makes goes into `context/decisions.md`:

| Date | Phase | Decision | Reason |
|---|---|---|---|

## Questions
- Use multiple-choice questions with AskUserQuestion when available.
- At most 4 questions per turn.
- Always leave a free-text answer possible.

## Registry skills
Before starting a phase, look in `registry/skills.md` for skills with status
`approved` whose **Phases** field contains the current phase, and load them. Say in one
line which skills were loaded.

## Shared references
- `${CLAUDE_PLUGIN_ROOT}/references/state.md` — format of `context/state.md`
- `${CLAUDE_PLUGIN_ROOT}/references/git.md` — Git rules
- `${CLAUDE_PLUGIN_ROOT}/references/memory.md` — reading and writing the registry
- `${CLAUDE_PLUGIN_ROOT}/references/inspiration.md` — gathering visual references (Awwwards and others)
