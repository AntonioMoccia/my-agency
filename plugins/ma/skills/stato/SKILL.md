---
name: stato
description: Mostra in sola lettura lo stato di un progetto - tabella delle fasi, fase corrente, cosa è in attesa, prossimo passo e le skill del registro che servono alla prossima fase. Da usare quando l'utente dice "a che punto siamo", "stato del progetto", "cosa manca", "cosa è in attesa", "mostrami le fasi".
---

# Stato del progetto

Questa skill **non modifica nessun file**: solo lettura. Nessun commit.

Leggere `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md`.

## Passo 1 — Leggere
- `contesto/stato.md` del progetto corrente.
- `registro/skills.md` del plugin (dalla cache o dal clone locale, vedi `memoria.md`).

Se `contesto/stato.md` non esiste, dire in una riga che il progetto non è ancora avviato e suggerire `/ma:progetto`. Fermarsi.

## Passo 2 — Mostrare
1. **Intestazione**: progetto, modalità, fase corrente, ultimo aggiornamento.
2. **Fasi**, nell'ordine della modalità:

| Fase | Stato | Data | File |
|---|---|---|---|

3. **In attesa**: elenco di ciò che serve dall'utente o dal cliente. Se è vuoto, scrivere "niente".
4. **Prossimo passo**: una sola riga.
5. **Skill del registro per la prossima fase**: le skill con stato `approvata` il cui campo **Fasi** contiene la fase successiva.

| Skill | Quando usarla |
|---|---|

Se non ce ne sono, scrivere "nessuna skill aggiuntiva per questa fase".

## Passo 3 — Coerenza
Se i file in `contesto/` non corrispondono alla tabella (per esempio esiste `contesto/stile.md` ma la fase `stile` è ancora `da fare`), segnalarlo in una riga come avviso, **senza correggere il file**: la correzione la fa la skill della fase.
