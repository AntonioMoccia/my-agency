---
name: contract
description: Drafts a web development contract from the project's discovery, costs and decisions, with deliverables, exclusions, milestones, revision rounds, payments, ownership and account holders, leaving placeholders for whatever is missing. Use when the user says "let's do the contract", "prepare the proposal", "send the quote", "what does the client sign", "facciamo il contratto", "preparami la proposta", "manda il preventivo".
---

# Contract — draft for the client

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md`, `${CLAUDE_PLUGIN_ROOT}/references/git.md`
and `${CLAUDE_PLUGIN_ROOT}/references/memory.md`. The template to fill in is in
`references/template.md`.

The contract is written in the **project language** from `context/state.md`.

## Step 1 — Choose the template
Use `references/template.md`. If `registry/preferences.md` (`contract` scope) names a
**validated template** of the user's, use that one and say so in one line.

## Step 2 — Read the context
| From | What to take |
|---|---|
| `context/discovery.md` | Client, typology, features, deadline and its reason, who decides and approves, who supplies the content |
| `context/costs.md` | Services, who pays for them, account holders, annual total |
| `context/decisions.md` | Stack, mode, design choices already made |
| `context/state.md` | Completed phases, to set realistic milestones |

If the client's billing details are missing, run the `questionnaire` skill with the
`admin` set instead of leaving the draft full of holes.

## Step 3 — Fill it in
Fill in every section of the template:
parties · subject · deliverables · exclusions · timing and milestones · number of
revision rounds · payments per milestone · domain, hosting and accounts held by the
client · ownership of code and design on full payment · who provides the content ·
optional maintenance · termination.

Criteria:
- **Deliverables**: list what is delivered, verifiably (number of pages or screens,
  languages, environments).
- **Exclusions**: write explicitly what is **not** included. This is the part that
  prevents arguments: content, photos, translations, ongoing SEO, ad campaigns,
  maintenance, features not listed.
- **Milestones**: tie them to the project's real phases (design approved, development,
  testing, launch).
- **Revisions**: a precise number per phase, and what happens afterwards (hourly or
  per-round rate).
- **Payments**: a percentage per milestone; they must add up to 100%.
- **Account holders**: domain, hosting and service accounts in the **client's** name,
  with the agency as a collaborator. Take the items from `context/costs.md`.
- **Ownership**: code and design pass to the client on **full payment**; state what
  stays with the agency (own tools and libraries, portfolio rights).
- **Content**: who supplies it and by when; what happens if it arrives late.

## Step 4 — What not to invent
Missing information stays as a placeholder:

```
[TO COMPLETE: supplier legal name, VAT number and registered office]
[TO COMPLETE: total amount]
```

Never invent: supplier details, VAT numbers, amounts, hourly rates, signing dates, quote
numbers. Close with the list of placeholders still to fill in.

## Step 5 — Mandatory notice
Always put at the **top** of the document:

> **Draft to be reviewed by a lawyer or an accountant. It requires an issuing entity
> with a VAT number or a registered company.**

Do not remove this notice and do not soften it: this skill produces a working draft, not
a legal instrument.

## Closing
1. Save to `contract/draft.md`.
2. Record the contractual choices in `context/decisions.md`.
3. Update `context/state.md`: phase `contract` = `done`.
4. Commit `ma: contract`.
5. Summary table (`Section | Status`) and the list of remaining `[TO COMPLETE]` items,
   then the next phase.
