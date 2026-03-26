# Geliştirme

## Genel Kurallar

- Tüm geliştirmeler yalnızca `$MAIN_PROJECT` (`MAIN_PROJECT` env) projesinde yapılır.
- Geliştirme öncesinde `/app/workspace/$MAIN_PROJECT` dizinindeki proje okunur; varsa `README.md`, `project_context.md` incelenir.
- İhtiyaç duyulduğunda `$RELATED_PROJECTS` kapsamındaki projelerde de `README.md`, `project_context.md` incelenir.
- Bu dosyalardan edinilen bilgiler yeterli olmadığında ilgili projelerin tüm kodları incelenebilir.
- Geliştirmeye başlamadan önce `$MAIN_PROJECT` reposu yoksa clone'lanır, varsa `git pull` ile güncellenir ve sonra feature branch açılır.
- Geliştirme yalnızca feature branch üzerinde yapılır.
- Mevcut kod yapısına ve projedeki konvansiyonlara uyulur.
- Blocker ile karşılaşılırsa detaylar Jira'ya yorum olarak yazılır ve task `DEVELOPMENT XL BLOCK` statüsüne alınır.

## Geliştirme Detayları

### Planlama

- Hangi bileşenler oluşturulacak / güncellenecek belirlenir.
- Hangi sayfalar etkilenecek belirlenir.
- State yönetiminde değişiklik gerekip gerekmediği değerlendirilir.
- API entegrasyon noktaları belirlenir.

### Uygulama

- Mevcut kod yapısına ve konvansiyonlara uygun şekilde geliştirilir.
- Bileşenler oluşturulur / güncellenir.
- Sayfalar güncellenir.
- API entegrasyonu yapılır.
- State yönetimi güncellenir (gerekliyse).


> **Not:** Geliştirme aşamasında geliştirmeye engel olan bir durum ortaya çıkarsa `05-jira.md` kuralları doğrultusunda durumu detaylıca açıklayan bir Jira yorumu girilir ve task `DEVELOPMENT XL BLOCK` statüsüne alınır.
