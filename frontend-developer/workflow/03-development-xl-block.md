# Entrypoint: Development XL Block

Bu entrypoint, `DEVELOPMENT XL BLOCK` statüsündeki bir task ile tetiklenir.

## Workflow

```
Yorumları Oku
    ↓
XL Block sebebine cevap verilmiş mi?
    ├── Hayır → Jira'ya "XL block çözümü bekleniyor" yorumu gir → XL BLOCK'ta bırak → Akış tamamlanır
    └── Evet → Cevap XL Block'u kaldırmak için yeterli mi?
                    ├── Hayır → Jira'ya yorum gir → XL BLOCK'ta bırak → Akış tamamlanır
                    └── Evet → Task → DEVELOPMENT → Development Akışını Koştur
```

## Adımlar

### 1. Yorumları Oku
Task üzerindeki tüm yorumlar en eskiden en yeniye tarih sırasına göre okunur.

### 2. XL Block Sebebine Cevap Verilmiş mi?
XL block nedenini açıklayan yoruma cevap verilip verilmediği kontrol edilir.

- **Cevap verilmemişse:** Jira task'ına *"XL block çözümü bekleniyor"* yorumu girilir. Task `DEVELOPMENT XL BLOCK` statüsünde bırakılır, akış tamamlanır.
- **Cevap verilmişse:** Bir sonraki adıma geç.

### 3. Cevap Yeterli mi?
Developer ajan, gelen cevabın XL block'u kaldırmak için yeterli olup olmadığını değerlendirir.

- **Yeterli değilse:** Eksikliği veya belirsizliği açıklayan bir yorum Jira'ya girilir. Task `DEVELOPMENT XL BLOCK` statüsünde bırakılır.
- **Yeterliyse:** Bir sonraki adıma geç.

### 4. Task → DEVELOPMENT
Task statüsü **DEVELOPMENT** olarak güncellenir.

### 5. Development Akışını Koştur
`entrypoint/development.md` akışı baştan koşturulur.
