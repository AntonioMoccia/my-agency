# Servizi esterni

Usa solo le sezioni delle tecnologie scelte in `onboarding.md`. Mai credenziali in questo file.

## Vercel (hosting)
1. Repository Git della cartella `sito/` → Vercel → Add New Project, root directory `sito`.
2. Variabili d'ambiente da `sito/.env.example`.
3. Ogni branch ha un URL di anteprima: è lo staging da mandare al cliente.

## Dominio
1. Salva i record DNS esistenti (soprattutto MX, SPF, DKIM delle email) prima di modificarli.
2. Vercel → Settings → Domains → aggiungi dominio e www, inserisci i record mostrati.
3. Verifica HTTPS e che le email del cliente funzionino ancora.

## CMS (Sanity o Payload)
- Sanity: dati sul cloud Sanity, editor curato; progetto intestato al cliente.
- Payload: admin dentro l'app Next.js, dati sul tuo database.

## Shopify (ecommerce)
- Store intestato al cliente, tu entri come collaboratore.
- Headless: canale Headless → token Storefront API nelle variabili d'ambiente.
- Pochi prodotti: in alternativa Stripe Payment Links.

## Obblighi minimi (Italia)
- Privacy e cookie policy, banner consenso, dati societari nel footer.
- Ecommerce: condizioni di vendita, recesso, spedizioni.
