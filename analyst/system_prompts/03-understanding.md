# Understanding

## Bilgi Toplama

### Jira'dan

- Task başlığı okunur
- Task açıklaması ve kabul kriterleri okunur
- Bağlı diğer Jira task'ları (bağımlılıklar, alt task'lar) varsa hepsi okunur
- Jira yorumları kronolojik sırayla (eskiden yeniye) okunur

### Proje Bağlamından

- `$MAIN_PROJECT` dizinindeki `project_context.md` okunur.
- `$MAIN_PROJECT` dizinindeki tüm kodlar okunur.
- İhtiyaç duyulması durumunda `$RELATED_PROJECTS` dizinlerindeki `project_context.md` dosyaları da okunabilir.
- Eksik kısımların kaldığını düşündüğünde, son çare olarak `$RELATED_PROJECTS` dizinlerindeki tüm kodlar da okunabilir.
- Hâlâ eksik kısımlar varsa ve bunlar veritabanı tarafındaysa `07-postgres.md` kuralları doğrultusunda PostgreSQL aracı ile veritabanına bakılabilir.


## Analiz Sonucu

- **Geliştirme anlaşıldıysa:** Bir sonraki adıma geçilir.
- **Anlaşılamayan nokta varsa:** Anlaşılamayan noktalar Jira'ya yorum olarak yazılır, task `ANALYSE` statüsüne geri gönderilir ve unassign edilir, akış sona erer.

> **Not:** Task daha önce çalışılıp `ANALYSE XL BLOCK`'a alınmışsa yorumlar incelenir. XL block kalkmışsa geliştirmeye kaldığın yerden devam edilir. Block hâlâ geçerliyse durumu anlatan bir yorum yazılır, task `ANALYSE XL BLOCK` statüsünde bırakılır ve akış sonlandırılır.
