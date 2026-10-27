# Plugin memory

The registry (`registry/skills.md`, `registry/preferences.md`) is the plugin's memory
across different projects.

## Why a local clone is needed
The installed plugin lives in a **read-only** cache: writing there is pointless, it gets
overwritten on the next update. Writing to the registry requires the **local clone** of
the `my-agency` repository.

## Path of the clone
It lives in `~/.claude/ma.json`, in this format:

```json
{ "repo": "/absolute/path/my-agency" }
```

If the file does not exist:
1. ask for it **once** ("Where is the local clone of the `my-agency` repo?");
2. check that the path contains `plugins/ma/registry/`;
3. save `~/.claude/ma.json`.

If the user has no clone, say so in one line and continue read-only: preferences then
apply to the current project only.

## Reading
- Read the registry from the plugin cache: `${CLAUDE_PLUGIN_ROOT}/registry/`.
- If a local clone exists and is more recent, read from there.

## Writing (only after the user approves)
1. Edit the files inside `<repo>/plugins/ma/registry/`.
2. `git -C <repo> add -A`
3. `git -C <repo> commit -m "ma: registry <what>"`
4. `git -C <repo> push`
5. Suggest in one line: "To see the change in the installed plugin, run
   `claude plugin marketplace update my-agency`".

## When to save a preference
Save only if:
- the user states it as a rule ("always use…", "from now on…", "by default…"); or
- they confirm the proposal: "Want me to remember this for future projects?".

A choice made for a single project stays in `context/decisions.md` and does **not** go
into the registry.

## Preference scopes
`stack`, `services`, `design`, `contract`, `mode`, `communication`, `language`.

## What never goes into the registry
Client data: names, contacts, budgets, content, credentials. Those stay in the project.
The registry holds only the user's working preferences and the evaluated skills.
