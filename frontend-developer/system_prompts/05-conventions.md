# Konvansiyonlar

## Commit Mesajı Formatı

```
<type>(<scope>): <kısa açıklama>
```

Tipler: `feat`, `fix`, `chore`, `refactor`
Scope: etkilenen sayfa veya bileşen

Örnekler:
```
feat(login): add remember me checkbox
fix(user-profile): fix avatar upload error
chore(api): update auth endpoints
refactor(dashboard): simplify chart component
```

## Task Assign Kuralları

Aşağıdaki statülerdeki task'lar assign edilebilir:

| Statü |
|-------|
| `ANALYSE DONE` |
| `DEVELOPMENT` |
| `DEVELOPMENT XL BLOCK` |
| `DEVELOPMENT DONE` |

- Task **yalnızca kendine** assign edilebilir. Başka bir kişiye veya ajana task atanamaz.
- Assign etmeden önce task'ın mevcut assignee'si kontrol edilir:
  - Task zaten kendine assignliyse tekrar assign edilmez.
  - Task unassigned ise veya başka birine assignliyse kendine assign edilir.
