---
name: costs
description: Proposes the project's technical stack and works out the cost of its services by checking prices online at the time, with a one-off and monthly table, cheaper alternatives, annual total and a comparison against the budget. Use when the user says "how much does it cost", "which stack do we use", "what does the client pay monthly", "are we within budget", "quanto costa", "che stack usiamo", "facciamo i costi".
---

# Costs — stack and service costs

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md`, `${CLAUDE_PLUGIN_ROOT}/references/git.md`
and `${CLAUDE_PLUGIN_ROOT}/references/memory.md`. The service categories per typology
are in `references/services.md`.

## Step 1 — Read the context
From `context/discovery.md`: **typology**, required **features**, **indicative budget**,
languages, who updates the content.
From `registry/preferences.md` (`stack` and `services` scopes): the preferred stack.

Follow the golden rule: if the stack is in the preferences, **do not ask for it again**.
Confirm it in one line ("Using Next.js on Vercel, as per your preferences") and ask only
about the variations the typology forces.

## Step 2 — Propose the stack
Cover these items, choosing on the basis of typology and features (detail in
`references/services.md`):

| Item | Notes |
|---|---|
| Framework | |
| Hosting | |
| CMS | Only if the client updates the content |
| Ecommerce | Only if the typology is ecommerce |
| Transactional email | Forms, orders, password resets |
| Analytics | |
| Cookies and privacy | Consent banner, mandatory in Italy |
| Domain | |

For **every** choice write the reason in one line, tied to the discovery ("CMS because
the client updates the copy weekly"). If an item is not needed, say so and explain why.

## Step 3 — Check the prices
**Check prices online, now**, for every service. Cite **source and date** for each price.

Do not use remembered prices: plans change. If a price cannot be verified (quote on
request, volume pricing), write it as `to verify` and do not invent it. Watch out for:
currency (prefer EUR, say when a price is in USD), VAT included or excluded, price per
user or per site, monthly versus annual.

## Step 4 — Write `context/costs.md`

| Service | Recommended option | One-off | Monthly | Cheaper alternative | Trade-off |
|---|---|---|---|---|---|

Below the table:
- **One-off total** and **monthly total**, then the **annual total** (one-off + monthly × 12).
- **Comparison against the budget** from the discovery: `within`, `at the limit` or `over`.
- If it is **over budget**, propose a complete **alternative stack** (second table) that
  fits, saying what is lost.
- **Sources**: list of links and the date they were checked.

## Rules
- **Do not estimate the agency's own work**: only service costs belong here. Days and
  project price live in the contract.
- Separate what the client pays directly (domain, hosting, CMS) from what is billed to
  the agency.
- Prefer free plans only if they hold up for the real case: state the limit beyond which
  it starts costing.

## Closing
1. Record the chosen stack in `context/decisions.md`.
2. If the user confirms the stack as a preference ("always use…"), offer to save it in
   the registry following `memory.md`.
3. Update `context/state.md`: phase `costs` = `done`.
4. Commit `ma: costs`.
5. State in one line the next phase according to the mode.
