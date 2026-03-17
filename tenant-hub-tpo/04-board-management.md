# Board Management

## Görevin

Task planlama aşamasında **Jira board'undaki "READY" kolonunu** kontrol et.
READY'da 3'ten az task varsa, backlog'dan öncelik sırasına göre task'ları "READY"'ye taşı. Backlog'da madde olduğu sürece "READY" kolonunu 3 task'ta tutmaya çalış. Backlog boşsa mevcut durumu olduğu gibi bırak.

---

## Tetiklenme Koşulları

Bu workflow şu durumlarda çalışır:

1. **"Planlama yap" komutu geldiğinde** — kullanıcı bu veya benzeri bir komutu gönderirse, bu dosyayı oku ve gerekli aksiyonları al

---

## Adımlar

### 1. Board'u Bul

Jira'daki TH projesi için tanımlı Kanban board'u bul ve ID'sini al. Bu ID sonraki adımlarda kullanılacak.

---

### 2. "READY" Kolonunu Kontrol Et

Aktif board üzerinden "READY" statüsündeki task'ları sorgula. Önemli: bu sorgu board'a özel yapılmalı — board dışında kalan (henüz board'a alınmamış backlog) task'lar sayıma dahil edilmemeli.

"READY" task sayısı 3 veya daha fazlaysa işlemi durdur, bir şey yapma.

---

### 3. Backlog'dan Adayları Getir

"READY" task sayısı 3'ten azsa, kaç tane taşıman gerektiğini hesapla (hedef: 3).

Jira backlog'undan (board dışındaki task'lardan) en yüksek öncelikli olanları sırala. Öncelik eşitse, en eski oluşturulanı öne al. Sadece ihtiyaç kadar task al.

---

### 4. Task'ları "READY"'ye Taşı

Seçilen her task için Jira'da statü geçişini gerçekleştir: Backlog("TO DO") → READY.

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
- **Hedef: tam 3.** Ready'yi 3'ün üzerine çıkarma; tam 3'e tamamla.
