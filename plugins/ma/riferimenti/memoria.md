# Memoria del plugin

Il registro (`registro/skills.md`, `registro/preferenze.md`) è la memoria del plugin fra progetti diversi.

## Perché serve un clone locale
Il plugin installato vive in una cache in **sola lettura**: scriverci non serve, viene sovrascritto al prossimo aggiornamento. Per scrivere nel registro serve il **clone locale** del repo `my-agency`.

## Percorso del clone
Sta in `~/.claude/ma.json`, in questo formato:

```json
{ "repo": "/percorso/assoluto/my-agency" }
```

Se il file non esiste:
1. chiederlo **una sola volta** ("Dov'è il clone locale del repo `my-agency`?");
2. verificare che il percorso contenga `plugins/ma/registro/`;
3. salvare `~/.claude/ma.json`.

Se l'utente non ha un clone, dirlo in una riga e continuare in sola lettura: le preferenze valgono solo per il progetto corrente.

## Lettura
- Leggere il registro dalla cache del plugin: `${CLAUDE_PLUGIN_ROOT}/registro/`.
- Se esiste il clone locale ed è più recente, leggere da lì.

## Scrittura (solo dopo approvazione dell'utente)
1. Modificare i file dentro `<repo>/plugins/ma/registro/`.
2. `git -C <repo> add -A`
3. `git -C <repo> commit -m "ma: registro <cosa>"`
4. `git -C <repo> push`
5. Suggerire in una riga: "Per vedere la modifica nel plugin installato esegui `claude plugin marketplace update my-agency`".

## Quando salvare una preferenza
Salvare solo se:
- l'utente la esprime come regola ("usa sempre…", "d'ora in poi…", "di default…"); oppure
- conferma la proposta: "Vuoi che lo ricordi per i prossimi progetti?".

Una scelta fatta per un singolo progetto resta in `contesto/decisioni.md` e **non** va nel registro.

## Cosa non salvare mai nel registro
Dati del cliente: nomi, contatti, budget, contenuti, credenziali. Quelli restano nel progetto. Nel registro vanno solo le preferenze di lavoro dell'utente e le skill valutate.
