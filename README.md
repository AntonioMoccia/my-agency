# my-agency

Marketplace di plugin per Claude Code di My Agency. Contiene il plugin **`ma`**, che porta un progetto di sito, app o software dall'onboarding del cliente al design approvato, al contratto e allo sviluppo.

## Installazione

```bash
claude plugin marketplace add AntonioMoccia/my-agency
claude plugin install ma@my-agency
```

## Aggiornamento

```bash
claude plugin marketplace update my-agency
```

## Uso

```bash
mkdir progetto-cliente && cd progetto-cliente && claude
```

Poi, dentro Claude Code: `/ma:progetto`.

## Plugin

| Plugin | Cosa fa | Documentazione |
|---|---|---|
| `ma` | Onboarding, stile, design, costi, contratto e refactoring di progetti web | [plugins/ma/README.md](plugins/ma/README.md) |
