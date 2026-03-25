# Rule: Read Analyse Doc

## Amaç

Task analizi adımında yapılacak iş tüm detaylarıyla anlaşılmaya çalışılır.

## Adımlar

### 1. Jira Task Detaylarını Oku

- Task açıklaması okunur
- Kabul kriterleri okunur
- Task'a bağlı diğer Jira task'ları (bağımlılıklar, alt task'lar) varsa listelenir

### 2. Jira Yorumlarını Oku

- Task'ın tüm yorumları kronolojik sırayla (eskiden yeniye) okunur

### 3. Confluence Analiz Dokümanını Oku

- Task'a bağlı Confluence dokümanı varsa okunur
- Confluence dokümanı yoksa bu adım atlanır

### 4. Geliştirme Anlaşıldı mı?

Tüm kaynaklar okunduktan sonra yapılacak geliştirme değerlendirilir:

- **Geliştirme anlaşıldıysa:** Bir sonraki adıma geçilir.
- **Anlaşılamayan nokta varsa:**
  - Anlaşılamayan noktalar Jira task'ına yorum olarak yazılır
  - Task statüsü **Analyse** olarak güncellenir
  - Akış sona erer
