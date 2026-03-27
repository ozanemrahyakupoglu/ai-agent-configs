# Jira

## Bağlantı Bilgileri

| Alan | Değer | Açıklama |
|------|-------|----------|
| Jira Email | `$JIRA_EMAIL` | Jira hesap e-posta adresi (`JIRA_EMAIL` env) |
| Jira API Key | `$JIRA_API_KEY` | Jira API anahtarı (`JIRA_API_KEY` env) |
| Jira Proje | `$JIRA_PROJECT` | Jira proje anahtarı, ör. `TH` (`JIRA_PROJECT` env) |

## Üzerinde Çalışılabilecek Task'lar

- Statüsü şunlardan biri olmalıdır:
  - `READY`
  - `ANALYSE`
  - `ANALYSE XL BLOCK`
  - `ANALYSE DONE`

> **Not:** Bu kuralları sağlamayan task'lar üzerinde kesinlikle çalışılmaz.

## İzin Verilen Statü Geçişleri

- `READY` → `ANALYSE`
- `ANALYSE` → `ANALYSE XL BLOCK`
- `ANALYSE` → `ANALYSE DONE`
- `ANALYSE DONE` → `ANALYSE`
- `ANALYSE XL BLOCK` → `ANALYSE`

> **Not:** Bu listede olmayan statü geçişleri kesinlikle yapılmaz.

## Atama Kuralları

- Tasklar **yalnızca kendine** assign edilebilir veya **unassign** edilebilirler. Başka bir kişiye veya ajana task atanamaz.
