# Git

## Bağlantı Bilgileri

| Alan | Değer | Açıklama |
|------|-------|----------|
| Workspace | `/app/workspace` | Tüm projeler bu dizin altına clone'lanır |
| Ana Proje | `$MAIN_PROJECT` | Proje adı; tam yolu `/app/workspace/$MAIN_PROJECT` (`MAIN_PROJECT` env) |
| Ana Proje Git URL | `$MAIN_PROJECT_GIT_URL` | Ana projenin clone URL'i (`MAIN_PROJECT_GIT_URL` env) |
| İlgili Projeler | `$RELATED_PROJECTS` | Proje adları `,` ile ayrılır, ör. `backend,mobile-api` (`RELATED_PROJECTS` env) |
| İlgili Projeler Git URL | `$RELATED_PROJECTS_GIT_URLS` | `$RELATED_PROJECTS` ile aynı sırada `,` ile ayrılmış Git URL'leri (`RELATED_PROJECTS_GIT_URLS` env) |
| Git Token | `$GITHUB_TOKEN` | GitHub erişim token'ı (`GITHUB_TOKEN` env) |

## Clone / Pull

- Workspace dizini: `/app/workspace`
- Repo daha önce clone'lanmadıysa `git clone` yapılır.
- Repo zaten mevcutsa `main` branch'e geçilir, sonra `git pull` yapılır.
- Bu adım `$MAIN_PROJECT` ve `$RELATED_PROJECTS` kapsamındaki tüm projeler için geçerlidir.

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
  2. `main` branch'ine geçilir.
  3. `main` branch'i pull alınır.
  4. Feature branch `main` branch'ine merge edilir.
  5. `main` branch'i push'lanır.
