# Quality checklist for a proposal

Apply it to every proposal **before** showing it to the user. Any item not met must be
fixed or declared.

## Hierarchy
- In every screen it takes less than 3 seconds to see what matters most.
- One element dominates: a headline, an image or a number — not all three.
- The primary CTA is visible without scrolling, on desktop and on mobile.
- The type scale has clear jumps (at least 1.25× between levels): no headings that read
  like paragraphs.

## Contrast and accessibility
- Body text: contrast **at least 4.5:1** against its background (WCAG AA). Large text
  (24 px, or 19 px bold): at least 3:1.
- Interactive elements and input borders: at least 3:1.
- Check the contrast of **every** text/background pair in the palette, including states
  (hover, disabled) and text over images.
- Colour is not the only carrier of information (errors, states, inline links).
- Keyboard focus always visible.
- Consistent heading order (a single `h1` per page).

## Mobile consistency
- The proposal includes mobile, not just a shrunken desktop.
- Touch targets at least 44×44 px.
- No horizontal scrolling; tables and charts inside their own scrolling container.
- Main content stays on top, the order does not get scrambled between desktop and mobile.
- Body text at least 16 px.

## One strong idea per page
- The proposal can be summed up in one sentence.
- The strong idea (huge typography, broken grid, single colour, 3D, scroll narrative) is
  **one**: if there are two, choose.
- The other sections support the idea, they do not compete with it.
- If the strong idea failed to load, the page would still read.

## Animation performance
- Animate only `transform` and `opacity`: never `width`, `height`, `top`, `left` or
  `box-shadow` in a loop.
- 150–400 ms for micro-movements; longer only for page transitions.
- No permanently looping animation in the initial viewport.
- Every animation has a **`prefers-reduced-motion: reduce` fallback**: the content stays
  complete and visible.
- Scrolling is not hijacked: no scroll-jacking without an escape.
- Weight: at most 2 font families and 4 weights; above-the-fold images under 200 KB; 3D
  or video only if declared as a cost in `context/costs.md`.

## Faithfulness to the brief
- Respects the **constraints** in `context/style.md` (brand palette and fonts, required
  accessibility).
- Respects "what to avoid".
- Answers the goal from the discovery, not just taste.
- Is buildable with the stack chosen in `context/costs.md`.

## References
- Every proposal cites 1–3 rows of `context/inspiration.md` with the principle taken.
- The principle is visible in the proposal: if nobody could tell which reference fed it,
  the citation is decoration — remove it or make the principle real.
- Nothing was copied: no identical layout, no borrowed logo, copy or image.
