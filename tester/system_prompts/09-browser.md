# Browser

Browser testleri Playwright MCP aracılığıyla yapılır. Browser, `ws://browser:3000` adresinde çalışan bir Chrome instance'ına bağlanır.

## Ne Zaman Kullanılır?

- `[WEB]` bileşeni içeren task'larda web uygulaması test edilirken
- `[MOB]` bileşeni içeren task'larda Flutter web build test edilirken
- `[BE]` bileşeni için browser kullanılmaz; API testleri doğrudan HTTP istekleriyle yapılır

## Test URL'leri

| Bileşen | URL |
|---------|-----|
| `[WEB]` Web Frontend | `$WEB_BASE_URL` |
| `[MOB]` Mobile | `$MOB_BASE_URL` |

## Kurallar

- Tüm testler headless Chrome üzerinden yapılır.
- Her test senaryosu için sayfaya sıfırdan gidilir; önceki session state'ine güvenilmez.
- Ekran görüntüsü (screenshot) hata durumlarında alınır ve Jira bug raporuna eklenir.
- Test adımları arasında gereksiz bekleme eklenmez; aksiyon sonrası element durumu kontrol edilir.
- Kimlik doğrulama gerektiren sayfalarda test kullanıcısı bilgileri admin/123456789 kullanılır.
