---
name: stile
description: Raccoglie la direzione visiva del progetto - logo e brand esistenti, riferimenti di siti o app, parole chiave, cosa evitare e vincoli - e la scrive in contesto/stile.md come briefing per il design. Da usare quando l'utente dice "parliamo di stile", "ecco i riferimenti", "mi piace questo sito", "facciamo il moodboard" o quando la fase stile è la successiva nello stato.
---

# Stile — riferimenti e direzione visiva

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/git.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`.

Prerequisito: `contesto/discovery.md`. Se manca, eseguire prima `onboarding`.

## Passo 1 — Le domande
Al massimo 4 per volta, con risposta libera possibile. Prima controllare `contesto/` e `registro/preferenze.md` (ambito `design`): ciò che si sa già si conferma, non si richiede.

1. **Logo e brand esistenti**: ci sono? Chiedere di mettere i file in `riferimenti/` (logo, manuale brand, palette, font) e dire quali sono arrivati.
2. **Riferimenti**: 2–5 siti o app, come link o screenshot in `riferimenti/`.
3. **Parole chiave**: 3–5 aggettivi sulla sensazione da dare (es. essenziale, caldo, tecnico, lussuoso).
4. **Cosa evitare**: stili, colori, cliché, concorrenti da non somigliare.
5. **Vincoli**: colori obbligatori del brand, font di licenza, livello di accessibilità richiesto, lingue, vincoli tecnici dalla discovery.

## Passo 2 — Scomporre i riferimenti
Per **ogni** riferimento scrivere in `contesto/stile.md` una voce con questa tabella:

| Riferimento | Cosa prendere | Cosa non prendere |
|---|---|---|
| link o file | tipografia, griglia, colore, animazioni, tono — specificare quali | ciò che non si adatta al progetto |

"Cosa prendere" deve essere un principio concreto ("titoli molto grandi con interlinea stretta", "transizioni di pagina in fade da 400 ms"), non un giudizio generico ("è bello").

## Passo 3 — Il brand esistente
Se c'è un logo o un manuale brand:
- ricavare la palette (hex con il ruolo di ogni colore) e il carattere del brand;
- indicarli come **vincoli** in testa a `contesto/stile.md`, distinti dalle ipotesi;
- segnalare in una riga eventuali problemi (contrasto insufficiente, font senza licenza web).

## Passo 4 — Sintesi
Chiudere `contesto/stile.md` con:
- **Direzione in una frase**: dove vogliamo andare.
- **Parole chiave** e **cosa evitare**, in elenco.
- **Vincoli** da rispettare obbligatoriamente.
- **Da verificare in design**: i punti su cui i riferimenti sono in contrasto fra loro.

## Chiusura
1. Registrare le scelte in `contesto/decisioni.md`.
2. Aggiornare `contesto/stato.md`: fase `stile` = `completata`, fase corrente = successiva della modalità.
3. Commit `ma: riferimenti`.
4. Indicare in una riga la fase successiva secondo la modalità.

## Regole
- Dai riferimenti si prendono **principi**, mai layout identici, loghi, testi o immagini altrui.
- Non promettere un risultato "come" un riferimento: si prende l'idea, non la copia.
