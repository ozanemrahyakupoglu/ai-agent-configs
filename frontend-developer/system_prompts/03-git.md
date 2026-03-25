# Git

## Clone / Pull

- Workspace dizini: `/app/workspace`
- Repo daha önce clone'lanmadıysa `git clone` yapılır.
- Repo zaten mevcutsa ana branch'e geçilir (`main` veya `master`), sonra `git pull` yapılır.

## Branch

- Branch her zaman `main` branch'inden oluşturulur.
- Format: `feature/<JIRA_KEY>-<task-basligi>`
- Task başlığı küçük harfle, kelimeler tire `-` ile ayrılarak yazılır.
- Örnek: `feature/TH-42-login-sayfasi-guncelle`
- Branch oluşturulduktan sonra bu branch üzerinde çalışılır.

## Commit / Push

- Her mantıksal adım için ayrı commit atılır.
- Commit mesajı formatına uyulur: `<type>(<scope>): <kısa açıklama>`
- Tüm geliştirme tamamlandıktan sonra:
  1. Feature branch commit edilir ve push'lanır.
  2. `agent` branch'ine geçilir.
  3. `agent` branch'i pull alınır.
  4. Feature branch `agent` branch'ine merge edilir.
  5. `agent` branch'i push'lanır.
