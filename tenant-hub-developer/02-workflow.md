# Geliştirme İş Akışı

## Genel Akış

```
Task Al → Analiz Et → Branch Aç → Geliştir → Test Et → PR Aç → Jira Güncelle
```

---

## 1. Task Alma

- Jira'dan `TH` projesindeki `In Progress` veya sana atanmış task'ları listele.
- Eğer kullanıcı belirli bir task veriyorsa, önce o task'ın Jira detayını oku.
- Task'ın `Depends on` alanını kontrol et — bağımlı task'lar tamamlanmadan başlama.

---

## 2. Analiz

Task'ı almadan önce şunları oku:

1. `manifest.md` → repo listesi ve konfigürasyon
2. İlgili `project-context.md` dosyaları (bileşene göre)
3. Task'ın etkilediği mevcut kod dosyaları

Analiz sonunda kendine şu soruları sor:
- Hangi dosyalar/modüller değişecek?
- Yeni migration gerekiyor mu?
- Mevcut API kontratı değişiyor mu?
- Test senaryoları neler?

Eğer bu sorulardan birine cevap veremiyorsan, başlamadan önce eksikliği gider.

---

## 3. Branch Oluşturma

Branch adı formatı:

```
feature/TH-<jira-id>-<kisa-aciklama>
bugfix/TH-<jira-id>-<kisa-aciklama>
chore/TH-<jira-id>-<kisa-aciklama>
```

Örnekler:
- `feature/TH-42-login-jwt-integration`
- `bugfix/TH-87-tenant-filter-null-pointer`
- `chore/TH-15-update-flyway-config`

Her zaman `main` (veya projenin ana branch'i) üzerinden branch aç.

---

## 4. Geliştirme

### Commit Kuralları

Her mantıksal adım için ayrı commit at. Format:

```
<type>(<scope>): <kısa açıklama>

[opsiyonel gövde]
```

Tipler: `feat`, `fix`, `chore`, `test`, `refactor`, `docs`

Örnekler:
```
feat(auth): add JWT token generation on login
fix(tenant): fix null pointer when tenant config missing
test(user): add unit tests for UserService.createUser
chore(db): add migration V12__add_last_login_column
```

### Bileşene Göre Geliştirme Adımları

#### `[DB]` Database
1. Migration dosyası yaz (Flyway: `V<versiyon>__<aciklama>.sql`)
2. Entity/model sınıfını güncelle
3. Migration'ı lokal ortamda çalıştır ve doğrula

#### `[BE]` Backend (Spring Boot)
1. Repository katmanı → Service katmanı → Controller katmanı sırasıyla geliştir
2. DTO'ları tanımla
3. Exception handling ekle
4. Unit test yaz (JUnit + Mockito)
5. Lokal ortamda endpoint'i test et

#### `[WEB]` Web Frontend (React)
1. API servis fonksiyonunu yaz
2. Bileşeni geliştir
3. State yönetimini entegre et
4. Responsive davranışı kontrol et
5. Lokal ortamda görsel doğrulama yap

#### `[MOB]` Mobile (Flutter)
1. Repository/datasource katmanını güncelle
2. Bloc/Provider/Riverpod state'ini güncelle
3. Widget'ı geliştir
4. Android ve iOS'ta lokal test et

---

## 5. PR Açma

PR açmadan önce kontrol listesi:
- [ ] Kod derleniyor mu?
- [ ] Tüm testler geçiyor mu?
- [ ] Lint/format hataları temizlendi mi?
- [ ] Migration varsa, rollback senaryosu değerlendirildi mi?
- [ ] Commit geçmişi temiz mi? (her commit mantıklı bir adımı temsil ediyor mu?)

PR başlığı formatı:
```
[TH-<id>] <Task başlığı>
```

PR açıklaması şablonu:
```
## Değişiklikler
- [Ne yapıldı, kısaca]

## Test Edildi
- [ ] Unit testler geçti
- [ ] Lokal ortamda manuel test yapıldı
- [ ] [varsa özel test senaryosu]

## Jira
TH-<id>: <task linki>
```

---

## 6. Jira Güncelleme

PR açıldıktan sonra:
1. Jira task'ını `In Review` statüsüne al
2. PR linkini task'a ekle
3. Varsa blocker veya not bırak

PR merge edildikten sonra:
1. Task'ı `Done` statüsüne al

---

## Özel Durumlar

### Blocker ile Karşılaşıldığında
1. Task'ı `Blocked` statüsüne al
2. Jira'da blocker sebebini açıkla
3. Kullanıcıya veya TPO ajanına bildir

### Beklenmedik Teknik Borç Bulunduğunda
Geliştirme sırasında beklenmedik bir teknik sorun veya borç fark edersen:
- Mevcut task'ı etkilemiyorsa: Jira'ya ayrı bir `[CHORE]` task açılması için not bırak, devam et
- Mevcut task'ı engelliyorsa: Blocker olarak işaretle ve açıkla
