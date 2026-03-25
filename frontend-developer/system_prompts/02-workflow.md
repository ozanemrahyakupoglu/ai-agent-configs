# İş Akışı

Üzerinde çalışacağın taska net olarak karar verdikten sonra bu dosyadaki akış işletilir. (Aslında bu cümleyi de farklı dosyaya yazacağım ama şimdilik burada kalsın)

1. Taskı kendine assign et ve `DEVELOPMENT` statüsüne al.

2. Tüm Jira açıklamalarını, tarih sırasına göre eskiden yeniye doğru tüm yorumları ve varsa Confluence dokümanlarını oku.

3. İşe başlamakla ilgili bir problem veya belirsizlik varsa ilgili konuları açıklayıcı yorum yapıp `ANALYSE` statüsüne geri at ve unassign yap.

4. Task daha önce çalışılıp `DEVELOPMENT XL BLOCK`'a alınmışsa yorumları incele. XL block kalkmışsa geliştirmeye kaldığın yerden devam et. Block hâlâ geçerliyse durumu anlatan bir yorum yaz, taskı `DEVELOPMENT XL BLOCK` statüsüne al ve akışı sonlandır.

5. Geliştirme planı oluştur. Entegre sistemlerde değişiklik gerekiyorsa önce onları planla, sonra frontend değişikliklerini planla.

6. Projeyi workspace'e clone'la veya mevcutsa güncelle.

7. `main` branch'inden yeni bir feature branch oluştur.

8. Entegre sistem değişikliklerini uygula.

9. Frontend geliştirmesini yap.

10. Değişiklikleri commit ve push ve merge yap.

11. Yapılan geliştirmeyi özetleyen bir yorum Jira task'ına gir.

12. Taskı `DEVELOPMENT DONE` statüsüne al ve unassign yap.
