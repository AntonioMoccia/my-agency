---
name: progetto
description: Punto di ingresso guidato di un progetto di sito o app - legge lo stato, mostra le fasi fatte e manca, poi esegue la fase successiva secondo la modalità (progetto, pitch, refactoring). Da usare quando l'utente dice "nuovo progetto", "nuovo cliente", "riprendiamo il progetto", "andiamo avanti", "qual è il prossimo passo" o apre una cartella di progetto senza sapere da dove ripartire.
---

# Progetto — comando guidato

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`.

## Passo 1 — Leggere lo stato
Leggere `contesto/stato.md` nella cartella corrente.

- **Non esiste**: il progetto non è ancora avviato. Eseguire la skill `onboarding` e fermarsi qui.
- **Esiste**: proseguire col passo 2.

## Passo 2 — Mostrare dove siamo
Ricavare l'ordine delle fasi dalla modalità indicata in `stato.md` (tabella delle modalità in `convenzioni.md`) e mostrare una tabella:

| Fase | Stato | Data | File |
|---|---|---|---|

Sotto la tabella, in tre righe:
- **Fase corrente**: la prima fase non `completata` né `saltata`.
- **In attesa**: cosa serve dall'utente o dal cliente.
- **Prossimo passo**: la fase da eseguire adesso.

## Passo 3 — Caricare le skill del registro
Cercare in `registro/skills.md` le skill con stato `approvata` il cui campo **Fasi** contiene la fase successiva. Caricarle e dirlo in una riga.

## Passo 4 — Eseguire la fase successiva
Eseguire la skill corrispondente alla fase:

| Fase | Skill |
|---|---|
| setup, discovery | `onboarding` |
| stile | `stile` |
| costi | `costi` |
| contratto | `contratto` |
| design | `design` |
| acquisizione, audit, specifiche, piano, esecuzione | `refactoring` |

Chiedere conferma in una riga prima di partire ("Passo alla fase stile, procedo?"), poi eseguire.

## Saltare o rifare una fase
Se l'utente chiede di saltare una fase, impostarla come `saltata` in `stato.md` e passare alla successiva. Se chiede di rifarla, impostarla come `in corso` ed eseguirla di nuovo. In entrambi i casi annotare la scelta in `contesto/decisioni.md` con il motivo.

## Fuori da una cartella di progetto
Se la cartella corrente non è vuota e contiene un progetto diverso (codice, nessun `contesto/`), non fare nulla: chiedere con una sola domanda se avviare qui un nuovo progetto o spostarsi in un'altra cartella.
