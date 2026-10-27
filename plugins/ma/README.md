# ma — My Agency

A Claude Code plugin that takes a website, app or software project from client onboarding
through to an approved design, a contract and development, keeping track of where you got to.

**Usage guide: [English](docs/USAGE.en.md) · [Italiano](docs/USAGE.it.md)**

## Commands

| Command | What it does |
|---|---|
| `/ma:project` | Entry point: reads the state, shows the phases and runs the next one. If the project does not exist, starts the onboarding |
| `/ma:onboarding` | Folder setup (template, folders, git, state) and client discovery in 9 question groups |
| `/ma:status` | Shows phases, current phase, what is being waited on and the next step. Read-only |
| `/ma:questionnaire` | Builds a questionnaire for the client, publishes it as a fillable form, collects the answers and merges them into the context |
| `/ma:style` | Collects logo, references, keywords and constraints into `context/style.md`, and gathers Awwwards references automatically |
| `/ma:design` | 2–3 different design proposals backed by fresh references, selection down to individual parts, iteration until approval, resources table |
| `/ma:costs` | Proposes the stack and works out service costs by checking prices online, compared against the budget |
| `/ma:contract` | Contract draft from discovery, costs and decisions, with placeholders for what is missing |
| `/ma:refactoring` | Rebuilding an existing project: acquisition, audit, specs, plan, step-by-step execution |
| `/ma:skill` | Finds, evaluates, installs, lists and removes third-party skills, with a registry and a security checklist |

## The three modes

The mode is chosen during onboarding, lives in `context/state.md` and decides the order
of the phases.

| Mode | When | Phase order |
|---|---|---|
| **Project** | Full engagement, client already won | setup → discovery → style → costs → contract → design |
| **Pitch** | A proposal to win the client | setup → discovery → style → design (1 light proposal) → costs → contract |
| **Refactoring** | An existing website, app or software | setup → discovery → acquisition → audit → specs → costs → contract → plan → execution |

In Project mode the design comes **after** the contract: it is the most expensive part and
it is not given away. In Pitch mode the design comes first, but light.

## Quick start

```bash
mkdir client-project && cd client-project && claude
```

Then, inside Claude Code:

```
/ma:project
```

The plugin copies the template, runs `git init`, asks for name, mode and language, and
starts the discovery. Every phase closes with a `ma: <phase>` commit in the project repo.

To pick a project back up, from its folder: `/ma:project` to move forward, `/ma:status`
to just see where it stands.

## Language

The plugin's files are in English. What the plugin **writes and says** follows the
project language, asked once during onboarding and recorded in `context/state.md`
(default: Italian). Folder and file names stay in English.

## Project structure

```text
client-project/
├── CLAUDE.md
├── context/         state, discovery, style, inspiration, decisions, costs, questionnaire
├── references/      logo, brand, screenshots of the references
├── resources/       the resources table + images, texts, video
├── design/          proposals in design/proposals/vN/
├── contract/        contract draft
├── instructions/    how to configure the external services
└── site/            the code
```

## Plugin memory

The plugin remembers across projects in `registry/`:
- `registry/preferences.md` — stack, services, design, contract, mode, communication, language;
- `registry/skills.md` — evaluated third-party skills: `approved`, `rejected`, `link-only`.

The installed plugin lives in a **read-only** cache: writing to the registry requires the
local clone of the `my-agency` repo. The path is declared once in `~/.claude/ma.json`:

```json
{ "repo": "/absolute/path/my-agency" }
```

Preferences are saved **only** after the user confirms, and only when stated as a rule
("always use…"). Client data never enters the registry: it stays in the project.

## Updating the plugin

After writing to the registry, or changing the repo:

```bash
claude plugin marketplace update my-agency
```

Writing to the registry commits and pushes to the plugin repo; updating the marketplace
makes the change visible to the installed plugin.

## Shared references

The rules common to every skill live in `references/`: `conventions.md` (language, modes,
golden rule, questions), `state.md` (state format), `git.md` (one commit per phase),
`memory.md` (reading and writing the registry), `inspiration.md` (gathering visual
references from Awwwards and others).
