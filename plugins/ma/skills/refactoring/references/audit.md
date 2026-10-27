# Checklist di audit di un progetto esistente

Compilare `contesto/audit.md` con queste tre colonne. Esito: `ok`, `da migliorare`, `critico`, `non applicabile`.

| Voce | Come verificarla | Esito |
|---|---|---|
| **Stack e versioni** | Leggere `package.json` (o equivalente), file di lock, runtime richiesto. Annotare framework e versione, e se è ancora supportata | |
| **Dipendenze obsolete** | `npm outdated` (o `pip list --outdated`, `composer outdated`). Contare quante major indietro sono le principali | |
| **Dipendenze vulnerabili** | `npm audit` (o equivalente). Annotare quante vulnerabilità critiche e alte | |
| **Struttura del codice** | Leggere l'albero delle cartelle: separazione delle responsabilità, duplicazioni, file enormi, codice morto, componenti riusabili | |
| **Presenza di test** | Cercare `test`, `spec`, `__tests__`, configurazioni di test. Eseguirli: passano? Che copertura dichiarano? | |
| **Build** | Eseguire la build da pulito: funziona? Quanto dura? Ci sono warning? | |
| **Lighthouse** | Eseguire Lighthouse sulla produzione, desktop e mobile: performance, accessibilità, SEO, best practice (0–100) | |
| **Core Web Vitals** | LCP (obiettivo < 2,5 s), INP (< 200 ms), CLS (< 0,1). Dati reali se disponibili, altrimenti da laboratorio | |
| **Peso delle pagine** | Peso totale e numero di richieste della home; immagini non ottimizzate; font caricati | |
| **SEO** | `title` e `description` unici per pagina, un solo `h1`, URL leggibili, `sitemap.xml`, `robots.txt`, canonical, dati strutturati, pagine indicizzate | |
| **Accessibilità** | Contrasto (AA: 4,5:1), navigazione da tastiera e focus visibile, `alt` sulle immagini, label sui form, landmark e ordine dei titoli | |
| **Sicurezza: segreti** | Cercare chiavi e password nel codice e nella storia Git (`git log -p` sui file di configurazione, `.env` committati) | |
| **Sicurezza: header** | Verificare HTTPS e redirect, HSTS, CSP, `X-Content-Type-Options`, `Referrer-Policy`, cookie con `Secure` e `HttpOnly` | |
| **Form e input** | Validazione lato server, protezione anti-spam, upload limitati, messaggi di errore che non espongono dettagli interni | |
| **Privacy e cookie** | Banner di consenso funzionante, script di tracciamento bloccati prima del consenso, privacy e cookie policy presenti, dati societari nel footer | |
| **Hosting e costi attuali** | Dove è ospitato, che piano, chi lo paga, a nome di chi sono dominio e account, quando scadono | |
| **Backup e ripristino** | Esiste un backup? Di cosa (codice, database, media)? È stato mai provato un ripristino? | |
| **Monitoraggio** | Error tracking, uptime, log accessibili | |
| **Contenuti** | Quante pagine, chi li aggiorna, c'è un CMS, contenuti duplicati o obsoleti | |
| **Integrazioni** | Servizi esterni collegati (pagamenti, email, CRM, analytics) e se funzionano ancora | |

## Chiusura dell'audit
1. **I 5 problemi più gravi**, in ordine di impatto sull'obiettivo del cliente, con una riga sulla conseguenza concreta.
2. **Cosa funziona e va conservato**: è importante quanto l'elenco dei problemi.
3. **Interventi obbligatori** (sicurezza, privacy, accessibilità di legge) separati da quelli **opzionali**.
4. **Stima dello sforzo** per ogni problema: basso, medio, alto. Nessuna stima in giornate: quella sta nel contratto.

## Note
- Verificare **sulla produzione** per Lighthouse, header e SEO; **sul codice** per dipendenze, struttura e test.
- Se un controllo non si può eseguire (nessun accesso, build rotta), scrivere `non verificabile` e il perché: non lasciare la riga vuota.
- Non modificare niente durante l'audit: è una fase di sola lettura.
