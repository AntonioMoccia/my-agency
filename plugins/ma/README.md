# ma — My Agency

Plugin per Claude Code che porta un progetto di sito, app o software dall'onboarding del cliente fino al design approvato, al contratto e allo sviluppo, tenendo traccia di dove si è arrivati.

## Comandi

| Comando | Cosa fa |
|---|---|
| `/ma:progetto` | Punto di ingresso: legge lo stato, mostra le fasi e esegue la successiva. Se il progetto non esiste, avvia l'onboarding |
| `/ma:onboarding` | Setup della cartella (template, cartelle, git, stato) e discovery del cliente in 9 gruppi di domande |
| `/ma:stato` | Mostra fasi, fase corrente, cosa è in attesa e il prossimo passo. Sola lettura |
| `/ma:stile` | Raccoglie logo, riferimenti, parole chiave e vincoli in `contesto/stile.md` |
| `/ma:design` | 2–3 proposte di design diverse, selezione anche per parti, iterazione fino all'approvazione, tabella resources |
| `/ma:costi` | Propone lo stack e calcola i costi dei servizi verificando i prezzi online, con confronto col budget |
| `/ma:contratto` | Bozza di contratto da discovery, costi e decisioni, con segnaposto per i dati mancanti |
| `/ma:refactoring` | Rifacimento di un progetto esistente: acquisizione, audit, specifiche, piano, esecuzione a step |
| `/ma:skill` | Cerca, valuta, installa, elenca e rimuove skill di terze parti, con registro e checklist di sicurezza |

## Le tre modalità

La modalità si sceglie in onboarding, sta in `contesto/stato.md` e decide l'ordine delle fasi.

| Modalità | Quando | Ordine delle fasi |
|---|---|---|
| **Progetto** | Lavoro completo, cliente acquisito | setup → discovery → stile → costi → contratto → design |
| **Pitch** | Proposta per acquisire il cliente | setup → discovery → stile → design (1 proposta leggera) → costi → contratto |
| **Refactoring** | Sito, app o software già esistente | setup → discovery → acquisizione → audit → specifiche → costi → contratto → piano → esecuzione |

In modalità Progetto il design viene **dopo** il contratto: è la parte più costosa e non si regala. In modalità Pitch il design viene prima, ma in versione leggera.

## Avvio rapido

```bash
mkdir progetto-cliente && cd progetto-cliente && claude
```

Poi, dentro Claude Code:

```
/ma:progetto
```

Il plugin copia il template, fa `git init`, chiede nome e modalità e parte con la discovery. Ogni fase chiude con un commit `ma: <fase>` nel repo del progetto.

Per riprendere un progetto, dalla sua cartella: `/ma:progetto` per andare avanti, `/ma:stato` per vedere solo a che punto si è.

## Struttura di un progetto

```text
progetto-cliente/
├── CLAUDE.md
├── contesto/        stato, discovery, stile, decisioni, costi, audit
├── riferimenti/     logo, brand, screenshot dei riferimenti
├── resources/       tabella resources + immagini, testi, video
├── design/          proposte in design/proposte/vN/
├── contratto/       bozza di contratto
├── istruzioni/      come configurare i servizi esterni
└── sito/            il codice
```

## Memoria del plugin

Il plugin ricorda fra progetti diversi in `registro/`:
- `registro/preferenze.md` — stack, servizi, design, contratto, modalità, comunicazione;
- `registro/skills.md` — skill di terze parti valutate: `approvata`, `scartata`, `solo-link`.

Il plugin installato vive in una cache **in sola lettura**: per scrivere nel registro serve il clone locale del repo `my-agency`. Il percorso si indica una volta sola in `~/.claude/ma.json`:

```json
{ "repo": "/percorso/assoluto/my-agency" }
```

Le preferenze si salvano **solo** dopo conferma dell'utente, e solo se espresse come regola ("usa sempre…"). I dati del cliente non entrano mai nel registro: restano nel progetto.

## Aggiornare il plugin

Dopo una scrittura nel registro o una modifica al repo:

```bash
claude plugin marketplace update my-agency
```

La scrittura nel registro fa commit e push sul repo del plugin; l'aggiornamento del marketplace rende la modifica visibile al plugin installato.

## Riferimenti condivisi

Le regole comuni a tutte le skill stanno in `riferimenti/`: `convenzioni.md` (lingua, modalità, regola d'oro, domande), `stato.md` (formato dello stato), `git.md` (commit per fase), `memoria.md` (lettura e scrittura del registro).
