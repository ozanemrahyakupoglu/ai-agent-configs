# İş Akışı

## Genel Akış

Mesaj alındığında:

1. Jira'dan task bilgisi çekilir (`$JIRA_PROJECT`)
2. Task statüsüne göre ilgili akış koşturulur

## Statüye Göre Akış

| Statü | Akış |
|-------|------|
| `ANALYSE DONE` | Task → DEVELOPMENT, sonra Development Akışı |
| `DEVELOPMENT` | Development Akışı |
| `DEVELOPMENT XL BLOCK` | XL Block Akışı |

Statü yukarıdaki listede yoksa şu yanıt verilir:
> "Bu task şu an işleme alınamaz. Geçerli statüler: ANALYSE DONE, DEVELOPMENT, DEVELOPMENT XL BLOCK."

---

## Development Akışı

### 1. Task Assign
Task kendine assign edilir. Zaten assignliyse tekrar atanmaz.

### 2. Task Analizi
Jira task detayları, yorumları ve varsa Confluence analiz dokümanı okunur:
- Task açıklaması ve kabul kriterleri okunur
- Task'a bağlı diğer Jira task'ları (bağımlılıklar, alt task'lar) varsa listelenir
- Jira yorumları kronolojik sırayla (eskiden yeniye) okunur
- Bağlı Confluence dokümanı varsa okunur; yoksa bu adım atlanır

Analiz sonucunda:
- **Geliştirme anlaşıldıysa:** Bir sonraki adıma geçilir.
- **Anlaşılamayan nokta varsa:** Anlaşılamayan noktalar Jira'ya yorum olarak yazılır, task **ANALYSE** statüsüne geri gönderilir, akış sona erer.

### 3. Geliştirme Planlaması
Toplanan bilgiler doğrultusunda geliştirme adımları planlanır:
- Önce entegre sistemlerde (API, backend vb.) değişiklik gerekip gerekmediği değerlendirilir
- Sonra frontend geliştirme adımları planlanır (bileşenler, sayfalar, state, API entegrasyonu)

### 4. Git Clone / Pull
- Repo yoksa: `git clone`
- Repo varsa: `main` branch'ine geç, `git pull`

### 5. Branch Oluştur
`main` branch'inden yeni feature branch oluşturulur.

### 6. Geliştirme
Plana uygun geliştirme yapılır. Blocker çıkarsa Jira'ya yorum girilir ve task **DEVELOPMENT XL BLOCK** statüsüne alınır.

### 7. Commit / Push
Her mantıksal adım için commit atılır, feature branch push'lanır. Ardından:
1. `agent` branch'ine geç
2. `agent` branch'ini pull al
3. Feature branch'i `agent` branch'ine merge et
4. `agent` branch'ini push'la

### 8. Jira Yorum Gir
Yapılan geliştirmenin özeti Jira task'ına yorum olarak girilir:
- Yapılan işin özeti
- Eklenen/güncellenen bileşenler ve sayfalar
- Entegre sistem değişiklikleri (varsa)
- Dikkat edilmesi gereken noktalar (varsa)

### 9. Task → DEVELOPMENT DONE
Tüm koşullar sağlandıktan sonra task **DEVELOPMENT DONE** statüsüne alınır ve assignee kaldırılır.

---

## XL Block Akışı

### 1. Yorumları Oku
Task üzerindeki tüm yorumlar en eskiden en yeniye okunur.

### 2. XL Block Sebebine Cevap Verilmiş mi?
- **Hayır:** Jira'ya *"XL block çözümü bekleniyor"* yorumu girilir, task XL BLOCK'ta bırakılır, akış sona erer.
- **Evet:** Bir sonraki adıma geç.

### 3. Cevap Yeterli mi?
- **Hayır:** Eksikliği açıklayan yorum Jira'ya girilir, task XL BLOCK'ta bırakılır, akış sona erer.
- **Evet:** Task **DEVELOPMENT** statüsüne alınır, Development Akışı baştan koşturulur.
