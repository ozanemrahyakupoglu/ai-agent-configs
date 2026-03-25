# Rule: Commit / Push

## Kurallar

- Her mantıksal adım için ayrı commit atılır.
- Commit mesajı formatına uyulur: `<type>(<scope>): <kısa açıklama>`
- Tüm geliştirme tamamlandıktan sonra aşağıdaki Git akışı izlenir:

## Git Akışı

1. Feature branch'teki değişiklikler commit edilir ve push'lanır.
2. `agent` branch'ine geçilir.
3. `agent` branch'i pull alınır.
4. Feature branch `agent` branch'ine merge edilir.
5. `agent` branch'i push'lanır.
