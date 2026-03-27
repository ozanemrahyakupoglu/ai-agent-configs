# Analiz

## Genel Kurallar

- Tüm analizler `$RELATED_PROJECTS` (`RELATED_PROJECTS` env) kapsamındaki projelerde yapılır.
- Analiz öncesinde ilgili projelerin `README.md` ve `project_context.md` dosyaları incelenir.
- Bu dosyalardan edinilen bilgiler yeterli olmadığında ilgili projelerin tüm kodları incelenebilir.
- Bağlam için ihtiyaç duyulduğunda `/app/workspace/$MAIN_PROJECT` dizinindeki `README.md`, `project_context.md` de okunabilir.
- Blocker ile karşılaşılırsa detaylar Jira'ya yorum olarak yazılır ve task `ANALYSE XL BLOCK` statüsüne alınır.

## Analiz Detayları

### 1. Mevcut Durum Analizi

- Task ile ilgili servis, modül ve endpoint'ler tespit edilir ve detaylıca incelenir.
- Mevcut veri modeli ve ilgili veritabanı tabloları okunur.
- Mevcut iş akışı ve iş kuralları çıkarılır.
- Task içeriği proje bağlamıyla karşılaştırılarak eksikler tespit edilir.

### 2. Talep Analizi

- Task'ta istenen değişiklik veya yeni özellik net olarak anlaşılır.
- Mevcut durum ile istenen durum arasındaki farklar belirlenir.
- "Çalışmalı", "gösterilmeli" gibi muğlak acceptance criteria'lar ölçülebilir kriterlere dönüştürülür.
- Duplicate, anlamsız veya scope dışı içerik ayıklanır; yeni özellik türetilmez.

### 3. Etki Analizi

- Değişiklikten etkilenecek servisler, endpoint'ler ve tablolar listelenir.
- Bileşen etiketleri (`[DB]`, `[BE]`, `[WEB]`, `[MOB]`) doğrulanır; eksik olanlar eklenir.
- Bağımlılıklar (`Depends on`) kontrol edilir; eksik bağımlılıklar eklenir.
- Diğer projeler veya bağımlı sistemler üzerindeki etkisi değerlendirilir.
- Breaking change riski analiz edilir.

### 4. Analiz Çıktısı

- Yapılması gerekenler net ve uygulanabilir şekilde maddeler hâlinde yazılır.
- Varsa API contract değişiklikleri belirtilir.
- Varsa veritabanı şema değişiklikleri belirtilir.
- Efor tahmininin makul olup olmadığı değerlendirilir.
- Geliştirici için dikkat edilmesi gereken noktalar vurgulanır.
- Her değişiklik için kısa bir gerekçe belirtilir; sessizce düzenleme yapılmaz.
- Tüm bulgular doğrultusunda Jira task'ı güncellenir (açıklama, AC, etiketler, bağımlılıklar).
- Yapılan düzenlemeler ve gerekçeleri Jira task'ına yorum olarak eklenir.


> **Not:** Analiz aşamasında analizi engelleyen bir durum ortaya çıkarsa `05-jira.md` kuralları doğrultusunda durumu detaylıca açıklayan bir Jira yorumu girilir ve task `ANALYSE XL BLOCK` statüsüne alınır.
