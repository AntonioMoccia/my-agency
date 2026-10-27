---
name: onboarding
description: Prepara la cartella del progetto (template, cartelle, git, stato) e conduce la discovery del cliente con domande su attività, obiettivo, pubblico, mercato, tipologia, funzioni, contenuti, vincoli ed esistente. Da usare quando l'utente dice "avvia l'onboarding", "nuovo progetto", "nuovo cliente", "iniziamo il sito", "facciamo la discovery" oppure quando la skill progetto non trova contesto/stato.md.
---

# Onboarding — setup e discovery

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/git.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`.

---

# Parte A — Setup

## A1 — Copiare il template
Se manca `contesto/stato.md`, copiare il template senza sovrascrivere nulla:

```
cp -Rn "${CLAUDE_PLUGIN_ROOT}/template/." .
```

Se `${CLAUDE_PLUGIN_ROOT}` non è disponibile, cercare la cartella `template` del plugin `ma` nella cache dei plugin (`~/.claude/plugins/`). Dire in una riga cosa è stato copiato.

Casi particolari:
- La cartella ha già `contesto/stato.md`: non copiare niente, saltare alla parte B.
- La cartella contiene già un progetto diverso (codice, nessun `contesto/`): chiedere con **una sola domanda** se copiare il template qui o in una sottocartella nuova.

## A2 — Cartelle di lavoro
Assicurarsi che esistano `contesto/`, `riferimenti/`, `design/proposte/`, `contratto/`. Creare **solo** quelle mancanti, con un `.gitkeep` se restano vuote. Non rinominare né spostare niente altro.

## A3 — Progetto e modalità
Chiedere in un'unica domanda:
1. **Nome del progetto o del cliente**.
2. **Modalità**: `progetto` (lavoro completo), `pitch` (proposta per acquisire il cliente), `refactoring` (sito, app o software già esistente).

Se in `registro/preferenze.md` c'è una modalità predefinita (ambito `modalità`), proporla già selezionata e dirlo in una riga.

## A4 — Git e stato
1. `git init` se la cartella non è un repo, con il `.gitignore` indicato in `git.md`.
2. Creare `contesto/stato.md` col formato di `stato.md`: progetto, modalità, fase corrente `discovery`, data di oggi, e la tabella delle fasi della modalità scelta tutte a `da fare` tranne `setup` = `completata`.
3. Commit `ma: setup`.

---

# Parte B — Discovery

Scrivere le risposte in `contesto/discovery.md`, **una sezione per gruppo**, nell'ordine della tabella. Fare al massimo 4 domande per volta e seguire la regola d'oro: ciò che è già in `contesto/` o nelle preferenze non si chiede, si conferma.

| Gruppo | Domande |
|---|---|
| Attività | Settore, cosa vende o offre, da quanto tempo, dimensione, territorio |
| Obiettivo | Cosa deve ottenere il progetto in 6–12 mesi (un numero se possibile), perché ora |
| Pubblico | Cliente ideale, dove arriva, cosa deve fare sul sito o nell'app, dubbi prima di comprare |
| Mercato | 2–3 concorrenti, cosa fanno meglio o peggio |
| Tipologia | Vetrina, portfolio, ecommerce, blog, web app, app mobile, software gestionale |
| Funzioni | Funzioni chiave per la tipologia (form, prenotazioni, catalogo, area riservata, integrazioni, lingue) |
| Contenuti | Chi scrive i testi, chi fornisce foto e video, chi aggiorna dopo il lancio e ogni quanto |
| Vincoli | Budget indicativo, scadenza e motivo, chi decide e chi approva |
| Esistente | Sito, app o software attuale (**obbligatorio in refactoring**), domini e account già esistenti |

Note:
- **Tipologia** e **Funzioni**: proporre le opzioni a scelta multipla, non lasciarle aperte.
- **Esistente** in modalità refactoring: chiedere anche repository o accessi, perché serviranno nella fase di acquisizione.
- Ogni scelta rilevante va anche in `contesto/decisioni.md`.

## Chiusura
1. Riepilogo in tabella (`Gruppo | Risposta in breve`), con una riga per i punti rimasti aperti.
2. Aggiornare `contesto/stato.md`: `discovery` = `completata`, fase corrente = fase successiva della modalità, data di oggi, `In attesa` e `Prossimo passo`.
3. Commit `ma: discovery`.
4. Dire in una riga qual è la fase successiva secondo la modalità e chiedere se procedere.
