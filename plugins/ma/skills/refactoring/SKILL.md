---
name: refactoring
description: Drives the rebuild of an existing website, app or software in five phases - acquiring the code, audit, specs, a step-by-step plan and execution - working on the refactoring branch with one commit per step and a check after each one. Use when the user says "let's rebuild the site", "let's migrate this project", "restyling", "clean up the existing code", "the client already has a site", "rifacciamo il sito", "restyling", "il cliente ha gia un sito".
---

# Refactoring — rebuilding an existing project

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md`, `${CLAUDE_PLUGIN_ROOT}/references/git.md`
and `${CLAUDE_PLUGIN_ROOT}/references/memory.md`. The audit checklist is in
`references/audit.md`.

Prerequisite: `context/discovery.md` with the **Existing** group filled in. Run one
phase at a time, in order, with **one commit per phase**.

| Phase | What to do | Files |
|---|---|---|
| Acquisition | Ask for the repository or the path (or the URL, if only the public site exists). Clone or link it into `site/`, create the `refactoring` branch | `context/source.md` |
| Audit | Follow `references/audit.md` | `context/audit.md` |
| Specs | Types of work, goals, what must not change, acceptance criteria | `context/specs.md` |
| Plan | Small, verifiable steps, each with a check, a risk and a rollback | `context/plan.md` |
| Execution | One step at a time, then build, tests, check and commit `ma: step N` | code |

---

## 1. Acquisition
Ask, in a single question, what is available: **Git repository**, **local folder** or
**only the public site** (URL).

- Repository: clone it into `site/`. If `site/` is not empty, ask how to proceed.
- Local folder: copy or link it into `site/`, after checking its contents.
- URL only: there is no code to reuse. Say so plainly — the work will be a rebuild, not a
  refactor. Save screenshots of the main pages as reference.

If the client holds the access and the details are missing, run the `questionnaire`
skill with the `existing` set.

Create the branch: `git -C site checkout -b refactoring`.

Write `context/source.md`: provenance, production URL, access received (**never the
credentials**: only which access exists and where it is kept), starting branch, initial
commit, size and languages.

Commit `ma: acquisition`.

## 2. Audit
Follow the checklist in `references/audit.md` and write `context/audit.md` with the
columns `item | how to check it | outcome`.

Close with: the 5 most serious problems in order of impact, and what **works** and must
be preserved.

Commit `ma: audit`.

## 3. Specs
Define with the user:
- **Types of work** (combinable): `restyling`, `migration`, `code quality`, `new features`.
- **Goals**: measurable where possible (load time, Lighthouse score, conversions).
- **What must not change**: URLs, content, appearance, integrations, data.
- **Acceptance criteria**: for every goal, how to verify it was reached.

Write `context/specs.md`. Commit `ma: specs`.

## 4. Plan
Break the work into **small, verifiable steps**, one per row:

| # | Step | Check | Risk | Rollback |
|---|---|---|---|---|

Rules: one step changes one thing; every step has an objective check (build, tests,
screenshot, a page that responds); high-risk steps are isolated and placed after the
safe ones.

Write `context/plan.md`. Commit `ma: plan`.

## 5. Execution
Before touching the code: **if there are no tests**, create characterisation tests (they
pin the current behaviour, imperfections included) or reference screenshots of the main
pages, desktop and mobile. Without a safety net, do not start.

Then, for every step:
1. apply **only** that step;
2. build;
3. tests;
4. the check named in the plan;
5. commit `ma: step N`.

If a check **fails**: stop, do not move to the next step, explain what failed and ask for
confirmation on how to proceed (fix it or roll the step back).

## Rules per type of work
- **Restyling**: use the `style` and `design` skills — including the automatic Awwwards
  references. The **content stays unchanged**: the form changes, not the copy.
- **Migration**: produce the table of **old and new URLs**, set up the **301 redirects**
  and preserve the SEO metadata (title, description, canonical, structured data,
  sitemap, `robots.txt`).
- **Code quality**: the appearance **must not change**. Verify against the reference
  screenshots after every step.
- **New features**: respect the acceptance criteria in `context/specs.md`; no features
  that were not agreed.

## General rules
- **Always** work on the `refactoring` branch. Merging to `main` is the user's call.
- No `git push`, unless explicitly asked.
- Update `context/state.md` at the end of every phase.
- Never touch production data or a live database without a verified backup.
