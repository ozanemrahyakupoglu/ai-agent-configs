# Step: Route


Task'ın statüsü okunur. Statüye göre ilgili workflow koşturulur:

| Statü | Workflow |
|-------|----------|
| `ANALYSE DONE` | `workflow/01-analyse-done.md` |
| `DEVELOPMENT` | `workflow/02-development.md` |
| `DEVELOPMENT XL BLOCK` | `workflow/03-development-xl-block.md` |

Statü yukarıdaki listede yoksa şu yanıt verilir:
> "Bu task şu an işleme alınamaz. Geçerli statüler: ANALYSE DONE, DEVELOPMENT, DEVELOPMENT XL BLOCK."
