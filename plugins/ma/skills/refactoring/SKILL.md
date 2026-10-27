---
name: refactoring
description: Porta avanti il rifacimento di un sito, app o software esistente in cinque fasi - acquisizione del codice, audit, specifiche, piano a step e esecuzione - lavorando sul branch refactoring con un commit per step e un controllo dopo ognuno. Da usare quando l'utente dice "rifacciamo il sito", "migriamo questo progetto", "restyling", "sistemiamo il codice esistente", "il cliente ha già un sito".
---

# Refactoring — rifacimento di un progetto esistente

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/stato.md`, `${CLAUDE_PLUGIN_ROOT}/riferimenti/git.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`. La checklist dell'audit è in `references/audit.md`.

Prerequisito: `contesto/discovery.md` con il gruppo **Esistente** compilato. Eseguire una fase per volta, nell'ordine, con **un commit per fase**.

| Fase | Cosa fare | File |
|---|---|---|
| Acquisizione | Chiedere il repo o il percorso (o l'URL, se c'è solo il sito pubblico). Clonare o collegare in `sito/`, creare il branch `refactoring` | `contesto/sorgente.md` |
| Audit | Seguire `references/audit.md` | `contesto/audit.md` |
| Specifiche | Tipi di intervento, obiettivi, cosa non deve cambiare, criteri di accettazione | `contesto/specifiche.md` |
| Piano | Step piccoli e verificabili, ognuno con controllo, rischio e rollback | `contesto/piano.md` |
| Esecuzione | Uno step alla volta, poi build, test, controllo e commit `ma: step N` | codice |

---

## 1. Acquisizione
Chiedere, in un'unica domanda, cosa c'è a disposizione: **repository Git**, **cartella locale** o **solo il sito pubblico** (URL).

- Repository: clonare in `sito/`. Se `sito/` non è vuota, chiedere come procedere.
- Cartella locale: copiarla o collegarla in `sito/`, dopo averne verificato il contenuto.
- Solo URL: non c'è codice da riusare. Dirlo chiaramente: il lavoro sarà una ricostruzione, non un refactoring. Salvare gli screenshot delle pagine principali come riferimento.

Creare il branch: `git -C sito checkout -b refactoring`.

Scrivere `contesto/sorgente.md`: provenienza, URL di produzione, accessi ricevuti (**mai le credenziali**: solo quali accessi ci sono e dove sono conservati), branch di partenza, commit iniziale, dimensione e linguaggi.

Commit `ma: acquisizione`.

## 2. Audit
Seguire la checklist di `references/audit.md` e scrivere `contesto/audit.md` con le colonne `voce | come verificarla | esito`.

Chiudere con: i 5 problemi più gravi in ordine di impatto, e cosa **funziona** e va conservato.

Commit `ma: audit`.

## 3. Specifiche
Definire con l'utente:
- **Tipi di intervento** (combinabili): `restyling`, `migrazione`, `qualità del codice`, `nuove funzioni`.
- **Obiettivi**: misurabili dove possibile (tempo di caricamento, punteggio Lighthouse, conversioni).
- **Cosa non deve cambiare**: URL, contenuti, aspetto, integrazioni, dati.
- **Criteri di accettazione**: per ogni obiettivo, come si verifica che è raggiunto.

Scrivere `contesto/specifiche.md`. Commit `ma: specifiche`.

## 4. Piano
Scomporre in **step piccoli e verificabili**, ognuno in una riga:

| # | Step | Controllo | Rischio | Rollback |
|---|---|---|---|---|

Regole: uno step modifica una cosa sola; ogni step ha un controllo oggettivo (build, test, screenshot, pagina che risponde); gli step ad alto rischio vanno isolati e messi dopo quelli sicuri.

Scrivere `contesto/piano.md`. Commit `ma: piano`.

## 5. Esecuzione
Prima di toccare il codice: **se mancano i test**, creare test di caratterizzazione (che fissano il comportamento attuale, anche se imperfetto) oppure screenshot di riferimento delle pagine principali, in desktop e mobile. Senza una rete di sicurezza non si inizia.

Poi, per ogni step:
1. applicare **solo** quello step;
2. build;
3. test;
4. controllo indicato nel piano;
5. commit `ma: step N`.

Se un controllo **fallisce**: fermarsi, non passare allo step successivo, spiegare cosa è fallito e chiedere conferma su come procedere (correggere o fare rollback dello step).

## Regole per tipo di intervento
- **Restyling**: usare le skill `stile` e `design`. I **contenuti restano invariati**: cambia la forma, non il testo.
- **Migrazione**: produrre la tabella delle **URL vecchie e nuove**, impostare i **redirect 301** e preservare i metadati SEO (title, description, canonical, dati strutturati, sitemap, `robots.txt`).
- **Qualità del codice**: l'aspetto **non deve cambiare**. Verificare confrontando con gli screenshot di riferimento dopo ogni step.
- **Nuove funzioni**: rispettare i criteri di accettazione di `contesto/specifiche.md`; niente funzioni non concordate.

## Regole generali
- Lavorare **sempre** sul branch `refactoring`. Il merge su `main` lo fa l'utente.
- Niente `git push`, salvo richiesta esplicita.
- Aggiornare `contesto/stato.md` alla fine di ogni fase.
- Non toccare dati di produzione né database live senza un backup verificato.
