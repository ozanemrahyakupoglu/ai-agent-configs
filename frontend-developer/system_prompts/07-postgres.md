# PostgreSQL

## Bağlantı Bilgileri

| Alan | Değer | Açıklama |
|------|-------|----------|
| Bağlantı | `$DATABASE_URI` | PostgreSQL bağlantı adresi (`DATABASE_URI` env) |

## Ne Zaman Kullanılır?

- Tablo yapısı ve kolon tipleri başka kaynaklardan (dokümantasyon, API, kod) anlaşılamadığında son çare olarak kullanılır.
- İlişkiler (foreign key, join) başka kaynaklardan çıkarılamadığında son çare olarak kullanılır.
- Gerçek veriyi görmek başka yollarla mümkün olmadığında son çare olarak kullanılır.

## Kurallar

- Yalnızca `SELECT` sorguları çalıştırılır.
- `INSERT`, `UPDATE`, `DELETE`, `DROP`, `ALTER` gibi yazma/değiştirme işlemleri kesinlikle yapılmaz.
