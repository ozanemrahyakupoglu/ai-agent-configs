# Konvansiyonlar

## Tablo ve Kolon Adlandırma

- Tablo adları: `snake_case`, tekil (ör. `tenant_config`, `order`). **İstisna:** `users` tablosu çoğul kalır.
- Kolon adları: `snake_case` (ör. `created_at`, `is_active`)
- Primary key: `id` BIGSERIAL — her tablo için `<tablo_adi>_seq` adında bir sequence oluşturulur ve `id` bu sequence'ten birer birer artar (ör. `users_seq`, `order_seq`)
- Foreign key: `<tablo_adi>_id` — tablo adı tekil ise tekil, çoğul ise çoğul kullanılır (ör. `users_id`, `tenant_id`)
- Timestamp kolonları: `created_at`, `updated_at` — her tabloda bulunur
- Audit kolonları: `created_by`, `updated_by` — her tabloda bulunur, işlemi yapan kullanıcının `id`'si yazılır
- Soft delete: `deleted_at` (NULL = aktif, değer varsa silinmiş)

---

## History Tabloları

Her tablo için `<tablo_adi>_his` adında bir history tablosu oluşturulur. Bu tablo ve ilgili trigger **zorunludur** — ana tablo oluşturulduğunda mutlaka birlikte yazılır.

History tablosu, ana tablonun tüm kolonlarını içerir. Ek olarak şu kolonlar bulunur:

| Kolon | Tip | Açıklama |
|---|---|---|
| `dml_type` | CHAR(1) | `I` = INSERT, `U` = UPDATE, `D` = DELETE |
| `dml_at` | TIMESTAMP | INSERT'te `created_at`, diğer işlemlerde `updated_at` değeri yazılır |
| `dml_by` | BIGINT | INSERT'te `created_by`, diğer işlemlerde `updated_by` değeri yazılır |

Trigger, ana tablodaki her INSERT/UPDATE/DELETE işleminden sonra otomatik olarak history tablosuna kayıt atar.

---

## Migration Dosyaları

### İsimlendirme
```
V<versiyon>__<aciklama>.sql
```

Örnekler:
```
V1__create_users_table.sql
V2__add_email_index_to_users.sql
V3__add_deleted_at_to_tenants.sql
```

### Kurallar
- Her migration tek bir mantıksal değişikliği kapsar.
- Açıklama kısmı ne yapıldığını net ifade eder (`add_`, `create_`, `drop_`, `alter_`, `rename_`).
- Versiyon numarası sıralı ve benzersiz olur; mevcut en yüksek versiyonun bir üstü alınır.
- Migration dosyaları bir kez uygulandıktan sonra **değiştirilmez** — gerekirse yeni migration yazılır.

---

## Index Kuralları

- Her foreign key kolonu için index oluştur.
- Sık sorgulanan filtre kolonlarına index ekle.
- Composite index sırasında yüksek kardinalite olan kolon öne alınır.
- Index adı: `idx_<tablo>_<kolon(lar)>` (ör. `idx_users_email`, `idx_orders_tenant_id_created_at`)
- Gereksiz/duplicate index oluşturma — önce mevcut index'leri kontrol et.

---

## Constraint Kuralları

- `NOT NULL`: Zorunlu olan her kolon için eklenir.
- `UNIQUE`: Benzersizlik gerektiren kolonlara eklenir; adı `uq_<tablo>_<kolon>`.
- `CHECK`: İş kuralı kısıtlamaları için kullanılır; adı `chk_<tablo>_<kural>`.
- `FOREIGN KEY`: Referans bütünlüğü için eklenir; adı `fk_<tablo>_<referans_tablo>`.

---

## Commit Mesajı Formatı

```
<type>(<scope>): <kısa açıklama>
```

Tipler: `feat`, `fix`, `chore`, `refactor`
Scope: etkilenen tablo veya alan (ör. `users`, `migrations`, `indexes`)

Örnekler:
```
feat(users): add email unique constraint
chore(migrations): add V5 create orders table
fix(indexes): add missing index on tenant_id
```
