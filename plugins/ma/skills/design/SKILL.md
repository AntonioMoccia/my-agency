---
name: design
description: Genera 2-3 direzioni di design diverse (palette, tipografia, griglia, animazioni, home desktop e mobile), fa scegliere o combinare le proposte, itera fino all'approvazione e tiene aggiornata la tabella resources con testi e immagini mancanti. Da usare quando l'utente dice "fammi il design", "genera le proposte", "facciamo i mockup", "genera le risorse", "mi piace la A ma con la tipografia della B".
---

# Design — proposte, selezione, iterazione

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/git.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`. La checklist di qualità è in `references/proposte.md`: applicarla a ogni proposta prima di mostrarla.

## Passo 0 — Prerequisiti
Servono `contesto/discovery.md` e `contesto/stile.md`. Se mancano, eseguire prima `onboarding` o `stile`.

In modalità **Progetto**, se in `contesto/stato.md` la fase `contratto` non è `completata`, avvisare in una riga ("Il contratto non è ancora chiuso: il design è la parte più costosa") e chiedere conferma prima di procedere.

## Passo 1 — Proposte
Generare **2–3 direzioni realmente diverse**: non tre varianti della stessa idea, ma tre risposte diverse al briefing. In modalità **Pitch**, una sola proposta leggera, solo l'hero.

Ogni proposta contiene:

| Voce | Dettaglio |
|---|---|
| Nome | Una parola che la identifichi |
| Idea | Una frase: su cosa punta e perché funziona per questo cliente |
| Palette | Hex con il ruolo di ogni colore (sfondo, testo, primario, accento, bordi, stati) |
| Tipografia | Coppia di font **open source** (Google Fonts o simili), con scala e pesi |
| Griglia | Colonne, gutter, larghezza massima, ritmo verticale |
| Animazioni | 3–5 animazioni chiave, ognuna col **fallback senza animazione** (`prefers-reduced-motion`) |
| Home | Desktop **e** mobile |

## Passo 2 — Dove produrre il design
In quest'ordine, usando il primo disponibile:
1. **artifact type Design**, se disponibile;
2. **Figma**, se collegato;
3. **pagina HTML statica** in `design/proposte/vN/<nome-proposta>/index.html`.

Dire in una riga quale strada è stata usata.

Salvare sempre in `design/proposte/vN/README.md` la descrizione di ogni proposta (la tabella del passo 1) e il link o il percorso del design.

## Passo 3 — Selezione
Chiedere, in un'unica domanda:
- quale proposta tenere, oppure
- quali proposte, oppure
- **quali parti di ognuna** (es. "palette della A, tipografia della B, hero della C");

e sempre **il motivo**. Registrare tutto in `contesto/decisioni.md`: data, fase `design`, decisione, motivo.

## Passo 4 — Iterazione
Generare `vN+1` come **sintesi delle scelte**, non come nuovo giro di proposte. Ripetere il ciclo proposte → selezione finché l'utente approva. Ogni iterazione chiude con il commit `ma: design vN`.

## Passo 5 — Risorse
Compilare e aggiornare `resources/resources.md` con una riga per ogni risorsa che il design richiede davvero. Stati: `Mancante`, `Presente`, `Generata`, `Da approvare`.
- Generare i **testi** realistici per ogni sezione, nel tono delle parole chiave: **mai lorem ipsum**. Stato `Da approvare`.
- Per ogni **immagine mancante** scrivere nelle note soggetto, inquadratura e formato, così l'utente può generarla o fotografarla. Se è disponibile un generatore di immagini, usarlo e segnare `Generata`.
- Non sovrascrivere le risorse con stato `Presente`.

## Passo 6 — Approvazione
Quando l'utente approva:
1. scrivere "Design approvato il AAAA-MM-GG" in `contesto/stato.md` e in `contesto/decisioni.md`;
2. fase `design` = `completata`;
3. riepilogo in tabella: `Presenti | Generate | Da approvare | Ancora mancanti`;
4. commit `ma: design vN`;
5. un solo prossimo passo (di norma lo sviluppo in `sito/`, o la fase successiva della modalità).

## Regole
- Dai riferimenti si prendono **principi**: mai layout identici, loghi, testi o immagini altrui.
- Niente foto di persone reali prese dal web.
- Usare solo palette, font e testi decisi nei passi precedenti: nessun colore o font "a sorpresa".
- Non iniziare il codice in `sito/` prima dell'approvazione.
