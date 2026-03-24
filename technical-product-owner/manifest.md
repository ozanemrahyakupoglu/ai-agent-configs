# Manifest: TECHNICAL_PRODUCT_OWNER

Bu dosya Technical Product Owner ajanının giriş noktasıdır.
Ajan çalışmaya başladığında ilk bu dosyayı okur ve
buradan diğer tüm kaynaklara yönlendirilir.

## System Prompt Dosyaları

Dosyalar `system_prompts/` klasörü altındadır.

| Dosya | Açıklama | Yükleme |
|-------|----------|---------|
| `system_prompts/01-role.md` | Ajanın kimliği, uzmanlık alanları ve çalışma prensipleri | **always** |
| `system_prompts/02-normalize.md` | Talep normalizasyon kuralları | on-demand: talep alındığında |
| `system_prompts/03-decompose.md` | Task decomposition kuralları | on-demand: task üretim aşamasında |
| `system_prompts/04-board-management.md` | Board yönetim kuralları | on-demand: "Planlama yap" komutuyla |

## Repo Yönetimi
Tüm repolar **startup workflow'da bir kez** `/app/workspace` altına clone'lanır ve buradan yönetilir.

- Repo yoksa: `git clone`
- Repo varsa: `git pull` ile güncelle

Her session başında, ilk işlem olarak tüm repolar `git pull` ile güncellenir.

## Proje Bağlamı
Task üretmeden önce, ilgili context dosyalarını lokal clone'dan oku:

| Repo | Bileşen(ler) | Dosya | Yükleme |
|------|-------------|-------|---------|
| `tenant-hub` | Genel proje bağlamı | `/app/workspace/tenant-hub/project-context.md` | **always** |
| `tenant-hub-service` | `[BE]` Backend, `[DB]` Database | `/app/workspace/tenant-hub-service/project-context.md` | on-demand: ilgili bileşen etkilendiğinde |
| `tenant-hub-web` | `[WEB]` Web Frontend | `/app/workspace/tenant-hub-web/project-context.md` | on-demand: ilgili bileşen etkilendiğinde |
| `tenant-hub-mobile` | `[MOB]` Mobile | `/app/workspace/tenant-hub-mobile/project-context.md` | on-demand: ilgili bileşen etkilendiğinde |

## MCP Konfigürasyonu

MCP server tanımları `mcp.json` dosyasında tutulur.
Bu dosya container başlatılırken `/home/claude-bot/.claude/mcp.json` olarak mount edilir.

## Konfigürasyon

| Alan | Değer |
|------|-------|
| Workspace | `/app/workspace` — tüm projeler bu dizin altına clone'lanır |
| Ana Proje | `$MAIN_PROJECT` (env) — proje adı; tam yolu `/app/workspace/$MAIN_PROJECT` |
| Ana Proje Git URL | `$MAIN_PROJECT_GIT_URL` (env) — ana projenin clone URL'i |
| İlgili Projeler | `$RELATED_PROJECTS` (env) — proje adları `,` ile ayrılır (ör. `backend,mobile-api`) |
| İlgili Projeler Git URL | `$RELATED_PROJECTS_GIT_URLS` (env) — `$RELATED_PROJECTS` ile aynı sırada, `,` ile ayrılmış Git URL'leri |
| Git Token | `$GITHUB_TOKEN` (env) |
| Jira Email | `$JIRA_EMAIL` (env) — Atlassian hesap e-posta adresi |
| Jira API Key | `$JIRA_API_KEY` (env) |
| Jira Proje | `$JIRA_PROJECT` (env) — Jira proje anahtarı (ör. `TH`) |
