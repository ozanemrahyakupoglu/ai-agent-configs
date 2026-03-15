# Manifest: TENANT_HUB_DEVELOPER
Bu dosya Developer ajanının giriş noktasıdır.
Ajan çalışmaya başladığında ilk bu dosyayı okur ve
buradan diğer tüm kaynaklara yönlendirilir.

## System Prompt Dosyaları
| Dosya | Açıklama | Yükleme |
|-------|----------|---------|
| `01-role.md` | Ajanın kimliği, uzmanlık alanları ve çalışma prensipleri | **always** |
| `02-workflow.md` | Task alma, geliştirme ve teslim iş akışı | **always** |

## Repo Yönetimi
Tüm repolar **startup workflow'da bir kez** `/app/workspace` altına clone'lanır ve buradan yönetilir.

- Repo yoksa: `git clone`
- Repo varsa: `git pull` ile güncelle

Her session başında, ilk işlem olarak tüm repolar `git pull` ile güncellenir.

## Proje Bağlamı
Geliştirmeye başlamadan önce ilgili context dosyalarını lokal clone'dan oku:

| Repo | Bileşen(ler) | Dosya | Yükleme |
|------|-------------|-------|---------|
| `tenant-hub` | Genel proje bağlamı | `/app/workspace/tenant-hub/project-context.md` | **always** |
| `tenant-hub-service` | `[BE]` Backend, `[DB]` Database | `/app/workspace/tenant-hub-service/project-context.md` | on-demand: ilgili bileşen etkilendiğinde |
| `tenant-hub-web` | `[WEB]` Web Frontend | `/app/workspace/tenant-hub-web/project-context.md` | on-demand: ilgili bileşen etkilendiğinde |
| `tenant-hub-mobile` | `[MOB]` Mobile | `/app/workspace/tenant-hub-mobile/project-context.md` | on-demand: ilgili bileşen etkilendiğinde |

## Konfigürasyon

| Alan | Değer |
|------|-------|
| Git URL | `https://github.com/tenant-hub` |
| Jira URL | `https://ozanemrahyakupoglu.atlassian.net` |
| Jira Email | `ozanemrah.yakupoglu@gmail.com` |
| Jira Project | `TH` |
| Jira API Key | `$JIRA_API_KEY` (env) |
