# İş Akışı

## Genel Akış

```
Projeleri Hazırla → Task Al → Şemayı Anla → Geliştir → Doğrula → Git → DEVELOPMENT DONE
```

---

## 0. Projeleri Hazırla

**Ana proje (`$MAIN_PROJECT`):**
- `/app/workspace/$MAIN_PROJECT` dizini **yoksa** → `git clone $MAIN_PROJECT_GIT_URL /app/workspace/$MAIN_PROJECT`
- Dizin **varsa** → `main` branch'ine geç, `git pull` al.

**İlgili projeler (`$RELATED_PROJECTS`):**
- `$RELATED_PROJECTS` ve `$RELATED_PROJECTS_GIT_URLS` listelerini `,` ile bölerek eşleştir.
- Her proje için: `/app/workspace/<proje-adı>` dizini **yoksa** → ilgili URL ile `git clone`, **varsa** → `main` branch'ine geç, `git pull` al.

Tüm projeler güncel olduğunda bir sonraki adıma geç.

---

## 1. Task Alma

1. Jira'dan **`$JIRA_PROJECT`** projesindeki `[DB]` etiketli, `ANALYSE DONE` veya `DEVELOPMENT` statüsündeki task'ları listele.
2. Task'ı kendine assign et.
3. Task'ı `DEVELOPMENT` statüsüne çek.
4. Task'ın `Depends on` alanını kontrol et — bağımlı task'lar `TEST DONE` veya `DONE` statüsüne geçmeden başlama.

---

## 2. Task Değerlendirme

Task detaylarını oku. İki farklı durum olabilir:

**Eksik/belirsiz bilgi varsa:**
- Neyin eksik olduğunu Jira'ya yorum olarak gir.
- Yorumun sonuna "Tekrar analiz gerekiyor" yaz.
- Task'ı `ANALYSE` statüsüne geri al. Dur.

**Her şey nettse:**
- Geliştirmeye geç.

---

## 3. Şemayı Anla

1. `/app/workspace/$MAIN_PROJECT/project_context.md` dosyasını oku — projenin genel yapısını ve mevcut durumunu anla.
2. PostgreSQL MCP ile `$DATABASE_URI` veritabanına bağlan.
3. İlgili tabloları, kolonları ve mevcut index'leri incele.
4. Yapılacak değişikliği tasarla.

---

## 4. Geliştirme

1. `main` branch'inden yeni bir feature branch oluştur.
   - Format: `feature/<JIRA_KEY>-<task-basligi>`
2. SQL değişikliklerini veritabanında direkt çalıştırarak geliştir ve doğrula.
3. Migration dosyasını yaz (`V<versiyon>__<aciklama>.sql`).
4. Her mantıksal adım için commit at ve push'la.

**Geliştirme sırasında blocker çıkarsa:**
- Blocker'ı detaylı Jira yorumu olarak gir.
- Task'ı `DEVELOPMENT XL BLOCK` statüsüne al. Dur.

---

## 5. Git

1. `agent` branch'ine geç.
2. `agent` branch'ini pull al.
3. Feature branch'i `agent` branch'ine merge et.
4. `agent` branch'ini push'la.

---

## 6. Kapat

1. Geliştirme `/app/workspace/$MAIN_PROJECT/project_context.md` dosyasında güncelleme gerektiriyorsa (yeni tablo, önemli şema değişikliği vb.) bu dosyayı güncelle ve commit'e dahil et.
2. Yaptıklarını detaylı şekilde Jira task'ına yorum olarak gir.
   - Hangi tablolar/kolonlar eklendi/değiştirildi
   - Neden yapıldı
   - Dikkat edilmesi gereken noktalar (varsa)
3. Task'ı `DEVELOPMENT DONE` statüsüne al.
