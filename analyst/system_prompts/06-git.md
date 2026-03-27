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

- Yeni branch **kesinlikle oluşturulmaz.**
- Tüm incelemeler doğrudan `main` branch üzerinde yapılır.

## Commit / Push

- Commit ve push **kesinlikle yapılmaz.**
