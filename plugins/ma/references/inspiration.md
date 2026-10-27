# Visual inspiration — automatic reference gathering

Used by the `style` skill (step 2) and by the `design` skill (step 1). The goal: never
start a design proposal from a blank page. Collect real, recent, award-level references
for this project's sector and keywords, and extract **principles** from them.

This runs **automatically**, without the user having to ask, every time a design
proposal is about to be produced.

## Source order
1. **Awwwards** — primary source, always queried first.
2. Secondary galleries, only if Awwwards yields fewer than 6 usable references:
   `godly.website`, `siteinspire.com`, `land-book.com`, `lapa.ninja`, `httpster.net`,
   `onepagelove.com`, `mobbin.com` (apps), `dribbble.com` (components only, never whole
   layouts).
3. **Client-supplied references** already in `context/style.md`: always kept in the
   list, never replaced by the automatic ones.

## Awwwards URL shapes
Base listing: `https://www.awwwards.com/websites/`

| Kind | Path | Known slugs |
|---|---|---|
| Category | `/websites/<category>/` | `e-commerce`, `architecture`, `business-corporate`, `design-agencies`, `fashion`, `hotel-restaurant`, `photography`, `portfolio` |
| Tag | `/websites/<tag>/` | `animation`, `scrolling`, `single-page`, `ui-design`, `header-design`, `3d`, `webgl`, `interaction-design`, `typography` |
| Technology | `/websites/<tech>/` | `wordpress`, `shopify`, `react`, `gsap-animation`, `framer-motion`, `webflow` |
| Honours | `/websites/<honour>/` | `sites_of_the_day`, `sites_of_the_month`, `sites_of_the_year`, `honorable`, `nominees` |
| Country | `/websites/<Country>/` | URL-encoded, e.g. `/websites/United%20States/` |
| Paging | `?page=N` | append to any of the above |

Slugs change over time: if a path returns nothing usable, do not retry it twice — fall
back to search (step 2 below) and say so in one line.

## How to fetch, first available
1. **WebFetch** on the Awwwards category/tag/honours page — ask it for the site names,
   studio, and the URL of each entry.
2. **WebSearch** — `site:awwwards.com <sector> <keyword>`, or the same query on the
   secondary galleries.
3. **Chrome browser tools** (`claude-in-chrome`) — only when the pages are
   JavaScript-rendered and steps 1–2 return nothing useful. Save screenshots into
   `references/inspiration/`.
4. **Manual** — ask the user for 3–5 links.

If after steps 1–3 there are fewer than 3 usable references, say so in one line and
**carry on**: missing inspiration never blocks the phase.

## Building the queries
Read the sector, typology and audience from `context/discovery.md`; the keywords,
what to avoid and the constraints from `context/style.md`. Then build 2–4 queries:

- one by **category**, from the sector;
- one or two by **tag**, from the keywords (map below);
- one by **honours** for the current year, for freshness.

| Keyword in the brief | Awwwards tag to try |
|---|---|
| essential, minimal, clean | `ui-design`, `single-page` |
| warm, editorial, human | `typography`, `scrolling` |
| technical, precise, engineered | `ui-design`, `interaction-design` |
| luxury, premium, couture | `fashion`, `3d` |
| immersive, spatial | `webgl`, `3d` |
| narrative, storytelling | `scrolling`, `interaction-design` |
| playful, bold, fun | `animation`, `interaction-design` |

Skip any query that collides with "what to avoid" in `context/style.md`.

## What to record
Write `context/inspiration.md`:

| # | Reference | Source | Seen on | Sector / tag | What to take (principle) | What not to take |
|---|---|---|---|---|---|---|

Rules for the table:
- **What to take** must be a concrete principle — "oversized headlines with tight
  leading", "400 ms fade page transitions", "product grid with no card borders" — never
  a verdict like "it looks great".
- 3 rows minimum, 12 maximum.
- At least 2 references **from the client's sector** and at least 2 **from outside it**:
  it is what keeps the proposal off the sector cliché.
- Only references actually opened. A URL that could not be fetched is written as
  `not reachable` — never listed as if it had been reviewed.
- Prefer entries from the **last 24 months**; note the year when it is relevant.
- Mark the origin of each row: `auto` (gathered here) or `client` (given by the user).

## Using them in the design
- Every proposal in `design/proposals/vN/README.md` cites **1–3 rows** of
  `context/inspiration.md` and the principle it took from each.
- A proposal with no reference is allowed, but it must state which idea it comes from.
- When the user picks or combines proposals, the reference rows that fed the chosen
  parts stay in `context/inspiration.md`; the others are kept as discarded, not deleted.

## Hard rules
- **Principles only, never assets.** No identical layouts, no logos, no copy, no images
  taken from a reference.
- No photographs of real people taken from the web.
- Never promise a result "like <reference>": the idea is borrowed, not the site.
- Screenshots in `references/inspiration/` are working material: they never go to the
  client and never end up in `site/`.
- Read public pages only: no bulk scraping, nothing behind a login, respect each site's
  terms and `robots.txt`.
- Always cite link and date of consultation: an inspiration row without a source is
  worthless in the next iteration.
