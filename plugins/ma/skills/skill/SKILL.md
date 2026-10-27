---
name: skill
description: Cerca, valuta, installa, elenca e rimuove skill di terze parti nel plugin ma, tenendo un registro di quelle approvate e scartate e applicando una checklist di sicurezza prima di ogni installazione. Da usare quando l'utente dice "cerca una skill per...", "aggiungi questa skill", "quali skill abbiamo", "rimuovi la skill", "serve qualcosa per le animazioni".
---

# Skill — autoalimentazione del plugin

Leggere prima `${CLAUDE_PLUGIN_ROOT}/riferimenti/convenzioni.md` e `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`. I criteri di valutazione e la checklist di sicurezza sono in `references/valutazione.md`: applicarli sempre.

Azioni: `cerca <esigenza>` · `aggiungi <link o percorso>` · `elenca` · `rimuovi <nome>`.

---

## cerca `<esigenza>`

1. **Prima il registro.** Leggere `registro/skills.md`. Se esiste già una skill `approvata` o `scartata` per quell'esigenza, dirlo in una riga (con il motivo se scartata) e **fermarsi**, salvo che l'utente chieda esplicitamente alternative.
2. **Cercare sul web** nelle fonti di `references/valutazione.md`, partendo dalle ufficiali e scendendo di priorità.
3. **Proporre al massimo 3 candidate** in tabella:

| Nome | Fonte | Licenza | Popolarità | Ultimo aggiornamento | Cosa fa | Script inclusi |
|---|---|---|---|---|---|---|

   Popolarità = stelle o installazioni. "Script inclusi" = sì/no.
4. **Per la candidata scelta dall'utente**: scaricarla in una cartella temporanea, leggerla **per intero** (ogni file, non solo il `SKILL.md`) e applicare la checklist di sicurezza.
5. **Mostrare**: riassunto di cosa fa e cosa modifica, e **il contenuto integrale di ogni script** incluso. Poi chiedere l'approvazione esplicita. Senza approvazione non si installa niente.

## aggiungi `<link o percorso>`

Stessa valutazione e stessa approvazione della `cerca`, partendo dal link, file o cartella forniti dall'utente. Il passo 1 (controllo del registro) serve comunque, per non duplicare una skill già presente.

## Installazione (solo dopo approvazione)

Scrivere nel **clone locale** del repo, come indicato in `memoria.md`.

**Licenza compatibile con la copia** (MIT, Apache-2.0, BSD, ISC e simili):
1. Copiare in `<repo>/plugins/ma/skills/<nome>/`.
2. Aggiungere `<repo>/plugins/ma/skills/<nome>/FONTE.md` con: url, autore, licenza, versione o commit, data di acquisizione.
3. Se il `name` del frontmatter va in conflitto con una skill esistente, adattarlo (es. `gsap-anim` invece di `anim`) e annotarlo in `FONTE.md`.

**Licenza assente o incompatibile** (nessuna licenza, GPL quando non compatibile, "all rights reserved", solo uso personale):
- **non copiare niente**;
- registrare la skill con stato `solo-link`, così resta consultabile come riferimento senza finire nel plugin.

**In entrambi i casi:**
1. Aggiornare `registro/skills.md` compilando **"Quando usarla"** (una frase concreta) e **"Fasi"** (le fasi in cui va caricata: setup, discovery, stile, costi, contratto, design, acquisizione, audit, specifiche, piano, esecuzione).
2. Alzare la **versione patch** del plugin in `plugins/ma/.claude-plugin/plugin.json` (es. 0.3.0 → 0.3.1).
3. Commit e push secondo `memoria.md`, con messaggio `ma: registro skill <nome>`.
4. Suggerire `claude plugin marketplace update my-agency`.

**Se la skill viene scartata**: registrarla con stato `scartata` e il motivo in "Quando usarla" (es. "scartata: script che invia dati a URL esterno"). Serve a non riproporla la prossima volta. Commit e push come sopra.

## elenca

Mostrare `registro/skills.md` in tabella, raggruppato per stato (`approvata`, `solo-link`, `scartata`). Aggiungere una riga di conteggio. Nessuna modifica ai file.

## rimuovi `<nome>`

1. Chiedere conferma, mostrando la riga del registro.
2. Eliminare `<repo>/plugins/ma/skills/<nome>/` nel clone locale.
3. Togliere la voce da `registro/skills.md`, oppure spostarla a `scartata` col motivo se l'utente vuole ricordare la scelta.
4. Alzare la versione patch, commit e push secondo `memoria.md`.

## Regole

- Nessuna installazione, copia o push senza approvazione esplicita dell'utente.
- Leggere **ogni** file di una skill prima di approvarla: le istruzioni possono nascondersi nei `references/`.
- Basta **un solo** elemento della checklist di sicurezza per scartare la skill o chiedere conferma esplicita mostrando il punto esatto del file.
- Non installare mai direttamente nella cache del plugin: è in sola lettura.
