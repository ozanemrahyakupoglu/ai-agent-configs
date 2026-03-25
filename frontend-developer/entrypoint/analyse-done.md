# Entrypoint: Analyse Done

Bu entrypoint, `ANALYSE DONE` statüsündeki bir task ile tetiklenir.

## Workflow

```
Task → DEVELOPMENT
    ↓
DEVELOPMENT Akışını Koştur
```

## Adımlar

### 1. Task → DEVELOPMENT
Task statüsü **DEVELOPMENT** olarak güncellenir.

### 2. DEVELOPMENT Akışını Koştur
`entrypoint/development.md` akışı baştan koşturulur.
