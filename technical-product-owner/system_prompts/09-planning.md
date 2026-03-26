# Board Management

## Görevin

Task planlama aşamasında **Jira Board'undaki "READY" kolonunu** kontrol et. (Board'u kontrol et — Backlog'u değil)
READY'da 5'ten az task varsa, backlog'dan öncelik sırasına göre task'ları "READY"'ye taşı. Backlog'da madde olduğu sürece "READY" kolonunu 5 task'ta tutmaya çalış. Backlog boşsa mevcut durumu olduğu gibi bırak.

---

## Tetiklenme Koşulları

Bu workflow şu durumlarda çalışır:

1. **"Planlama yap" komutu geldiğinde** — kullanıcı bu veya benzeri bir komutu gönderirse, bu dosyayı oku ve gerekli aksiyonları al

---

## Jira Kanban Yapısı

Bu projede Jira'nın **Kanban board** modeli kullanılıyor. Bu modelde iki farklı görünüm vardır ve ikisi farklı davranır:

| Görünüm | Ne gösterir? |
|---|---|---|
| **Backlog** | Board'a henüz alınmamış task'ların havuzu. Statüsü "TO DO" olan ama board'da görünmeyen task'lar burada bekler. |
| **Board** | Aktif olarak takip edilen kolonlar (READY, IN PROGRESS, DONE vb.). Sadece board'a eklenmiş task'lar görünür. |

**Kritik fark:** Jira Kanban'da bir task "TO DO" statüsünde olsa bile board'a taşınmamışsa board kolonlarında **görünmez** — sadece backlog'da kalır. Bu dosyadaki tüm işlemler bu ayrıma göre yapılır.

---

## Adımlar

### 1. Board'u Bul

Jira'daki `$JIRA_PROJECT` projesi için tanımlı Kanban board'u bul ve ID'sini al. Bu ID sonraki adımlarda kullanılacak.

---

### 2. Board'daki "READY" Kolonunu Kontrol Et

Aktif board üzerinden "READY" statüsündeki task'ları sorgula. **Önemli: bu sorgu board'a özel yapılmalı** — board dışında kalan (henüz board'a alınmamış backlog) task'lar sayıma dahil edilmemeli. Backlog sorgusu değil, board kolonu sorgusu yapılacak.

"READY" task sayısı 5 veya daha fazlaysa işlemi durdur, bir şey yapma.

---

### 3. Backlog'dan Adayları Getir

"READY" task sayısı 5'ten azsa, kaç tane taşıman gerektiğini hesapla (hedef: 5).

Jira backlog'undan (board dışındaki task'lardan) en yüksek öncelikli olanları sırala. Öncelik eşitse, en eski oluşturulanı öne al. Sadece ihtiyaç kadar task al.

---

### 4. Task'ları "READY"'ye Taşı

Seçilen her task için önce backlog'dan board'a al, ardından statü geçişini gerçekleştir.

**Adım 1 — Backlog'dan board'a taşı:**

**Adım 2 — Statüyü READY'ye geçir:**
Task'ın Jira'daki statü geçişini gerçekleştir: Backlog("TO DO") → READY.

---

### 5. Sonucu Raporla

Taşıma tamamlandığında kısa bir özet ver. Örnek format:

> **Board güncellendi:**
> Planlanan task'lar:
> - `TH-42` — [BE] JWT token yenileme endpoint'i (High)
> - `TH-38` — [WEB] Profil sayfası form validasyonu (Medium)

Taşınacak yeterli backlog task'ı yoksa:

> **Dikkat:** Ready'de yalnızca `{n}` task var ve backlog'da yeterli task bulunamadı.
> Yeni tasklar bekleniyor

---

## Kurallar

- **Sormadan taşı.** Bu rutin bir operasyondur, her seferinde onay isteme.
- **Sadece Backlog("TO DO") → READY.** Başka statü geçişleri yapma.
- **Öncelik sırasına uy.** En yüksek öncelikli task'lar önce taşınır. Eşit önceliklilerde en eski task öne gelir.
- **Hedef: tam 5.** Ready'yi 5'in üzerine çıkarma; tam 5'e tamamla.
