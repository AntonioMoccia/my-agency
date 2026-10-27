# my-agency

My Agency's Claude Code plugin marketplace. It contains the **`ma`** plugin, which takes a
website, app or software project from client onboarding through to an approved design, a
contract and development.

## Installation

```bash
claude plugin marketplace add AntonioMoccia/my-agency
claude plugin install ma@my-agency
```

## Updating

```bash
claude plugin marketplace update my-agency
```

## Usage

```bash
mkdir client-project && cd client-project && claude
```

Then, inside Claude Code: `/ma:project`.

Full usage guide: **[English](plugins/ma/docs/USAGE.en.md)** ·
**[Italiano](plugins/ma/docs/USAGE.it.md)**

## Plugins

| Plugin | What it does | Documentation |
|---|---|---|
| `ma` | Onboarding, client questionnaire, style with automatic Awwwards references, design, costs, contract and refactoring of web projects | [plugins/ma/README.md](plugins/ma/README.md) |

## Language

The plugin's files are in English. What the plugin writes and says follows the project
language, asked once during onboarding (default: Italian).
