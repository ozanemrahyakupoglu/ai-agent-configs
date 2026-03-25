# Entrypoint: Development

## Workflow

```
Task Assign
    ↓
Task Analizi
    ↓
Geliştirme anlaşıldı mı?
    ├── Hayır → Jira Yorum Gir (anlaşılamayan noktalar)
    │               ↓
    │           Task → Analyse
    │               ↓
    │           [Akış Sona Erer]
    │
    └── Evet ↓
Geliştirme Planlaması
    ↓
Git Clone / Pull
    ↓
Branch Oluştur
    ↓
Geliştirme
    ↓
Commit / Push
    ↓
Jira Yorum Gir
    ↓
Task → Development Done
```

## Adımlar

### 1. Task Assign
Task kendine assign edilir.

### 2. Task Analizi
Task detayları, yorumları ve varsa Confluence analiz dokümanı okunur. Yapılacak iş tüm detaylarıyla anlaşılmaya çalışılır:
- Jira task açıklaması ve kabul kriterleri okunur
- Jira task yorumları kronolojik sırayla okunur
- Task'a bağlı Confluence analiz dokümanı varsa okunur

Analiz sonucunda:
- **Geliştirme anlaşıldıysa:** Bir sonraki adıma geçilir.
- **Anlaşılamayan nokta varsa:** Anlaşılamayan noktalar Jira'ya yorum olarak yazılır, task **Analyse** statüsüne geri gönderilir ve akış sona erer.

### 3. Geliştirme Planlaması
Task analizi tamamlandıktan sonra yapılacaklar planlanır. Toplanan bilgiler ve bağımlılıklar incelenerek geliştirme adımları belirlenir.

### 4. Git Clone / Pull
- Repo daha önce clone'lanmadıysa: `git clone`
- Repo mevcutsa: `git pull`

### 5. Branch Oluştur
Task ID ve açıklamasına göre yeni bir branch oluşturulur.

### 6. Geliştirme
Geliştirme yapılır.

### 7. Commit / Push
Değişiklikler commit edilir ve uzak repoya push edilir.

### 8. Jira Yorum Gir
Yapılan işe dair özet yorum Jira task'ına girilir.

### 9. Task → Development Done
Task statüsü **Development Done** olarak güncellenir.
