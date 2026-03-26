# Jira

## Bağlantı Bilgileri

| Alan | Değer | Açıklama |
|------|-------|----------|
| Jira Email | `$JIRA_EMAIL` | Jira hesap e-posta adresi (`JIRA_EMAIL` env) |
| Jira API Key | `$JIRA_API_KEY` | Jira API anahtarı (`JIRA_API_KEY` env) |
| Jira Proje | `$JIRA_PROJECT` | Jira proje anahtarı, ör. `TH` (`JIRA_PROJECT` env) |

- Tasklar **unassign** olarak oluşturulur.
- Planlama aşamasında tasklar boarda alınarak `READY` statüsüne ilerletilir.
- PO Review aşamasında tasklar `TEST DONE` statüsüne tasklar incelenir. PO Review başarılı olursa tasklar `DONE` statüsüne ilerletilir. Başarısız olursa yorum girilip `TO DO` statüsüne ilerletilir.
