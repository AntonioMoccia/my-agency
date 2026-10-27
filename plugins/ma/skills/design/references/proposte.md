# Checklist di qualità di una proposta

Applicarla a ogni proposta **prima** di mostrarla all'utente. Una voce non rispettata va corretta o dichiarata.

## Gerarchia
- In ogni schermata si capisce in meno di 3 secondi cosa è la cosa più importante.
- Un solo elemento domina: un titolo, un'immagine o un numero, non tutti e tre.
- La CTA principale è visibile senza scorrere, su desktop e su mobile.
- La scala tipografica ha salti netti (almeno 1,25× tra i livelli): niente titoli che sembrano paragrafi.

## Contrasto e accessibilità
- Testo normale: contrasto **almeno 4,5:1** sul suo sfondo (WCAG AA). Testo grande (24 px o 19 px grassetto): almeno 3:1.
- Elementi interattivi e bordi di input: almeno 3:1.
- Verificare il contrasto di **ogni** coppia testo/sfondo della palette, compresi gli stati (hover, disabilitato) e il testo sopra le immagini.
- Il colore non è l'unico veicolo di informazione (errori, stati, link nel testo).
- Focus da tastiera sempre visibile.
- Ordine dei titoli coerente (un solo `h1` per pagina).

## Coerenza mobile
- La proposta include il mobile, non solo il desktop ridotto.
- Area toccabile dei controlli almeno 44×44 px.
- Niente scroll orizzontale; tabelle e grafici in un contenitore che scorre da solo.
- Il contenuto principale resta sopra, l'ordine non si stravolge tra desktop e mobile.
- Testo minimo 16 px per il corpo.

## Una sola idea forte per pagina
- La proposta si riassume in una frase.
- L'idea forte (tipografia enorme, griglia spezzata, colore unico, 3D, scroll narrativo) è **una**: se ce ne sono due, scegliere.
- Le altre sezioni sostengono l'idea, non competono.
- Se l'idea forte non funzionasse, la pagina resta leggibile.

## Performance delle animazioni
- Animare solo `transform` e `opacity`: mai `width`, `height`, `top`, `left`, `box-shadow` in loop.
- Durate 150–400 ms per i micro-movimenti, oltre solo per le transizioni di pagina.
- Nessuna animazione in loop permanente nell'area visibile iniziale.
- Ogni animazione ha un **fallback con `prefers-reduced-motion: reduce`**: il contenuto resta completo e visibile.
- Lo scroll non è bloccato: niente scroll-hijacking senza via d'uscita.
- Peso: font al massimo 2 famiglie e 4 pesi; immagini dell'area iniziale sotto i 200 KB; animazioni 3D o video solo se dichiarati come costo in `contesto/costi.md`.

## Coerenza col briefing
- Rispetta i **vincoli** di `contesto/stile.md` (palette e font del brand, accessibilità richiesta).
- Rispetta "cosa evitare".
- Risponde all'obiettivo della discovery, non solo al gusto.
- È realizzabile con lo stack scelto in `contesto/costi.md`.
