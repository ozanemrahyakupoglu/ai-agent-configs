# PostgreSQL MCP Kullanımı

PostgreSQL MCP (`@crystaldba/postgres-mcp`), `$DATABASE_URI` ortam değişkeniyle tanımlanan veritabanına bağlanır. Geliştirme sırasında bu araç üzerinden şema analizi yapılır ve SQL komutları çalıştırılır.

---

## Ne Zaman Kullanılır?

| Durum | Yapılacak |
|---|---|
| Task alındığında | Mevcut şemayı anlamak için ilgili tabloları incele |
| Migration yazmadan önce | Mevcut index'leri, constraint'leri ve kolon tiplerini kontrol et |
| Migration uygulandıktan sonra | Değişikliklerin doğru uygulandığını doğrula |
| Performans sorununda | `EXPLAIN ANALYZE` ile sorgu planını analiz et |

---

## Şema Analizi

Geliştirmeye başlamadan önce şu soruları cevapla:

- İlgili tablolar mevcut mu?
- Hangi kolonlar var, tipleri ne?
- Mevcut index'ler neler?
- Foreign key ilişkileri doğru mu?
- Flyway'in en son uyguladığı migration versiyonu nedir? (`flyway_schema_history` tablosunu kontrol et)

---

## SQL Çalıştırma

- Tüm DDL değişiklikleri (`CREATE`, `ALTER`, `DROP`) doğrudan veritabanında çalıştırılır.
- Büyük tablo değişikliklerinde transaction kullanılır; hata durumunda rollback yapılır.
- Destructive işlemler (`DROP TABLE`, `DROP COLUMN`) doğrudan çalıştırılmaz — önce deprecated kolon/tablo işaretle, yeni migration versiyonunda kaldır.

---

## Doğrulama

Her değişiklikten sonra doğrula:

- Tablo/kolon beklenen şekilde oluşturuldu mu?
- Index aktif ve kullanılıyor mu?
- Constraint ihlali var mı?
- `flyway_schema_history` tablosunda migration başarılı olarak kayıtlı mı?
