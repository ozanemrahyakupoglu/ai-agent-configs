# Test

## Genel Kurallar

- Task'ın `Depends on` bağımlılıkları kontrol edilir — bağımlı task'lar test edilmeden bu task test edilmez.
- Blocker ile karşılaşılırsa detaylar Jira'ya yorum olarak yazılır ve task `TEST XL BLOCK` statüsüne alınır.

## Tetiklenme Koşulları

Bu workflow şu durumlarda çalışır:

1. **"Test et" komutu geldiğinde** — kullanıcı bu veya benzeri bir komutu gönderirse, bu dosyayı oku ve gerekli aksiyonları al
2. **Sadece bir Jira issue key geldiğinde** — kullanıcı yalnızca bir issue key gönderirse (örn. `TH-42`), o task'ın Jira'daki statüsünü kontrol et; eğer statüsü `TEST` veya `DEVELOPMENT_DONE` ise yalnızca o task için test yap

   **Örnek:** Kullanıcı yalnızca `TH-42` gönderdi → `TH-42`'nin statüsü kontrol edildi → `TEST` veya `DEVELOPMENT_DONE` olduğu görüldü → sadece `TH-42` test edildi

---

## Analiz

Test etmeye başlamadan önce şunlar okunur:

1. Task'ın Jira detayı: açıklama, acceptance criteria, PR linki ve yorumlar
2. İlgili `project_context.md` dosyaları
3. Varsa PR diff'i — neyin değiştiğini anlamak için

## Test Senaryoları

Her acceptance criteria için en az bir test senaryosu yazılır. Format:

```
### Senaryo: <Senaryo Adı>
**AC:** [Hangi acceptance criteria'ya karşılık geliyor]
**Ön Koşul:** [Test öncesi gerekli durum]
**Adımlar:**
1. [Adım 1]
2. [Adım 2]
**Beklenen Sonuç:** [Ne olması gerekiyor]
```

Her testte şu senaryolar değerlendirilir:
- **Happy path** — normal kullanım akışı
- **Edge case** — sınır değerler, boş input, uzun string
- **Hata durumu** — geçersiz veri, yetkisiz erişim, bağlantı hatası

## Bileşene Göre Test Adımları

### `[DB]` Database
- DB task'ları için browser veya API testi yapılmaz.
- Migration'ın başarıyla uygulandığını doğrulamak için PostgreSQL MCP ile ilgili tabloya SELECT sorgusu çekilir.
- Kolon varlığı, veri tipi veya kısıt gibi yapısal değişiklikler `information_schema` üzerinden kontrol edilir.
- Doğrulama tamamlandıktan sonra task direkt `TEST DONE` statüsüne alınır.

### `[BE]` Backend
- API endpoint'leri `$BE_BASE_URL` üzerinden test edilir
- HTTP status kodları doğrulanır (200, 201, 400, 401, 403, 404, 500)
- Response body yapısı AC ile karşılaştırılır
- Auth/role kontrolleri doğrulanır

### `[WEB]` Web Frontend
- Web uygulaması `09-browser.md` kuralları doğrultusunda `$WEB_BASE_URL` üzerinden test edilir
- Form validasyonları kontrol edilir
- API entegrasyonu doğrulanır (doğru veri gösteriliyor mu?)
- Hata mesajlarının kullanıcıya doğru gösterildiği kontrol edilir

### `[MOB]` Mobile
- Flutter web build'i `09-browser.md` kuralları doğrultusunda `$MOB_BASE_URL` üzerinden test edilir
- Android ve iOS için ayrı test yapılmaz — tüm testler browser üzerinden yapılır
- Temel kullanıcı akışları test edilir
- Form validasyonları kontrol edilir
- API entegrasyonu doğrulanır
- Navigasyon akışı doğrulanır
- Hata durumları ve kullanıcı geri bildirimleri kontrol edilir

## Bulgu Raporlama

### Test Geçti
Tüm AC'ler karşılandıysa task `TEST DONE` statüsüne alınır ve kısa bir test özeti Jira'ya yorum olarak yazılır (kaç senaryo test edildi, sonuç ne).

### Bug Bulundu
Her bug için Jiraya aşağıdaki formatta yorum girilir:

```
[BUG]<Kısa açıklama>

**Ortam:** [backend/web/mobile, versiyon/branch]
**Önem:** [Critical | High | Medium | Low]

**Repro Adımları:**
1. [Adım 1]
2. [Adım 2]

**Beklenen Sonuç:** [Ne olması gerekiyordu]
**Gerçekleşen Sonuç:** [Ne oldu]

```

Bug açıldıktan sonra task `DEVELOPMENT` statüsüne geri alınır ve unassign yapılır.
