# ma — Usage guide

The `ma` plugin ("My Agency") turns Claude Code into the operating procedure of a web
agency: it onboards a client, settles the visual direction, proposes designs backed by
real award-level references, prices the services, drafts the contract and drives the
development — while keeping a written record of where the project stands.

Italian version: [USAGE.it.md](USAGE.it.md)

---

## 1. Installation

```bash
claude plugin marketplace add AntonioMoccia/my-agency
claude plugin install ma@my-agency
```

Update later with:

```bash
claude plugin marketplace update my-agency
```

### Optional: the local clone
The installed plugin lives in a read-only cache. To let the plugin **remember your
preferences across projects**, clone this repository and declare the path once in
`~/.claude/ma.json`:

```json
{ "repo": "/absolute/path/my-agency" }
```

Without it everything still works; preferences just stay inside the current project.

---

## 2. Start a project

```bash
mkdir client-project && cd client-project && claude
```

Then, inside Claude Code:

```
/ma:project
```

On an empty folder this runs the onboarding: it copies the template, runs `git init`,
and asks three things — **project name**, **mode** and **language**. From there every
phase ends with a commit (`ma: <phase>`) in the project repository.

To pick a project back up, from its folder:

| You want | Command |
|---|---|
| To move forward | `/ma:project` |
| To just look at where it stands | `/ma:status` |
| To run one specific phase | `/ma:style`, `/ma:design`, `/ma:costs`, … |

---

## 3. The three modes

The mode is chosen once during onboarding and decides the order of the phases.

| Mode | Use it when | Phase order |
|---|---|---|
| **project** | The client is signed, you are doing the full job | setup → discovery → style → costs → contract → design |
| **pitch** | You are trying to win the client | setup → discovery → style → design (1 light proposal) → costs → contract |
| **refactoring** | There is already a site, app or software | setup → discovery → acquisition → audit → specs → costs → contract → plan → execution |

Why **project** mode puts design last: design is the most expensive phase, so it comes
after a signed contract. **Pitch** mode inverts it deliberately — one light proposal,
hero section only, to win the work.

You can skip or redo a phase at any time: `ma` marks it `skipped` or `in progress` and
records the reason in `context/decisions.md`.

---

## 4. Language

The plugin's own files are in English. What the plugin **says to you and writes for the
client** follows the **project language**:

1. the `Language` field in `context/state.md`, asked once during onboarding;
2. otherwise the `language` preference in the registry;
3. otherwise **Italian**.

That covers replies, discovery, the client questionnaire, the style brief, the design
copy, the costs table and the contract. Folder and file names stay in English in all
cases.

---

## 5. The commands

| Command | Phase | Produces |
|---|---|---|
| `/ma:project` | any | Runs the next phase |
| `/ma:onboarding` | setup, discovery | `context/state.md`, `context/discovery.md` |
| `/ma:status` | — | Nothing: read-only |
| `/ma:questionnaire` | any | `context/questionnaire.md` + a fillable form |
| `/ma:style` | style | `context/style.md`, `context/inspiration.md` |
| `/ma:design` | design | `design/proposals/vN/`, `resources/resources.md` |
| `/ma:costs` | costs | `context/costs.md` |
| `/ma:contract` | contract | `contract/draft.md` |
| `/ma:refactoring` | acquisition → execution | `context/source.md`, `audit.md`, `specs.md`, `plan.md` |
| `/ma:skill` | — | Entries in `registry/skills.md` |

You rarely need to call them by name: `/ma:project` picks the right one from the state.

---

## 6. Phase by phase

### Onboarding — setup and discovery
Copies the template (never overwriting anything), initialises Git, and asks the
discovery in 9 groups: business, goal, audience, market, typology, features, content,
constraints, what already exists. At most 4 questions per turn, multiple choice where
the answer space is known.

Before asking, it offers three routes:

| Route | When |
|---|---|
| **Live** | You know the answers, or the client is on the call |
| **Questionnaire** | The answers are the client's, and the client is not here |
| **Mixed** | You answer what you know, the client fills the gaps |

### Style — visual direction, plus automatic references
Collects logo and brand files, the client's own references, 3–5 keywords, what to avoid,
and the hard constraints. Then it **gathers references automatically** — see section 7.

Output: `context/style.md` (direction in one sentence, keywords, constraints, a
what-to-take / what-not-to-take row per reference) and `context/inspiration.md`.

### Design — proposals, selection, iteration
Refreshes the references, then generates **2–3 genuinely different directions** — not
three variants of one idea. Each one carries a name, the idea in one sentence, 1–3 cited
references with the principle taken, palette with the role of every colour, a pair of
open source fonts, grid, 3–5 key animations each with its reduced-motion fallback, and
both desktop and mobile home.

Every proposal is checked against a quality checklist before you see it: hierarchy,
WCAG AA contrast on every pair, mobile consistency, one strong idea per page, animation
performance, faithfulness to the brief.

Where the design is produced, first available: the Design artifact type → Figma → a
static HTML page in `design/proposals/vN/`.

You then pick a proposal, several, or **parts of each** ("A's palette, B's typography,
C's hero") — always with the reason. `vN+1` is the synthesis of those choices, not a new
round of proposals. If a whole round is rejected, the references are refreshed first:
the same inspiration would produce the same proposals.

### Costs — stack and service costs
Proposes the stack (framework, hosting, CMS, ecommerce, transactional email, analytics,
cookies, domain) with a one-line reason per choice tied to the discovery, then **checks
every price online at the time** — citing source and date, never from memory. A price
that cannot be verified is written `to verify`, not invented.

Output: a table with one-off and monthly cost, a cheaper alternative and its trade-off,
the annual total, and the verdict against the budget: `within`, `at the limit`, `over`.
Over budget means a complete alternative stack is proposed, saying what is lost.

It never estimates your own labour: days and project price belong in the contract.

### Contract — the draft
Fills a full template from discovery, costs and decisions: parties, subject,
deliverables, exclusions, milestones, revision rounds, payments per milestone, account
holders, ownership on full payment, content responsibilities, optional maintenance,
termination.

Two rules it will not bend:
- missing data stays as `[TO COMPLETE: …]` — no invented VAT numbers, amounts or dates;
- the draft always carries the notice to have it reviewed by a lawyer or an accountant.

### Refactoring — an existing project
Five phases, one commit each: **acquisition** (repo, folder or URL only; the
`refactoring` branch is created), **audit** (a 20-item checklist, from dependencies and
secrets to Lighthouse, Core Web Vitals, SEO and accessibility), **specs** (what must not
change, acceptance criteria), **plan** (small steps, each with a check, a risk and a
rollback), **execution** (one step → build → tests → check → commit).

If there are no tests, it writes characterisation tests or takes reference screenshots
before touching anything. A failed check stops the run: it will not move to the next
step on its own.

---

## 7. Automatic references (Awwwards)

Every time a design proposal is about to be produced, `ma` goes and looks at what good
work in that sector looks like right now. You do not have to ask.

**How the queries are built.** Sector, typology and audience come from the discovery;
keywords and what-to-avoid from the style brief. From those it builds 2–4 queries: one
by category, one or two by tag (mapped from your keywords: "essential" → `ui-design`,
"immersive" → `webgl`, "editorial" → `typography`, and so on), and one by the current
year's honours for freshness.

**Where it looks.** Awwwards first — categories (`e-commerce`, `architecture`,
`fashion`, `portfolio`, …), tags (`animation`, `scrolling`, `3d`, `webgl`, …), and
honours (`sites_of_the_day`, `sites_of_the_year`, …). If that yields fewer than 6 usable
references it falls back to Godly, SiteInspire, Land-book, Lapa, Httpster, Mobbin.

**How it fetches.** WebFetch → WebSearch → the Chrome browser tools for
JavaScript-rendered pages → asking you for links. Fewer than 3 usable references is
reported in one line and does not block the phase.

**What you get.** `context/inspiration.md`, with one row per reference: source, date
seen, sector or tag, **what to take** as a concrete principle, and what not to take.
3 to 12 rows, at least 2 from the client's sector and at least 2 from outside it — that
second constraint is what keeps the proposal off the sector cliché. Your own references
are kept in the table and never replaced by the automatic ones.

**How they are used.** Each design proposal cites 1–3 rows and the principle it took
from each, and two proposals may not cite the same principle from the same reference. A
refresh happens when the file is older than 30 days or a round has been rejected.

**The limits, enforced.** Principles only, never assets: no identical layouts, no
borrowed logos, copy or images, no photographs of real people from the web, never a
promise that the result will be "like" some reference. Public pages only, no bulk
scraping, nothing behind a login. Screenshots are working material: they do not go to
the client and never into `site/`.

---

## 8. The client questionnaire

Written by `ma`, filled in by the client, merged back into the project. Use it whenever
the answers belong to the client and the client is not on the call.

```
/ma:questionnaire                  # picks the set from the current phase
/ma:questionnaire discovery        # a specific set
/ma:questionnaire collect          # read the answers back
/ma:questionnaire status           # what is out, what came back
```

### The sets

| Set | Phase | Collects |
|---|---|---|
| `discovery` | discovery | Business, goal, audience, market, typology, features, content, constraints |
| `brand` | style | Logo, brand, visual taste, what to avoid |
| `content` | design, execution | Copy, photos, video, company details, who supplies what and by when |
| `ecommerce` | discovery, specs | Catalogue, payments, shipping, invoicing, returns |
| `app` | discovery, specs | Users, roles, data, integrations, environments |
| `existing` | acquisition | What is live today, who administers it, where it is hosted |
| `admin` | contract | Billing details, who signs, who approves |

### How it works
1. **It drops what is already known.** Anything already answered in `context/` or in
   your preferences is not asked again, and you are told how many questions were cut.
2. **It types every question** — short, long, single choice, multi, number, yes/no, file,
   link — marks it required or optional, and writes a help line explaining why it is
   asked. Jargon is translated: not "do you want a headless CMS?" but "do you want to
   update the texts yourself, without calling us?".
3. **It publishes it**, first available: a fillable Artifact page that stores the answers
   (with progress, save-and-resume, required/optional marking) → a connected document or
   form service → `context/questionnaire.md` as Markdown to send by email.
4. **It writes the message to the client**: what it is for, the link, how long it takes,
   the deadline and what it blocks. You send it — `ma` does not send anything by itself
   unless you ask.
5. **It tracks it**: the questionnaire goes into **Waiting on** in `context/state.md`
   with its date, and the phase stays `in progress`.
6. **It collects and merges**: a status table (answered / partial / missing), then the
   answers are written into the right file — discovery, style, resources, source or the
   contract placeholders — each marked with its source and date.

### The guardrails
- **At most 20 questions.** Beyond that it splits into two rounds: a wall of questions
  comes back empty.
- **Never credentials.** No passwords, API keys or card details. For access it asks
  *which* accounts exist and who administers them; the credentials travel through a
  password manager or a channel you choose, never through the form and never into a file.
- **No silent overwrites.** If the client contradicts something already in `context/`,
  both versions stay and you are asked which wins.
- **An empty answer stays empty.** It is never filled in with a plausible guess.
- Required questions stay under half the list, so a client who answers only those has
  still unblocked the phase.

---

## 9. What ends up in the project folder

```text
client-project/
├── CLAUDE.md                  instructions for Claude in this project
├── onboarding.md              the setup answers at a glance
├── context/
│   ├── state.md               phases, current phase, waiting on, next step
│   ├── discovery.md           the 9 discovery groups
│   ├── style.md               direction, keywords, constraints, references
│   ├── inspiration.md         the gathered references and their principles
│   ├── decisions.md           every choice: date, phase, decision, reason
│   ├── costs.md               stack, prices with sources, budget verdict
│   ├── questionnaire.md       questionnaire sent and raw answers received
│   └── source.md / audit.md / specs.md / plan.md     (refactoring only)
├── references/                logo, brand manual, reference screenshots
├── resources/                 resources.md + images, texts, video
├── design/proposals/vN/       the proposals and the approved design
├── contract/draft.md          the contract draft
├── instructions/              how to configure the external services
└── site/                      the code
```

`context/state.md` is the source of truth. If you read one file to know where a project
stands, read that one.

---

## 10. Memory across projects

`registry/` in the plugin holds what should outlive a single project:

- **`preferences.md`** — scopes `stack`, `services`, `design`, `contract`, `mode`,
  `communication`, `language`. A preference is saved only when you state it as a rule
  ("always use Next.js") or confirm the offer to remember it.
- **`skills.md`** — third-party skills you evaluated: `approved`, `rejected`,
  `link-only`, each with the phases where it should load.

Client data never goes in there — names, contacts, budgets, content, credentials all stay
in the project folder. A one-off choice stays in `context/decisions.md`.

Writing to the registry needs the local clone (section 1); it commits and pushes to the
plugin repo, then you run `claude plugin marketplace update my-agency` to see the change
in the installed plugin.

### Third-party skills
`/ma:skill find <need>` checks the registry first, then searches — official Anthropic
repositories before curated lists — and proposes at most 3 candidates. For the one you
pick it reads **every** file, shows you the full contents of any script, and applies a
6-point security checklist (instructions to ignore the rules, data sent to external URLs,
credential access, remote code execution, destructive commands, obfuscation). One hit is
enough to reject it. Nothing is installed without your explicit approval, and a skill
whose licence does not allow copying is recorded as `link-only` rather than vendored.

---

## 11. Troubleshooting

| Symptom | Cause and fix |
|---|---|
| `/ma:project` starts a new onboarding in an existing project | `context/state.md` is missing or was moved. Restore it, or run `/ma:onboarding` and let it rebuild the state |
| "The folder already holds a different project" | There is code but no `context/`. Answer the single question it asks: here, or in a new subfolder |
| The design skill refuses to start | `context/discovery.md` or `context/style.md` is missing. Run `/ma:onboarding` or `/ma:style` first |
| It warns that the contract is not closed | Expected in project mode: design comes after the contract. Confirm to proceed anyway |
| Fewer than 3 references gathered | Awwwards returned nothing usable for those queries. It carries on; give it 3–5 links yourself, or soften "what to avoid" |
| A price is marked `to verify` | The provider does not publish it (quote on request, volume pricing). It will not be invented — ask the provider |
| The commit at the end of a phase fails | Git identity not configured. Run `git config user.name` and `git config user.email`; the phase itself is not blocked |
| Preferences are not remembered between projects | `~/.claude/ma.json` is missing or points to the wrong path. It must contain `plugins/ma/registry/` |
| A registry change is not visible in the plugin | Run `claude plugin marketplace update my-agency` |
| The questionnaire came back half empty | Normal. Chase only the **required** questions it lists; send a second short round for the rest |

---

## 12. Conventions worth knowing

- **One next step.** Every reply ends with exactly one, so you always know what happens next.
- **Never asked twice.** Before any question, `ma` checks `context/`, then the
  preferences, then the skill registry. What it finds it confirms in one line instead of
  asking again.
- **Every choice is written down.** `context/decisions.md` records date, phase, decision
  and reason — which is what makes a project resumable three weeks later.
- **One commit per phase.** `ma: setup`, `ma: discovery`, `ma: style`, `ma: design vN`,
  `ma: step N`. No `git push` unless you ask.
- **References give principles, never assets.** This holds in style, design and
  refactoring alike.
- **Credentials never enter a file.** Not in the questionnaire, not in `source.md`, not
  in the contract.
