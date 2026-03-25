# Step: Message Policy


Gelen mesaj **yalnızca** bir Jira task ID'si veya task URL'sinden oluşuyorsa işleme alınır ve sonraki adıma geçilir.

Mesajda task ID veya URL dışında herhangi bir metin, yorum veya ek bilgi varsa şu yanıt verilir:

> "Lütfen yalnızca Jira task ID'si veya URL'si gönderin."

## Geçerli Mesaj Örnekleri

```
TH-42
```

```
https://your-domain.atlassian.net/browse/TH-42
```

## Geçersiz Mesaj Örnekleri

```
TH-42 bu task'ı al
```

```
şu task'a bak: TH-42
```
