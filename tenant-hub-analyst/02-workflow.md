# Analiz İş Akışı

## Genel Akış

```
Task Al → Bağlamı Oku → Analiz Et → Jira Güncelle
```

---

## 1. Task Alma

- Yalnızca board'da görünen, `To Do` statüsündeki task'larla çalış. Backlog'daki task'ları alma.
- Board dışındaki veya farklı statüdeki task'lara dokunma.

---

## 2. Bağlamı Okuma

Task'ı analiz etmeden önce şunları oku:

1. `manifest.md` → repo listesi ve konfigürasyon
2. İlgili `project-context.md` dosyaları (task'ın bileşenine göre)
3. Varsa bağımlı task'ların içerikleri

---

## 3. Analiz Kontrol Listesi

Her task için aşağıdaki soruları sırayla değerlendir:

### Açıklama
- [ ] Task'ın amacı net anlaşılıyor mu?
- [ ] "Ne yapılacak" ve "neden yapılacak" belirtilmiş mi?

### Acceptance Criteria
- [ ] Her AC test edilebilir ve ölçülebilir mi?
- [ ] "Çalışmalı", "gösterilmeli" gibi muğlak ifade var mı? → Somutlaştır
- [ ] Eksik senaryo var mı? (hata durumu, edge case, auth kontrolü)
- [ ] Duplicate AC var mı? → Kaldır

### Bileşen Etiketleri
- [ ] Task başlığındaki bileşen etiketi (`[BE]`, `[WEB]`, vb.) doğru mu?
- [ ] Task birden fazla bileşeni etkiliyor ama tek task olarak yazılmış mı? → Bölünmesi gerekebilir, not al

### Bağımlılıklar
- [ ] `Depends on` alanı dolu mu?
- [ ] Bağımlı olması gereken ama belirtilmemiş task var mı? → Ekle

### Efor Tahmini
- [ ] Tahmin makul mu? (3 günden uzunsa büyük ihtimalle bölünmeli)
- [ ] Tahmin hiç girilmemiş mi? → Tahminde bulun veya not bırak

---

## 4. Değişiklik Raporu ve Uygulama

Analiz tamamlandığında değişiklikleri doğrudan Jira'ya uygula. Ardından şu formatta özet yaz:

```
## Task: TH-<id> — <Task Başlığı>

### Eklenenler
- [Ne eklendi ve neden]

### Çıkarılanlar
- [Ne çıkarıldı ve neden]

### Güncellenenler
- [Ne değiştirildi: eski → yeni, neden]

### Değişiklik Yok
- [Herhangi bir sorun bulunamadıysa bunu belirt]
```

---

## 5. Jira Güncelleme

Analiz tamamlandıktan sonra task'ta şunları güncelle:
- Açıklama (gerekiyorsa)
- Acceptance criteria listesi
- `Depends on` alanı
- Efor tahmini
- Varsa yorum: `[Analyst] <kısa değişiklik özeti>`

Tüm güncellemeler tamamlandıktan sonra task'ın statüsünü `To Do` → `Ready` olarak değiştir.

---

## Özel Durumlar

### Task Bölünmesi Gerekiyorsa
Task'ı kendin bölme. Bunun yerine:
1. Jira'ya yorum bırak: `[Analyst] Bu task bölünmeli: <gerekçe>`
2. Task'ı `To Do` statüsünde bırak, statüsünü değiştirme

### Kritik Eksiklik Varsa
Task'ta temel bilgi (AC yok, bileşen yok, açıklama yok) eksikse:
1. Jira'ya yorum bırak: `[Analyst] Eksik bilgi: <liste>`
2. Task'ı `To Do` statüsünde bırak, statüsünü değiştirme
