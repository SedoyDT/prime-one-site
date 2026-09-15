---
publish: true
title: "Задача: Docker Compose: основы, `docker-compose.yml`"
---

# Задача: Docker Compose: основы, `docker-compose.yml`

Опишите `docker-compose.yml` с одним сервисом `app`, который собирается из `Dockerfile` в текущей папке (`build: .`), пробрасывает порт `3000:3000` и получает переменную окружения `APP_ENV=dev`.

<details>
<summary>Решение</summary>

```yaml
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - APP_ENV=dev
```
Запуск: `docker compose up -d` — Docker соберёт образ по `Dockerfile` из текущей папки и запустит контейнер с указанными портом и переменной.

</details>
