---
name: costi
description: Propone lo stack tecnico del progetto e ne calcola i costi dei servizi verificando i prezzi online al momento, con tabella una tantum e mensile, alternative economiche, totale annuo e confronto col budget. Da usare quando l'utente dice "quanto costa", "che stack usiamo", "quanto spende il cliente al mese", "facciamo i costi", "stiamo nel budget".
---

# Costi — stack e costi dei servizi

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/git.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`. Le categorie di servizi per tipologia sono in `references/servizi.md`.

## Passo 1 — Leggere il contesto
Da `contesto/discovery.md`: **tipologia**, **funzioni** richieste, **budget indicativo**, lingue, chi aggiorna i contenuti.
Da `registro/preferenze.md` (ambito `stack` e `servizi`): lo stack preferito.

Seguire la regola d'oro: se lo stack è nelle preferenze, **non richiederlo**. Confermarlo in una riga ("Uso Next.js su Vercel come da tue preferenze") e chiedere solo le varianti che la tipologia impone.

## Passo 2 — Proporre lo stack
Coprire queste voci, scegliendo in base a tipologia e funzioni (dettaglio in `references/servizi.md`):

| Voce | Note |
|---|---|
| Framework | |
| Hosting | |
| CMS | Solo se i contenuti li aggiorna il cliente |
| Ecommerce | Solo se la tipologia è ecommerce |
| Email transazionali | Form, ordini, recupero password |
| Analytics | |
| Cookie e privacy | Banner di consenso, obbligatorio in Italia |
| Dominio | |

Per **ogni** scelta scrivere il motivo in una riga, legato alla discovery ("CMS perché i testi li aggiorna il cliente ogni settimana"). Se una voce non serve, dirlo e spiegare perché.

## Passo 3 — Verificare i prezzi
**Verificare i prezzi online al momento**, per ogni servizio. Citare **fonte e data** di ogni prezzo.

Non usare prezzi a memoria: i piani cambiano. Se un prezzo non è verificabile (preventivo su richiesta, prezzo per volume), scriverlo come `da verificare` e non inventarlo. Attenzione a: valuta (preferire EUR, dire se il prezzo è in USD), IVA inclusa o esclusa, prezzo per utente o per sito, differenza mensile/annuale.

## Passo 4 — Scrivere `contesto/costi.md`

| Servizio | Opzione consigliata | Una tantum | Mensile | Alternativa economica | Trade-off |
|---|---|---|---|---|---|

Sotto la tabella:
- **Totale una tantum** e **totale mensile**, poi il **totale annuo** (una tantum + mensile × 12).
- **Confronto col budget** di discovery: `dentro`, `al limite` o `fuori`.
- Se è **fuori budget**, proporre uno **stack alternativo** completo (seconda tabella) che ci rientri, dicendo cosa si perde.
- **Fonti**: elenco di link e data di consultazione.

## Regole
- **Non stimare il lavoro dell'agenzia**: qui vanno solo i costi dei servizi. Le giornate e il prezzo del progetto stanno nel contratto.
- Distinguere ciò che paga il cliente direttamente (dominio, hosting, CMS) da ciò che è intestato all'agenzia.
- Preferire i piani gratuiti solo se reggono il caso reale: dire il limite oltre il quale si paga.

## Chiusura
1. Registrare lo stack scelto in `contesto/decisioni.md`.
2. Se l'utente conferma lo stack come preferenza ("usa sempre…"), proporre di salvarlo nel registro secondo `memoria.md`.
3. Aggiornare `contesto/stato.md`: fase `costi` = `completata`.
4. Commit `ma: costi`.
5. Indicare in una riga la fase successiva secondo la modalità.
