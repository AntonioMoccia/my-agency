# ma — Guida all'uso

Il plugin `ma` ("My Agency") trasforma Claude Code nella procedura operativa di un'agenzia
web: fa l'onboarding del cliente, fissa la direzione visiva, propone design costruiti su
riferimenti reali e premiati, calcola i costi dei servizi, prepara il contratto e porta
avanti lo sviluppo — tenendo scritto a che punto è il progetto.

Versione inglese: [USAGE.en.md](USAGE.en.md)

---

## 1. Installazione

```bash
claude plugin marketplace add AntonioMoccia/my-agency
claude plugin install ma@my-agency
```

Per aggiornare, in seguito:

```bash
claude plugin marketplace update my-agency
```

### Opzionale: il clone locale
Il plugin installato vive in una cache in sola lettura. Per far sì che il plugin
**ricordi le tue preferenze fra progetti diversi**, clona questo repository e indica il
percorso una volta sola in `~/.claude/ma.json`:

```json
{ "repo": "/percorso/assoluto/my-agency" }
```

Senza clone tutto funziona comunque: le preferenze restano dentro il progetto corrente.

---

## 2. Avviare un progetto

```bash
mkdir progetto-cliente && cd progetto-cliente && claude
```

Poi, dentro Claude Code:

```
/ma:project
```

In una cartella vuota parte l'onboarding: copia il template, esegue `git init` e chiede
tre cose — **nome del progetto**, **modalità** e **lingua**. Da lì ogni fase si chiude con
un commit (`ma: <fase>`) nel repository del progetto.

Per riprendere un progetto, dalla sua cartella:

| Vuoi | Comando |
|---|---|
| Andare avanti | `/ma:project` |
| Solo vedere a che punto sei | `/ma:status` |
| Eseguire una fase precisa | `/ma:style`, `/ma:design`, `/ma:costs`, … |

---

## 3. Le tre modalità

La modalità si sceglie una volta in onboarding e decide l'ordine delle fasi.

| Modalità | Quando usarla | Ordine delle fasi |
|---|---|---|
| **project** | Il cliente è acquisito, fai il lavoro completo | setup → discovery → style → costs → contract → design |
| **pitch** | Stai cercando di acquisire il cliente | setup → discovery → style → design (1 proposta leggera) → costs → contract |
| **refactoring** | Esiste già un sito, un'app o un software | setup → discovery → acquisition → audit → specs → costs → contract → plan → execution |

Perché in **project** il design è ultimo: è la fase più costosa, quindi viene dopo un
contratto firmato. In **pitch** l'ordine è invertito di proposito — una proposta leggera,
solo l'hero, per vincere il lavoro.

Puoi saltare o rifare una fase in qualsiasi momento: `ma` la segna `skipped` o
`in progress` e scrive il motivo in `context/decisions.md`.

---

## 4. Lingua

I file del plugin sono in inglese. Ciò che il plugin **dice a te e scrive per il cliente**
segue la **lingua del progetto**:

1. il campo `Language` in `context/state.md`, chiesto una volta in onboarding;
2. altrimenti la preferenza `language` nel registro;
3. altrimenti **italiano**.

Vale per le risposte, la discovery, il questionario al cliente, il briefing di stile, i
testi del design, la tabella dei costi e il contratto. I nomi di cartelle e file restano
in inglese in ogni caso.

---

## 5. I comandi

| Comando | Fase | Produce |
|---|---|---|
| `/ma:project` | qualsiasi | Esegue la fase successiva |
| `/ma:onboarding` | setup, discovery | `context/state.md`, `context/discovery.md` |
| `/ma:status` | — | Niente: sola lettura |
| `/ma:questionnaire` | qualsiasi | `context/questionnaire.md` + un modulo compilabile |
| `/ma:style` | style | `context/style.md`, `context/inspiration.md` |
| `/ma:design` | design | `design/proposals/vN/`, `resources/resources.md` |
| `/ma:costs` | costs | `context/costs.md` |
| `/ma:contract` | contract | `contract/draft.md` |
| `/ma:refactoring` | acquisition → execution | `context/source.md`, `audit.md`, `specs.md`, `plan.md` |
| `/ma:skill` | — | Voci in `registry/skills.md` |

Raramente serve chiamarli per nome: `/ma:project` sceglie quello giusto leggendo lo stato.

---

## 6. Fase per fase

### Onboarding — setup e discovery
Copia il template (senza sovrascrivere niente), inizializza Git e conduce la discovery in
9 gruppi: attività, obiettivo, pubblico, mercato, tipologia, funzioni, contenuti, vincoli,
esistente. Al massimo 4 domande per volta, a scelta multipla dove le opzioni si conoscono.

Prima di cominciare propone tre strade:

| Strada | Quando |
|---|---|
| **Dal vivo** | Conosci le risposte, o il cliente è in chiamata |
| **Questionario** | Le risposte sono del cliente, e il cliente non c'è |
| **Mista** | Rispondi tu a ciò che sai, il cliente compila il resto |

### Style — direzione visiva, più i riferimenti automatici
Raccoglie logo e file del brand, i riferimenti del cliente, 3–5 parole chiave, cosa
evitare e i vincoli rigidi. Poi **raccoglie i riferimenti in automatico** — vedi la
sezione 7.

Output: `context/style.md` (direzione in una frase, parole chiave, vincoli, una riga
cosa-prendere / cosa-non-prendere per ogni riferimento) e `context/inspiration.md`.

### Design — proposte, selezione, iterazione
Aggiorna i riferimenti, poi genera **2–3 direzioni realmente diverse** — non tre varianti
della stessa idea. Ognuna porta un nome, l'idea in una frase, 1–3 riferimenti citati con
il principio preso da ciascuno, la palette con il ruolo di ogni colore, una coppia di font
open source, la griglia, 3–5 animazioni chiave ognuna col fallback `prefers-reduced-motion`,
e la home in desktop **e** mobile.

Ogni proposta passa una checklist di qualità prima che tu la veda: gerarchia, contrasto
WCAG AA su ogni coppia, coerenza mobile, una sola idea forte per pagina, performance delle
animazioni, fedeltà al briefing.

Dove viene prodotto il design, primo disponibile: artifact type Design → Figma → pagina
HTML statica in `design/proposals/vN/`.

Poi scegli una proposta, più di una, o **parti di ognuna** ("palette della A, tipografia
della B, hero della C") — sempre col motivo. `vN+1` è la sintesi di quelle scelte, non un
nuovo giro di proposte. Se un intero giro viene bocciato, i riferimenti vengono aggiornati
prima: la stessa ispirazione produrrebbe le stesse proposte.

### Costs — stack e costi dei servizi
Propone lo stack (framework, hosting, CMS, ecommerce, email transazionali, analytics,
cookie, dominio) con una riga di motivo per ogni scelta legata alla discovery, poi
**verifica ogni prezzo online al momento** — citando fonte e data, mai a memoria. Un
prezzo non verificabile viene scritto `to verify`, non inventato.

Output: una tabella con costo una tantum e mensile, un'alternativa più economica col suo
trade-off, il totale annuo e il verdetto sul budget: `within`, `at the limit`, `over`.
Fuori budget significa che viene proposto uno stack alternativo completo, dicendo cosa si
perde.

Non stima mai il tuo lavoro: giornate e prezzo del progetto stanno nel contratto.

### Contract — la bozza
Compila un modello completo da discovery, costi e decisioni: parti, oggetto, deliverable,
esclusioni, milestone, giri di revisione, pagamenti per milestone, intestazioni degli
account, proprietà a saldo, responsabilità sui contenuti, manutenzione opzionale, recesso.

Due regole che non piega:
- i dati mancanti restano `[TO COMPLETE: …]` — nessuna P.IVA, cifra o data inventata;
- la bozza porta sempre l'avviso di farla verificare da un legale o da un commercialista.

### Refactoring — un progetto esistente
Cinque fasi, un commit ciascuna: **acquisition** (repo, cartella o solo URL; viene creato
il branch `refactoring`), **audit** (checklist di 20 voci, da dipendenze e segreti fino a
Lighthouse, Core Web Vitals, SEO e accessibilità), **specs** (cosa non deve cambiare,
criteri di accettazione), **plan** (step piccoli, ognuno con controllo, rischio e
rollback), **execution** (uno step → build → test → controllo → commit).

Se non ci sono test, scrive test di caratterizzazione o prende screenshot di riferimento
prima di toccare qualsiasi cosa. Un controllo fallito ferma tutto: non passa allo step
successivo da solo.

---

## 7. Riferimenti automatici (Awwwards)

Ogni volta che sta per produrre una proposta di design, `ma` va a vedere com'è fatto il
lavoro buono in quel settore in questo momento. Non devi chiederglielo.

**Come costruisce le query.** Settore, tipologia e pubblico vengono dalla discovery;
parole chiave e cosa-evitare dal briefing di stile. Da lì costruisce 2–4 query: una per
categoria, una o due per tag (mappati dalle tue parole chiave: "essenziale" → `ui-design`,
"immersivo" → `webgl`, "editoriale" → `typography`, e così via), e una per i premi
dell'anno corrente, per freschezza.

**Dove guarda.** Awwwards per primo — categorie (`e-commerce`, `architecture`, `fashion`,
`portfolio`, …), tag (`animation`, `scrolling`, `3d`, `webgl`, …) e premi
(`sites_of_the_day`, `sites_of_the_year`, …). Se da lì escono meno di 6 riferimenti
utilizzabili, passa a Godly, SiteInspire, Land-book, Lapa, Httpster, Mobbin.

**Come li recupera.** WebFetch → WebSearch → gli strumenti del browser Chrome per le
pagine renderizzate in JavaScript → chiedere i link a te. Meno di 3 riferimenti
utilizzabili viene detto in una riga e non blocca la fase.

**Cosa ottieni.** `context/inspiration.md`, con una riga per riferimento: fonte, data in
cui è stato visto, settore o tag, **cosa prendere** come principio concreto e cosa non
prendere. Da 3 a 12 righe, almeno 2 dal settore del cliente e almeno 2 da fuori — è il
secondo vincolo che tiene la proposta lontana dal cliché di settore. I tuoi riferimenti
restano nella tabella e non vengono mai sostituiti da quelli automatici.

**Come vengono usati.** Ogni proposta di design cita 1–3 righe e il principio preso da
ciascuna, e due proposte non possono citare lo stesso principio dallo stesso riferimento.
L'aggiornamento scatta quando il file ha più di 30 giorni o quando un giro è stato bocciato.

**I limiti, applicati.** Solo principi, mai asset: nessun layout identico, nessun logo,
testo o immagine preso in prestito, nessuna foto di persone reali dal web, mai la promessa
di un risultato "come" un riferimento. Solo pagine pubbliche, nessuno scraping massivo,
niente dietro login. Gli screenshot sono materiale di lavoro: non vanno al cliente e non
finiscono mai in `site/`.

---

## 8. Il questionario al cliente

Scritto da `ma`, compilato dal cliente, riportato dentro il progetto. Da usare ogni volta
che le risposte sono del cliente e il cliente non è in chiamata.

```
/ma:questionnaire                  # sceglie il set dalla fase corrente
/ma:questionnaire discovery        # un set specifico
/ma:questionnaire collect          # rilegge le risposte
/ma:questionnaire status           # cosa è stato mandato, cosa è tornato
```

### I set

| Set | Fase | Raccoglie |
|---|---|---|
| `discovery` | discovery | Attività, obiettivo, pubblico, mercato, tipologia, funzioni, contenuti, vincoli |
| `brand` | style | Logo, brand, gusto visivo, cosa evitare |
| `content` | design, execution | Testi, foto, video, dati societari, chi fornisce cosa ed entro quando |
| `ecommerce` | discovery, specs | Catalogo, pagamenti, spedizioni, fatturazione, resi |
| `app` | discovery, specs | Utenti, ruoli, dati, integrazioni, ambienti |
| `existing` | acquisition | Cosa è online oggi, chi lo amministra, dov'è ospitato |
| `admin` | contract | Dati di fatturazione, chi firma, chi approva |

### Come funziona
1. **Toglie ciò che si sa già.** Tutto ciò a cui `context/` o le preferenze hanno già
   risposto non viene richiesto, e ti dice quante domande ha tagliato.
2. **Tipizza ogni domanda** — breve, lunga, scelta singola, multipla, numero, sì/no, file,
   link — la segna obbligatoria o opzionale e scrive una riga di aiuto che spiega perché
   la si chiede. Il gergo viene tradotto: non "vuoi un CMS headless?" ma "vuoi aggiornare
   i testi da solo, senza chiamarci?".
3. **Lo pubblica**, primo disponibile: una pagina Artifact compilabile che memorizza le
   risposte (con avanzamento, salva-e-riprendi, obbligatorie segnate) → un documento o
   servizio di form collegato → `context/questionnaire.md` in Markdown da mandare per
   email.
4. **Scrive il messaggio al cliente**: a cosa serve, il link, quanto tempo richiede, la
   scadenza e cosa blocca. Lo mandi tu — `ma` non manda niente da solo, se non glielo
   chiedi.
5. **Lo traccia**: il questionario finisce in **Waiting on** in `context/state.md` con la
   data, e la fase resta `in progress`.
6. **Raccoglie e unisce**: una tabella di stato (risposto / parziale / mancante), poi le
   risposte vengono scritte nel file giusto — discovery, stile, resources, source o i
   segnaposto del contratto — ognuna con fonte e data.

### Le protezioni
- **Massimo 20 domande.** Oltre, lo spezza in due giri: un muro di domande torna vuoto.
- **Mai credenziali.** Nessuna password, chiave API o dato di carta. Per gli accessi
  chiede *quali* account esistono e chi li amministra; le credenziali passano da un
  password manager o da un canale che scegli tu, mai dal modulo e mai in un file.
- **Nessuna sovrascrittura silenziosa.** Se il cliente contraddice qualcosa già in
  `context/`, restano entrambe le versioni e ti viene chiesto quale vince.
- **Una risposta vuota resta vuota.** Non viene riempita con un'ipotesi plausibile.
- Le domande obbligatorie restano sotto la metà dell'elenco, così un cliente che risponde
  solo a quelle ha già sbloccato la fase.

---

## 9. Cosa finisce nella cartella del progetto

```text
progetto-cliente/
├── CLAUDE.md                  istruzioni per Claude in questo progetto
├── onboarding.md              le risposte del setup a colpo d'occhio
├── context/
│   ├── state.md               fasi, fase corrente, in attesa, prossimo passo
│   ├── discovery.md           i 9 gruppi della discovery
│   ├── style.md               direzione, parole chiave, vincoli, riferimenti
│   ├── inspiration.md         i riferimenti raccolti e i loro principi
│   ├── decisions.md           ogni scelta: data, fase, decisione, motivo
│   ├── costs.md               stack, prezzi con le fonti, verdetto sul budget
│   ├── questionnaire.md       questionario inviato e risposte grezze ricevute
│   └── source.md / audit.md / specs.md / plan.md     (solo refactoring)
├── references/                logo, manuale brand, screenshot dei riferimenti
├── resources/                 resources.md + immagini, testi, video
├── design/proposals/vN/       le proposte e il design approvato
├── contract/draft.md          la bozza di contratto
├── instructions/              come configurare i servizi esterni
└── site/                      il codice
```

`context/state.md` è la fonte di verità. Se devi leggere un solo file per sapere a che
punto è un progetto, leggi quello.

---

## 10. Memoria fra progetti

`registry/` nel plugin tiene ciò che deve sopravvivere al singolo progetto:

- **`preferences.md`** — ambiti `stack`, `services`, `design`, `contract`, `mode`,
  `communication`, `language`. Una preferenza si salva solo se la esprimi come regola
  ("usa sempre Next.js") o se confermi la proposta di ricordarla.
- **`skills.md`** — skill di terze parti valutate: `approved`, `rejected`, `link-only`,
  ognuna con le fasi in cui va caricata.

I dati del cliente non entrano mai lì — nomi, contatti, budget, contenuti e credenziali
restano nella cartella del progetto. Una scelta valida per un solo progetto resta in
`context/decisions.md`.

Scrivere nel registro richiede il clone locale (sezione 1); il plugin fa commit e push sul
repo del plugin, poi esegui `claude plugin marketplace update my-agency` per vedere la
modifica nel plugin installato.

### Skill di terze parti
`/ma:skill find <esigenza>` controlla prima il registro, poi cerca — repository ufficiali
Anthropic prima delle liste curate — e propone al massimo 3 candidate. Di quella che
scegli legge **ogni** file, ti mostra il contenuto integrale di ogni script e applica una
checklist di sicurezza a 6 voci (istruzioni per ignorare le regole, dati inviati a URL
esterni, accesso alle credenziali, esecuzione di codice remoto, comandi distruttivi,
offuscamento). Basta un riscontro per scartarla. Niente viene installato senza la tua
approvazione esplicita, e una skill la cui licenza non permette la copia viene registrata
come `link-only` invece di essere copiata dentro.

---

## 11. Risoluzione dei problemi

| Sintomo | Causa e rimedio |
|---|---|
| `/ma:project` avvia un nuovo onboarding in un progetto esistente | `context/state.md` manca o è stato spostato. Ripristinalo, o esegui `/ma:onboarding` e lascia che ricostruisca lo stato |
| "La cartella contiene già un progetto diverso" | C'è codice ma non `context/`. Rispondi all'unica domanda che fa: qui, o in una nuova sottocartella |
| La skill design si rifiuta di partire | Manca `context/discovery.md` o `context/style.md`. Esegui prima `/ma:onboarding` o `/ma:style` |
| Avvisa che il contratto non è chiuso | Normale in modalità project: il design viene dopo il contratto. Confermi e procede |
| Raccolti meno di 3 riferimenti | Awwwards non ha dato niente di utile per quelle query. Prosegue comunque; dagli 3–5 link tu, o ammorbidisci "cosa evitare" |
| Un prezzo è segnato `to verify` | Il fornitore non lo pubblica (preventivo su richiesta, prezzo a volume). Non verrà inventato: chiedilo al fornitore |
| Il commit a fine fase fallisce | Identità Git non configurata. Esegui `git config user.name` e `git config user.email`; la fase non è bloccata |
| Le preferenze non vengono ricordate fra progetti | `~/.claude/ma.json` manca o punta al percorso sbagliato. Deve contenere `plugins/ma/registry/` |
| Una modifica al registro non si vede nel plugin | Esegui `claude plugin marketplace update my-agency` |
| Il questionario è tornato mezzo vuoto | Normale. Inseguine solo le domande **obbligatorie** che ti elenca; per il resto manda un secondo giro breve |

---

## 12. Convenzioni che vale la pena conoscere

- **Un solo prossimo passo.** Ogni risposta finisce con uno, così sai sempre cosa succede dopo.
- **Mai chiesto due volte.** Prima di ogni domanda `ma` controlla `context/`, poi le
  preferenze, poi il registro delle skill. Ciò che trova lo conferma in una riga invece di
  richiederlo.
- **Ogni scelta è scritta.** `context/decisions.md` registra data, fase, decisione e
  motivo — ed è quello che rende un progetto ripartibile tre settimane dopo.
- **Un commit per fase.** `ma: setup`, `ma: discovery`, `ma: style`, `ma: design vN`,
  `ma: step N`. Nessun `git push` se non lo chiedi.
- **Dai riferimenti si prendono principi, mai asset.** Vale in style, design e refactoring.
- **Le credenziali non entrano mai in un file.** Non nel questionario, non in `source.md`,
  non nel contratto.
