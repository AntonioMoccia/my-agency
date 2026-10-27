# Question banks for the client questionnaire

Source material, not a script. Pick the set, drop what is already known, keep at most 20
questions. Types: `short`, `long`, `single`, `multi`, `number`, `yes-no`, `file`, `link`.
Translate every question into the project language and into the client's own words.

The **Why** column is not decoration: it becomes the help line under the question, and
it is the test of whether the question deserves to exist.

---

## Set `discovery`

### Business
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 1 | What do you sell or offer, in one sentence? | short | yes | It becomes the site's opening line |
| 2 | What sector are you in, and since when? | short | yes | Sets the tone and the references |
| 3 | How big is the team? | single | no | Drives the about page and the tone |
| 4 | Where are your customers? (city, region, Italy, abroad) | multi | yes | Languages, currency, shipping |
| 5 | What do you do better than your competitors? | long | yes | It is the claim of the home page |

### Goal
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 6 | What should this project achieve in the next 6-12 months? | long | yes | Everything else is judged against this |
| 7 | How would you measure it? (calls, quotes, orders, signups) | single | yes | It defines the primary CTA |
| 8 | Why now? Is there a date you have to hit? | short | yes | Deadline and phasing |
| 9 | What is not working today? | long | no | The list of things not to repeat |

### Audience
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 10 | Describe your ideal customer | long | yes | Tone, images, hierarchy |
| 11 | How do they find you today? | multi | no | SEO, social, word of mouth, ads |
| 12 | What do they need to do on the site? | multi | yes | It defines the main flow |
| 13 | What makes them hesitate before buying? | long | yes | It becomes the FAQ and the reassurance blocks |

### Market
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 14 | Two or three competitors, with links | link | yes | Benchmark and differentiation |
| 15 | What do you like about their sites, and what do you not? | long | no | Faster than any abstract style question |
| 16 | Is there anyone you must not look like? | short | no | Hard constraint for the design |

### Typology and features
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 17 | What kind of project is it? (brochure site, portfolio, ecommerce, blog, web app, mobile app, business software) | single | yes | It decides stack and costs |
| 18 | How many pages or screens, roughly? | number | no | Scope and quote |
| 19 | Which features do you need? (contact form, bookings, catalogue, members area, payments, multi-language, newsletter, chat) | multi | yes | It is the deliverables list in the contract |
| 20 | Do you need to sell online, now or later? | single | yes | It changes the architecture |

### Content
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 21 | Who writes the texts? (you, us, mixed) | single | yes | Timeline and quote |
| 22 | Do you have professional photos and video? | single | yes | The biggest hidden cost in any project |
| 23 | Who will update the site after launch, and how often? | single | yes | It decides whether a CMS is needed |

### Constraints
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 24 | What budget band are you working with? | single | yes | Avoids designing something unbuildable |
| 25 | Who decides and who approves? | short | yes | Prevents endless review rounds |
| 26 | Any constraint we should know? (corporate rules, legal, accessibility, existing suppliers) | long | no | Surfaces blockers early |

### Existing
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 27 | Do you already have a site or app? Link please | link | yes | Starting point, redirects, SEO |
| 28 | Who owns the domain, and where is it registered? | short | yes | Handover and go-live |
| 29 | Which accounts are already in place? (hosting, analytics, email, social, ecommerce) | multi | yes | Avoids duplicate costs. **Names only, never passwords** |

---

## Set `brand`
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 1 | Do you have a logo? Send the file in the best quality you have | file | yes | Vector or raster changes everything |
| 2 | Is there a brand manual, or set colours and fonts? | file | no | They become hard constraints |
| 3 | Three adjectives for how the site should feel | short | yes | The brief for the design |
| 4 | Three sites you like, in any sector, with one line on why | link | yes | More useful than any adjective |
| 5 | Colours, styles or cliches to avoid | long | yes | It saves one whole design round |
| 6 | Are there photos of the team, the shop or the product we can use? | single | no | It decides whether the design can lean on photography |
| 7 | Does anything have to stay as it is? (logo, colours, a slogan) | long | no | Non-negotiables |

---

## Set `content`
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 1 | For each page, do you have the text, or should we draft it? | multi | yes | It is the critical path to launch |
| 2 | Send the texts you already have, in any format | file | no | Better messy than invented |
| 3 | Photos: who supplies them and by when? | short | yes | Deadline that actually blocks the design |
| 4 | Any video? Where is it hosted? | link | no | Weight and player |
| 5 | Exact company details for the footer (legal name, VAT number, registered office, REA) | short | yes | Legally required in Italy |
| 6 | Real contacts to publish (email, phone, address, opening hours) | short | yes | They go live, so they must be right |
| 7 | Social profiles to link | link | no | Footer and schema markup |
| 8 | Numbers or claims you want to show (years in business, clients, awards) | long | no | They must be true, so only you can give them |
| 9 | Do you have certifications, partners or press mentions? | file | no | Trust blocks |

---

## Set `ecommerce`
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 1 | How many products, and how many variants each? | number | yes | It decides the platform |
| 2 | Do you have a product file or a spreadsheet? | file | yes | Import vs manual entry |
| 3 | Which payment methods do you need? | multi | yes | Gateway and fees |
| 4 | How do you ship, and with which couriers? | multi | yes | Rates and integrations |
| 5 | Free shipping over a threshold? | yes-no | no | It is a rule in the checkout |
| 6 | Do you need electronic invoicing? | yes-no | yes | Mandatory in Italy, it is an integration |
| 7 | How do you handle returns? | long | yes | Required policy page |
| 8 | Do you have a warehouse system to connect? | short | no | Stock sync |
| 9 | Discount codes, bundles or loyalty? | multi | no | Platform features |
| 10 | Do you sell abroad? Which countries and currencies? | multi | yes | VAT, languages, shipping |

---

## Set `app`
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 1 | Who are the users, and what types are there? | long | yes | Roles and permissions |
| 2 | What must each type be able to do? | long | yes | It is the feature list |
| 3 | Is there a login? Who creates the accounts? | single | yes | Auth and onboarding |
| 4 | What data does the app handle? Any sensitive or health data? | long | yes | GDPR and security level |
| 5 | Which systems must it talk to? | multi | no | Integrations |
| 6 | Is there a tool you use today, even a spreadsheet? Send it | file | no | The real spec is usually in there |
| 7 | How many people will use it, and how often? | number | no | Sizing and costs |
| 8 | Does it need to work on mobile, offline, or on a tablet in the field? | multi | yes | It changes the architecture |

---

## Set `existing`
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 1 | Link to the current site or app | link | yes | Starting point |
| 2 | Who built it, and are they still involved? | short | yes | Handover and access |
| 3 | Do you know what it is built with? | short | no | We will verify anyway |
| 4 | Is there a repository or source code? Who has it? | short | yes | Refactoring vs rebuild |
| 5 | Where is it hosted, and who pays for it? | short | yes | Migration and costs |
| 6 | Which accounts exist, and who administers each? | multi | yes | **Names and roles only, never credentials** |
| 7 | What must absolutely not change? (URLs, content, integrations) | long | yes | It becomes the acceptance criteria |
| 8 | Is there traffic or SEO ranking worth protecting? | yes-no | yes | Redirect plan |

---

## Set `admin`
| # | Question | Type | Required | Why we ask |
|---|---|---|---|---|
| 1 | Exact billing details (legal name, VAT number, tax code, registered office, SDI code or PEC) | short | yes | They go in the contract and the invoice |
| 2 | Who signs, and in what role? | short | yes | The contract needs a signatory |
| 3 | Who approves the design, and who gives the final sign-off? | short | yes | Prevents review deadlock |
| 4 | Purchase order or reference number needed on the invoice? | short | no | Corporate clients require it |
| 5 | Payment terms you work with | single | no | It is negotiated, better to know early |

---

## Rules for every set
- **Never ask for passwords, API keys, card numbers or recovery codes.** Access is
  arranged separately, through a password manager or a channel the user chooses.
- Every `file` question needs a size limit and accepted formats, and a plain-email
  alternative.
- Every `single` and `multi` question lists the options plus "something else" with a
  free-text box.
- Money questions use **bands**, not an open field: a client who has to type a number
  abandons the form.
- Questions that only the client can answer come first; the nice-to-haves go last, so a
  half-finished questionnaire is still usable.
