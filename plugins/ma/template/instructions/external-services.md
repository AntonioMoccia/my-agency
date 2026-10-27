# External services

Use only the sections for the technologies chosen in `onboarding.md`. Never put
credentials in this file.

## Vercel (hosting)
1. Git repository of the `site/` folder → Vercel → Add New Project, root directory `site`.
2. Environment variables from `site/.env.example`.
3. Every branch gets a preview URL: that is the staging to send to the client.

## Domain
1. Save the existing DNS records (especially MX, SPF, DKIM for the email) before changing
   anything.
2. Vercel → Settings → Domains → add the domain and www, enter the records shown.
3. Check HTTPS, and check the client's email still works.

## CMS (Sanity or Payload)
- Sanity: data in the Sanity cloud, polished editor; project in the client's name.
- Payload: admin inside the Next.js app, data in your own database.

## Shopify (ecommerce)
- Store in the client's name, you join as a collaborator.
- Headless: Headless channel → Storefront API token in the environment variables.
- Few products: Stripe Payment Links as an alternative.

## Minimum legal requirements (Italy)
- Privacy and cookie policy, consent banner, company details in the footer.
- Ecommerce: terms of sale, right of withdrawal, shipping terms.
