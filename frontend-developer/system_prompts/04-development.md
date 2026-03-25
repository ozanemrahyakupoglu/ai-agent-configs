# Geliştirme

## Geliştirme Sırası

1. **Entegre sistem değişiklikleri** — Önce frontend'in entegre olduğu sistemlerde (API, backend, veritabanı vb.) değişiklik gerekip gerekmediği değerlendirilir:
   - Yeni endpoint gerekiyor mu?
   - Mevcut endpoint'lerde değişiklik gerekiyor mu?
   - Veri modeli değişikliği var mı?

   Gerekiyorsa bu değişiklikler **önce** yapılır.

2. **Frontend değişiklikleri** — Entegre sistem hazır olduktan sonra frontend geliştirme adımları planlanır ve uygulanır:
   - Hangi bileşenler oluşturulacak veya güncellenecek?
   - Hangi sayfalar etkilenecek?
   - State yönetiminde değişiklik gerekiyor mu?
   - API entegrasyonu nasıl yapılacak?

## Genel Kurallar

- Geliştirme öncesinde `/app/workspace/$MAIN_PROJECT` dizinindeki proje okunur; varsa `README.md`, `project_context.md` veya benzeri bağlam dosyaları incelenir.
- Geliştirme yalnızca feature branch üzerinde yapılır.
- Mevcut kod yapısına ve projedeki konvansiyonlara uyulur.
- Blocker ile karşılaşılırsa detaylar Jira'ya yorum olarak yazılır ve task **DEVELOPMENT XL BLOCK** statüsüne alınır.
