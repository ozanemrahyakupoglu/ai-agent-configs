# Tasklara Böl

## Görevin

Onaylanmış **Standart Talep Şablonu**'nu alarak Jira-uyumlu task'lar üret.
Her etkilenen bileşen için ayrı task oluştur. Epic, Story veya Subtask üretme — sadece Task üret.

---

## Decomposition Kuralları

### 1. Her Bileşen Ayrı Task Olur
Talep birden fazla bileşeni etkiliyorsa her bileşen için en az bir task yaz.

| Bileşen | Task prefix |
|---------|-------------|
| `[DB]` | Database |
| `[BE]` | Backend |
| `[WEB]` | Web Frontend |
| `[MOB]` | Mobile |

### 2. Task Bağımsız Olmalı
Her task, diğerlerinden bağımsız olarak test edilebilir ve teslim edilebilir olmalı.
Eğer bir task başka birinin bitmesini bekliyorsa, bunu `Depends on` alanında belirt.

### 3. Scope Küçük Olmalı
Her task tek bir somut iş birimini temsil etmeli. Eğer bir task 3 günden uzun sürüyorsa, daha küçük task'lara böl.

❌ Kötü: `[WEB] Login ekranını geliştir`

✅ İyi: `[WEB] Login form validasyonu ekle (email format, boş alan kontrolü)`

### 4. Kabul Kriterleri Her Task'ta Olmalı
Her task'ın acceptance criteria'ları, şablondaki kabul kriterlerinden türetilmeli.
Test edilebilir, somut kriterler yaz.

### 5. Duplicate Kontrolü
Task üretmeden önce mevcut backlog'u kontrol et. Aynı işi kapsayan bir task varsa, yenisini üretme.

---

## Task Çıktı Formatı

Her task için aşağıdaki yapıyı kullan:

```
### 📋 Task: [Bileşen prefix] [Task Başlığı]
**Tür:** [feature | bug | chore | spike]
**Açıklama:** [Task'ın amacı, ne yapılacağı]
**Kullanıcı Hikayesi:** Bir [rol] olarak, [eylem] istiyorum, böylece [fayda].
**Kabul Kriterleri:**
- [ ] [AC 1]
- [ ] [AC 2]
**Öncelik:** [Critical | High | Medium | Low | BELİRTİLMEMİŞ]
**Tahmini Efor:** [gün]
**Depends on:** [varsa task adı, yoksa "-"]
```

---

## Özel Durumlar

### Bug Fix Talebi
Task başlığına `[BUG]` prefix ekle, bileşen prefix'iyle birlikte kullan.
Örnek: `[BUG][BE] Login endpoint 500 hatası`

### Chore / Teknik Borç
`[CHORE]` prefix kullan. Kullanıcı hikayesi yazmak zorunda değilsin, ama etkilenen bileşenleri ve riski belirt.

### Spike / Araştırma
`[SPIKE]` prefix kullan. Çıktı olarak "karar belgesi" veya "POC" tanımla.

---

## Decomposition Sonrası Kontrol Listesi

Çıktıyı ürettikten sonra kendi kendine şunu kontrol et:

- [ ] Her etkilenen bileşen için en az bir task var mı?
- [ ] Bağımlılıklar `Depends on` alanında belirtildi mi?
- [ ] Tüm kabul kriterleri test edilebilir mi?
- [ ] Efor tahminleri makul mu? (Bir task 3 günden uzunsa daha küçük parçalara böl)
- [ ] Mevcut backlog'ta duplicate var mı?

Eğer kontrol listesinde eksik varsa, üretmeden önce düzelt.

---

## Çıktı Sonrası

Task'ları ürettikten sonra kullanıcıya özet liste göster ve onay iste:

> **Oluşturulacak Task'lar:**
> 1. `[BE] Login endpoint - JWT token üretimi`
> 2. `[WEB] Login form validasyonu`
> 3. `[DB] Users tablosuna last_login kolonu ekle`
>
> *"Bu task'ları Jira'ya oluşturmamı onaylıyor musun?"*

Kullanıcı onayladığında task'ları Jira'ya oluştur.
Kullanıcı değişiklik isterse, ilgili task'ı düzenle ve tekrar onay iste.