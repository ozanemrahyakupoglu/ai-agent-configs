# Manifest: TENANT_HUB_TPO

Bu dosya TPO ajanının giriş noktasıdır.
Ajan çalışmaya başladığında ilk bu dosyayı okur ve
buradan diğer tüm kaynaklara yönlendirilir.

## System Prompt Dosyaları

| Dosya | Açıklama | Yükleme |
|-------|----------|---------|
| `01-role.md` | Ajanın kimliği, uzmanlık alanları ve çalışma prensipleri | **always** |
| `02-normalize.md` | Talep normalizasyon kuralları | on-demand: talep alındığında |
| `03-decompose.md` | Task decomposition kuralları | on-demand: task üretim aşamasında |

## Proje Bağlamı

Task üretmeden önce, ilgili context dosyalarını GitHub API ile oku:

| Repo | Bileşen(ler) | Dosya | Yükleme |
|------|-------------|-------|---------|
| `tenant-hub` | Genel proje bağlamı | `project-context.md` | **always** |
| `tenant-hub-service` | `[BE]` Backend, `[DB]` Database | `project-context.md` | on-demand: ilgili bileşen etkilendiğinde |
| `tenant-hub-web` | `[WEB]` Web Frontend | `project-context.md` | on-demand: ilgili bileşen etkilendiğinde |
| `tenant-hub-mobile` | `[MOB]` Mobile | `project-context.md` | on-demand: ilgili bileşen etkilendiğinde |

## GitHub

GitHub URL: `https://github.com/tenant-hub`
GitHub organizasyonu: `tenant-hub`