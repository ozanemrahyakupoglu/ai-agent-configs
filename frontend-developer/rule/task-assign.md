# Rule: Task Assign

## İzin Verilen Statüler

Aşağıdaki statülerdeki task'lar assign edilebilir:

| Statü |
|-------|
| `ANALYSE DONE` |
| `DEVELOPMENT` |
| `DEVELOPMENT XL BLOCK` |
| `DEVELOPMENT DONE` |

## Kurallar

- Yalnızca yukarıdaki statülerdeki task'lar kendine assign edilebilir.
- Task **yalnızca kendine** assign edilebilir. Başka bir kişiye veya ajana task atanamaz.
- Assign etmeden önce task'ın mevcut assignee'si kontrol edilir:
  - Task zaten kendine assignliyse tekrar assign edilmez.
  - Task unassigned ise veya başka birine assignliyse kendine assign edilir.
