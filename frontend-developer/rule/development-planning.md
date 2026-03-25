# Rule: Development Planning

## Amaç

Task analizi tamamlandıktan sonra geliştirme adımları planlanır.

## Planlama Sırası

### 1. Entegre Sistem Değişiklikleri

Önce frontend'in entegre olduğu sistemlerde (API, backend, veritabanı vb.) değişiklik gerekip gerekmediği değerlendirilir.

- Yeni endpoint gerekiyor mu?
- Mevcut endpoint'lerde değişiklik gerekiyor mu?
- Veri modeli değişikliği var mı?

Eğer entegre sistemlerde değişiklik gerekiyorsa bu değişiklikler **önce** yapılır, sonraki adıma geçilir.

### 2. Frontend Değişiklikleri

Entegre sistem değişiklikleri tamamlandıktan (veya gerekmiyorsa) sonra frontend geliştirme adımları planlanır:

- Hangi bileşenler oluşturulacak veya güncellencek?
- Hangi sayfalar etkilenecek?
- State yönetiminde değişiklik gerekiyor mu?
- API entegrasyonu nasıl yapılacak?
