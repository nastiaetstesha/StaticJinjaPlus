# StaticJinjaPlus Docker Port

Этот репозиторий содержит инструменты для сборки Docker-образов генератора статических сайтов [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) с поддержкой нескольких версий и базовых образов.
## Как получить checksum

`curl -sL https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/<VERSION>.zip | sha256sum`

## 📦 Сборка образов

### Ubuntu 22.04
### Dockerfile.ubuntu - Для стабильной версии — с checksum
ADD --checksum=sha256:47fe12da6118698bbea0ec1bb6f174b9b33540c1643119d41dd2046d2f37e6c7 \
    https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/${APP_VERSION}.zip /tmp/app.zip

### Если используешь APP_VERSION=main, закомментируй строку выше и раскомментируй строку ниже:
`# ADD https://github.com/MrDave/StaticJinjaPlus/archive/refs/heads/main.zip /tmp/app.zip`

```
docker build -f Dockerfile.ubuntu -t nastiaetstesha/static-jinja-plus:0.1.1 .
docker build -f Dockerfile.ubuntu --build-arg APP_VERSION=main -t nastiaetstesha/static-jinja-plus:develop .
```
## Python 3.12 slim
### Dockerfile.slim -  Для стабильной версии — с checksum
ADD --checksum=sha256:47fe12da6118698bbea0ec1bb6f174b9b33540c1643119d41dd2046d2f37e6c7 \
    https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/${APP_VERSION}.zip /tmp/app.zip

#### Для develop-сборки (если APP_VERSION=main):
`# ADD https://github.com/MrDave/StaticJinjaPlus/archive/refs/heads/main.zip /tmp/app.zip`
```
docker build -f Dockerfile.slim --build-arg APP_VERSION=0.1.1 -t nastiaetstesha/static-jinja-plus:0.1.1-slim .
docker build -f Dockerfile.slim --build-arg APP_VERSION=main -t nastiaetstesha/static-jinja-plus:develop-slim .
```
## 🚀 Публикация образов
```
docker push nastiaetstesha/static-jinja-plus:0.1.1
docker push nastiaetstesha/static-jinja-plus:develop
docker push nastiaetstesha/static-jinja-plus:0.1.1-slim
docker push nastiaetstesha/static-jinja-plus:develop-slim
```
#### ❗
Исходники StaticJinjaPlus не включаются в репозиторий.

Используется ADD --checksum для проверки целостности при сборке.

Версия указывается с помощью аргумента APP_VERSION.

## 🧪 Примеры запуска
```
docker run -it nastiaetstesha/static-jinja-plus:0.1.1
docker run -it nastiaetstesha/static-jinja-plus:develop
```