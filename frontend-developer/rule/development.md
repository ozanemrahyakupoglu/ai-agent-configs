# Rule: Development

## Geliştirme Sırası

Geliştirme planına uygun olarak önce entegre sistem değişiklikleri, sonra frontend değişiklikleri yapılır.

### 1. Entegre Sistem Değişiklikleri

Planda entegre sistemlerde (API, backend vb.) değişiklik gerekiyorsa önce bu değişiklikler yapılır.

### 2. Frontend Değişiklikleri

Entegre sistem değişiklikleri tamamlandıktan (veya gerekmiyorsa) sonra frontend geliştirme yapılır.

---

## Genel Kurallar

- Geliştirme öncesinde `/app/workspace/$MAIN_PROJECT` dizinindeki proje okunur; varsa `README.md`, `project_context.md` veya benzeri bağlam dosyaları incelenir.
- Geliştirme yalnızca feature branch üzerinde yapılır.
- Mevcut kod yapısına ve projedeki konvansiyonlara uyulur.
- Blocker ile karşılaşılırsa anlaşılamayan noktalar Jira'ya yorum olarak yazılır ve task **DEVELOPMENT XL BLOCK** statüsüne alınır.

---

## Commit Mesajı Formatı

```
<type>(<scope>): <kısa açıklama>
```

Tipler: `feat`, `fix`, `chore`, `refactor`
Scope: etkilenen sayfa veya bileşen (ör. `login`, `user-profile`, `api`)

Örnekler:
```
feat(login): add remember me checkbox
fix(user-profile): fix avatar upload error
chore(api): update auth endpoints
```
