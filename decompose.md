# Adım 2: Tasklara Böl

## Görevin

Onaylanmış **Standart Talep Şablonu**'nu alarak Jira-uyumlu task hiyerarşisi üret.

---

## Jira Hiyerarşisi

```
Epic
└── Story
    ├── Subtask
    ├── Subtask
    └── Subtask
```

### Tanımlar

| Seviye | Ne zaman kullanılır | Kapsam |
|--------|---------------------|--------|
| **Epic** | Birden fazla story içeren büyük iş paketi | 1–4 sprint |
| **Story** | Bağımsız olarak teslim edilebilen kullanıcı değeri | 1–5 gün |
| **Subtask** | Story'nin teknik alt adımı | Yarım gün – 2 gün |

---

## Decomposition Kuralları

### 1. Her Bileşen Ayrı Story Olur
Talep birden fazla bileşeni etkiliyorsa her bileşen için en az bir Story yaz.

| Bileşen | Story prefix önerisi |
|---------|----------------------|
| Database | `[DB]` |
| Backend | `[BE]` |
| Web Frontend | `[WEB]` |
| Mobile | `[MOB]` |

### 2. Story Bağımsız Olmalı
Her Story, diğerlerinden bağımsız olarak test edilebilir ve teslim edilebilir olmalı. Eğer bir Story başka birinin bitmesini bekliyorsa, bunu `Depends on` alanında belirt. Ayrıca storynin parent alanını ilgili epice bağla

### 3. Subtask Granülaritesi
Subtasklar somut teknik adımlar olmalı. "Geliştir" gibi muğlak subtasklar yazma. Eğer storyler altında sub task yazma ihtiyacın varsa. Yazdığın her sub task için jirada subtask kaydı oluştur ve storye bağla

❌ Kötü: `Login ekranını geliştir`

✅ İyi: `Login form validasyonu ekle (email format, boş alan kontrolü)`

### 4. Kabul Kriterleri Story Seviyesinde Yaz
Her Story'nin AC'leri, şablondaki kabul kriterlerinden türetilmeli.

### 5. Subtask Sahipliği
Her Subtask tek bir bileşene ait olmalı. Eğer bir iş birden fazla 
bileşeni etkiliyorsa, her bileşen için ayrı Subtask yaz.

---

## Çıktı Formatı

Her Epic/Story/Subtask için aşağıdaki yapıyı kullan:

```
## 🗂 Epic: [Epic Başlığı]
**Açıklama:** [Epic'in genel amacı]
**Öncelik:** [Critical | High | Medium | Low]

---

### 📋 Story: [Bileşen prefix] [Story Başlığı]
**Açıklama:** [Story'nin amacı, kullanıcıya kattığı değer]
**Kullanıcı Hikayesi:** As a [rol], I want to [eylem], so that [fayda].
**Kabul Kriterleri:**
- [ ] [AC 1]
- [ ] [AC 2]
**Öncelik:** [Critical | High | Medium | Low]
**Tahmini Efor:** [story point veya gün]
**Depends on:** [varsa story adı, yoksa "-"]

#### ✅ Subtask: [Subtask Başlığı]
- **Açıklama:** [Ne yapılacak]
- **Tahmini Efor:** [saat veya yarım gün / 1 gün]

#### ✅ Subtask: [Subtask Başlığı]
- **Açıklama:** [Ne yapılacak]
- **Tahmini Efor:** [saat veya yarım gün / 1 gün]

---

#### ✅ Subtask: [Subtask Başlığı]
- **Açıklama:** [Ne yapılacak]
- **Tahmini Efor:** [saat veya yarım gün / 1 gün]
- **Bileşen:** [DB | BE | WEB | MOB]
- **Teknik Notlar:** [varsa önemli teknik detay, yoksa "-"]
```

---

## Özel Durumlar

### Bug Fix Talebi
Bug fix talepleri genellikle Epic gerektirmez. Doğrudan Story + Subtask yaz.
Story başlığına `[BUG]` prefix ekle.

### Chore / Teknik Borç
`[CHORE]` prefix kullan. Kullanıcı hikayesi yazmak zorunda değilsin, ama etkilenen bileşenleri ve riski belirt.

### Spike / Araştırma
`[SPIKE]` prefix kullan. Subtasklar araştırma adımları olsun ve çıktı olarak "karar belgesi" veya "POC" tanımla.

---

## Decomposition Sonrası Kontrol Listesi

Çıktıyı ürettikten sonra kendi kendine şunu kontrol et:

- [ ] Her etkilenen bileşen için en az bir Story var mı?
- [ ] Her Story'nin en az 2 Subtask'ı var mı?
- [ ] Bağımlılıklar `Depends on` alanında belirtildi mi?
- [ ] Tüm kabul kriterleri test edilebilir mi?
- [ ] Efor tahminleri makul mu? (Bir Story 5 günden uzunsa daha küçük parçalara böl)

Eğer kontrol listesinde eksik varsa, üretmeden önce düzelt.