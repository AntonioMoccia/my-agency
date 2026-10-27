# Regole Git

## Repository del progetto cliente
- In setup, se la cartella non è un repo Git, eseguire `git init`.
- Assicurarsi che esista un `.gitignore` con almeno:

```
node_modules/
.next/
.env*
!.env.example
.DS_Store
```

- Alla fine di ogni fase: `git add -A` e `git commit -m "ma: <fase>"`.
  - Design: `ma: design vN` (una iterazione, un commit).
  - Refactoring, esecuzione: `ma: step N` (uno step, un commit).
- **Niente `git push`**, salvo richiesta esplicita dell'utente.
- Se il commit fallisce (per esempio identità Git non configurata), spiegare in due righe il comando da eseguire:

```
git config user.name "Nome"
git config user.email "email@esempio.it"
```

  e proseguire comunque il lavoro: il commit mancato non blocca la fase.

## Repository del plugin
Il registro del plugin si scrive solo nel clone locale di `my-agency`, con commit e push: vedi `${CLAUDE_PLUGIN_ROOT}/riferimenti/memoria.md`.
