# Test İş Akışı

## Genel Akış

```
Task Al → AC Oku → Test Senaryoları Yaz → Test Et → Bulgular Raporla → Jira Güncelle
```

---

## 1. Task Alma

- Jira'dan `DEVELOPMENT DONE` statüsündeki task'ları listele.
- Task'ın Jira detayını oku: açıklama, acceptance criteria, PR linki ve yorumlar.
- Task'ın `Depends on` bağımlılıklarını kontrol et — bağımlı task'lar test edilmeden bu task'ı test etme.

---

## 2. Analiz

Test etmeye başlamadan önce şunları oku:

1. `manifest.md` → repo listesi ve konfigürasyon
2. İlgili `project-context.md` dosyaları (bileşene göre)
3. Task'ın acceptance criteria'ları
4. Varsa PR diff'i — neyin değiştiğini anla

---

## 3. Test Senaryoları

Her AC için en az bir test senaryosu yaz. Format:

```
### Senaryo: <Senaryo Adı>
**AC:** [Hangi acceptance criteria'ya karşılık geliyor]
**Ön Koşul:** [Test öncesi gerekli durum]
**Adımlar:**
1. [Adım 1]
2. [Adım 2]
**Beklenen Sonuç:** [Ne olması gerekiyor]
```

Ayrıca şu senaryoları her zaman değerlendir:
- **Happy path** — normal kullanım akışı
- **Edge case** — sınır değerler, boş input, uzun string
- **Hata durumu** — geçersiz veri, yetkisiz erişim, bağlantı hatası
- **Multi-tenant izolasyon** — bir tenant'ın verisi diğerini etkilemiyor mu?

---

## 4. Bileşene Göre Test Adımları

> **Not:** `[DB]` bileşenleri için test yapma. DB task'larını direkt `TEST DONE` statüsüne çek.

### `[BE]` Backend
- API endpoint'lerini `http://tenant-hub-backend.onbtech.com` üzerinden test et
- HTTP status kodlarını doğrula (200, 201, 400, 401, 403, 404, 500)
- Response body yapısını AC ile karşılaştır
- Auth/role kontrollerini doğrula

### `[WEB]` Web Frontend
- Web uygulamasını Chrome üzerinden test et: `https://tenant-hub-web.onbtech.com/`
- Form validasyonlarını kontrol et
- API entegrasyonunu doğrula (doğru veri gösteriliyor mu?)
- Hata mesajlarının kullanıcıya doğru gösterildiğini kontrol et

### `[MOB]` Mobile
- Flutter web build'i Chrome üzerinden test et: `https://tenant-hub-mobile.onbtech.com/`
- Android ve iOS için ayrı test yapma — tüm testler Chrome browser üzerinden yapılır
- Temel kullanıcı akışlarını test et
- Form validasyonlarını kontrol et
- API entegrasyonunu doğrula
- Navigasyon akışını doğrula
- Hata durumları ve kullanıcı geri bildirimlerini kontrol et

---

## 5. Bulgu Raporlama

### Test Geçti
Tüm AC'ler karşılandıysa:
- Jira task'ını `TEST DONE` statüsüne al
- Kısa test özeti yaz: kaç senaryo test edildi, sonuç ne

### Bug Bulundu
Her bug için Jira'da ayrı bug task'ı aç:

```
Başlık: [BUG][<Bileşen>] <Kısa açıklama>

**Ortam:** [backend/web/mobile, versiyon/branch]
**Önem:** [Critical | High | Medium | Low]

**Repro Adımları:**
1. [Adım 1]
2. [Adım 2]

**Beklenen Sonuç:** [Ne olması gerekiyordu]
**Gerçekleşen Sonuç:** [Ne oldu]

**İlgili Task:** TH-<id>
```

Bug açıldıktan sonra orijinal task'ı `DEVELOPMENT` statüsüne geri al ve Developer ajanına bildir.

---

## 6. Jira Güncelleme

| Durum | Task Statüsü |
|-------|-------------|
| Test başladı | `TEST` |
| Tüm AC geçti | `TEST DONE` |
| Bug bulundu | `DEVELOPMENT` (developer'a geri) |
| Blocker var | `TEST XL BLOCK` |