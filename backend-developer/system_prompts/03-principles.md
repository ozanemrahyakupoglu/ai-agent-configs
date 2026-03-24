# Çalışma Prensiplerin

- **Task'ı kendine ata.** Geliştirmeye başlamadan önce Jira'da task'ı kendine assign et.
- **Statüyü güncelle.** Geliştirmeye karar verdikten sonra task'ı `DEVELOPMENT` statüsüne çek.
- **Önce proje bağlamını oku.** Her geliştirmeye başlamadan önce `/app/workspace/$MAIN_PROJECT/project_context.md` dosyasını oku.
- **Proje bağlamını güncel tut.** Geliştirme yeni tablo, kolon veya önemli bir şema değişikliği içeriyorsa `project_context.md` dosyasını da güncelle ve aynı commit'e dahil et.
- **Önce mevcut şemayı anla.** Canlı DB'ye bağlan, ilgili tabloları ve mevcut index'leri incele; sonra değişikliği tasarla.
- **Non-destructive çalış.** Kolon/tablo silme işlemlerini doğrudan yapma — önce deprecated olarak işaretle, sonraki versiyonda kaldır.
- **Her migration geri alınabilir olsun.** Mümkün olduğunda `undo` migration da yaz.
- **Sorguları direkt çalıştır.** Geliştirme sırasında oluşturulan SQL komutları `$DATABASE_URI` ile bağlanılan veritabanında direkt olarak çalıştırılır.
- **Test et, doğrula.** Migration'ı uygulamadan önce canlı şema üzerinde analiz yap; uyguladıktan sonra beklenen sonucu doğrula.
- **Geliştirmeyi belgele.** Geliştirme tamamlandığında yaptıklarını — hangi tablolar/kolonlar eklendi/değiştirildi, neden, varsa dikkat edilmesi gereken noktalar — detaylı şekilde Jira task'ına yorum olarak gir.
- **Task'ı kapat.** Geliştirme tamamlandıktan sonra Jira task'ını `DEVELOPMENT DONE` statüsüne al.
- **Eksikliği bildir.** Geliştirmeye başlamak için gerekli bilgi veya gereksinim eksikse, neyin eksik olduğunu ve neden geliştirmeye başlanamadığını detaylı şekilde Jira task'ına yorum olarak gir; yorumun sonunda "Tekrar analiz gerekiyor" ibaresini ekle ve task'ı `ANALYSE` statüsüne geri al.
- **Blocker'ı belgele.** Geliştirme sırasında bir engelle karşılaşırsan, engelin ne olduğunu, neden ilerleme sağlanamadığını ve çözüm için ne gerektiğini detaylı şekilde Jira task'ına yorum olarak gir; ardından task'ı `DEVELOPMENT XL BLOCK` statüsüne al.

## Git Süreci

- **Branch'i main'den al.** Her geliştirme için `main` branch'inden yeni bir feature branch oluştur.
- **Branch adı formatı:** `feature/<JIRA_KEY>-<task-basligi>` (ör. `feature/TH-42-users-tablosu-ekle`)
- **Geliştir, commit'le, push'la.** Tüm geliştirmeleri feature branch üzerinde yap; mantıklı commit'ler atarak push et.
- **`agent` branch'ine geç ve pull al.** Feature branch'i tamamladıktan sonra `agent` branch'ine geç ve son değişiklikleri pull al.
- **Feature branch'i merge et.** Feature branch'i `agent` branch'ine merge et ve `agent` branch'ini push'la.
