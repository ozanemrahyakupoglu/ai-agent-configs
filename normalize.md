# Adım 1: Talebi Normalleştir

## Görevin

Kullanıcıdan gelen serbest metni analiz et ve aşağıdaki **Standart Talep Şablonu**'na oturtur.

---

## Standart Talep Şablonu

```
### Talep Özeti
[Talebin tek cümlelik özü]

### İş Tanımı
- Tür: [feature | bug | chore | spike]
- Açıklama: [Ne yapılmak isteniyor, neden isteniyor]

### Kullanıcı Hikayesi
As a [kullanıcı rolü],
I want to [yapmak istediği şey],
So that [elde etmek istediği fayda].

### Etkilenen Bileşenler
- [ ] Database
- [ ] Backend
- [ ] Web Frontend
- [ ] Mobile

### Kabul Kriterleri
- [ ] [Kriter 1]
- [ ] [Kriter 2]
- [ ] [Kriter 3]

### Öncelik
- Seviye: [Critical | High | Medium | Low]
- Gerekçe: [Neden bu öncelik?]

### Ek Notlar
[Bağlam, kısıtlar, referanslar — varsa]
```

---

## Normalleştirme Kuralları

1. **Eksik alan varsa uydurma.** Kullanıcının metninden çıkaramadığın alanları boş bırak veya `[BELİRTİLMEMİŞ]` olarak işaretle.
2. **Kullanıcı hikayesi yazılamazsa sor.** Kimin için yapıldığı belli değilse, "Bu özelliği kim kullanacak?" diye sor.
3. **Birden fazla talep varsa ayır.** Gelen metin aslında birden fazla bağımsız iş içeriyorsa, her biri için ayrı şablon oluştur ve kullanıcıya bildir.
4. **Tür belirsizse sor.** Feature mi, bug fix mi, teknik iyileştirme mi olduğu anlaşılamıyorsa kullanıcıya sor.
5. **Bileşen tespiti için ipuçlarına bak.** "API", "endpoint", "servis" → Backend. "Ekran", "sayfa", "buton" → Frontend/Mobile. "Tablo", "migration", "şema" → Database.

---

## Eksik Bilgi Durumunda Davranış

Şablonu doldurmaya çalış. Eğer şu alanlardan **biri bile doldurulamazsa**, task üretimine geçmeden önce kullanıcıya sor:

- Kullanıcı hikayesindeki **rol** (`As a [?]`)
- **Etkilenen bileşenler** (hiçbiri tespit edilemiyorsa)
- **Kabul kriterleri** (tamamen belirsizse)

Soruları tek seferde, liste halinde sor. Her soru için neden sorduğunu kısaca belirt.

**Örnek:**
> Talebi anladım, ancak şablonu tamamlamak için birkaç bilgiye ihtiyacım var:
> 1. **Kullanıcı rolü:** Bu özelliği kim kullanacak? (örn. admin, kiracı, mülk sahibi)
> 2. **Etkilenen bileşenler:** Bu değişiklik sadece arayüzde mi olacak, yoksa backend/veritabanı da etkilenecek mi?

---

## Çıktı Formatı

Normalleştirme tamamlandığında şunu yap:

1. Doldurulmuş şablonu göster
2. Eğer varsayım yaptıysan, bunları şablonun altında listele:
   > ⚠️ **Varsayımlar:**
   > - Kullanıcı rolü "tenant" olarak varsayıldı, çünkü metinde "kiracı" geçiyor.
3. Kullanıcıya sor: *"Bu şablonu onaylıyor musun? Devam etmemi istersen tasklara böleceğim."*
