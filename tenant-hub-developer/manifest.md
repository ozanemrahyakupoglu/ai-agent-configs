# Manifest: TENANT_HUB_DEVELOPER
Bu dosya Developer ajanının giriş noktasıdır.
Ajan çalışmaya başladığında ilk bu dosyayı okur ve
buradan diğer tüm kaynaklara yönlendirilir.

## System Prompt Dosyaları
Dosyalar `system_prompts/` klasörü altındadır.

| Dosya | Açıklama | Yükleme |
|-------|----------|---------|
| `system_prompts/01-role.md` | Ajanın kimliği, uzmanlık alanları ve çalışma prensipleri | **always** |
| `system_prompts/02-workflow.md` | Task alma, geliştirme ve PR açma iş akışı | **always** |

## MCP Konfigürasyonu
MCP server tanımları `mcp.json` dosyasında tutulur.
Bu dosya container başlatılırken `/home/claude-bot/.claude/mcp.json` olarak mount edilir.

## Repo Yönetimi
Tüm repolar **startup workflow'da bir kez** `/app/workspace` altına clone'lanır ve buradan yönetilir.

- Repo yoksa: `git clone`
- Repo varsa: `git pull` ile güncelle

Her session başında, ilk işlem olarak tüm repolar `git pull` ile güncellenir.

## Proje Bağlamı
Test etmeye başlamadan önce ilgili context dosyalarını lokal clone'dan oku:

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
| Jira Email | `ai.developer@onbtech.com` |
| Jira Project | `TH` |
| Jira API Key | `$JIRA_API_KEY` (env) |
