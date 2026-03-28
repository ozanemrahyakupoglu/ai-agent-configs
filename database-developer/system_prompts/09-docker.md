# Docker

## Bağlantı Bilgileri

| Alan | Değer | Açıklama |
|------|-------|----------|
| Username | `$DOCKER_USERNAME` | Docker Hub kullanıcı adı (`DOCKER_USERNAME` env) |
| Image Adı | `$DOCKER_IMAGE_NAME` | Docker image adı (`DOCKER_IMAGE_NAME` env) |
| Access Token | `$DOCKER_ACCESS_TOKEN` | Docker Hub erişim token'ı (`DOCKER_ACCESS_TOKEN` env) |


## Versiyonlama

- Image versiyonu semantik versiyonlama (`major.minor.patch`) kullanır.
- Her yeni build'de yalnızca `patch` numarası `1` artırılır.
- Örnek: Docker Hub'da `1.0.3` varsa yeni versiyon `1.0.4` olur.
- Tag formatı: `$DOCKER_USERNAME/$DOCKER_IMAGE_NAME:<major>.<minor>.<patch>`

Docker Hub'daki en son tag'i öğrenme:
```bash
curl -s "https://hub.docker.com/v2/repositories/$DOCKER_USERNAME/$DOCKER_IMAGE_NAME/tags?page_size=100" \
  | grep -o '"name":"[0-9]*\.[0-9]*\.[0-9]*"' | grep -o '[0-9]*\.[0-9]*\.[0-9]*' \
  | sort -t. -k1,1n -k2,2n -k3,3n | tail -1
```

## Image Build & Push

```bash
# Login
echo $DOCKER_ACCESS_TOKEN | docker login -u $DOCKER_USERNAME --password-stdin

# Build
docker build -t $DOCKER_USERNAME/$DOCKER_IMAGE_NAME:<versiyon> .

# Push
docker push $DOCKER_USERNAME/$DOCKER_IMAGE_NAME:<versiyon>
```

## Migration Çalıştır

Database developer agent bir container içinde çalışır. Migration container'ı iç içe (nested) değil, host üzerinde sibling container olarak ayağa kalkar. Bunun için host'un Docker socket'i agent container'ına mount edilmiş olmalıdır (`-v /var/run/docker.sock:/var/run/docker.sock`).

```bash
docker run --rm \
  -e FLYWAY_URL="jdbc:postgresql://46.225.97.71:5432/postgres?currentSchema=tenant_hub" \
  -e FLYWAY_USER="postgres" \
  -e FLYWAY_PASSWORD="123456789" \
  $DOCKER_USERNAME/$DOCKER_IMAGE_NAME:<versiyon>
```

## Kurallar

- Build öncesinde Docker Hub'dan mevcut en yüksek `patch` versiyonu okunur ve `1` artırılır.
- Migration çalıştırılmadan önce image yeniden build edilir.
- Migration başarısız olursa hata çıktısı incelenir ve ilgili SQL dosyası düzeltilir.
- `docker run` sonrası container otomatik silinir (`--rm` flag zorunludur).
