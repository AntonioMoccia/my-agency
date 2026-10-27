---
name: contratto
description: Compila una bozza di contratto di sviluppo web partendo da discovery, costi e decisioni del progetto, con deliverable, esclusioni, milestone, revisioni, pagamenti, proprietà e intestazioni, lasciando segnaposto per i dati mancanti. Da usare quando l'utente dice "facciamo il contratto", "preparami la proposta", "manda il preventivo", "cosa firma il cliente".
---

# Contratto — bozza per il cliente

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/git.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`. Il modello da compilare è in `references/modello.md`.

## Passo 1 — Scegliere il modello
Usare `references/modello.md`. Se in `registro/preferenze.md` (ambito `contratto`) è indicato un **modello validato** dall'utente, usare quello e dirlo in una riga.

## Passo 2 — Leggere il contesto
| Da | Cosa prendere |
|---|---|
| `contesto/discovery.md` | Cliente, tipologia, funzioni, scadenza e motivo, chi decide e approva, chi fornisce i contenuti |
| `contesto/costi.md` | Servizi, chi li paga, intestazioni, totale annuo |
| `contesto/decisioni.md` | Stack, modalità, scelte di design già prese |
| `contesto/stato.md` | Fasi completate, per definire le milestone realistiche |

## Passo 3 — Compilare
Compilare tutte le sezioni del modello:
parti · oggetto · deliverable · esclusioni · tempi e milestone · numero di revisioni · pagamenti a milestone · intestazione di dominio, hosting e account al cliente · proprietà del codice e del design a saldo · contenuti a carico di chi · manutenzione opzionale · recesso.

Criteri:
- **Deliverable**: elencare cosa viene consegnato, in modo verificabile (numero di pagine o schermate, lingue, ambienti).
- **Esclusioni**: scrivere esplicitamente cosa **non** è compreso. È la parte che evita le discussioni: contenuti, foto, traduzioni, SEO continuativa, campagne, manutenzione, funzioni non elencate.
- **Milestone**: legarle alle fasi reali del progetto (design approvato, sviluppo, collaudo, lancio).
- **Revisioni**: un numero preciso per fase, e cosa succede dopo (tariffa a ore o a giro).
- **Pagamenti**: percentuale per milestone; la somma fa 100%.
- **Intestazioni**: dominio, hosting e account dei servizi **al cliente**, con l'agenzia come collaboratore. Riprendere le voci da `contesto/costi.md`.
- **Proprietà**: codice e design passano al cliente **a saldo completo**; dire cosa resta all'agenzia (strumenti e librerie proprie, portfolio).
- **Contenuti**: chi li fornisce ed entro quando; cosa succede se arrivano in ritardo.

## Passo 4 — Cosa non inventare
Le informazioni che mancano restano come segnaposto:

```
[DA COMPLETARE: denominazione, P.IVA e sede dell'emittente]
[DA COMPLETARE: importo complessivo]
```

Non inventare mai: dati dell'emittente, P.IVA, importi, tariffa oraria, date di firma, numeri di preventivo. Chiudere con l'elenco dei segnaposto da compilare.

## Passo 5 — Avviso obbligatorio
In **testa** al documento inserire sempre:

> **Bozza da far verificare a un legale o commercialista. Serve un soggetto emittente con P.IVA o società.**

Non togliere questo avviso e non attenuarlo: la skill produce una bozza di lavoro, non un atto legale.

## Chiusura
1. Salvare in `contratto/bozza.md`.
2. Registrare le scelte contrattuali in `contesto/decisioni.md`.
3. Aggiornare `contesto/stato.md`: fase `contratto` = `completata`.
4. Commit `ma: contratto`.
5. Riepilogo in tabella (`Sezione | Stato`) e l'elenco dei `[DA COMPLETARE]` rimasti, poi la fase successiva.
