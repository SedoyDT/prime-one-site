---
publish: true
title: "Docker Compose с нуля"
---

# Docker Compose с нуля

Уровень сложности: ~65/100. Нужен Docker с Docker Compose (входит в Docker Desktop и в современный `docker` CLI как подкоманда `docker compose`).

**Предполагается:** понимание портов, переменных окружения и того, что своя сеть даёт резолвинг по имени контейнера — [[konteynery-dannye-i-peremennye|Управление контейнерами]] и [[docker-seti-i-svyaz-mezhdu-konteynerami|Docker-сети]].

## Проблема, которую решает Compose

Реальное приложение редко состоит из одного контейнера. Веб-сервер + база данных + кэш — это как минимум три `docker run` с сетью, портами и переменными окружения, которые нужно помнить и повторять при каждом перезапуске. Compose описывает всё это одним файлом и поднимает одной командой.

## Минимальный проект

Структура папки:

```
compose-demo/
  docker-compose.yml
  html/
    index.html
```

`html/index.html`:
```html
<h1>Привет из Compose</h1>
```

`docker-compose.yml`:
```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html:ro
    depends_on:
      - api

  api:
    image: alpine
    command: sh -c "while true; do echo -e 'HTTP/1.1 200 OK\n\nAPI работает' | nc -l -p 5000; done"
```

Запуск из папки `compose-demo`:

```
docker compose up -d
curl http://localhost:8080
docker compose exec web wget -qO- http://api:5000
```

Второй `curl`-эквивалент (`wget` внутри контейнера `web`, потому что `curl` не установлен в `nginx:alpine`) подтверждает главное: сервис `web` обращается к `api` просто по имени — Compose сам создал общую сеть для всех сервисов файла, без единой ручной команды `docker network create`. Это прямое следствие механизма из туториала про сети — Compose лишь автоматизирует то, что там делалось руками.

## Что означают ключи

- **`services:`** — список контейнеров проекта; имя каждого сервиса (`web`, `api`) — одновременно и DNS-имя внутри сети проекта.
- **`image:`** — какой образ использовать (можно заменить на `build: .`, чтобы Compose сам собирал образ из Dockerfile рядом).
- **`ports:`** — то же самое, что `-p` у `docker run`.
- **`volumes:`** — то же самое, что `-v`; суффикс `:ro` — том смонтирован только для чтения.
- **`depends_on:`** — порядок запуска: `api` стартует раньше `web`. Важная оговорка: это ждёт только *запуска* контейнера, а не готовности сервиса внутри него (медленно стартующая база данных может быть ещё не готова принимать соединения, хотя контейнер уже "up") — эта проблема решается healthcheck'ами на следующем уровне.

## Переменные окружения и .env

```yaml
services:
  api:
    image: alpine
    environment:
      - GREETING=${GREETING:-по умолчанию}
    env_file:
      - .env
```

`.env` в той же папке, что и `docker-compose.yml`, подхватывается автоматически — как для `environment:`, так и для подстановки `${...}` в самом файле. `${GREETING:-по умолчанию}` — значение переменной, если она есть, иначе — текст после `:-`.

## Именованные тома в Compose

```yaml
services:
  db:
    image: alpine
    volumes:
      - db-data:/data

volumes:
  db-data:
```

Том нужно объявить в верхнеуровневом ключе `volumes:` — иначе Compose создаст анонимный том, который сложно найти повторно после `docker compose down`.

## Управление проектом

```
docker compose ps          # статус контейнеров проекта
docker compose logs -f web  # логи конкретного сервиса, live
docker compose down         # остановить и удалить контейнеры (тома — по умолчанию НЕ трогает)
docker compose down -v      # то же самое, но и удалить тома проекта
```

## Проверка себя

Добавьте в `docker-compose.yml` третий сервис `redis` (образ `redis:alpine`, без `ports`, чтобы не открывать наружу), подключите к нему `api` по имени `redis` через `nc -zv redis 6379` внутри контейнера `api` и убедитесь, что порт виден изнутри проекта Compose без единой строчки про сеть — она уже общая по умолчанию.

## Что дальше

[[healthcheck-restart-i-otladka|Healthcheck, restart policy и отладка]] — Compose умеет запускать несколько сервисов; следующий шаг — сделать так, чтобы они сами восстанавливались после сбоя.
