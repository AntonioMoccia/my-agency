# Formato dello stato del progetto

File: `contesto/stato.md` nella cartella del progetto cliente. È la fonte di verità su dove siamo.

## Modello da usare

```markdown
# Stato del progetto
| Voce | Valore |
|---|---|
| Progetto | |
| Modalità | progetto / pitch / refactoring |
| Fase corrente | |
| Ultimo aggiornamento | AAAA-MM-GG |

## Fasi
| Fase | Stato | Data | File |
|---|---|---|---|

## Prossimo passo
-

## In attesa
-
```

## Regole
- Aggiornare `stato.md` alla fine di ogni fase, prima del commit.
- Stati possibili di una fase: `da fare`, `in corso`, `completata`, `saltata`.
- La colonna **File** indica i file prodotti dalla fase (es. `contesto/discovery.md`).
- **Fase corrente** è la prima fase non `completata` né `saltata` secondo l'ordine della modalità.
- **In attesa** elenca ciò che serve dall'utente o dal cliente (materiali, approvazioni, dati).
- `Ultimo aggiornamento` sempre in formato `AAAA-MM-GG`.
- Le fasi da elencare sono quelle della modalità scelta: vedi la tabella in `convenzioni.md`.
