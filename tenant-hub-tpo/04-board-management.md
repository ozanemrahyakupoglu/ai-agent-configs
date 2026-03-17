# Board Management

## Görevin

Task planlama aşamasında **Jira board'undaki "TO DO" kolonunu** kontrol et.
Todo'da 3'ten az task varsa, backlog'dan öncelik sırasına göre task'ları "TO DO"'ya taşı. Backlog'da madde olduğu sürece "TO DO" kolonunu 3 task'ta tutmaya çalış. Backlog boşsa mevcut durumu olduğu gibi bırak.

---

## Tetiklenme Koşulları

Bu workflow şu durumlarda çalışır:

1. **"Planlama yap" komutu geldiğinde** — kullanıcı bu komutu gönderirse, bu dosyayı oku ve gerekli aksiyonları al

---

## Adımlar

### 1. Board'u Bul

Jira'daki TH projesi için tanımlı Kanban board'u bul ve ID'sini al. Bu ID sonraki adımlarda kullanılacak.

---

### 2. "TO DO" Kolonunu Kontrol Et

Aktif board üzerinden "TO DO" statüsündeki task'ları sorgula. Önemli: bu sorgu board'a özel yapılmalı — board dışında kalan (henüz board'a alınmamış backlog) task'lar sayıma dahil edilmemeli.

"TO DO" task sayısı 3 veya daha fazlaysa işlemi durdur, bir şey yapma.

---

### 3. Backlog'dan Adayları Getir

"TO DO" task sayısı 3'ten azsa, kaç tane taşıman gerektiğini hesapla (hedef: 3).

Jira backlog'undan (board dışındaki task'lardan) en yüksek öncelikli olanları sırala. Öncelik eşitse, en eski oluşturulanı öne al. Sadece ihtiyaç kadar task al.

---

### 4. Task'ları "TO DO"'ya Taşı

Seçilen her task için Jira'da statü geçişini gerçekleştir: Backlog → To Do.

---

### 5. Sonucu Raporla

Taşıma tamamlandığında kısa bir özet ver:

> **Board güncellendi:**
> Todo kolonuna taşınan task'lar:
> - `TH-42` — [BE] JWT token yenileme endpoint'i (High)
> - `TH-38` — [WEB] Profil sayfası form validasyonu (Medium)
>
> Todo kolonu şu an 3 task içeriyor.

Taşınacak yeterli backlog task'ı yoksa:

> **Dikkat:** Todo'da yalnızca `{n}` task var ve backlog'da yeterli task bulunamadı.
> Yeni task üretilmesi gerekebilir.

---

## Kurallar

- **Sormadan taşı.** Bu rutin bir operasyondur, her seferinde onay isteme.
- **Sadece Backlog → To Do.** Başka statü geçişleri yapma.
- **Öncelik sırasına uy.** En yüksek öncelikli task'lar önce taşınır. Eşit önceliklilerde en eski task öne gelir.
- **Hedef: tam 3.** Todo'yu 3'ün üzerine çıkarma; tam 3'e tamamla.
