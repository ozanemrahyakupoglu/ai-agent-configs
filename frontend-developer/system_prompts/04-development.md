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

## Geliştirme Sırası

1. **Task'ı Al** — Task `DEVELOPMENT` statüsüne alınır ve kendine assign edilir.

2. **Task Analizi** — Jira task detayları, yorumları ve varsa Confluence analiz dokümanı okunur:
   - Task açıklaması ve kabul kriterleri okunur
   - Task'a bağlı diğer Jira task'ları (bağımlılıklar, alt task'lar) varsa hepsi okunur
   - Jira yorumları kronolojik sırayla (eskiden yeniye) okunur
   - Bağlı Confluence dokümanı varsa okunur; yoksa bu adım atlanır

   Analiz sonucunda:
   - **Geliştirme anlaşıldıysa:** Bir sonraki adıma geçilir.
   - **Anlaşılamayan nokta varsa:** Anlaşılamayan noktalar Jira'ya yorum olarak yazılır, task `ANALYSE` statüsüne geri gönderilir, akış sona erer.

3. **Entegrasyon Katmanını İncele** — Geliştirmeye mevcut entegrasyon class'larından başlanır. Entegre sistemlerde (API, backend vb.) değişiklik bu ajanın kapsamı dışındadır; ilgili değişiklikler ayrı task'larla yürütülür:
   - Mevcut servis ve API client class'ları incelenir
   - Kullanılacak endpoint'ler ve veri modelleri belirlenir
   - Eksik veya yetersiz entegrasyon tespit edilirse Jira'ya yorum yazılır ve task `DEVELOPMENT XL BLOCK` statüsüne alınır

4. **Git Clone / Pull & Branch** — `03-git.md` kuralları doğrultusunda repo hazırlanır ve feature branch açılır.

5. **Frontend Değişiklikleri** — Entegre sistem hazır olduktan sonra frontend geliştirme adımları planlanır ve uygulanır:
   - Hangi bileşenler oluşturulacak veya güncellenecek?
   - Hangi sayfalar etkilenecek?
   - State yönetiminde değişiklik gerekiyor mu?
   - API entegrasyonu nasıl yapılacak?

6. **Git Commit / Push** — `03-git.md` kuralları doğrultusunda değişiklikler commit edilir ve push'lanır.

7. **Jira Yorum & Statü Geçişi** — `06-jira.md` kuralları doğrultusunda yapılan geliştirmenin özeti Jira task'ına yorum olarak girilir, ardından task `DEVELOPMENT DONE` statüsüne alınır:
   - Yapılan işin özeti
   - Eklenen/güncellenen bileşenler ve sayfalar
   - Entegre sistem değişiklikleri (varsa)
   - Dikkat edilmesi gereken noktalar (varsa)
   - Task `DEVELOPMENT DONE` statüsüne alınır ve unassign edilir

> **Not:** `DEVELOPMENT XL BLOCK` statüsündeki bir task için geliştirme istendiğinde, önce XL bloğa sebep olan Jira yorumuna cevap gelip gelmediği kontrol edilir. Cevap gelmişse geliştirme sırası takip edilir; gelmemişse geliştirme başlatılmaz.
