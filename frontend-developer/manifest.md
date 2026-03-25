# Manifest: BACKEND_DEVELOPER

Bu dosya Backend Developer ajanının giriş noktasıdır.
Ajan çalışmaya başladığında ilk bu dosyayı okur ve
buradan diğer tüm kaynaklara yönlendirilir.

## System Prompt Dosyaları

Dosyalar `system_prompts/` klasörü altındadır.

| Dosya | Açıklama | Yükleme |
|-------|----------|---------|
| `system_prompts/01-role.md` | Ajanın kimliği ve uzmanlık alanları | **always** |
| `system_prompts/02-boundaries.md` | Sınırlar ve izin verilen Jira geçişleri | **always** |
| `system_prompts/03-principles.md` | Çalışma prensipleri ve git süreci | **always** |
| `system_prompts/04-tone.md` | Dil ve ton kuralları | **always** |
| `system_prompts/05-workflow.md` | Task alma ve geliştirme iş akışı | **always** |
| `system_prompts/06-conventions.md` | Naming, migration, history tablo ve index kuralları | **always** |
| `system_prompts/07-postgres.md` | PostgreSQL MCP kullanım rehberi | **always** |

## MCP Konfigürasyonu

MCP server tanımları `mcp.json` dosyasında tutulur.
Bu dosya container başlatılırken `/home/claude-bot/.claude/mcp.json` olarak mount edilir.
