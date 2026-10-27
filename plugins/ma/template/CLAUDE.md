# Instructions for Claude

Project created with the `ma` plugin (My Agency).

1. Before any work, read `context/` (state, discovery, style, decisions, inspiration),
   `onboarding.md` and `resources/resources.md`.
2. If `context/state.md` is missing, or the onboarding is not filled in, run `/ma:project`.
3. Reply and write deliverables in the **project language** recorded in `context/state.md`.
4. Do not start the code in `site/` until the design in `design/` is approved.
5. Every generated resource goes into its folder under `resources/` (or `design/`) and is
   marked "Generated" in `resources.md`.
6. Never put credentials in a file: use environment variables.
