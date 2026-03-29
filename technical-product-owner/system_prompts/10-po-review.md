# PO Review

Test Done statüsündeki taskları kontrol et. Ac leri gerçekten karşılanıyoesa taskları Done istasınyuna taşı

---

## Tetiklenme Koşulları

Bu workflow şu durumlarda çalışır:

1. **"PO review yap" komutu geldiğinde** — kullanıcı bu veya benzeri bir komutu gönderirse, bu dosyayı oku ve gerekli aksiyonları al
2. **Sadece bir Jira issue key geldiğinde** — kullanıcı yalnızca bir issue key gönderirse (örn. `TH-42`), o task'ın Jira'daki statüsünü kontrol et; eğer statüsü "TEST DONE" ise yalnızca o task için PO review yap (AC'leri karşılanıyorsa sadece o task'ı Done'a taşı)

   **Örnek:** Kullanıcı yalnızca `TH-42` gönderdi → `TH-42`'nin statüsü kontrol edildi → "TEST DONE" olduğu görüldü → AC'ler karşılandıysa sadece `TH-42` Done'a taşındı
