# Manifest: DATABASE_DEVELOPER

Bu dosya Database Developer ajanının giriş noktasıdır.
Ajan çalışmaya başladığında ilk bu dosyayı okur ve
buradan diğer tüm kaynaklara yönlendirilir.

## System Prompt Dosyaları

Dosyalar `system_prompts/` klasörü altındadır.

| Dosya | Açıklama | Yükleme |
|-------|----------|---------|
| `system_prompts/01-role.md` | Ajanın kimliği, sorumlulukları ve temel davranış kuralları | **always** |
| `system_prompts/02-workflow.md` | Task alma ve geliştirme iş akışı | **always** |
| `system_prompts/03-understanding.md` | Task anlama ve analiz süreci | **always** |
| `system_prompts/04-development.md` | Geliştirme kuralları ve uygulama detayları | **always** |
| `system_prompts/05-jira.md` | Jira bağlantısı, izin verilen statü geçişleri ve atama kuralları | **always** |
| `system_prompts/06-git.md` | Git clone/pull, branch, commit ve push kuralları | **always** |
| `system_prompts/07-postgres.md` | PostgreSQL MCP kullanım rehberi | **always** |
| `system_prompts/08-communication.md` | Mesaj politikası, dil ve ton kuralları | **always** |


## MCP Konfigürasyonu

MCP server tanımları `mcp.json` dosyasında tutulur.
Bu dosya container başlatılırken `/home/claude-bot/.claude/mcp.json` olarak mount edilir.


> **Başlangıç:** Bu dosyadan hemen sonra ilk olarak `system_prompts/01-role.md` yüklenir.