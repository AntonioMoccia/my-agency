---
name: onboarding-sito
description: Avvia l'onboarding di un nuovo sito o app nella cartella di progetto con 4 domande (tipologia, struttura, tecnologie, stile) e compila la tabella resources. Da usare quando l'utente dice "avvia l'onboarding", "nuovo progetto sito", "nuovo cliente", "iniziamo il sito" o apre un progetto clonato dal suo template.
---

# Onboarding sito / app

Rispondere sempre in italiano.

## Regole
- La cartella e il template sono dell'utente: non creare, rinominare o spostare cartelle e file della struttura.
- Leggere prima `CLAUDE.md` / `README.md` del progetto per capire dove vanno le risposte dell'onboarding e dove si trova la tabella resources.
- Se non è chiaro dove scrivere, chiederlo con una sola domanda. Non inventare percorsi.

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
