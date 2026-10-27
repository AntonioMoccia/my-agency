---
name: onboarding-sito
description: Avvia l'onboarding di un nuovo sito o app - copia il template del progetto se manca, poi 4 domande (tipologia, struttura, tecnologie, stile) e compila la tabella resources. Da usare quando l'utente dice "avvia l'onboarding", "nuovo progetto sito", "nuovo cliente", "iniziamo il sito".
---

# Onboarding sito / app

Rispondere sempre in italiano.

## Passo 0 — Preparare la cartella
Il template del progetto si trova in `${CLAUDE_PLUGIN_ROOT}/template/`.

- **Cartella senza `resources/resources.md`** (vuota o nuova): copiare il contenuto del template nella cartella corrente senza sovrascrivere file esistenti, ad esempio con `cp -Rn "${CLAUDE_PLUGIN_ROOT}/template/." .`. Se `${CLAUDE_PLUGIN_ROOT}` non è disponibile, cercare la cartella `template` del plugin `ma` nella cache dei plugin (`~/.claude/plugins/`). Dire in una riga cosa è stato copiato.
- **Cartella che ha già `resources/resources.md`**: non copiare nulla, usare la struttura esistente.
- **Cartella con un progetto diverso** (es. codice, nessun `onboarding.md`): chiedere con una sola domanda se copiare il template qui o in una sottocartella nuova.

## Regole
- Dopo il Passo 0 non creare, rinominare o spostare cartelle e file della struttura.
- Le risposte vanno in `onboarding.md`, le risorse in `resources/resources.md`. Se il progetto ha un `CLAUDE.md` che indica percorsi diversi, seguire quelli.

## Passo 1 — Le 4 domande
Usare domande a scelta multipla (AskUserQuestion se disponibile), al massimo due per volta, lasciando sempre possibile una risposta libera.

1. **Tipologia**: Vetrina · Portfolio · Ecommerce · Blog · Web app.
2. **Struttura**: proporre la struttura standard (tabella sotto) e chiedere: va bene / la modifico / ne ho una mia.
3. **Tecnologie**: proporre il default e chiedere solo le varianti utili alla tipologia.
   - Framework: Next.js + TypeScript + Tailwind (default)
   - Motion: GSAP + ScrollTrigger + Lenis (default) · Framer Motion · React Three Fiber per 3D
   - CMS: nessuno (default) · Sanity · Payload
   - Ecommerce (solo ecommerce): Shopify headless · tema Shopify · Stripe Payment Links
   - Hosting: Vercel (default)
4. **Stile**: 3–5 parole chiave, 2–5 riferimenti (link o file), cosa evitare.

### Strutture standard
| Tipologia | Pagine / schermate | Sezioni home |
|---|---|---|
| Vetrina | Home, Chi siamo, Servizi, Contatti | Hero, servizi, perché noi, testimonianze, CTA |
| Portfolio | Home, Lavori, Dettaglio lavoro, About, Contatti | Hero, lavori in evidenza, manifesto, clienti, CTA |
| Ecommerce | Home, Catalogo, Prodotto, Carrello, Chi siamo, Policy | Hero, categorie, prodotti in evidenza, storia, recensioni |
| Blog | Home, Archivio, Articolo, Categoria, Autore, About | Articolo in evidenza, ultimi articoli, categorie, newsletter |
| Web app | Landing, Login, Dashboard, Dettaglio, Impostazioni | Hero, funzioni, come funziona, prezzi, CTA |

## Passo 2 — Registrare le risposte
Scrivere le risposte nel file previsto dal progetto: tipologia, tecnologie, struttura (pagina → sezioni), stile.

## Passo 3 — Compilare la tabella resources
Aggiungere una riga per ogni risorsa che la struttura scelta richiede davvero, usando le colonne già presenti nella tabella (se è vuota: Risorsa · Cartella · Pagina · Stato · Fonte).
- Sempre: logo, palette, font, riferimenti di stile.
- Per pagina: testi delle sezioni, immagine o video hero.
- Portfolio: per ogni lavoro titolo, testo, immagini.
- Ecommerce: catalogo (nome, prezzo, varianti, SKU), foto prodotto, testi policy.
- Blog: autori, categorie, primi articoli.
- Web app: icone, illustrazioni degli stati vuoti, testi dei messaggi.

Stato: "Presente" se il file è già nella cartella indicata, altrimenti "Mancante".

## Passo 4 — Prossimo passo
Chiedere all'utente come procedere:
- **Inserisco io le risorse**: indicare in quali cartelle metterle e chiedere di scrivere "controlla le risorse" a lavoro finito. Al controllo, confrontare cartelle e tabella, aggiornare gli stati ed elencare ciò che manca.
- **Le genera Claude**: passare alla skill `genera-risorse`.
- **Mista**: chiedere quali risorse inserisce l'utente e passare il resto a `genera-risorse`.
