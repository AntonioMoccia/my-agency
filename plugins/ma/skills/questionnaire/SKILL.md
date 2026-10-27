---
name: questionnaire
description: Builds a client-facing questionnaire from the project's open questions, publishes it as a fillable form (an Artifact that stores the answers, or a Markdown fallback to send by email), tracks what came back and merges the answers into the project context. Use when the user says "send a questionnaire to the client", "let the client fill it in", "prepare the client brief", "collect the answers", "manda il questionario al cliente", "fallo compilare al cliente", "raccogli le risposte", or when discovery is blocked waiting on the client.
---

# Questionnaire — written to the client, filled in by the client

Read first `${CLAUDE_PLUGIN_ROOT}/references/conventions.md`,
`${CLAUDE_PLUGIN_ROOT}/references/state.md`, `${CLAUDE_PLUGIN_ROOT}/references/git.md`
and `${CLAUDE_PLUGIN_ROOT}/references/memory.md`. The question banks are in
`references/questions.md`.

Actions: `create [set]` · `send` · `collect` · `merge` · `status`.

Prerequisite: `context/state.md`. The questionnaire is written in the **project
language** from `state.md`, not in the language of the plugin files.

---

## Step 1 — Choose the set
Pick the question set from `references/questions.md`, based on the current phase or on
what the user asks:

| Set | Phase | What it collects |
|---|---|---|
| `discovery` | discovery | Business, goal, audience, market, typology, features, content, constraints |
| `brand` | style | Logo, brand, visual taste, what to avoid |
| `content` | design, execution | Copy, photos, video, who supplies what and by when |
| `ecommerce` | discovery, specs | Catalogue, payments, shipping, invoicing, returns |
| `app` | discovery, specs | Users, roles, data, integrations, environments |
| `existing` | acquisition | What is live today, who administers it, where it is hosted |
| `admin` | contract | Billing details, who signs, who approves |

Sets can be combined, but see the 20-question cap in the rules.

## Step 2 — Build the list
1. **Drop everything already known.** Apply the golden rule: a question whose answer is
   already in `context/` or in the preferences is not asked. Say in one line how many
   questions were dropped and why.
2. Group the remaining ones with the group headings of the set.
3. For each question, define:

| Field | Values |
|---|---|
| Question | In the project language, plain words, no jargon |
| Type | `short`, `long`, `single`, `multi`, `number`, `yes-no`, `file`, `link` |
| Required | yes / no |
| Help | One line: why it is asked, plus an example answer |

4. Translate the jargon: not "do you want a headless CMS?" but "do you want to update
   the texts yourself, without calling us?".

## Step 3 — Where to publish it
In this order, using the first one available:

1. **Artifact form** — a page the client fills in, which stores the answers.
   Load the `artifact-capabilities` skill **before** writing the page, then publish with
   the capabilities that persist state and identify the viewer. The page must:
   - show progress ("4 of 12") and allow saving half-finished and coming back;
   - mark required vs optional, and let a client who answers only the required ones
     submit;
   - accept file uploads only if the capability for it is available, otherwise ask for
     a link or an email attachment;
   - state in the footer who is collecting the answers and where they are stored.
   Save the published URL in `context/questionnaire.md`.
2. **Connected document or form service** (a first-party docs connector, Notion, Google
   Drive), if one is attached.
3. **Markdown fallback** — `context/questionnaire.md` with a blank line under each
   question, ready to be sent as an email, a PDF or a shared document.

Say in one line which route was used. Never invent a link: if nothing published, the
fallback is the deliverable.

## Step 4 — Send it
Produce the message to the client in the project language, short, with:
- what it is for, in one sentence;
- the link or the attachment;
- how long it takes ("about 10 minutes");
- the deadline, and what it blocks if it is late;
- who to contact for help.

Do not send anything yourself: hand the message to the user unless they explicitly ask
for it to be sent through a connected channel.

Then update `context/state.md`: the questionnaire goes into **Waiting on** with the
date it was sent and the deadline. The phase it belongs to stays `in progress`.
Commit `ma: questionnaire`.

## Step 5 — Collect
On `collect`, read the answers back:
- Artifact route: read the stored answers of the published page;
- connected document: read the document;
- fallback: ask the user to paste the filled file, or read it from `context/`.

Show a status table:

| Group | Answered | Partial | Missing |
|---|---|---|---|

Then list in one line the **required** questions still unanswered: those, and only
those, are worth chasing.

## Step 6 — Merge
Write the answers into the project context, by destination:

| Set | Destination |
|---|---|
| `discovery`, `ecommerce`, `app` | `context/discovery.md` |
| `brand` | `context/style.md` |
| `content` | `resources/resources.md` and `context/decisions.md` |
| `existing` | `context/source.md` |
| `admin` | `contract/` (placeholders in the draft) |

Rules for merging:
- Mark every merged answer with its source: `client questionnaire, YYYY-MM-DD`.
- **Never silently overwrite** an existing answer. If the client contradicts something
  already in `context/`, leave both, flag the conflict in one line and ask which wins.
- An empty answer stays empty: do not fill it with a plausible guess.
- Keep the raw answers in `context/questionnaire.md` under "Answers received": the
  client's own words are useful later for the copy.

Then: update `context/state.md` (clear the **Waiting on** row, set the phase back to
`done` if nothing required is missing), record the decisions, commit
`ma: questionnaire answers`, and say in one line which phase resumes.

## `status`
Read-only: show which questionnaires exist, when they were sent, what came back and
what is still missing. No file changes, no commit.

## Rules
- **At most 20 questions** in one questionnaire. More than that, split it into two
  rounds and send the second only after the first comes back: a wall of questions comes
  back empty.
- **Never ask for credentials.** No passwords, API keys, card details. For access, ask
  *which* accounts exist and who administers them; the credentials travel through a
  password manager or a channel the user chooses, never through the questionnaire and
  never into a file.
- Ask only personal data the project actually needs, and say in the footer where the
  answers are stored.
- Every question earns its place: if the answer does not change what gets built, cut it.
- Required questions are the ones without which the phase cannot proceed. Keep them
  under half the list.
- One question, one thing: no "what is your goal and who is your audience?".
- Offer options whenever the answer space is known (typology, features, budget bands):
  a client picks faster than they write.
- Never present the questionnaire as a contract or ask for a signature in it.
