# Convenzioni comuni

Valgono per tutte le skill del plugin `ma`.

## Lingua e forma
- Rispondere sempre in italiano.
- Output schematici: tabelle dove possibile, frasi brevi, nessun giro di parole.
- Un solo prossimo passo alla fine di ogni risposta.

## Le tre modalità
La modalità è scritta in `contesto/stato.md` e decide l'ordine delle fasi.

| Modalità | Ordine delle fasi |
|---|---|
| Progetto | setup → discovery → stile → costi → contratto → design |
| Pitch | setup → discovery → stile → design (1 proposta leggera) → costi → contratto |
| Refactoring | setup → discovery → acquisizione → audit → specifiche → costi → contratto → piano → esecuzione |

## Regola d'oro: non chiedere ciò che si sa già
Prima di fare una domanda, controllare in quest'ordine:
1. `contesto/` del progetto (`discovery.md`, `stile.md`, `decisioni.md`, `costi.md`);
2. `registro/preferenze.md` del plugin;
3. `registro/skills.md` del plugin.

Se la risposta c'è già, usarla e dirlo in una riga: "Uso Next.js come da tue preferenze". Chiedere solo conferma, non ripetere la domanda.

## Decisioni
Ogni scelta dell'utente va registrata in `contesto/decisioni.md`:

| Data | Fase | Decisione | Motivo |
|---|---|---|---|

## Domande
- Usare domande a scelta multipla con AskUserQuestion quando disponibile.
- Massimo 4 domande per volta.
- Lasciare sempre possibile una risposta libera.

## Skill del registro
Prima di iniziare una fase, cercare in `registro/skills.md` le skill con stato `approvata` il cui campo **Fasi** contiene la fase corrente, e caricarle. Dire in una riga quali skill sono state caricate.

## Riferimenti condivisi
- `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md` — formato di `contesto/stato.md`
- `${CLAUDE_PLUGIN_ROOT}/riferimenti/git.md` — regole Git
- `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md` — lettura e scrittura del registro
