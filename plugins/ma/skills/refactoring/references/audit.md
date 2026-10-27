# Audit checklist for an existing project

Fill in `context/audit.md` with these three columns. Outcome: `ok`, `needs work`,
`critical`, `not applicable`.

| Item | How to check it | Outcome |
|---|---|---|
| **Stack and versions** | Read `package.json` (or equivalent), lock files, required runtime. Note framework and version, and whether it is still supported | |
| **Outdated dependencies** | `npm outdated` (or `pip list --outdated`, `composer outdated`). Count how many majors behind the main ones are | |
| **Vulnerable dependencies** | `npm audit` (or equivalent). Note how many critical and high vulnerabilities | |
| **Code structure** | Read the folder tree: separation of concerns, duplication, huge files, dead code, reusable components | |
| **Tests present** | Look for `test`, `spec`, `__tests__`, test configuration. Run them: do they pass? What coverage do they claim? | |
| **Build** | Run a clean build: does it work? How long does it take? Any warnings? | |
| **Lighthouse** | Run Lighthouse against production, desktop and mobile: performance, accessibility, SEO, best practices (0–100) | |
| **Core Web Vitals** | LCP (target < 2.5 s), INP (< 200 ms), CLS (< 0.1). Field data if available, otherwise lab | |
| **Page weight** | Total weight and number of requests on the home page; unoptimised images; fonts loaded | |
| **SEO** | Unique `title` and `description` per page, a single `h1`, readable URLs, `sitemap.xml`, `robots.txt`, canonical, structured data, indexed pages | |
| **Accessibility** | Contrast (AA: 4.5:1), keyboard navigation and visible focus, `alt` on images, labels on forms, landmarks and heading order | |
| **Security: secrets** | Look for keys and passwords in the code and in the Git history (`git log -p` on config files, committed `.env`) | |
| **Security: headers** | Check HTTPS and redirects, HSTS, CSP, `X-Content-Type-Options`, `Referrer-Policy`, cookies with `Secure` and `HttpOnly` | |
| **Forms and input** | Server-side validation, anti-spam protection, upload limits, error messages that do not leak internals | |
| **Privacy and cookies** | Working consent banner, tracking scripts blocked before consent, privacy and cookie policy present, company details in the footer | |
| **Hosting and current costs** | Where it is hosted, which plan, who pays, whose name the domain and accounts are in, when they expire | |
| **Backup and restore** | Is there a backup? Of what (code, database, media)? Has a restore ever been tested? | |
| **Monitoring** | Error tracking, uptime, accessible logs | |
| **Content** | How many pages, who updates them, is there a CMS, duplicate or stale content | |
| **Integrations** | Connected external services (payments, email, CRM, analytics) and whether they still work | |

## Closing the audit
1. **The 5 most serious problems**, in order of impact on the client's goal, each with one
   line on its concrete consequence.
2. **What works and must be preserved**: as important as the list of problems.
3. **Mandatory work** (security, privacy, legally required accessibility) separated from
   the **optional** work.
4. **Effort estimate** per problem: low, medium, high. No estimate in days: that belongs
   in the contract.

## Notes
- Check **on production** for Lighthouse, headers and SEO; **on the code** for
  dependencies, structure and tests.
- If a check cannot be run (no access, broken build), write `cannot verify` and why: never
  leave the row empty.
- Change nothing during the audit: it is a read-only phase.
