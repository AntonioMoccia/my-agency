---
name: genera-risorse
description: Genera risorse e design di un sito o app partendo dai riferimenti di stile e dalla tabella resources del progetto. Da usare dopo l'onboarding, quando l'utente dice "genera le risorse", "fammi il design", "crea lo stile dai riferimenti" o sceglie che sia Claude a produrre le risorse mancanti.
---

# Genera risorse e design

Rispondere sempre in italiano.

## Regole
- Non toccare la struttura della cartella: salvare ogni file nella cartella indicata dalla tabella resources.
- Generare solo le righe con stato "Mancante" assegnate a Claude. Non sovrascrivere risorse "Presente".
- Dai riferimenti prendere principi (griglia, ritmo, tipografia, tipo di animazione), mai layout identici, loghi, testi o immagini altrui.
- Non usare foto di persone reali trovate sul web.

## Passo 1 — Leggere il contesto
Leggere le risposte dell'onboarding (tipologia, struttura, tecnologie, stile) e la tabella resources. Se mancano i riferimenti, chiederne 2–5 (link o immagini) prima di iniziare.

## Passo 2 — Direzione di stile
Proporre 2 direzioni brevi (nome, idea in una frase, palette, coppia di font, animazione chiave) e far scegliere l'utente. Poi scrivere il file di stile del progetto con:
- palette in hex con il ruolo di ogni colore e contrasto testo/sfondo adeguato
- font open source o Google Fonts, scala tipografica fluida
- spaziature e griglia
- 3–5 animazioni chiave coerenti con la tecnologia scelta (es. GSAP + Lenis) e il loro fallback senza animazione

## Passo 3 — Testi
Per ogni sezione della struttura scrivere testi realistici nel tono indicato dalle parole chiave (mai lorem ipsum). Segnarli come da approvare.

## Passo 4 — Design
Generare il design delle pagine, partendo dalla home (desktop e mobile), poi una pagina per ogni tipo di template:
1. se è disponibile un artifact type Design, creare il design da quel tipo;
2. altrimenti, se Figma è collegato, crearlo in Figma;
3. altrimenti scrivere una pagina HTML statica nella cartella di design del progetto.

Usare solo palette, font e testi generati nei passi precedenti. Fermarsi dopo la home e chiedere conferma prima delle altre pagine.

## Passo 5 — Immagini
Per ogni immagine mancante: usare un generatore di immagini se disponibile; altrimenti scrivere in Note soggetto, inquadratura e formato, così l'utente può generarla o fotografarla.

## Passo 6 — Aggiornare la tabella
Per ogni risorsa creata impostare Stato = "Generata" e Fonte = "Claude". Chiudere con un riepilogo in tabella (Presenti / Generate / Ancora mancanti) e un solo prossimo passo, di solito l'approvazione del design.
