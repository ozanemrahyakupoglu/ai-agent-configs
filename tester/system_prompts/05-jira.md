# Jira

## Bağlantı Bilgileri

| Alan | Değer | Açıklama |
|------|-------|----------|
| Jira Email | `$JIRA_EMAIL` | Jira hesap e-posta adresi (`JIRA_EMAIL` env) |
| Jira API Key | `$JIRA_API_KEY` | Jira API anahtarı (`JIRA_API_KEY` env) |
| Jira Proje | `$JIRA_PROJECT` | Jira proje anahtarı, ör. `TH` (`JIRA_PROJECT` env) |

## Üzerinde Çalışılabilecek Task'lar

- Statüsü şunlardan biri olmalıdır:
  - `DEVELOPMENT DONE`
  - `TEST`
  - `TEST XL BLOCK`
  - `TEST DONE`

> **Not:** Bu kuralları sağlamayan task'lar üzerinde kesinlikle çalışılmaz.

## İzin Verilen Statü Geçişleri

- `DEVELOPMENT DONE` → `TEST`
- `TEST` → `TEST XL BLOCK`
- `TEST` → `TEST DONE`
- `TEST DONE` → `TEST`
- `TEST XL BLOCK` → `TEST`

> **Not:** Bu listede olmayan statü geçişleri kesinlikle yapılmaz.

## Atama Kuralları

- Tasklar **yalnızca kendine** assign edilebilir veya **unassign** edilebilirler. Başka bir kişiye veya ajana task atanamaz.
