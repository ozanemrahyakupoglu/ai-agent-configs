# Review İş Akışı

## Genel Akış

```
PR Al → Bağlamı Oku → Kodu İncele → Review Raporu Yaz → Karar Ver → Jira/PR Güncelle
```

---

## 1. PR Alma

- Jira'dan `In Review` statüsündeki task'ların PR linklerini listele.
- PR diff'ini oku — hangi dosyalar değişmiş, ne eklenmiş, ne çıkarılmış.
- İlgili Jira task'ını oku: açıklama ve acceptance criteria.

---

## 2. Bağlamı Okuma

Review'a başlamadan önce şunları oku:

1. `manifest.md` → repo listesi ve konfigürasyon
2. İlgili `project-context.md` dosyaları (bileşene göre)
3. Değiştirilen dosyaların mevcut hallerini (diff bağlamını anlamak için)

---

## 3. Review Kontrol Listesi

### Genel
- [ ] Kod derleniyor mu? (CI/lint çıktısı varsa kontrol et)
- [ ] Testler yazılmış mı? Kritik iş mantığı kapsanmış mı?
- [ ] Commit geçmişi temiz mi?
- [ ] PR açıklaması yeterli mi?

### Güvenlik
- [ ] Injection açığı var mı? (SQL, command, vb.)
- [ ] Hassas veri (token, şifre, PII) log'a yazılıyor veya response'a dönüyor mu?
- [ ] Yetkilendirme kontrolleri eksik mi?
- [ ] Multi-tenant izolasyon ihlali var mı?

### Kod Kalitesi
- [ ] Tekrar eden kod var mı? (DRY)
- [ ] Sorumluluklar doğru ayrılmış mı? (tek sorumluluk prensibi)
- [ ] Magic number/string var mı? Constant'a alınmalı mı?
- [ ] Gereksiz karmaşıklık veya aşırı mühendislik var mı?

### Bileşene Özgü

#### `[BE]` Backend
- [ ] Controller iş mantığı içeriyor mu? (içermemeli)
- [ ] Transaction sınırları doğru mu?
- [ ] N+1 sorgu riski var mı?
- [ ] Exception'lar uygun şekilde yakalanıp dönüştürülüyor mu?

#### `[DB]` Database
- [ ] Migration geri alınabilir mi?
- [ ] Yeni kolonlar/tablolar için index değerlendirildi mi?
- [ ] Mevcut veriyle uyumluluk sağlandı mı?

#### `[WEB]` Frontend
- [ ] API hata durumları handle edilmiş mi?
- [ ] State güncellemeleri tutarlı mı?
- [ ] Gereksiz re-render tetikleyen yapı var mı?

#### `[MOB]` Mobile
- [ ] Widget dispose işlemleri yapılmış mı?
- [ ] Platform farkı gözetilen alan varsa her iki platform için de kontrol edildi mi?

---

## 4. Review Raporu

Her bulgu için format:

```
### [Blocker | Major | Minor] — <Kısa Başlık>
**Dosya:** `<dosya yolu>:<satır numarası>`
**Sorun:** [Ne yanlış ve neden sorun]
**Öneri:** [Nasıl düzeltilmeli]
```

Rapor sonunda özet:

```
## Review Özeti
- Toplam bulgu: X (Blocker: X, Major: X, Minor: X)
- Karar: [Approved | Changes Requested]
```

---

## 5. Karar

### Approved (Onaylandı)
Koşul: Hiç `Blocker` yok, `Major` sayısı 2'den az.

- PR'ı GitHub'da approve et
- Jira task'ını `In Review` olarak bırak (Tester devralacak)
- Jira'ya yorum bırak: `[Reviewer] Approved. Tester'a geçebilir.`

### Changes Requested (Değişiklik Gerekli)
Koşul: En az 1 `Blocker` veya 2+ `Major` bulgu var.

- PR'ı GitHub'da "Request Changes" ile geri çevir
- Jira task'ını `In Progress` statüsüne al
- Jira'ya yorum bırak: `[Reviewer] Changes requested. <blocker sayısı> blocker, <major sayısı> major bulgu.`
- Developer ajanına bildir

---

## 6. Sonraki Adım

| Karar | Sonraki Ajan | Jira Statüsü |
|-------|-------------|--------------|
| Approved | Tester ajanı devralır | `In Review` |
| Changes Requested | Developer ajanına geri döner | `In Progress` |
